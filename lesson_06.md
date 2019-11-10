# 06 | HEAD

A Git **`HEAD`** is a **pointer** to current **branch** `AND` **tip** _(latest commit)_, of our branch we are currently working on.

---

## Understanding HEAD pointer

Git store reference where git **HEAD** is pointing at current stage of our project in `.git/HEAD` file

```bash
cat .git/HEAD
ref: refs/head/master
```

> [**`cat`** (concatenate)](https://www.geeksforgeeks.org/cat-command-in-linux-with-examples/) - command used very frequently in Linux. It reads data from the file and gives their content as output. It helps us to create, view, concatenate files.

```bash
.git
├── HEAD
├── config
├── description
├── objects
│   ├── info
│   └── pack
└── refs
    ├── heads
    └── tags
```

Git `HEAD` is a pointer referencing a latest state of progress (tip) in branches always assigned to last commit in given branch.

We are still working only in MASTER branch of our project repository, but way how Git use `HEAD` is identical in each branch.

We will come back to `HEAD` pointer in lesson about `branches`. We can also change where `HEAD` is points to, but we will talk about these manipulation a bit later.

### demonstration

- Create a new project
- initiate git
- add and commit one file

```bash
~/ cd desktop
~/desktop > mkdir headTest
~/desktop > cd headTest
~/desktop/headTest > git init
~/desktop/headTest > echo "Title 01" > one.txt
~/desktop/headTest > git add .
```

- commit

```bash
~/desktop/headTest > git commit -m "add first file"

> [master (root-commit) 177b7f0] add first file
 1 file changed, 1 insertion(+)
 create mode 100644 one.txt
```

we see that we are on `master` branch and our `root-commit` have hash `177b7f0`

- check git tree

```bash
~/desktop/headTest > tree .git

> .git
  ├── COMMIT_EDITMSG
  ├── HEAD
  ├── config
  ├── description
  ├── objects
  │   ├── 17
  │   │   └── 7b7f0d046edaf6da0903056631f0dc6d3f07ff // commit (yours will be different)
  │   ├── 34
  │   │   └── 0c6e4bb000c67b1bd6e284402edd0cf75ed165
  │   ├── 78
  │   │   └── 807a2a37fa6f08cacfcbf5759607f0e3ebc145
  │   ├── info
  │   └── pack
  └── refs
      ├── heads
      │   └── master
      └── tags
```

- check content of `.git/HEAD`

```bash
~/desktop/headTest > cat .git/HEAD

> ref: refs/heads/master
```

we see that HEAD hold reference (path) to a `master` object

- we can get value of `master` object

```bash
~/desktop/headTest > cat .git/refs/heads/master

> 177b7f0d046edaf6da0903056631f0dc6d3f07ff
```

Now we can confirm that **HEAD** refers to `master` branch object and hash of `master` corresponds with hash of latest commit. So we can say that `HEAD` hold `reference to` a current active `branch` **and** also to its latest `commit`
