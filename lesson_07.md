# 07 | Branching

Before we will start talk about what branch is we should know what branching actually is.

---

Branching give us opportunity to step out from the project main line of development and continue to work on project changes or new features safely in a **new developing line**, without fear to introduce and implement mistakes into project **main line**.

## Git Branching

Git Branching system is unique compare to other VCS, is lightweight and incredibly fast. Making branch is almost instantaneous and switching between brunches is just as fast.

Because of this Git speed and simplicity we can branch and merge very often. Understanding and mastering this feature gives us a powerful and unique tool and can entirely change the way that we develop.

---

## Master branch

When Git is initiated it will for us create **first** branch and give it name **master**. This branch is **not** special by any means, its exactly like any other branch, so we can delete or rename it. Because common practice is that 90% developers keep is as it is I will stay with that too.

Because our **master** will be our project developing **main line** we do not want to make and commit our changes into this **master** branch directly. I have already mentioned then **master** should be always our fully functional project version.

That is why Git give us option to step out and create object called **branch**.

---

## Branch

### Create branch

To create a new branch we use command `branch` followed by our branch name. If we would like to work separately on website menu our command can look like `git branch web_menu`

`git` `branch` `branch_name` - create a new branch

```bash
~ git branch main_menu
```

At this stage a new branch is only created. To be able start to work in this _a new developing line_ we have to make this _branch_ active by switch into it.

### Switch to branch

In previous step we have created a new branch, to **switch** into this branch we use command `checkout` followed by `branch name`.

`git` `checkout` `branch_name` - get into branch

```bash
~ git checkout web_menu
```

Once a new branch is created and initialized, git will now watch our changes in this branch. Git commands to stage and commit our work progress will work as usual.

### Create & Move into branch (shortcut)

We can use shortcut to do these two steps above _(Create & Move)_ in one command
`git checkout -b web_menu`

This code mean: Hey Git, go to branch **`checkout`**, but before you do that you have to create this branch for me **`-b`** and give it name **`web_menu`**.

---

## Head and new branch

When we create and check into a new branch, Git will assign HEAD on this branch and contain pointer to last commit from `master` branch. Because commits hold pointers to its parent commit a new branch will have access to all commits from `master` branch.

[branch-HEAD video](https://www.dropbox.com/s/dhc6vo2wmyaku2p/branch-HEAD.m4v?raw=1)

With progress head will be always assigned to latest commit in this branch. When we then switch back to MASTER branch, HEAD will be pointing to our last commit in MASTER branch.

---

## Merge

Once we are done with new version of our project and everything works as we expected we can bring our features into any existing branch that in 90% cases is MASTER branch (MAIN PROJECT). We can merge one version (branch) with any other branch in our project.

### Merge into branch

Applying

`git` `merge` `branch_name` - merge branch

```bash
~ git merge menu
```

---

## Delete branch

`-d` - give a warning if branch is not already merged in
`-D` - force deletion

```bash
~ git branch -d branch_name
~ git branch -D branch_name
```
