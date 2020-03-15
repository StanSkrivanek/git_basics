# Taking data from remote repositories

## git pull

Pull **WILL APPLY MERGE** onto our project

git `pull` will **pull down from a remote** whatever you ask (so, whatever trunk you're asking for) **and instantly merge it into the branch you're in** when you make the request. Pull is a high-level request that runs `fetch` then a `merge` by default, or a rebase with `–rebase` parameter. You could do without it, it's just a convenience.

```bash
  git checkout localBranch
  git pull origin master
  git branch

  master
* localBranch

```

## git fetch

<!-- Fetch is similar to pull, except it won't do any merging. -->

Fetch take (pull out) **changes** from remote repository and place these changes into `.git` folder. When this changes (commits) are in `.git` folder we have access to them and we CAN use them in our project way we need. Main advantage is that **FETCH doesn't do MERGE**, this mean **fetch do NOT WRITE changes** to our project that can cause overwriting our code. This give us opportunity to merge changes from remote repository **into new branch**.

Git's `fetch` will have pulled down the "remoteBranch" and put it into a local branch called `remoteBranch`.
It creates a local copy of a remote branch which you **shouldn't manipulate directly**. Instead create a proper local branch and work on that. The `git checkout` has a confusing feature though.

**NOTE:** If you "checkout" a local copy of a remote branch, it creates a local copy and sets up a merge to it by default.

```bash
  git checkout localBranch
  git fetch origin remoteBranch
  git branch

master
* localBranch
remoteBranch
```

## git rebase

Finally, git rebase is pretty cool. Anything you've changed by committing to your current branch but are no in the upstream are saved to a temporary area, so your branch is the same as it was before you started your changes, IE, clean.

It then grabs the latest version of the branch from the remote If you do 'git pull –rebase', git will pull down the remote changes, rewind your local branch, then replays all your changes over the top of your current branch one by one, until you're all up to date. Awesome huh?

---

Place code **into** remote repository

## Git push

TODO: add text
