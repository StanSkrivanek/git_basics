# Git - lessons | 01

---

## Create project

- Using `mkdir`

```bash
~
cd desktop
~ / desktop > mkdir project_01
~ / desktop > cd project_01
```

now we have new project folder

## Git initialization

once we are inside out project folder we can start Git by `git` `init`

```bash
~ / desktop / project_01 > git init
```

## from now on Git will track all changes inside our project folder

---

## Create project & Git initialization (shortcut)

- Using only `git init` `project_name`

```bash
~ / desktop > git init project_01
~ / desktop> cd project_01
```

or

```bash
~ git init desktop/project_01
```

---

## Rename project

we can rename our project

**`mw`** `old name` `new name`

```bash
~ / desktop > mv project_01 newSite
```

---

## Delete

### Delete Git (.git)

by deleting `.git` folder from our project we will loose ALL uncommitted data

**`rf`** `-rf` `file_name`

```bash
~ / desktop / newSite > rm -rf .git
```

### Delete project

**`rf`** `-rf` `file_name`

```bash
~ / desktop > rm -rf project_01
```

---

## How Git works

Git have 3 Areas:
-Working Area (untracked)
-Staging Area
-Repository

### Working Area

We are coding and saving our changes as usual. At this stage Git do nothing, only monitoring and remembering our changes in code.

### Staging Area

When we are done with our changes in code we have tell Git to add our changes into memory (cache) by `git` `add`

If we would like to place into memory only certain file (or files) we have to specify these files `git add filename` `filename`

If we would like to place into memory **all** files we can use dot `.` Command will look like this `git add .`

Placing changes into memory Git will know what changes are going to be part of the next commit.
**The staging area is how git knows what will change between the current commit and the next commit**.

### Repository

Once Git have changes **staged** in memory we need to tell Git to write reference to these changes into file on our computer by git `commit -m "message"`

All our commits are stored in **`.git`** folder

![You will find Git principle video in class folder](https://www.dropbox.com/s/ars5fp4acwazrky/git_local_basics.png?raw=1)

[Git basic principle (video)](https://www.dropbox.com/s/juv012b573xqoc1/git_local_basics.m4v?raw=1)

---

## Git commands

`git` `init` - Git initialization
`git` `status` - Git status (staging/commit)
`git` `add` `file name` / `.` - adding to staging area (memory)
`git` `rm` `--cached` `file name` - removing from staging area (memory)
`git` `commit` `-m` `"message"` - adding changes to file on computer

`git` `log` `--oneline` - show all commits (one line overview)
