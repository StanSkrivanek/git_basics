# 04 | Blob

Previously I have mentioned word _**blob**_ very shortly. Now is time to take a closer look what **blob** is.

---

## WTF is blob

A simply said a **blob** is used to store file data, and it is generally a file.

A Git **blob** _(binary large object)_ is lowest level **object** type used **to store the contents** of each file snapshot **in a git repository**.

> **NOTE:** Important to remember is that **Git generated hash is based on file content** and **_not on file it self_**. This mean that two files with identical content will produce only one **blob** even that they will have different name or path.

In previous section we have learned basics about SHA-1 hash. Now, when SHA-1 hash for our staged snapshot is generated, Git will store it in a blob object together with other information about this snapshot.

`git show` `SHA-1 hash number`
[blob](http://shafiul.github.io/gitbook/1_the_git_object_model.html)

### How blob is created

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
~ mkdir blobs
~ cd blobs
```

Initiate git and show tree

```bash
~ git init
~ tree .git
```

In working area create file `first.txt` with string content `"File One"`

```bash
~ echo "File One" > first.txt
~ ls
```

Add file first.txt into _Staging_ area (memory)

```bash
~ git add first.txt
```

Check git objects folder

```bash
~ tree .git/objects
> .git/objects
  ├── 30
  │   └── 3ff981c488b812b6215f7db7920dedb3b59d9a
  ├── info
  └── pack
```

We can see than our Stashed file was stored in `git/object` folder. Git run SHA-1 on file snapshot, used hash's first two digits as sub-folder name and stored hash inside.

#### Git objects details

To get information about git object type and its content we can use command `git cat-file` followed by flag and hash number

use `cat-file` command with flag **`-t`** followed by hash to show **type** of file

- `git cat-file` **`-t`** `SHA hash`

```bash
~/desktop/blobs > git cat-file -t 303ff981c488b812b6215f7db7920dedb3b59d9a

> blob
```

We can use `cat-file` command with flag **`-p`** followed by hash to show file **content**

- `git cat-file` **`-p`** `SHA hash`

```bash
~/desktop/blobs > git cat-file -p 303ff981c488b812b6215f7db7920dedb3b59d9a

> File One
```

Check git status

```bash
~ git status

> On branch master

  No commits yet

  Changes to be committed:
    (use "git rm --cached <file>..." to unstage)
          new file:   first.txt"
```

Thats all we need to know about **blob**

---

### TODO

- [ ] blob creation and data types visualization
