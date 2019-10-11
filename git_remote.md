# Git and collaboration

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
