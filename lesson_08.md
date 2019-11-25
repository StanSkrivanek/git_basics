# 08 | Stash

Storing untracked changes for later use

---

## What is Stashing

Stashing is used for storing changes or new ideas we work on but we don't want them to be a part of next commit. We can thing about Stashing placing ideas into drawer for later.

We can later pull out stashed material back from Stashing Area into Untracked Area to continue.

---

### Demo

```bash
~ cd desktop
~ desktop > mkdir stash
~ desktop > cd stash
~ desktop/stash > echo "A" > first.txt
~ desktop/stash > git add .
~ desktop/stash > git commit -m "add first.txt"
~ desktop/stash > echo "B" > second.txt
~ desktop/stash > echo "C" > third.txt
~ desktop/stash > git add second.txt
~ desktop/stash > git status
```

Now we should have identical output

```bash
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   second.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        third.txt

```

At this moment we have in our project "stash" one root commit _(first.txt)_, one staged file _(second.txt)_ and one untracked file _(third.txt)_

### View the Contents of the Staging Area

Under the hood, the staging area is a file that contains a list of files, as well as the SHA1 of the version that's in the repository.

Use `git ls-files -s` to view the `first.txt` file that we checked in previously. The SHA1 hash displayed points to the blob object - which contains the contents of the file.

```bash
$> git ls-files -s
100644 f70f10e4db19068f79bc43844b49f3eece45c4e8 0       first.txt
100644 223b7836fb19fdf64ba2d3cd6173c6a283141f78 0       second.txt
```

### Store in Stash directory

**Stashing** give us opportunity to **place our ideas/changes** into Stashing Area **from Staging area** or **Untracked area**.

### Stash from Staging area

Let say that we have worked on our project features and we have staged several changes in Staging area, suddenly will come client or project manager to see current state of our working project. At this moment we don't want to make commit because our work on features is in progress. We can move these unfinished changes into Stashing area to work on them later.

### Stash

#### `stash` - from Staging area (tracked files)

Use `git stash` to stash your uncommitted changes.

```bash
git stash save
```

At this moment we have only **one** staged file _(second.txt)_ If we have **staged** more snapshots, all will be **stashed**.

If we want to stash all snapshots we don't need to type default command `save`, git will automatically execute this command for us. All we need is:

```bash
git stash
```

---

#### `stash -u` Stash all tracked & untracked files (Working area)

Let's imagine when our project manager is coming we have beside changes in Staging area also some changes in Working area. As we already know git will recognize these as **untracked** files.

To stash **all** changes that are in **staging and working** area we will use command `stash` with use of flag `-u` for untracked snapshots.

```bash
git stash -u
```

After command with `-u` flag are stashed files from both (working and staging) areas

When we run command `git status` we will have clean working area (directory). Nothing will be in Staging Area.

#### Stash with message

Is always better to add descriptive message to stashed and /or untracked snapshot(s)

```bash
git stash save "descriptive message"
```

```bash
git stash save -u "descriptive message"
```

---

### Stash list

We can call list of snapshots stored in Stashing area with `list` flag
`WIP` - Work In Progress

```bash
git stash list
```

#### Show specific number of stashed snapshots

We can specify how many stashes we would like to show by use flag `-n`. THe argument `n` is number of stashes counted (and include) from last one

```bash
git stash list -3
```

#### Show content of stash

`stash@{n}` - show content of specific stash where `n` is stash number.

```bash
git stash show stash@{n}
```

---

### Call back from Stash Area

When we use command `apply` we will call back last stashed snapshot
NOTE: even after calling out snapshot from stashed area, snapshot will stay in stashed area

```bash
git stash apply
```

#### Call back specific stash

`apply stash@{n}` - call out specific stash, where `n` is stash number

```bash
git stash apply stash@{n}
```

---

### Give Stash message for easy reference

When we use standard command `git stash` git give us only SHA-1 pointer as description, that is not very useful when we come to stashed snapshots a few days or weeks later. We can assign to stash useful message to remember what changes we have worked on.

```bash
git stash save "descriptive message"
```

#### Call back & Delete from Stash

If we want to call out all stashed snapshots and delete them at once we will use command `pop`
The `pop` command will call out last stashed snapshot and delete it from Stashing area

```bash
git stash pop
```

---

### Delete Action

#### `drop` - Delete last or specific stash

When we call out lasts stash we can delete this stash. To do that we will use command `drop`
`drop` - delete last stash

```bash
git stash drop
```

We can use stash ID to delete specific stash `git stash drop 'stash ID'`

```bash
git stash drop stash@{n}
```

#### `clear` - Delete all stashed snapshots at once

We can delete all stashed file at once with command `clear`

```bash
git stash clear
```

---

### Start a new branch from a stash

We can create a new branch from **latest** stash. This command creates a new branch and then deletes the latest stash ( like stash pop).

```bash
git stash branch <branch name>
```

If we need a a branch from particular stash we can specify the stash ID after branch name.

```bash
git stash branch <branch name> stash@{n}>
```
