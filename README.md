# Git

- [Git](#git)
  - [Introduction](#introduction)
    - [Snapshot](#snapshot)
    - [Working Flow](#working-flow)
      - [Working Directory](#working-directory)
      - [Staging Area](#staging-area)
      - [Repository](#repository)
  - [Actions](#actions)
    - [diff](#diff)
    - [rm](#rm)
    - [mv](#mv)
    - [reset](#reset)
  - [Issue](#issue)
  - [Commit](#commit)
    - [Verb](#verb)

## Introduction

Git 是一種分散式版本控制系統(**Distributed Version Control System**)。不同於集中式管理一切都是圍繞著 Server 進行操作，一旦集中式系統的伺服器中斷或毀損，專案檔案將無法存取或操作。

而 Git 採用分散式的設計，每一台主機的本地端都會保存一份完整的專案版本庫，即使沒有伺服器，也能進行版本管理與開發作業。

### Snapshot

可以看到，Git 使用的方式，每個版本都會進行一次快照，即使該檔案沒被更動，也還是會記錄一次在新的版本中。

![snapshot](../Git-new/images/snapshot-flow.jpg)

### Working Flow

#### Working Directory

首先，這個地方就是你的本機檔案。

接著你修改了檔案，本地已修改，Git 也知道你修改了，但是你必須進行 Snapshot 讓 Git 知道你要把當前的版本暫存起來。

```bash
git add <filename>
```

#### Staging Area

接著剛剛被快照的檔案會被放在這個暫存區中。
暫存區可以讓我們在要儲存到 Repository 的時候可以思考是否真的要放到儲存庫中。

舉例，Staging Area 有 Ａ、Ｂ、Ｃ 三個快照，但你的主管臨時說這次的更新只能有 A 跟 Ｂ，那你就可以只儲存 Ａ、B。

而我們一直用快照的概念是因為，對於 Git 來說你快照後，若繼續修改 A 或者是 Ｂ 的檔案，並不會影響到 Staging Area 的快照。

可以使用 `git status` 來確認當前暫存區的狀態

```bash
git status
```

![](../Git-new/images/file-flow.png)

若確定沒問題，則可以保存到 Repository 中。

```bash
git commit -m "your message"
```

![](../Git-new/images/first-commit.png)

#### Repository

在這個地方我們可以使用 `git log --oneline` 來查看目前所有的紀錄

```bash
git log --oneline
```

![](../Git-new/images/commits.png)

可以發現 `30e27b3` 就是剛剛 commit 的雜湊 ID

## Actions

### diff

比對本地版本和當前 Staging Area 的快照差異

```bash
git diff
git diff <filename>
```

比對最後一次 commit 的紀錄和當前在 Staging Area 的快照差異

```bash
git diff --staged
git diff --staged <filename>

```

### rm

從 Staging Area 移除該檔案的快照

```bash
git rm --cache <filename>
```

![](../Git-new/images/rm-cache.png)

注意！這個指令是會連同 Working Directory 也一併刪掉，並不是刪除快照

```bash
git rm <filename>
```

### mv

修改工作區的檔案名稱，並且在 Git 中標記為 `renamed`

此部分已提交至 Repository

```
//renameFile
This is second commit
```

接著在 Working Directory 修改為以下內容

```
//renameFile
This is third commit
```

並且改名至 file
![](../Git-new/images/mv.png)

我們可以發現對於 Git 來說，標記為改名後，實際上就是執行了以下的操作:

1. `mv <a> <b>`
2. `git rm <a>`
3. `git add <b>`

![](../Git-new/images/mv-info.png)

### reset

原本打算分兩次進行 commit，但是不小心也把 `images/mv.png`也放到 Staging Area

![](../Git-new/images/reset-1.png)

我們可以使用 `reset HEAD` 來讓快照從 Staging Area 退出。

```bash
git reset HEAD <filename>
```

可以看到 `images/mv.png` 的快照被移除了
![](../Git-new/images/reset-2.png)

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
