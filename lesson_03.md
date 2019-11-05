# 03 | Data accessibility

---

## Data accessibility from bottom up

In this lesson we will learn basics how and where Git store data, how create referrals to them to access these and why is so fast. To understand we need know what is **blob**, **commit**, **tree**, **SHA - 1** and **HEAD** and their purpose.

---

One of the reasons why Git is amazingly fast is use of referrals to snapshots (set of changes between commits). All these snapshots and referrals Git store in `.git` folder that is created inside of our project folder when we initiate Git `git init`

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

### Where Git store objects

Objects are stored in `.git/object` folder. Git take **first two** digits of hash as prefix and assign this prefix as sub-folder name. Because hash is hexadecimal number we can have max 256 sub-folders. Each hash that start with identical prefix will be stored in this directory. This system save lots of search time on large projects. I know that is a bit confusing at this moment but it will all make sense later.

> **SHA** for **blob** and **tree** should be **identical** for every user, **SHA** for **commit** will be **different**.

Why? Don't forget that SHA-1 generate number that is directly related to content of data, therefore tree will have identical hash. But commit hash will be different for each user even if content () will be identical because There will be different metadata - _different user, different day/time_.

#### Demonstration where SHA-1 is stored

**`-w`** - write

```bash
$ echo 'Hi all!' | git hash-object -w --stdin
c2fea86a95fc1286b5c806ca3a7ffa4fc970ca9c
$ tree .git
```

Show only `objects` tree

```bash
$ tree .git/objects
```

```bash
.git/objects
├── c2
│   └── fea86a95fc1286b5c806ca3a7ffa4fc970ca9c
├── info
└── pack
```

#### Git objects details

To get information about git object type and its content we can use command `git cat-file` followed by flag and hash number

- show **type** of git object
  `git cat-file` **`-t`** `SHA hash`

```bash
~/desktop/project_01 > git cat-file -t c2fea86a95fc1286b5c806ca3a7ffa4fc970ca9c

> blob
```

- show **content** of git object
  `git cat-file` **`-p`** `SHA hash`

```bash
~/desktop/project_01 > git cat-file -p c2fea86a95fc1286b5c806ca3a7ffa4fc970ca9c

> Hi all!
```

---

### WTF is blob

Previously I have mentioned word _**blob**_ very shortly. Now is time to take a closer look what **blob** is.

A simply said a **blob** is used to store file data, and it is generally a file.

A Git **blob** _(binary large object)_ is lowest level **object** type used **to store the contents** of each file snapshot **in a git repository**.

> **NOTE:** Important to remember is that **Git generated hash is based on file content** and **_not on file it self_**. This mean that two files with identical content will produce only one **blob** even that they will have different name or path.

In previous section we have learned basics about SHA-1 hash. Now, when SHA-1 hash for our staged snapshot is generated, Git will store it in a blob object together with other information about this snapshot.

`git show` `SHA-1 hash number`
[blob](http://shafiul.github.io/gitbook/1_the_git_object_model.html)

### How blob is created

We already know that **Staging** is term used for placing our changes into memory with use of `git add`
When we decide to store our changes into Stashing Area (memory) Git will:

1. make snapshot of current content state of file('s) (with our changes)
2. run SHA-1 on data (content) to create unique hash
3. create object type **blob** with its unique hash
4. store required information in a **blob** object (SHA - 1 hash, data ...)
5. create sub-folder in `.git/objects` based on first two letters of hash
6. place encrypted blob (SHA-1 hash) into this sub-folder

**NOTE:** Take this description as non-technical and **very** brief
