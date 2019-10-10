# GIT - Version Control System

---

## Basics

### Git version

`git` `version` - _GIT version_

### Initializing Git

Once we are **in main project folder** we will **initialize Git** by command `git init`. When Git is initialized it will start tracking all our changes in project. Git will create “MASTER” branch. To check if its work type `git branch`. If we don't remember our branches we can use this command later to show all created branches.

When we have initialized `git` in our project folder we should create our first `branch` before we will do any changes. I we don't work in our `branch` all changes we will do will be applied into `MASTER` branch.

### Git setup

Before we will start using git we need to set our user name and email for fluent communication e.g. between Git on our computer and Github. If we do not provide those information Git will set them itself based on your computer setup. This automatic setting is not always reliable because we may use different settings (name & email) for Github.

These settings are important when we will work in the team, because our commits to project will contain also information who is the author of those commits.

#### user name

`git` `config` `--global` `user.name` `"Your Name"`

#### user email

make sure that email you will set is identical with email on your Github profile
`git` `config` `--global` `user.email` `"Your@mail.com"`

#### check

We can check our current setting by
`git` `config` `--global` `--list`

we can always change these global settings anytime

---

### Create a new Branch

To create a new branch we use command `branch` followed by our branch name.
If our next step in project will be adding website menu our command can looks like `git branch web_menu`

At this stage a new branch is created, but to be able to work on this version we need to switch into newly created branch.

### Move into branch

To **switch into** any **branch** we use command `checkout` . In our case to switch into our new branch command will be `git checkout web_menu`

### Create & Move into branch (shortcut)

There is shortcut to do two steps above _(Create & Move)_ in one command
`git checkout -b web_menu`

This code mean: go to branch **`checkout`**, but before you do that create for me a new brunch **`-b`** with this specific name **`web_menu`**.

Now a new branch will be created, initialized to watch our changes in code.

---

## STAGE & COMMIT

Once we make our changes we have to apply two commands. For basic use of Git, you don't need to understand what is going behind the scenes, this is an advanced topic. All you need to know that first we have to **`add`** our changes into memory and then **`commit`** _(assign)_ our changes into file(s).

We can edit more than one file at once when it make sense, e.g. add button in HTML with function call in index.html and javaScript function in main.js that's run on button.

But before you will be familiar with Git you should stick with editing one file at the time.

### STAGING - Adding changes into memory

To add our changes into memory we use command **`add`** and then we have two options what will be added into memory.

- to add all files _(if we make changes in more than one file)_ we will use **`.`** _(dot)_ => `git add .`
- to add only specific file we will use filename with its extension => `git add index.html`

After saving our files and staging in Git are our changes in memory and are ready to be printed into file. We can check our changes with command `diff` => `git diff`.

### COMMIT - writing changes into computer file

**commit** - confirm that changes in staged files (in memory) can be written into file(s) on computer.
We can commit files by command `git commit -m “descriptive message of changes”`

There is a shortcut do `add` and `commit` changes on **current** branch at once with command:
`git commit -a -m “descriptive message of changes”`.
**`-a`** = **`add`**

This mean `add` and `commit` will be made into branch you are currently in.

Another common rule we should follow is writing your commit messages short and descriptive. Important is than messages should be written in PRESENT tense, that's because commit comment is about what committed code do (Not what we did).

## Merge branches into MASTER

When we have our code written into file on the current branch, we can
merge branch with another. All we have to do is to **switch into a branch we want to merge INTO !!!**.

If you want to merge your changes from branch let say “menu” into “master” first we have to switch into master branch with the command `git checkout master`. Once in “master”, we can merge our branch menu by command `git merge source_branch` in this case, it will be `git merge menu`.

**NOTE:** We can of course merge e.g. _branch 2_ into _branch 1_ then delete _branch 2_ and later merge _branch 1_ into _branch MASTER_. **Whhhaaaaattttt 8)**

---

**NOTE:** Best practice is to do staging and commit very often. For example if you will add card into HTML page.

- create branch **_card_**
- in this branch create a basic html structure (skeleton) of the card
- stage branch
- add css classes (save file)
- stage branch
- commit branch
- create branch card_css
- set your style (save file)
- stage branch
- if you happy commit branch

---

## Delete branches

When branch is no longer needed we can delete it with command `git branch -d branch_name`

If you have for some reason created branch upfront and didn’t make any changes in it, \
sometime system doesn't delete this untouched branch. In this case we can use **FORCED** delete by typing \
`git branch -D branch_name`

---

## Git and collaboration

---

Get code **from** remote repository

## Clone - Pull - Fetch

### git clone

Git clone will clone a repo into a newly created directory. It’s useful for when you’re setting up your local doodah

```bash
  cd newfolder
  git clone git@<span class="skimlinks-unlinked">github.com:whatever/something.git</span>
  git branch

* master
remoteBranch
```

Git `clone` additionally **creates** a remote called `origin` for the repo cloned from, sets up a local branch based on the remote’s active branch (generally master), and creates remote-tracking branches for all the branches in the repo.

### git pull

git `pull` will **pull down from a remote** whatever you ask (so, whatever trunk you’re asking for) **and instantly merge it into the branch you’re in** when you make the request. Pull is a high-level request that runs `fetch` then a `merge` by default, or a rebase with `–rebase`. You could do without it, it’s just a convenience.

```bash
  git checkout localBranch
  git pull origin master
  git branch

  master
* localBranch

```

### git fetch

Fetch is similar to pull, except it won’t do any merging.

Git's `fetch` will have pulled down the "remoteBranch" and put it into a local branch called `remoteBranch`.
It creates a local copy of a remote branch which you **shouldn’t manipulate directly**. Instead create a proper local branch and work on that. The `git checkout` has a confusing feature though.

**NOTE:** If you "checkout" a local copy of a remote branch, it creates a local copy and sets up a merge to it by default.

```bash
  git checkout localBranch
  git fetch origin remoteBranch
  git branch

master
* localBranch
remoteBranch
```

### git rebase

Finally, git rebase is pretty cool. Anything you’ve changed by committing to your current branch but are no in the upstream are saved to a temporary area, so your branch is the same as it was before you started your changes, IE, clean. It then grabs the latest version of the branch from the remote If you do ‘git pull –rebase’, git will pull down the remote changes, rewind your local branch, then replays all your changes over the top of your current branch one by one, until you’re all up to date. Awesome huh?

---

Place code **into** remote repository

### Git push

---

## Basic Git Commands

These are common Git commands used in various situations:

**start a working area** (see also: git help tutorial)

- `init` Create an empty Git repository or reinitialize an existing one **\*\***
- `clone` Clone a repository into a new directory

**work on the current change** (see also: git help everyday)

- `add` Add file contents to the index **\*\***
- `mv` Move or rename a file, a directory, or a symlink
- `reset` Reset current HEAD to the specified state
- `rm` Remove files from the working tree and from the index

**examine the history and state** (see also: git help revisions)

- `bisect` Use binary search to find the commit that introduced a bug
- `grep` Print lines matching a pattern
- `log` Show commit logs - `show` Show various types of objects
- `status` Show the working tree status **\*\***

**grow, mark and tweak your common history**

- `branch` List, create, or delete branches **\*\***
- `checkout` Switch branches or restore working tree files **\*\***
- `commit` Record changes to the repository **\*\***
- `diff` Show changes between commits, commit and working tree, etc **\*\***
- `merge` Join two or more development histories together **\*\***
- `rebase` Reapply commits on top of another base tip
- `tag` Create, list, delete or verify a tag object signed with GPG

**collaborate** (see also: git help workflows)

- `fetch` Download objects and refs from another repository
- `pull` Fetch from and integrate with another repository or a local branch
- `push` Update remote refs along with associated objects

`git help -a` and `git help -g` list available subcommands and some
concept guides. See `git help <command>` or `git help <concept>`
to read about a specific subcommand or concept.
