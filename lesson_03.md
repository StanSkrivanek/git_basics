# Git - lessons | 02

---

## Write - Stage - Commit

### - create project

- create project folder on desktop `mkdir`
- get inside project folder `cd`
- initiate Git `git init`

### - commit files

- create file index.html & style.css `touch`
- show list of files `ls`
- show changes `git status`
- add **index.html** into Git memory
- show changes `git status`
- add **style.css** into Git memory
- show changes `git status`
- create **first commit** `git commit -m "message"`
- show changes `git status`
- show log `git log`
- quit `q`

### - commit code

- open project in VSCode `code .`
- place template code inside html `!`
- show differences `git diff`
- quit `q`
- show changes `git status`
- create **second commit** `git commit -m "message"`
- show log `git log`
- quit `q`

---

### - add & commit code

- add `h1` into html
- show differences `git diff`
- add to memory `git add index.html`
- show log `git log` | no commit -> no changes
- add `p` with some text into html
- show changes `git status`
- add to memory `git add .`
- add second `p` with some text into html
- show differences `git diff`
- change `p` for `h2`
- show differences `git diff`
- add to memory `git add .`
- commit with wrong messsage `git commit -m "message"`

### - fix commit message

- check logs `git log` | OMG I've made mistake
- fix **last** commit`git commit --amend -m "correct message"`
