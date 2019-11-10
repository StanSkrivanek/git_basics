# 06 | HEAD

A Git **`HEAD`** is a **pointer to "tip"** (last commit) of our currently check-out branch in repository.

---

## Understanding HEAD pointer

Git store reference where git HEAD is pointing to in `.git/HEAD` file

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

Git HEAD is pointer always assigned to last commit. Git use HEAD to point to a latest state of progress (tip) in branches.

We are still working only in MASTER branch of our project repository, but way how Git use HEAD is identical in each branch.

We will come back to `HEAD` pointer in lesson about `branches`. We can also change where HEAD is points to, but we will talk about these manipulation a bit later.
