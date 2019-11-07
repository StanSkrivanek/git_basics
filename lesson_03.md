# 03 | Git under-hood

In this lesson we will learn basics how and where Git store data, how create referrals to them to access these and why is so fast. To understand we need know what is **blob**, **commit**, **tree**, **SHA - 1** and **HEAD** and their purpose.

---

## Data accessibility

One of the reasons why Git is amazingly fast is use of referrals to snapshots (set of changes between commits). All these snapshots and referrals are stored by Git in `.git` folder that is created inside of our project folder when we initiate Git `git init`

When we staging and then committing snapshots from Staging area to Repository, Git runs a few actions to save referrals (pointers) to snapshots.

Before we will move forward we should know what SHA-1 is and for what is used in Git

### SHA - 1

**SHA - 1** is a cryptographic function that generate 40 character long hexadecimal hash _[ 0-9, a-z ]_

When we run command `git add` or `git commit`, Git will run a **checksum** on snapshot(s) using **SHA - 1** hash (algorithmic function), and convert snapshot(s) into simple number.

We can imagine Git like **key** - **value** pair store, where **value** are **data** and **key** to these data is **hash (SHA - 1)**

The value (number) of the key is **unique** and its combination is based on data content. In other words, the content generate the key and **any** change in content will generate a new key combination.

> Generated key will be **always** identical if data input is the same. In other words - different data input will generate different key.

- **`checksum`** - running a program that puts data file through an algorithm. Typical algorithms used for this include MD5, SHA-1, SHA-256, and SHA-512

- **`snapshot`** - set of changes in our project usually stored in Stashing area, that will be part of next commit. Snapshot contains not only `diff` (code we add or removed) but exact file content at the point a stash/commit is made

### Demonstration

We can demonstrate how Git create a hash (SHA-1) from given input. We use command terminal command `echo` which will return a value, in this case our string `'Hi all!'`, then we feed this value (string) into git command `git hash-object` to create SHA-1 hash and we have to also use flag `--stdin`. Returned value will be a hash number.

Type in your terminal exactly as in example

```bash
$ echo 'Hi all!' | git hash-object --stdin
```

result

```bash
c2fea86a95fc1286b5c806ca3a7ffa4fc970ca9c
```

If you type on your computer exact string `'Hi all'` you see that generated **hash** number on your computer **will be identical** to everyone's else.

If you will change only one letter e.g. [a for A] in word `all` generated hash will be different. THis just show direct relation of data input on generated hash combination.

`|` - Pipe is used to combine two or more commands, and in this, the output of one command acts as input to another command, on so on\
`git hash-object` - Computes the object ID value for an object\
`--stdin` - Read the object from standard input ( from keyboard) instead of from a file

---

## Git Objects

Git works with four different types of objects : a **blob**, a **tree**, a **commit**, and **tag**. Every Git object type consists of two things: _content_ and _size_. The size is simply the size of the content and the content depend on what type of object it is.

### Where Git store these objects

Before we will look on Git objects we should know where Git store all objects. When we open git hidden folder with "tree" plugin

```bash
~/desktop/myProject > git init
~/desktop/myProject > tree .git
```

as result we will get tree view of `.git` folder similar to this

```bash
.git
├── COMMIT_EDITMSG
├── HEAD
├── config
├── description
├── hooks
├── index
├── info
│   └── exclude
├── logs
│   ├── HEAD
│   └── refs
│       └── heads
│           └── master
├── objects
│   ├── info
│   └── pack
└── refs
    ├── heads
    │   └── master
    └── tags

```

When we take a closer look on this tree we see that there is folder _objects_

### Git objects folders structure

WE already know that Git runs SHA-1 encryption function on file snapshot to create unique _hash_. Here is coming explanation why is blazing fast.
When _hash_ is created Git will take **first two** digits of that _hash_ as prefix and assign this prefix as sub-folder name and place rest of _hash_ number inside this folder.

Each _hash_ that start with identical prefix will be stored in the same directory. This system save lots of search time on large projects. I know that is a bit confusing at this moment but it will all make sense later.

Because _hash_ is hexadecimal number we can have max 256 sub-folders.

---

### Why will commit have always different hash

There is one thing we should remember before we will talk about each object in detail:

> **SHA** for **blob** and **tree** should be **identical** for every user if data are identical, but **SHA** for **commit** will be for each user **different**.

We know that SHA-1 generate hash number that is directly related to content of data, therefore blob and tree can have an identical hash.

But commit hash will be **always** different for each user even if content of commit will be identical because commit contain extra information (metadata) as name of committer and date and time of commit.

> _different user_ and/or _different day/time_ **=** _different SHA-1 hash_

#### What does it mean

##### Time

Image that you are only user creating commits, so each commit hash will be different because will be created at different time (hr-min-sec)

##### Name of committer

We didn't talk about team work yet but imagine for a moment than you work in a team on one project. Now, even if each team member will create commit with identical content at the same time (that's very unlikely), there is another factor for creating unique hash and that is committers name.

---

#### Demonstration where objects are stored

To store git objects we need to create a project and initiate git

```bash
~ cd desktop
~/desktop > mkdir gtest
~/desktop > cd gtest
~/desktop/gtest > git init
```

To store git object we will use **`-w`** bash flag **write**

```bash
~/desktop/gtest > master > echo 'Hi all!' | git hash-object -w --stdin
c2fea86a95fc1286b5c806ca3a7ffa4fc970ca9c
```

Show only `objects` folder in project tree

```bash
~/desktop/gtest > master > tree .git/objects
```

We see SHA of our stashed file

```bash
.git/objects
├── c2
│   └── fea86a95fc1286b5c806ca3a7ffa4fc970ca9c
├── info
└── pack
```
