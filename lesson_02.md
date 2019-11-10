# 02 | Write - Stage - Commit

This lesson is only practice how to work with most common Git commands
[Basic Git principle - local (video)](https://www.dropbox.com/s/qi6q35zq5l9oqdv/git_local_principle.m4v?raw=1)

---

## Practice Area

### Create a project

- Using `mkdir`

```bash
~/ cd desktop
~/desktop > mkdir project_01
```

now we have a new project folder

## Git initialization

When project folder is created, we have to initiate Git to be able start tracking our project. To do that we have to move inside our project folder.

```bash
~/desktop > cd project_01
```

once we are inside out project folder we can start Git by `git` `init`

```bash
~/desktop/project_01 > git init
```

from now on Git will track all changes inside our project folder.

---

## Create project & Git initialization (shortcut)

- Using only `git init` `project_name`

```bash
~/desktop > git init project_01
~/desktop > cd project_01
```

or

```bash
~ git init desktop > project_01
```

---

### Stage and commit

We will create first commit in project known also as _"root commit"_.

- create file index.html & style.css `touch`

```bash
~/desktop/project_01 > touch index.html style.css
```

- show list of files `ls`
- show changes `git status`
- add **index.html** into Git memory

```bash
~/desktop/project_01 > git add index.html
```

- show changes `git status`
- add **style.css** into Git memory

```bash
~/desktop/project_01 > git add style.css
```

- show changes `git status`
- create **first commit** `git commit -m "message"`

```bash
~/desktop/project_01 > git commit -m "Add files index.html & style css"
```

- show changes `git status`
- show log `git log`
- quit `q`

### Untracked changes

- place template code inside html by `!`
- show differences `git diff`
- quit `q`
- show changes `git status`

### Create a second commit

We had changed file index.html by adding basic code template. Now is time to save our changes and we do that with second commit

1. add changes into Staging area
2. create **second commit** `git commit -m "message"`

```bash
~/desktop/project_01 > git add index.html
~/desktop/project_01 > git commit -m "Add basic template into index.html "
```

- show log `git log`
- quit `q`

### Create a third commit

We create a new change in our project by adding some code into index.html and save these changes with third commit.

- add `h1` into html
- show differences `git diff`
- add to memory `git add index.html`

```bash
~/desktop/project_01 > git add index.html
```

- show log `git log` | no commit -> no changes
- add `p` with some text into html
- show changes `git status`
- add to memory `git add .`

```bash
~/desktop/project_01 > git add .
```

- add second `p` with some text into html
- show differences `git diff`
- change `p` for `h2`
- show differences `git diff`
- add to memory `git add .`

```bash
~/desktop/project_01 > git add .
```

- commit with deliberately wrong message `git commit -m "message"`

```bash
~/desktop/project_01 > git commit -m "Add style.css code"
```

### Fix commit message

If we commit changes with wrong message here is small tip how fix last commit message

- check logs `git log` | OMG I've made mistake
- fix **last** commit`git commit --amend -m "correct message"`

### Rename project

If we decide to rename our project we ca use command `mv`

**`mv`** `old name` `new name`

```bash
~/desktop > mv project_01 newSite
```

## Delete

As we know Git is storing all changes in `.git` folder. If we delete this folder from our project we will loose **ALL** uncommitted and/or not merged changes to a **Master** branch

### Delete Git (.git)

**`rf`** `-rf` `file_name`

```bash
~/desktop/newSite > rm -rf .git
```

### Delete project

We can also use `rf` command to remove any type of file, so we can remove whole project if needed.

```bash
~/desktop > rm -rf newSite
```

### Open in VSCode

We can open our project in VSCode using command `code .`

```bash
~/desktop/project_01 > code .
```

---

### Often used Git commands so far

- `git` `init` - Git initialization
- `git` `status` - Git status (staging/commit)
- `git` `diff` - Show difference (used in working area)
- `git` `add` `file name` / `.` - adding to staging area (memory)
- `git` `rm` `--cached` `file name` - removing from staging area (memory)
- `git` `commit` `-m` `"message"` - adding changes to file on computer
- `git` `log` `--oneline` - show all commits (one line overview)
