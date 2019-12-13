# 09 | Git diff and difftool

Git command `diff` is one stop shop if you need answer the question what's a difference between two elements as file, tree, blob, commit etc.

Command `git diff` can be used to show us the difference between the **version of a file in the working directory**, index and most recent commit.

Show changes between:

- between the working tree and the index or a tree
- between the index and a tree
- between two trees
- between two blob objects
- between two files on disk

---

**REMEMBER**
`diff` or `difftool` show changes between committed snapshots and/or snapshots in Index (staging area)

---

```bash
man git-diff
```

## Example project

```bash
~ cd desktop
~ desktop > mkdir stash
~ desktop > cd stash
~ desktop > git init
~ desktop/stash > master > echo "A" > first.txt
~ desktop/stash > master > git add .
~ desktop/stash > master > git commit -m "add first.txt"
~ desktop/stash > master > echo "B" > second.txt
~ desktop/stash > master > git status
```

Result

```bash
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        second.txt  //red

nothing added to commit but untracked files present (use "git add" to track)
```

If we will use `git diff` now we don't get any result back because we didn't make any changes in current files.

Lets do some changes to committed file `first.txt`. We can open file in our favorite text editor (in our case `VS Code`), `GNU nano` or `Vim`.

**NOTE:** `GNU nano` is text editor program run in terminal (linux,macOS)

---

### Install Vim on linux (ubuntu)

On linux is already preinstalled _lite_ version of `Vim` called `Vi`. We can use `Vi` as it is but lets install its advanced version `Vim`

1. update ubuntu - open favorite terminal and type

```bash
sudo apt-get update
```

2. install Vim

```bash
sudo apt-get install vim
```

### Edit file in Vim

<!-- Because we will be using `vimdiff` we will open file in Vim. -->

To open file in Vim we use command `vim` followed by path to our file. In our case file `first.txt` is in root directory, mean that file is not nested and path is just name of the file.

```bash
~ desktop/stash > master > vim first.txt
```

1. Once file is open in Vim to be able edit file we have to switch into `INSERT` mode by pressing letter `i`
2. after edit we have to escape from insert mode by `esc` key
3. switch to `command` mode with colon punctuation mark `:`
4. write changes with letter `w`
5. quit Vim by `q`

so our command in Vim after escaping `insert` mode will look like this `:wq`

---

### Use `git diff`

now we can check difference by using `git diff` command

```bash
~ desktop/stash > master > git diff
```

result

```bash
diff --git a/first.txt b/first.txt
index f70f10e..1ea4210 100644
--- a/first.txt
+++ b/first.txt
@@ -1 +1,3 @@
 A //original
+some changes in code // added code
```

But as you see this way of showing difference is not really human friendly.

We can read more about `git diff` when we type in terminal `man git-diff`.

IMPORTANT: **commit our changes**

### diff of two commits

As we saw `git diff` output doesn't say much about changes. To see comprehensive human readable comparison of two files we can use Git `difftool`.
[Git difftool](https://git-scm.com/docs/git-difftool)

```bash
git difftool <sha1> <sha2> -- path/to/file
```

```bash
git difftool <sha1> <sha2> -- first.txt
```

```bash
This message is displayed because 'diff.tool' is not configured.
See 'git difftool --tool-help' or 'git help config' for more details.
'git difftool' will now attempt to use one of the following tools:
kompare emerge vimdiff

```

### Set `vimdiff` as main `difftool`

There are some tools to show differences in more human friendly form. In our case we will use `vimdiff` that will show differences next to each other. But first let set this tool as default diff tool.

To set `vimdiff` globally use followed command in terminal. This command will add code into `.gitconfig` file

```bash
~ git config --global diff.tool vimdiff
```

Another way how to do it is edit `.gitconfig` file manually

1. open `.gitconfig` in Vim

```bash
vim ~/.gitconfig
```

2. add following lines into it

```bash
[diff]
        tool = vimdiff
```

---

### Customizing Vim - Color theme

We can customize Vim to our needs but this is not part of this course. We will only focus how to change Vim color theme.

1. because we have just install Vim, first we need to do is to create `.vimrc` file in our home directory.

2. once `.vimrc` file is created we can open it in our favorite text editor. We will use Vim

```bash
~ vim ~/.vimrc
```

3. Once `.vimrc` is open we will type customize Vim to our needs. To change color theme and turning on syntax highlighting we can place into `.vimrc` this text.

```bash
colorscheme murphy
syntax on
```

**NOTE:**
Customizing Vim is only our choice and does not have effect on Vim functionality.

On macOS we can find vim installation under `usr/share/vim/vim81/`.
`vim81` is folder of your current Vim version and can differ with your version. There is also `vimrc` file but **DO NOT EDIT THIS FILE**. We can find Vim color themes in `usr/share/vim/vim81/colors`

---

### Compare Last commit to its nearest Parent

Now we have set `vimdiff` as main `difftool`

For comparing two commits we can use SHA-1 where _sha1_ is latest commit and _sha2_ previous commit.

```bash
git difftool <sha1> <sha2> -- path/to/file
```

Easiest way to achieve same result we can use `HEAD`

```bash
git difftool HEAD HEAD^
```

`HEAD` - last commit
`HEAD^` - nearest (first) parent of last commit
`^` - caret

If we have more files edited in commit, we can specify to see changes in specific file.

```bash
git difftool HEAD HEAD^ -- <filename>
```

In our case we have two commits, both only for `first.txt` file. If there will be more files edited and we would like to see differences only in `first.txt` file, we can show diff between commits in `first.txt` like this.

```bash
git difftool HEAD HEAD^ -- first.txt
```

### Compare changes in INDEX to last commit

Lets add file `second.txt` to INDEX (staging area)

```bash
git add second.txt
```

We have change state of git by adding new file into INDEX but when we try to see diff between indexed file and latest commit we get no result back

```bash
git difftool
```

To get diff result we have to use flag `--cached` because our file is in index (cache)

```bash
git difftool --cached
```

### Compare changes in INDEX (staged area)

Let say that we have staged file but before committing we would like to edit this file again. The result of `git status` can be a bit confusing.

We have our `second.txt` in INDEX and we will make some changes to this staged file.

```bash
vim second.txt
```

We do some changes in `second. txt` , save them and quit Vim. Now see `git status`

We can see staged file `second.txt` (green) and **identical** file `second.txt` as modified (red)

```bash
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   second.txt  //green

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   second.txt  //red
```

As we know `difftool` show us changes between committed snapshots or snapshots in Index (staging area)

---

**IMPORTANT**
Now, when we use `difftool` result will be difference between **cached** and **modified** version of `second.txt` that is in `untracked area`

---

To see difference between last commit and snapshot(s) in INDEX we have to use `--cashed` operator

```bash
vim difftool --cached
```
