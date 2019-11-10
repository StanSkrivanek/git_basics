# 05 | Commit & Tree

When we make a commit of snapshots from staging area, Git will create a two new object types **commit** and **tree**.

---

## Tree

A **tree** is very simple object that contains referrals to blobs and/or other trees. Simply said git **tree** represent path to data (files) in directory and subdirectory structure. Its very similar to standard folders structure in any computer.

For example when we commit single file Git create **tree** that holds pointer to a **blob** and this **commit** will hold pointer to this **tree**

![one tree](https://www.dropbox.com/s/lsfooa1vgj3hdft/gitOneTree.jpeg?raw=1)

> **Each folder in our project will have its own tree, to hold map (pointers) to files or sub-folders**

When we stage a folder with file inside git will create a **two trees**. The first tree will point to blob and second to a tree thats belong to our project sub-folder. You can see simple demonstration in this [video](https://www.dropbox.com/s/3dsbjsv9m7dhe16/git_with_folder.m4v?raw=1)

As I have mentioned before **you can thing about git tree as crossroad** with signs to destination and these sign are referrals (pointers) to blobs (data)

---

## Committing

**commit** - confirm that changes in staged files (in memory) can be written into file(s) on computer.

Commit points to a tree and contains metadata as **author**, **committer** _(not always same person as author)_, **date/time**, **message** and hash to parent commit _(one or more)_

![commit metadata](https://www.dropbox.com/s/gro9fraorsxk4pa/gitCommitMeta.png?raw=1)

We commit files by command `git commit -m “descriptive message”`

When object type **_commit_** is created Git will run SHA-1. Created hash is based on all these data contained in commit object.

### root commit

When we are ready to save our snapshots of our changes from staging area we will use command **commit**. When we **committing** in our project for the **first time**, we will “initialize” our git repository, and git will refer to this first commit as **root-commit**.

![root commit](https://www.dropbox.com/s/k02owo5463h592l/git_referrals_basic.png?raw=1)

All new commits made after _root-commit_ will have the previous one as parent, they are all related to each-others.

[Two simple commits (video)](https://www.dropbox.com/s/kadv8rfr8btfart/two_simple_commits.m4v?raw=1)

### Why will commit have always different hash

There is one thing we should remember before we will talk about each object in detail:

> **SHA** for **blob** and **tree** should be **identical** for every user if data are identical, but **SHA** for **commit** will be for each user **different**.

We know that SHA-1 generate hash number that is directly related to content of data, therefore blob and tree can have an identical hash.

On other side commit hash will be **always** different for each user even if content of commit will be identical or don't change because metadata as name of user/committer and date/time will be always different.

> _different user_ and/or _different day/time_ **=** _different SHA-1 hash_

#### What does it mean

##### Time

Image that you are only user creating commits, so each commit hash will be different because will be created at different time (hr-min-sec)

##### Name of committer

We didn't talk about team work yet but imagine for a moment than you work in a team on one project. Now, even if each team member will create commit with identical content at the same time (that's very unlikely), there is another factor for creating unique hash and that is committers name.

---

### Message

Another common rule we should follow is writing your commit messages short and descriptive. Important is to write messages in **present** tense, that's because **commit message is about what committed change do** (Not what we did).

### Shortcut - add & commit

There is a shortcut do `add` and `commit` changes on **current** branch at once with command:
`git commit -a -m “descriptive message of changes”`.
**`-a`** = **`add`**

This mean `add` and `commit` will be made into branch you are currently in.
