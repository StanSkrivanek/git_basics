# Git - lessons | 01

this is summary to for first lesson

---

## Create project and Git initialization

- Using `mkdir`

```bash
~
cd desktop
~ / desktop > mkdir project_01
~ / desktop > cd project_01
~ / desktop / project_01 > git init
```

- Using only `git init`

```bash
~ / desktop > git init project_01
~ / desktop> cd project_01
```

or

```bash
~ git init desktop/project_01
```

- Delete Project ( folder )
  **`rf`** `-rf` `file name`

```bash
~ / desktop > rm -rf project_01
```

- Rename Project
  **`mw`** `old name` `new name`

```bash
~ / desktop > mv project_01 newSite
```

## Git commands

`git` `init` - Git initialization
`git` `status` - Git status (staging/commit)
`git` `add` `file name` / `.` - adding to staging area (memory)
`git` `rm` `--cached` `file name` - removing from staging area (memory)
`git` `commit` `-m` `"message"` - adding changes to file on computer

`git` `log` `--oneline` - show all commits (one line overview)
