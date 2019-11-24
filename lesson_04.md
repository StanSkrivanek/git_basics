# 04 | Blob

Previous lesson 01 I have mentioned word _**blob**_ very shortly Now is time to take a closer look what **blob** is.

---

## WTF is blob

A simply said a **blob** is used to store file data, and it is generally a file.

A Git **blob** _(binary large object)_ is lowest level **object** type used **to store the contents** of each file snapshot **in a git repository**.

---

## How blob is created

We already know that **Staging** is term used for placing our changes into memory with use of `git add`
When we decide to store our changes into Stashing Area (memory) Git will:

1. make snapshot of current content state of file('s) (with our changes)
2. run SHA-1 on data (content) to create unique hash
3. create object type **blob** with its unique hash
4. store required information in a **blob** object (SHA - 1 hash, data ...)
5. create sub-folder in `.git/objects` based on first two letters of hash
6. place encrypted blob (SHA-1 hash) into this sub-folder

**NOTE:** Take this description as non-technical and **very** brief

### Demonstration

Create a new project

```bash
~ cd desktop
~ desktop > mkdir blob
~ desktop > cd blob
```

Initiate git and show tree

```bash
~ desktop/blob > git init
~ desktop/blob > tree .git
```

In working area create file `first.txt` with string content `"File One"`

```bash
~ desktop/blob > echo "File One" > first.txt
~ desktop/blob > ls
```

Add file first.txt into _Staging_ area (memory)

```bash
~ desktop/blob > git add first.txt
```

Check git objects folder

```bash
~ desktop/blob > tree .git/objects

> .git/objects
  ├── 30
  │   └── 3ff981c488b812b6215f7db7920dedb3b59d9a
  ├── info
  └── pack
```

We can see than our _staged_ file was stored in `git/object` folder. Git run SHA-1 on file snapshot, used hash's first two digits as sub-folder name and stored hash inside.

> **NOTE:** Important to remember is that **Git generated hash is based on file content** and **_not on file it self_**. This mean that two files with identical content will produce only one **blob** even that they will have different name or path.

### Two files - One blob

```bash
~ cd desktop
~ desktop > mkdir twofiles
~ cd twofiles
~ desktop/twofiles > git init
~ desktop/twofiles > master > echo "hello" > first.txt
~ desktop/twofiles > master > ls
~ desktop/twofiles > master > tree .git/objects
~ desktop/twofiles > master > git add first.txt
~ desktop/twofiles > master > tree .git/objects
~ desktop/twofiles > master > echo "hello" > second.txt
~ desktop/twofiles > master > ls
~ desktop/twofiles > master > git add second.txt
~ desktop/twofiles > master > tree .git/objects
```

If you have followed these commands, result should be **only one blob**

```bash
.git/objects
├── ce
│   └── 013625030ba8dba906f756967f9e9ca394464a
├── info
└── pack
```

In previous section we have learned basics about SHA-1 hash. Now, when SHA-1 hash for our staged file snapshot is generated, Git will store it in a blob object .

`git show` `SHA-1 hash number`

[blob](http://shafiul.github.io/gitbook/1_the_git_object_model.html)

---

### TODO

- [ ] blob creation and data types visualization
