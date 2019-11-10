# 07 | Branch

## Branch

When Git is initiated it will create **first** branch and give it name **MASTER**. We do not want commit our changes into this branch directly for several reasons.

That is why Git give us option to create a new copy of project from last commit that is called **branch**. In new branch we can work on features for our a **new** project **version** independently on **MASTER** branch.

To create a new branch we use command `branch` followed by our branch name. If our next step in project will be adding website menu our command can looks like `git branch web_menu`

---

### Create branch

`git` `branch` `branch_name` - create a new branch

```bash
$ git branch menu
```

At this stage a new branch is created, but to be able to work on this version we need to switch into newly created branch.

### Move into branch

To **switch into** any **branch** we use command `checkout` . In our case to switch into our new branch command will be `git checkout web_menu`

`git` `checkout` `branch_name` - get into branch

```bash
$ git checkout web_menu
```

Once a new branch is created and initialized, git will start watch our changes in code and we can use Git commands to stage and commit our work progress as usual.

### Create & Move into branch (shortcut)

There is shortcut to do two steps above _(Create & Move)_ in one command
`git checkout -b web_menu`

This code mean: Hey Git, go to branch **`checkout`**, but before you do that you have to create this branch for me **`-b`** and give it name **`web_menu`**.

---

## Merge

Once we are done with new version of our project and everything works as we expected we can bring our features into any existing branch that in 90% cases is MASTER branch (MAIN PROJECT). We can merge one version (branch) with any other branch in our project.

### Merge into branch

Applying

`git` `merge` `branch_name` - merge branch

```bash
$ git merge menu
```

---

## Delete branch

`-d` - give a warning if branch is not already merged in
`-D` - force deletion

```bash
$ git branch -d branch_name
$ git branch -D branch_name
```

---

## Head and new branch

When we create and check into a new branch, Git will assign HEAD to commits on this branch. With progress head will be always assigned to latest commit in this branch. When we then switch back to MASTER branch, HEAD will be pointing to our last commit in MASTER branch.
[HEAD video](https://www.dropbox.com/s/y6wdyxks1xxnch3/git-HEAD.m4v?raw=1)
