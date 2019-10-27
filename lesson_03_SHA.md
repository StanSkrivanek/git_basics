# Git - lessons | 03

---

## Data accessibility

One of the reasons why Git is blazingly fast is use of snapshots for set of changes between commits. In this lesson we will learn more about **SHA - 1** (Secure Hash Algorithm 1) that is used by Git as snapshots referrals.

Git generates a **checksum** using **SHA - 1** hash (algorithmic function) for each set of changes , in this case commit, that convert data into simple number.

`checksum` - running a program that puts data file through an algorithm. Typical algorithms used for this include MD5, SHA-1, SHA-256, and SHA-512

### SHA - 1

Git is like **key** - **value** pair store, where **key** is **hash (SHA - 1)** and **value** are **data**

**SHA - 1** is a cryptographic function that generate 40 character long hexadecimal hash _[ 0-9, a-z ]_

Value of key is **unique** and its combination is based on data content. In other words, the content generate the key and **any** change in content will generate a new key combination.

> Generated key will be **always** identical if data input is the same. In other words - different data input will generate different key.

### Demonstration

`|` - Pipe is used to combine two or more commands, and in this, the output of one command acts as input to another command, on so on\
`git hash-object` - Computes the object ID value for an object\
`--stdin` - Read the object from standard input instead of from a file

Type in your terminal

```bash
$ echo 'Hi all!' | git hash-object --stdin
```

result

```bash
c2fea86a95fc1286b5c806ca3a7ffa4fc970ca9c
```

### Where Git store data

Git store all data in `.git` folder that is created inside of our project folder when we initiate Git `git init`

Hash data are stored in `.git/object` folder. Git take **first two** digits of hash as prefix and assign this prefix as sub-folder name. Because hash is hexadecimal number we can have max 256 sub-folders. Each hash that start with identical prefix will be stored in this directory. This save lots of time on large projects.

> **SHA** for **blob** and **tree** should be **identical** for every user, **SHA** for **commit** will be **different**.

Don't forget that SHA generated number is directly related to content of data, therefore tree will have identical hash. But commit hash will be different for each user even if content () will be identical. Why? There will be different metadata - _different user, different day/time_.

**TEST:**
**`-w`** - write

```bash
$ echo 'Hi all!' | git hash-object -w --stdin
c2fea86a95fc1286b5c806ca3a7ffa4fc970ca9c
$ tree .git
```

```bash
.git
├── HEAD
├── config
├── description
├── hooks
│   ├── applypatch-msg.sample
│   ├── commit-msg.sample
│   ├── fsmonitor-watchman.sample
│   ├── post-update.sample
│   ├── pre-applypatch.sample
│   ├── pre-commit.sample
│   ├── pre-push.sample
│   ├── pre-rebase.sample
│   ├── pre-receive.sample
│   ├── prepare-commit-msg.sample
│   └── update.sample
├── info
│   └── exclude
├── objects
│   ├── c2
│   │   └── fea86a95fc1286b5c806ca3a7ffa4fc970ca9c
│   ├── info
│   └── pack
└── refs
    ├── heads
    └── tags
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

## HEAD

### Understanding HEAD pointer

HEAD is a **pointer to "tip"** (last commit) of our currently check-out branch in repository.

Git store reference where git HEAD is pointing to in `.git/HEAD` file

```bash
cat .git/HEAD
ref: refs/head/master
```

> [**`cat`** (concatenate)](https://www.geeksforgeeks.org/cat-command-in-linux-with-examples/) - very frequently command used in Linux. It reads data from the file and gives their content as output. It helps us to create, view, concatenate files.

```bash
.git
├── HEAD
├── config
├── description
├── hooks
│   ├── applypatch-msg.sample
│   ├── commit-msg.sample
│   ├── fsmonitor-watchman.sample
│   ├── post-update.sample
│   ├── pre-applypatch.sample
│   ├── pre-commit.sample
│   ├── pre-push.sample
│   ├── pre-rebase.sample
│   ├── pre-receive.sample
│   ├── prepare-commit-msg.sample
│   └── update.sample
├── info
│   └── exclude
├── objects
│   ├── info
│   └── pack
└── refs
    ├── heads
    └── tags
```

In [git principle video](https://www.dropbox.com/s/reb43ilf93gmpkz/git-local-principle.m4v?raw=1) from last lesson we saw than HEAD pointer is always assigned to last commit. Git use HEAD to point to a latest state of progress (tip) in branches.

We are still working only in MASTER branch of our project repository, but way how Git use HEAD is identical in each branch.

When we create and check into a new branch, Git will assign HEAD to commits on this branch. With progress head will be always assigned to latest commit in this branch. When we then switch back to MASTER branch, HEAD will be pointing to our last commit in MASTER branch.
[HEAD video](https://www.dropbox.com/s/y6wdyxks1xxnch3/git-HEAD.m4v?raw=1)
