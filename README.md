# Git

- [Git](#git)
  - [Introduction](#introduction)
    - [Snapshot](#snapshot)
  - [Issue](#issue)
  - [Commit](#commit)
    - [Verb](#verb)

## Introduction

Git 是一種分散式版本控制系統(**Distributed Version Control System**)。不同於集中式管理一切都是圍繞著 Server 進行操作，一旦集中式系統的伺服器中斷或毀損，專案檔案將無法存取或操作。

而 Git 採用分散式的設計，每一台主機的本地端都會保存一份完整的專案版本庫，即使沒有伺服器，也能進行版本管理與開發作業。

### Snapshot

可以看到，Git 使用的方式，每個版本都會進行一次快照，即使該檔案沒被更動，也還是會記錄在新的版本中。

ss
![snapshot](../Git-new/images/snapshot-flow.jpg)

## Issue

## Commit

Git commit 盡量為單一事件，也就是說，如果你為了做一個 User 的 CRUD，一定會安裝到套件，或是建立 utils，這時候，建議為以下:

```bash
git commit -m "build: install mysql2 for database connection"
git commit -m "feat: add db entrypoint"
git commit -m "feat: implement user model"
git commit -m "feat: implement user service"
git commit -m "feat: implement user controller"
git commit -m "feat: add user routes"
```

### Verb

| Verb     | Description       | Example                                         |
| -------- | ----------------- | ----------------------------------------------- |
| feat     | 新增功能          | feat: add API POST /user                        |
| fix      | 修復 bug          | fix: infinite loop when click submit button     |
| docs     | 修改、新增文件    | docs: describe flow how to implement            |
| revert   | 回退 commit       | revert: forgot adding ignore item in .gitignore |
| init     | 初始化專案        | init                                            |
| release  | 發佈版本          | realease: v0.0.1                                |
| merge    | 合併分支          | merge: feature/user                             |
| style    | 修改 coding style | style: replace two spaces to tab                |
| refactor | 重構程式碼        | refactor: simplify password hashing logic       |
| modify   | 修改內容          | modify: add dockerfile and .sql into .gitignore |
| build    | 安裝套件          | build: install dayjs for date formatting        |
