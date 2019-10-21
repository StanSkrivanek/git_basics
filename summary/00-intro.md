### GIT - Version Control System

Git is most popular (distributed) version control. This mean that each user maintain their own repositories, they do NOT work from a central repository as in SCCS, RCS, CVS and SVN (other past VCS). All the changes are stored as sets or patches, and we're focused on tracking changes, not the versions of the documents.

**NOTE:** Keep in mind that **Git and Github are** two platform with **different** purpose.

We can use Git on our local projects but Git is really shining is team work where more coders is working on one project.

Distributed version control is an important part of the Git architecture, and it's important to learn about it.

We'll talk more about how Git tracks and merges these sets of changes as we go forward. For now, you just should understand that there is no central repository that we all work from. All repositories are considered equal by Git.

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
