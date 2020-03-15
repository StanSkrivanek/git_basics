# 10 | Github

---

As we know from [Git Introduction](../lesson_00.md) lesson Git is a _**distributed**_ VCS this mean there is **no central repository** on which everyone depend on. Instead, each copy of **main** project repository behave as independent project we can work on.

Until now we have been working only with **local** projects thats mean then project was on our local machine. Git will reveal its whole power when we start to collaborate on project with other people.

Big companies may use for their main repositories own local dedicated server, but for many companies are _repository management services_ key component of collaborative development.

## Repository management services

Repository management service enable software developers to manage changes to the source code and related files, create and maintain multiple versions in one central place. Using these services brings numerous benefits even if you work in a small team or you are just a one man army. Use of _repository management services_ enables teams to move faster and preserve efficiency as they scale up.

## Github

There is several _repository management services_ but most popular are **GitHub**, **Bitbucket** or **GitLab**. In our feature classes we will work with **GitHub** as it is **free** of use, most popular and also largest Git based repository hosting platform with more than 38 million hosted projects.

[GitHub](https://github.com) | [Bitbucket](https://bitbucket.org/product) | [Gitlab](https://about.gitlab.com)

## Get project from remote repository

### Download repo

When we have our first repository on GitHub is time to bring our repo into our computer. There is a few ways how to get remote repo from GitHub onto our local machine. Easies way is to download compressed repository by clicking on "**Clone or download**" button and choose option "**Download ZIP**".

Main disadvantage of downloaded repository is **absence** of `.git` folder. All we get are **only the files from the most recent commit of the default branch**. This mean that we don't have access to repo history, commits etc. We also can't run git commands because there is no git initiated.

Of course that we can initiate git on downloaded repo in our computer later, but it will be only for our use. This mean that all commits will be relative only to downloaded repo on our local machine.

### Cloning repo

There is a better way how to get repo from GitHub onto our local machine. We can clone repo with command `clone`.

Git `clone` will literally clone a remote repo into place from where command was executed, in our case it will be specific place on our local machine.

```bash
  ~ > cd projects
  ~ projects > git clone git@github.com:whatever/something.git
  # ~ projects > project-repo-name > git branch

* master
# remoteBranch
```

Git `clone` additionally **creates** a remote called `origin` for the repo cloned from, sets up a local branch based on the remote’s active branch (generally master), and creates remote-tracking branches for all the branches in the repo.

## Create GitHub Repository

To be able use GitHub we need to create GitHub account. Once we have our account activated we can create a new repository.

1. get into your account and from top menu choose `repositories`
2. in repositories choose green button `NEW` (on top right )

Once "Create a new repository" form is open we choose repository name and optionally description. We will leave repository as `public`, check `README.md` file and create repo with "create repository button.
