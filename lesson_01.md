# 01 | How Git works

---

## Areas

Git have 3 Areas:

- Working Area (untracked)
- Staging Area (in memory)
- Repository (stored)

For basic understanding of Git principles we will stay with these 3 main areas. There is also Stashing Area but we will talk about it a few lessons later.

### Working Area

At this stage Git do nothing, only monitoring and remembering our changes in code. We are coding and saving our changes in files as usual.
We can check these untracked changes with `git status`
We can check our changes with command `git diff`.

### Staging Area

When we are done with our changes we have to tell Git to add our changes into memory (cache) by command `git` `add`. Git will create a **blob** and place in it "snapshot" of the file's where changes were made. Beside this snapshot git will place into **blob** another useful data. We will talk about what **blob** is in detail later.

- If we would like to place into memory only changes in certain files we have to specify these files `git add filename` or `git add filename filename`

- If we would like to place into memory **all** files with changes we can use dot `.` Command will look like this `git add .`

in both cases Git will create _blob_ for each new snapshot.

By placing changes into memory, Git will know what changes are going to be part of the next commit.

**The staging area is how git knows what will change between the current commit and the next commit**.

### Repository

Once Git have **staged** snapshot of changes in memory we need to tell Git to store these changes into file on our computer by `git commit -m "descriptive message"`.

![image](https://www.dropbox.com/s/ars5fp4acwazrky/git_local_basics.png?raw=1)

[Git basics (video)](https://www.dropbox.com/s/juv012b573xqoc1/git_local_basics.m4v?raw=1)

When we execute commit command `git commit -m "message"` Git will store data, create referral to commit and also will create a **tree**. You can thing about a **tree** as a _"crossroad"_ to other objects. Again, we will talk about what tree is and what is its function in upcoming lessons.

<!-- > Git will add reference to **one commit** and **one tree** -->
