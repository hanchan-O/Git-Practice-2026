# 🎯 Git 实战使用指南（完整版）

> 从零开始掌握 Git 和 GitHub，包含完整流程、命令详解、多种场景处理和实战任务清单  
> **版本**: v6.1（远程分支管理版）  
> **最后更新**: 2026-03-12

---

## 📚 目录

1. [Git 基础概念](#1-git-基础概念)
2. [环境配置与初始化](#2-环境配置与初始化)
3. [完整工作流程](#3-完整工作流程)
4. [核心命令详解](#4-核心命令详解)
5. [命令对比与深度解析](#4-6-命令对比与深度解析-) ⭐⭐⭐
6. [分支管理与高级操作](#5-分支管理与高级操作)
7. [撤销与恢复操作](#6-撤销与恢复操作)
8. [远程仓库协作](#7-远程仓库协作)
9. [常见问题与解决方案](#8-常见问题与解决方案)
10. [实战任务清单](#9-实战任务清单) ⭐
11. [提交规范速查](#10-提交规范速查)
11. [实战问题解析](#11-实战问题解析) ⭐

---

## 1. Git 基础概念

### 1.1 什么是 Git？

**Git** 是一个**分布式版本控制系统**，就像一个"时光机"：
- ✅ 记录文件的每次修改历史
- ✅ 可以回退到任意历史版本
- ✅ 多人协作开发
- ✅ 创建分支进行并行开发

### 1.2 什么是 GitHub？

**GitHub** 是一个**代码托管平台**，就像一个"云端仓库"：
- ✅ 存储你的代码（远程仓库）
- ✅ 展示你的项目
- ✅ 与他人协作
- ✅ 构建技术身份

### 1.3 核心概念图解

```
工作区 (Working Directory)     你电脑上的文件
    ↓ git add
暂存区 (Staging Area)          准备提交的文件
    ↓ git commit
本地仓库 (Local Repository)    本地的 Git 数据库
    ↓ git push
远程仓库 (Remote Repository)   GitHub 上的仓库
```

**四个核心区域**：
1. **工作区**：你电脑上实际编辑文件的目录
2. **暂存区**：准备提交的文件临时存放区
3. **本地仓库**：本地的 Git 数据库（.git 文件夹）
4. **远程仓库**：GitHub 上的仓库

### 1.4 文件状态流转 
 
``` 
未跟踪 (Untracked)  
    ↓ git add 
已暂存 (Staged) 
    ↓ git commit 
已提交 (Committed) 
    ↓ 修改 
已修改 (Modified) 
    ↓ git add 
已暂存 (Staged) 
``` 
 
### 1.5 Git 三大区域详解 
 
``` 
┌─────────────────────────────────────────┐ 
│  仓库区 (Repository)                    │  ← 已保存的历史记录 
├─────────────────────────────────────────┤ 
│  暂存区 (Staging Area)                  │  ← 准备提交的"快照" 
├─────────────────────────────────────────┤ 
│  工作区 (Working Directory)             │  ← 你实际看到的文件 
└─────────────────────────────────────────┘
```

---

## 2. 环境配置与初始化

### 2.1 首次使用 Git 必须配置

```powershell
# 配置用户名（全局，只需配置一次）
git config --global user.name "你的 GitHub 用户名"

# 配置邮箱（必须与 GitHub 账号一致）
git config --global user.email "你的邮箱@example.com"

# 查看配置
git config --global --list

# 查看单个配置
git config --global user.name
git config --global user.email
```

### 2.2 配置凭证管理器（避免每次输入密码）

```powershell
# Windows 系统配置凭证管理器
git config --global credential.helper manager

# 或者使用 wincred
git config --global credential.helper wincred
```

### 2.3 配置中文显示（重要！）

```powershell
# 让 git status 显示中文而不是编码字符
git config --global core.quotepath false

# 配置编辑器为 VS Code
git config --global core.editor "code --wait"

# 配置默认分支名为 main
git config --global init.defaultBranch main
```

### 2.4 配置常用别名（提高效率）

```powershell
# 设置别名
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.lg "log --oneline --graph --all"
git config --global alias.lg2 "log --oneline --graph --decorate"

# 使用别名
git st      # 等同于 git status
git co      # 等同于 git checkout
git lg      # 等同于 git log --oneline --graph --all
```

---

## 3. 完整工作流程

### 3.1 从零开始的完整流程

#### 第一步：在 GitHub 创建仓库

1. **访问 GitHub**：https://github.com
2. **登录账号**
3. **创建新仓库**：
   - 点击右上角 "+" → "New repository"
   - Repository name: `Git-Practice-2026`
   - 选择 **Public**（公开）
   - ✅ 勾选 "Add a README file"
   - 点击 "Create repository"

---

#### 第二步：克隆到本地

```powershell
# 1. 进入工作目录
cd d:\AIcode\Github

# 2. 克隆远程仓库
git clone https://github.com/你的用户名/Git-Practice-2026.git

# 3. 进入项目目录
cd Git-Practice-2026

# 4. 查看当前状态
git status

# 5. 查看远程仓库地址
git remote -v
```

**预期输出**:
```
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

---

#### 第三步：创建项目结构并提交

```powershell
# 1. 创建目录结构
New-Item -ItemType Directory -Force -Path "01-学习笔记"
New-Item -ItemType Directory -Force -Path "02-代码示例"
New-Item -ItemType Directory -Force -Path "03-项目实战"

# 2. 创建文件
echo "# Git 学习笔记" > "01-学习笔记/Git 基础.md"
echo "这是 Git 基础学习笔记" >> "01-学习笔记/Git 基础.md"
echo "# 代码示例" > "02-代码示例/README.md"
echo "# 项目实战" > "03-项目实战/README.md"

# 3. 查看状态（查看有哪些新文件）
git status

# 4. 添加所有文件到暂存区
git add .

# 5. 再次查看状态（确认文件已暂存）
git status

# 6. 提交到本地仓库
git commit -m "初始化：创建项目目录结构和学习笔记"

# 7. 查看提交历史
git log --oneline
```

**预期输出**:
```
[main (root-commit) abc1234] 初始化：创建项目目录结构和学习笔记
 4 files changed, 6 insertions(+)
 create mode 100644 01-学习笔记/Git 基础.md
 create mode 100644 02-代码示例/README.md
 create mode 100644 03-项目实战/README.md
 create mode 100644 README.md
```

---

#### 第四步：推送到 GitHub

```powershell
# 首次推送，设置上游分支
git push -u origin main

# 如果提示输入凭证：
# Username: 输入你的 GitHub 用户名
# Password: 粘贴你的 Personal Access Token（不是密码）
```

**验证**:
1. 刷新 GitHub 仓库页面
2. 确认所有文件都已显示
3. 点击提交记录查看提交详情

---

### 3.2 每日工作流程

```powershell
# 早上开始工作
# 1. 拉取最新代码（确保是最新版本）
git pull

# 2. 编辑文件...（编写代码、写笔记等）

# 3. 查看修改（查看哪些文件被修改了）
git status

# 4. 查看具体修改内容（可选）
git diff

# 5. 添加修改到暂存区
git add .

# 6. 再次查看状态（确认）
git status

# 7. 提交到本地仓库
git commit -m "完成：今天的学习任务"

# 8. 推送到 GitHub
git push

# 9. 查看提交历史
git log --oneline -3
```

---

## 4. 核心命令详解

### 4.1 查看状态类命令

#### git status（最常用！）

```powershell
# 查看当前状态
git status

# 查看简洁状态
git status -s

# 查看未跟踪的文件
git status -u
```

**输出详解**:
```
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   README.md          # 新文件，已暂存
        modified:   src/index.js       # 修改的文件，已暂存

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
        modified:   package.json       # 修改的文件，未暂存

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .env                          # 新文件，未跟踪
```

---

#### git log（查看历史）

```powershell
# 查看完整历史
git log

# 查看简洁历史（推荐）
git log --oneline

# 查看图形化历史
git log --oneline --graph --all

# 查看最近 3 条
git log --oneline -3

# 查看某人的提交
git log --author="你的名字"

# 查看某个文件的修改历史
git log -- 文件名.md
```

---

#### git diff（查看差异）

```powershell
# 查看工作区与暂存区的差异
git diff

# 查看暂存区与最新提交的差异
git diff --staged

# 查看两个提交的差异
git diff commit1 commit2

# 查看某个文件的差异
git diff 文件名.md
```

---

### 4.2 添加与提交命令

#### git add（添加到暂存区）

```powershell
# 添加单个文件
git add README.md

# 添加多个文件
git add file1.md file2.md

# 添加整个目录
git add 目录名/

# 添加所有文件（最常用）
git add .

# 添加所有修改的文件（不包括新文件）
git add -u

# 添加所有文件（包括隐藏文件）
git add -A

# 交互式添加
git add -p
```

---

#### git commit（提交到本地仓库）

```powershell
# 基本提交
git commit -m "提交信息"

# 提交所有已跟踪的文件（跳过 git add）
git commit -a -m "提交信息"

# 修改上一次提交信息
git commit --amend -m "新的提交信息"

# 使用详细提交信息（会打开编辑器）
git commit

# 提交时跳过预提交钩子
git commit --no-verify
```

**提交信息规范**:
```
类型：简短描述

详细描述（可选）

- 修改点 1
- 修改点 2
```

---

### 4.5 推送与拉取进阶

#### upstream（上游分支）详解

**什么是 upstream？**
- upstream = 上游分支
- 本地分支与远程分支的关联关系
- 建立关联后，`git push` 和 `git pull` 会自动知道对应的远程分支

**首次推送分支**：
```powershell
# 方法 1: 完整写法
git push --set-upstream origin feature-login

# 方法 2: 简写（推荐）
git push -u origin feature-login

# 推送成功后，Git 会输出：
# Branch 'feature-login' set up to track remote branch 'feature-login' from 'origin'.
```

**建立关联后**：
```powershell
# 后续推送（直接）
git push

# 拉取远程变更
git pull
```

**查看 upstream 关联**：
```powershell
# 查看分支的 upstream
git branch -vv

# 输出示例：
# * feature-login    abc1234 [origin/feature-login] 新增：登录功能
#   main             def5678 [origin/main] 更新 README
```

**手动设置 upstream**：
```powershell
# 如果分支已经存在但没有 upstream
git branch --set-upstream-to=origin/feature-login feature-login
```

**取消 upstream**：
```powershell
git branch --unset-upstream feature-login
```

#### git push（推送到远程）

```powershell
# 首次推送，设置上游分支
git push -u origin main

# 后续推送（简化）
git push

# 推送所有分支
git push --all origin

# 强制推送（谨慎使用！）
git push -f

# 推送标签
git push --tags
```

---

#### git pull（从远程拉取）

```powershell
# 拉取并合并（最常用）
git pull

# 拉取并变基（推荐）
git pull --rebase

# 仅拉取，不合并
git fetch origin

# 查看远程分支
git fetch origin
git branch -r
```

---

### 4.4 分支管理命令

#### git branch（分支操作）

```powershell
# 查看所有本地分支
git branch

# 查看所有分支（包括远程）
git branch -a

# 查看当前所在分支
git branch --show-current

# 创建新分支
git branch feature-login

# 创建并切换分支
git checkout -b feature-login

# 切换分支（新版）
git switch feature-login

# 创建并切换分支（新版）
git switch -c feature-login

# 删除分支（已合并）
git branch -d feature-login

# 强制删除分支（未合并）
git branch -D feature-login

# 重命名分支
git branch -m old-name new-name

# 查看分支的最后提交
git branch -v
```

**分支操作常见问题**：

**Q1: 切换分支时提示 "changes would be overwritten"**
```powershell
# 错误信息：
error: Your local changes to the following files would be overwritten by checkout:
  file.txt

# 解决方案 1: 先提交更改
git add .
git commit -m "保存工作"
git checkout <分支>

# 解决方案 2: 暂存更改
git stash
git checkout <分支>
git stash pop

# 解决方案 3: 强制切换（会丢失更改！）
git checkout -f <分支>
```

**Q2: 删除分支时提示 "not fully merged"**
```powershell
# 错误信息：
error: The branch 'feature/xxx' is not fully merged.

# 解决方案 1: 先合并再删除
git checkout main
git merge feature/xxx
git branch -d feature/xxx

# 解决方案 2: 强制删除（谨慎使用！）
git branch -D feature/xxx
```

---

#### git merge（合并分支）

```powershell
# 切换到目标分支
git checkout main

# 合并功能分支
git merge feature-login

# 查看合并历史
git log --oneline --graph --all
```

---

## 5. 分支管理与高级操作

### 5.1 分支命名规范

```
main/master     - 主分支（生产环境）
develop         - 开发分支
feature-xxx     - 功能分支（如：feature-login）
bugfix-xxx      - Bug 修复分支（如：bugfix-memory-leak）
release-x.x.x   - 发布分支（如：release-1.0.0）
hotfix-xxx      - 紧急修复分支（如：hotfix-security）
```

### 4.6 命令对比与深度解析 ⭐⭐⭐

本节详细对比 Git 中容易混淆的命令，帮助你理解每个命令的适用场景。

---

#### 4.6.1 git restore vs git reset vs git checkout - 撤销修改三部曲

**问题**：这三个命令都可以用来"撤销"修改，但作用完全不同！**

##### 核心概念：三区域模型

```
┌─────────────────────────────────────────────────────────────┐
│  Git 三大区域                                                │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   工作区 (Working Directory)   ← 你眼睛看到的文件             │
│           ↓ git add                                        │
│   暂存区 (Staging Area)       ← 准备提交的"待确认"区域        │
│           ↓ git commit                                  │
│   仓库区 (Repository)         ← 已保存的历史记录              │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

**记住**：
- **工作区** = 你正在编辑的文件
- **暂存区** = 准备提交的文件（已 git add）
- **仓库区** = 已提交的历史（已 git commit）

---

##### 命令对比表

| 命令 | 作用区域 | 作用 | 场景 |
|------|----------|------|------|
| `git restore <文件>` | **工作区** | 用仓库的最新提交覆盖工作区 | 撤销工作区的修改 |
| `git restore --staged <文件>` | **暂存区** | 把文件从暂存区移回工作区 | 撤销 git add |
| `git reset HEAD <文件>` | **暂存区** | 同上，撤销 git add（旧语法） | 撤销 git add |
| `git checkout -- <文件>` | **工作区** | 同 git restore（旧语法） | 撤销工作区修改 |

---

##### 详细解析

**场景 1：工作区修改了文件，想撤销**

```powershell
# 你修改了文件，但还没有 git add
# 文件状态：Changes not staged for commit

# 查看状态
git status
# Changes not staged for commit:
#   modified: README.md

# 撤销工作区修改（恢复到上次提交的状态）
git restore README.md

# 或者用旧语法
git checkout -- README.md

# 结果：文件回到上次提交的状态
git status
# nothing to commit, working tree clean
```

**❌ 错误做法**：
```powershell
# 错误！git reset 是操作暂存区的，不能撤销工作区修改
git reset HEAD README.md
# 这个命令对工作区修改无效！
```

---

**场景 2：文件已 git add，想撤销**

```powershell
# 你执行了 git add，文件进入暂存区
# 文件状态：Changes to be committed

git add README.md
git status
# Changes to be committed:
#   new file:   README.md

# 撤销暂存（把文件从暂存区移回工作区）
git restore --staged README.md

# 或者用旧语法
git reset HEAD README.md

# 结果：文件回到工作区，但修改还在
git status
# Changes not staged for commit:
#   new file:   README.md
```

---

**场景 3：既想撤销 git add，又想撤销工作区修改**

```powershell
# 完整撤销：回到上次提交的状态
git restore --staged README.md  # 第一步：撤销暂存
git restore README.md           # 第二步：撤销工作区修改

# 或者一步到位（用 git checkout）
git checkout HEAD -- README.md
```

---

**场景 4：想撤销提交**

```powershell
# 撤销最后一次提交（保留修改在工作区）
git reset --soft HEAD^

# 撤销最后一次提交（保留修改在暂存区）
git reset --mixed HEAD^  # 默认就是这个

# 撤销最后一次提交（完全丢弃修改！）
git reset --hard HEAD^  # ⚠️ 危险！不可恢复！
```

---

#### 4.6.2 git checkout vs git switch - 切换分支

**问题**：git checkout 既能切换分支，又能撤销修改，到底是用来干嘛的？

##### 命令对比

| 命令 | 用途 | 适用对象 |
|------|------|----------|
| `git checkout <分支>` | 切换到指定分支 | 分支操作 |
| `git checkout -b <分支>` | 创建并切换到新分支 | 分支操作 |
| `git checkout -- <文件>` | 撤销文件修改 | 文件操作 |
| `git switch <分支>` | 切换到指定分支（仅限分支） | 分支操作（新版） |
| `git switch -c <分支>` | 创建并切换到新分支 | 分支操作（新版） |

##### 为什么有两个命令？

- **git checkout**：老命令，功能多（分支+文件），但容易混淆
- **git switch**：Git 2.23+ 新增的命令，专门用于分支操作，更清晰

##### 推荐

```powershell
# ✅ 推荐：使用 git switch（更清晰）
git switch main              # 切换到 main
git switch -b feature-login  # 创建并切换到新分支

# ⚠️ 谨慎：git checkout 两种用途
git checkout main            # 切换分支
git checkout -- README.md    # 撤销文件修改 ← 容易混淆
```

---

#### 4.6.3 git merge vs git rebase - 合并分支

**问题**：两个命令都能合并分支，有什么区别？

##### 核心区别

| 命令 | 特点 | 提交历史 | 适用场景 |
|------|------|----------|----------|
| **git merge** | 保留完整历史 | 产生合并提交 | 团队协作、公共分支 |
| **git rebase** | 线性历史 | 不产生合并提交 | 个人分支整理 |

##### 图解对比

**git merge（产生分叉）**：
```
A---B---C---M---main
     \         /
      D---E---F---feature
```
- 保留完整历史
- 有一个合并提交 M

**git rebase（线性历史）**：
```
A---B---C---D---E---F---main
                           (feature 先 D-E-F 再 rebase)
```
- 历史是一条线
- 没有合并提交
- ⚠️ 不要对公共分支使用！

##### 什么时候用哪个？

```powershell
# ✅ 使用 merge：合并功能分支到主分支
git checkout main
git merge feature-login
# 产生清晰的合并记录

# ✅ 使用 rebase：整理个人开发分支
# 假设你在 feature 分支开发，main 有新提交
git checkout feature-login
git rebase main
# 把 feature 的基础从 C 移到最新的 main

# ❌ 永远不要对公共分支（main）使用 rebase！
# 这会修改公共历史，影响其他人
```

---

#### 4.6.4 git pull vs git fetch - 拉取代码

**问题**：git pull 和 git fetch 都能获取远程更新，有什么区别？

##### 对比

| 命令 | 作用 | 特点 |
|------|------|------|
| `git fetch` | 下载远程更新 | **不合并**到本地 |
| `git pull` | 下载并合并 | **自动合并**到本地 |

##### 图解

```
git fetch:
  远程: origin/main (新提交)
         ↓ 下载
  本地: origin/main (本地副本更新)
         ↓ 需要手动
  本地: main (不变)

git pull:
  远程: origin/main (新提交)
         ↓ 下载 + 合并
  本地: main (自动更新)
```

##### 什么时候用哪个？

```powershell
# ✅ 使用 git pull：快速同步（最常用）
git pull

# ✅ 使用 git fetch + merge：更安全的做法
git fetch origin              # 只下载
git merge origin/main         # 再合并
git diff main origin/main    # 先查看差异

# ✅ 使用 git fetch + rebase：保持线性历史
git fetch origin
git rebase origin/main
```

---

#### 4.6.5 git stash 的使用场景

**问题**：什么时候需要暂存工作？

##### 使用场景

```powershell
# 场景 1：临时切换分支，但不想提交当前工作
# 你在 feature 分支开发到一半，需要紧急切换到 main 修 bug
git stash                    # 暂存当前工作
git checkout main
# ... 修 bug ...
git checkout feature
git stash pop                # 恢复工作

# 场景 2：拉取远程更新，但本地有冲突
git stash                    # 先暂存
git pull                     # 拉取远程
git stash pop                # 恢复并解决冲突

# 场景 3：想查看某个分支的干净状态
git stash
git checkout other-branch
# ... 查看 ...
git checkout original-branch
git stash pop
```

##### stash 命令详解

```powershell
git stash                    # 暂存当前工作（未跟踪的文件不会暂存）
git stash -u                 # 暂存包括未跟踪的文件
git stash push -m "描述"    # 暂存并添加描述
git stash list              # 查看所有暂存
git stash pop                # 恢复最近的暂存（并删除）
git stash apply              # 恢复最近的暂存（不删除）
git stash drop               # 删除最近的暂存
git stash clear              # 清空所有暂存
```

---

#### 4.6.6 git rm 的三种模式

**问题**：git rm、git rm --cached、git rm -f 有什么区别？

##### 对比

| 命令 | 删除位置 | 文件状态 | 场景 |
|------|----------|----------|------|
| `git rm <文件>` | 工作区 + 仓库 | 文件被删除 | 彻底删除文件 |
| `git rm --cached <文件>` | 仅仓库 | 文件保留在本地 | 不想跟踪但保留本地 |
| `git rm -f <文件>` | 工作区 + 仓库 | 强制删除 | 删除已修改的文件 |

##### 详细示例

```powershell
# 场景 1：彻底删除文件（本地和 Git 都删除）
git rm big-file.zip
# 工作区：文件删除
# 暂存区：删除操作已暂存
# 提交后：Git 也不再跟踪

# 场景 2：仅从 Git 移除（保留本地文件）
git rm --cached big-file.zip
# 工作区：文件保留
# 暂存区：移除跟踪操作已暂存
# 提交后：Git 不再跟踪，但本地文件还在
# 常用于：.gitignore 生效前已跟踪的文件

# 场景 3：强制删除（删除修改过的文件）
git rm -f important.txt
# 即使文件有修改，也强制删除
```

---

#### 4.6.7 git branch 的多种用法

##### 常用命令一览

```powershell
# 查看分支
git branch                    # 本地分支
git branch -r                 # 远程分支
git branch -a                # 所有分支
git branch -v                # 查看分支最后提交
git branch -vv               # 查看分支 upstream 关联

# 创建分支
git branch feature-login      # 创建但不切换
git checkout -b feature-login  # 创建并切换
git switch -c feature-login     # 新版：创建并切换

# 删除分支
git branch -d feature-login    # 删除（已合并）
git branch -D feature-login   # 强制删除（未合并）

# 重命名分支
git branch -m old-name new-name
```

---

### 5.2 分支开发流程

```powershell
# 1. 从主分支创建功能分支
git checkout main
git pull
git checkout -b feature-new-feature

# 2. 在功能分支上开发
# ... 编写代码 ...
git add .
git commit -m "新增：新功能模块"

# 3. 合并回主分支
git checkout main
git merge feature-new-feature

# 4. 删除功能分支
git branch -d feature-new-feature

# 5. 推送到远程
git push
```

### 5.3 解决合并冲突

**冲突产生时**:
```powershell
# 1. 查看冲突文件
git status

# 2. 打开冲突文件，会看到冲突标记
# <<<<<<<<< HEAD
# 你的修改
# =======
# 其他人的修改
# >>>>>>> feature-branch

# 3. 手动编辑，保留需要的内容，删除冲突标记

# 4. 标记冲突已解决
git add 冲突文件.md

# 5. 完成合并
git commit -m "合并：解决冲突"

# 6. 如果合并失败，可以取消合并
git merge --abort
```

---

## 6. 撤销与恢复操作

### 6.1 撤销工作区修改

```powershell
# 撤销单个文件的修改
git checkout -- 文件名.md

# 或者使用新命令
git restore 文件名.md

# 撤销所有修改（危险！）
git checkout -- .
```

---

### 6.2 撤销暂存区

```powershell
# 从暂存区移除单个文件
git restore --staged 文件名.md

# 或者使用旧命令
git reset HEAD 文件名.md

# 从暂存区移除所有文件
git reset HEAD
```

---

### 6.3 撤销提交

```powershell
# 撤销最后一次提交（保留修改）
git reset --soft HEAD^

# 撤销最后一次提交（丢弃修改，危险！）
git reset --hard HEAD^

# 撤销最近 3 次提交（保留修改）
git reset --soft HEAD~3

# 创建新提交来撤销（安全方式）
git revert <提交哈希>
```

---

### 6.4 暂存工作

```powershell
# 暂存当前工作
git stash

# 暂存并命名
git stash push -m "临时保存的工作"

# 查看暂存列表
git stash list

# 恢复最近的暂存
git stash pop

# 恢复指定暂存
git stash apply stash@{1}

# 删除暂存
git stash drop stash@{1}

# 清空所有暂存
git stash clear
```

---

## 7. 远程仓库协作

### 7.1 远程仓库管理

```powershell
# 查看远程仓库
git remote -v

# 查看远程仓库详细信息
git remote show origin

# 添加远程仓库
git remote add origin https://github.com/用户名/仓库名.git

# 修改远程仓库地址
git remote set-url origin https://github.com/新用户名/仓库名.git

# 移除远程仓库
git remote remove origin

# 重命名远程仓库
git remote rename origin upstream
```

---

### 7.2 远程分支管理

**为什么本地看不到其他分支？**

```
本地分支（git branch）：
* main

远程分支（git branch -r）：
  remotes/origin/main       ← GitHub 的 main
  remotes/origin/test        ← GitHub 的 test
  remotes/origin/user-login  ← GitHub 的 user-login
```

| 概念 | 说明 |
|------|------|
| **本地分支** | 你电脑上的分支（如 main、feature-xxx） |
| **远程分支** | GitHub 上的分支的引用（只读） |

**为什么这样设计？**
- 节省空间：不需要把远程所有分支都下载到本地
- 按需获取：只用的时候再创建本地分支
- 安全：避免不小心在本地操作远程分支

#### 查看远程分支

```powershell
# 查看本地分支
git branch

# 查看远程分支（仅远程）
git branch -r

# 查看所有分支（包括本地和远程）
git branch -a

# 查看分支详情（包括 upstream 关联）
git branch -vv
```

#### 创建远程分支

**方法 1：本地创建并推送**（最常用）
```powershell
# 1. 创建本地分支
git checkout -b feature-new

# 2. 推送到远程（自动创建远程分支）
git push -u origin feature-new

# -u 参数：建立 upstream 关联，之后可以直接 git push
```

**方法 2：直接创建远程分支**
```powershell
# 不需要本地有分支，直接推送
git push origin local-branch:remote-branch

# 例如：把本地的 main 推送到远程叫 new-branch
git push origin main:new-branch
```

#### 删除远程分支

```powershell
# 删除远程分支（GitHub 上的分支）
git push origin --delete test

# 或者用简写
git push origin -d test

# 删除后，远程的 test 分支就没了
```

#### 拉取远程分支到本地

```powershell
# 方法 1：创建本地分支并关联远程分支
git checkout -b test origin/test

# 方法 2：或者用新版命令
git switch -c test origin/test
```

---

### 7.3 Pull Request 流程

**步骤 1：创建功能分支**
```powershell
git checkout -b feature-practice
```

**步骤 2：开发功能**
```powershell
# ... 编写代码 ...
git add .
git commit -m "新增：PR 练习功能"
```

**步骤 3：推送到 GitHub**
```powershell
git push -u origin feature-practice
```

**步骤 4：在 GitHub 创建 PR**
1. 访问 https://github.com/你的用户名/仓库名/pulls
2. 点击 "New pull request"
3. 选择 base: main, compare: feature-practice
4. 填写 PR 标题和描述
5. 点击 "Create pull request"

**步骤 5：Code Review**
- 在 GitHub 网页查看文件变更
- 添加评论
- 请求他人审查

**步骤 6：合并 PR**
- 点击 "Merge pull request"
- 确认合并

**步骤 7：本地同步**
```powershell
git checkout main
git pull
git branch -d feature-practice
```

---

## 8. 常见问题与解决方案

### ❌ 问题 1: 中文文件名乱码

**现象**: `git status` 显示 `\345\222\214` 而不是中文

**解决方案**:
```powershell
git config --global core.quotepath false
```

---

### ❌ 问题 2: 推送时需要 Token

**解决方案**:
1. 访问 https://github.com/settings/tokens
2. 点击 "Generate new token (classic)"
3. 配置：
   - Note: `我的第一个 Token`
   - Expiration: `90 days`
   - 勾选：✅ repo
4. 点击 "Generate token"
5. 复制 Token（只显示一次！）
6. 推送时粘贴 Token

---

### ❌ 问题 3: GitHub 502 错误

**错误信息**:
```
fatal: unable to access 'https://github.com/...': The requested URL returned error: 502
```

**解决方案**:
- 等待几分钟后重试
- 检查 GitHub 状态：https://www.githubstatus.com/
- 切换网络环境

---

### ❌ 问题 4: 合并冲突

**解决方案**: 参考 5.3 节

---

### ❌ 问题 5: 忘记切换分支

**解决方案**:
```powershell
# 1. 暂存当前修改
git stash

# 2. 切换到正确的分支
git checkout feature-xxx

# 3. 恢复修改
git stash pop

# 4. 提交
git add .
git commit -m "新增：新功能"
```

---

### ❌ 问题 6: 提交了错误的文件

**解决方案**:
```powershell
# 情况 1：还未 push
git reset --soft HEAD^
# 修改文件后重新提交
git add .
git commit -m "正确的提交信息"

# 情况 2：已经 push
# 创建新提交来修复
git add 正确的文件
git commit -m "修复：删除错误文件"
git push
```

---

### ❌ 问题 7: 非快进更新被拒绝

**错误信息**:
```
! [rejected]        main -> main (non-fast-forward)
```

**解决方案**:
```powershell
# 方法 1：先拉取再推送
git pull --rebase
git push

# 方法 2：强制推送（谨慎！）
git push -f
```

---

### ❌ 问题 8: git rm 失败

**现象**: `git rm` 报错 "pathspec did not match any files"

**原因**: 路径不正确或文件不存在

**解决方案**:
```powershell
# 1. 使用完整路径（包含引号）
git rm "目录/文件名.md"

# 2. 检查文件是否存在
git status

# 3. 对于已删除的文件，使用 git add 添加删除操作
git add "已删除的文件.md"
```

---

### ❌ 问题 9: git reset HEAD 失败

**现象**: `git reset HEAD` 失败

**原因**: 路径包含空格或中文

**解决方案**:
```powershell
# 1. 使用引号包裹路径
git reset HEAD "包含空格的文件.md"

# 2. 使用相对路径
git reset HEAD "目录/文件.md"
```

---

### ❌ 问题 10: git add 失败

**现象**: `git add` 失败

**原因**: 路径解析错误

**解决方案**:
```powershell
# 1. 使用引号
git add "文件名.md"

# 2. 使用正斜杠（即使在 Windows 上）
git add "目录/文件.md"

# 3. 检查文件是否存在
ls "目录/文件.md"
```

---

### ❌ 问题 11: 本地看不到远程分支

**现象**:
```
git branch
* main
# 只看到 main，其他远程分支呢？
```

**原因**:
- 远程分支是独立的引用，不会自动下载到本地
- 需要手动创建本地分支来跟踪远程分支

**解决方案**:
```powershell
# 查看所有分支（包括远程）
git branch -a

# 创建本地分支并关联远程分支
git checkout -b test origin/test

# 或者用新版命令
git switch -c test origin/test
```

---

### ❌ 问题 12: 删除远程分支

**命令**:
```powershell
# 删除远程分支
git push origin --delete test

# 或者简写
git push origin -d test
```

---

### ❌ 问题 13: 推送失败 - 没有上游分支

**错误信息**:
```
fatal: The current branch xxx has no upstream branch.
```

**解决方案**:
```powershell
# 首次推送时设置 upstream
git push -u origin branch-name
```

---

## 9. 实战任务清单 ⭐

### 📋 任务概览

| 任务 | 主题 | 核心技能 | 预计时间 | 难度 |
|------|------|----------|----------|------|
| **Task 1** | 环境配置 | 配置、初始化 | 10 分钟 | ⭐ |
| **Task 2** | 从零创建项目 | clone、add、commit、push | 15 分钟 | ⭐ |
| **Task 3** | 文件管理 | status、diff、rm、mv | 15 分钟 | ⭐⭐ |
| **Task 4** | 分支开发 | branch、checkout、merge | 20 分钟 | ⭐⭐ |
| **Task 5** | 撤销操作 | reset、revert、stash | 15 分钟 | ⭐⭐⭐ |
| **Task 6** | 冲突解决 | merge conflict | 20 分钟 | ⭐⭐⭐ |
| **Task 7** | 远程协作 | fetch、pull、PR | 25 分钟 | ⭐⭐⭐ |
| **Task 8** | 综合实战 | 完整流程 | 30 分钟 | ⭐⭐⭐⭐ |
| **Task 9** | 分支管理进阶 | upstream、推送、同步 | 25 分钟 | ⭐⭐⭐⭐ |
| **Task 10** | 命令对比训练 | restore/reset/checkout/switch | 30 分钟 | ⭐⭐⭐⭐⭐ |

---

### Task 1: 环境配置与初始化

**目标**: 完成 Git 的初始配置，为后续练习做准备。

**验收标准**:
- [ ] 配置用户名和邮箱
- [ ] 配置中文显示
- [ ] 配置凭证管理器
- [ ] 配置常用别名
- [ ] 验证配置正确

**操作步骤**:

```powershell
# 1. 进入仓库目录
cd D:\AIcode\Github\Git-Practice-2026

# 2. 配置用户名和邮箱
git config --global user.name "你的 GitHub 用户名"
git config --global user.email "你的邮箱@example.com"

# 3. 配置中文显示
git config --global core.quotepath false

# 4. 配置凭证管理器
git config --global credential.helper manager

# 5. 配置常用别名
git config --global alias.st status
git config --global alias.lg "log --oneline --graph --all"

# 6. 验证配置
git config --global --list

# 7. 测试别名
git st
```

**预期输出**:
```
user.name=你的 GitHub 用户名
user.email=你的邮箱@example.com
core.quotepath=false
credential.helper=manager
alias.st=status
alias.lg=log --oneline --graph --all
```

---

### Task 2: 从零创建项目

**目标**: 创建一个练习项目，包含完整的目录结构，并成功推送到 GitHub。

**验收标准**:
- [ ] GitHub 仓库创建成功
- [ ] 本地仓库有完整的目录结构
- [ ] 所有文件成功推送到 GitHub
- [ ] 能够查看提交历史

**操作步骤**:

```powershell
# 1. 查看当前状态
git status

# 2. 创建目录结构
New-Item -ItemType Directory -Force -Path "01-Git 基础"
New-Item -ItemType Directory -Force -Path "02-GitHub 操作"
New-Item -ItemType Directory -Force -Path "03-分支管理"

# 3. 创建学习笔记文件
echo "# Git 基础学习笔记" > "01-Git 基础/README.md"
echo "## 什么是 Git？" >> "01-Git 基础/README.md"
echo "Git 是版本控制系统" >> "01-Git 基础/README.md"

echo "# GitHub 操作笔记" > "02-GitHub 操作/README.md"
echo "## 创建仓库" >> "02-GitHub 操作/README.md"

echo "# 分支管理笔记" > "03-分支管理/README.md"
echo "## 分支命令" >> "03-分支管理/README.md"

# 4. 查看状态
git status

# 5. 添加所有文件
git add .

# 6. 查看状态（确认）
git status

# 7. 提交
git commit -m "新增：项目目录结构和学习笔记"

# 8. 查看提交历史
git log --oneline

# 9. 推送到 GitHub
git push -u origin main

# 10. 验证
# 访问 GitHub 仓库页面，确认文件已显示
```

---

### Task 3: 文件管理

**目标**: 掌握文件的添加、修改、删除、移动等操作。

**验收标准**:
- [ ] 能够添加新文件
- [ ] 能够修改现有文件
- [ ] 能够删除文件（本地和 Git）
- [ ] 能够查看文件差异
- [ ] 理解暂存区概念

**操作步骤**:

```powershell
# ========== 场景 1: 添加新文件 ==========
# 1. 创建新文件
echo "# Git 命令速查表" > "01-Git 基础/命令速查.md"
echo "git status - 查看状态" >> "01-Git 基础/命令速查.md"

# 2. 查看状态
git status

# 3. 添加文件
git add "01-Git 基础/命令速查.md"

# 4. 查看状态（确认）
git status

# 5. 提交
git commit -m "新增：Git 命令速查表"


# ========== 场景 2: 修改文件 ==========
# 1. 修改文件
echo "git add - 添加文件" >> "01-Git 基础/命令速查.md"
echo "git commit - 提交" >> "01-Git 基础/命令速查.md"

# 2. 查看修改
git diff "01-Git 基础/命令速查.md"

# 3. 添加修改
git add "01-Git 基础/命令速查.md"

# 4. 提交
git commit -m "更新：补充 Git 命令速查表内容"


# ========== 场景 3: 删除文件 ==========
# 1. 创建测试文件
echo "测试文件" > "test-删除.md"
git add "test-删除.md"
git commit -m "新增：测试文件"

# 2. 从 Git 删除（保留本地文件）
git rm --cached "test-删除.md"
git commit -m "删除：从 Git 移除测试文件"

# 3. 彻底删除（本地和 Git 都删除）
git rm "test-删除.md"
git commit -m "删除：彻底移除测试文件"


# ========== 场景 4: 查看历史 ==========
# 1. 查看简洁历史
git log --oneline

# 2. 查看完整历史
git log

# 3. 查看图形化历史
git lg

# 4. 查看某个文件的历史
git log -- "01-Git 基础/命令速查.md"
```

---

### Task 4: 分支管理

**目标**: 掌握分支的创建、切换、合并、删除等操作。

**验收标准**:
- [ ] 能够创建新分支
- [ ] 能够切换分支
- [ ] 能够合并分支
- [ ] 能够删除分支
- [ ] 理解分支的作用

**操作步骤**:

```powershell
# ========== 场景 1: 创建功能分支 ==========
# 1. 确保在 main 分支
git checkout main
git pull

# 2. 查看当前分支
git branch

# 3. 创建并切换到新分支
git checkout -b feature-advanced-git

# 4. 确认切换成功
git branch  # 应该看到 * feature-advanced-git


# ========== 场景 2: 在分支上开发 ==========
# 1. 创建新功能文件
echo "# 高级 Git 技巧" > "01-Git 基础/高级 Git 技巧.md"
echo "## git rebase" >> "01-Git 基础/高级 Git 技巧.md"
echo "git rebase 用于变基操作" >> "01-Git 基础/高级 Git 技巧.md"

# 2. 添加并提交
git add .
git commit -m "新增：高级 Git 技巧笔记"

# 3. 查看提交历史
git log --oneline


# ========== 场景 3: 合并分支 ==========
# 1. 切换回 main 分支
git checkout main

# 2. 查看当前文件（应该没有高级技巧.md）
ls "01-Git 基础/"

# 3. 合并功能分支
git merge feature-advanced-git

# 4. 查看文件（现在应该有了）
ls "01-Git 基础/"

# 5. 查看合并后的历史
git lg

# 6. 推送到远程
git push


# ========== 场景 4: 删除分支 ==========
# 1. 删除已合并的分支
git branch -d feature-advanced-git

# 2. 查看分支列表
git branch

# 3. 如果分支未合并，强制删除
git branch -D feature-old-branch
```

---

### Task 5: 撤销操作

**目标**: 掌握各种撤销操作，包括撤销修改、撤销暂存、撤销提交。

**验收标准**:
- [ ] 能够撤销工作区修改
- [ ] 能够撤销暂存区文件
- [ ] 能够撤销提交（保留修改）
- [ ] 能够使用 stash 暂存工作
- [ ] 理解不同撤销方式的区别

**操作步骤**:

```powershell
# ========== 场景 1: 撤销工作区修改 ==========
# 1. 创建测试文件
echo "这是错误的内容" > "test-撤销.md"

# 2. 添加并提交
git add "test-撤销.md"
git commit -m "新增：测试撤销"

# 3. 修改文件
echo "修改了内容" >> "test-撤销.md"

# 4. 查看状态
git status

# 5. 撤销修改
git checkout -- "test-撤销.md"
# 或
git restore "test-撤销.md"

# 6. 查看文件（应该回到提交时的状态）
cat "test-撤销.md"


# ========== 场景 2: 撤销暂存区 ==========
# 1. 修改文件
echo "新的修改" >> "test-撤销.md"

# 2. 添加到暂存区
git add "test-撤销.md"

# 3. 查看状态
git status  # 应该在 Changes to be committed

# 4. 撤销暂存
git restore --staged "test-撤销.md"
# 或
git reset HEAD "test-撤销.md"

# 5. 查看状态（应该在 Changes not staged）
git status


# ========== 场景 3: 撤销提交（保留修改） ==========
# 1. 提交
git add "test-撤销.md"
git commit -m "更新：测试撤销"

# 2. 查看历史
git log --oneline -2

# 3. 撤销提交（保留修改）
git reset --soft HEAD^

# 4. 查看状态（修改还在暂存区）
git status

# 5. 继续撤销到工作区
git reset HEAD "test-撤销.md"

# 6. 查看状态（修改在工作区）
git status


# ========== 场景 4: 使用 stash 暂存工作 ==========
# 1. 修改文件
echo "临时修改 1" >> "test-撤销.md"

# 2. 暂存当前工作
git stash push -m "临时保存的修改"

# 3. 查看状态（工作区干净了）
git status

# 4. 查看暂存列表
git stash list

# 5. 恢复暂存
git stash pop

# 6. 查看状态（修改回来了）
git status

# 7. 清理测试文件
git rm "test-撤销.md"
git commit -m "删除：清理测试文件"
git push
```

---

### Task 6: 冲突解决

**目标**: 学会制造冲突、识别冲突、解决冲突。

**验收标准**:
- [ ] 能够理解冲突产生的原因
- [ ] 能够识别冲突标记
- [ ] 能够手动解决冲突
- [ ] 能够取消合并

**操作步骤**:

```powershell
# ========== 场景 1: 制造冲突 ==========
# 1. 确保在 main 分支
git checkout main

# 2. 修改文件
echo "main 分支的修改" >> "01-Git 基础/命令速查.md"
git add .
git commit -m "更新：main 分支修改"

# 3. 创建并切换到功能分支
git checkout -b feature-conflict

# 4. 修改同一个文件的同一行
echo "feature 分支的修改" >> "01-Git 基础/命令速查.md"
git add .
git commit -m "更新：feature 分支修改"


# ========== 场景 2: 合并产生冲突 ==========
# 1. 切换回 main 分支
git checkout main

# 2. 尝试合并（会产生冲突）
git merge feature-conflict

# 3. 查看状态（会显示冲突文件）
git status


# ========== 场景 3: 解决冲突 ==========
# 1. 打开冲突文件
# 内容类似：
# <<<<<<<<< HEAD
# main 分支的修改
# =======
# feature 分支的修改
# >>>>>>> feature-conflict

# 2. 手动编辑，保留需要的内容，删除冲突标记
# 例如：
# main 分支和 feature 分支的修改（合并后的内容）

# 3. 标记冲突已解决
git add "01-Git 基础/命令速查.md"

# 4. 完成合并
git commit -m "合并：解决冲突"

# 5. 查看历史
git lg

# 6. 删除功能分支
git branch -d feature-conflict

# 7. 推送
git push


# ========== 场景 4: 取消合并 ==========
# 1. 如果合并过程中想取消
git merge --abort

# 2. 查看状态（回到合并前）
git status
```

---

### Task 7: 远程协作

**目标**: 掌握远程仓库操作、Pull Request 流程。

**验收标准**:
- [ ] 能够推送分支到远程
- [ ] 能够拉取远程更新
- [ ] 能够创建 Pull Request
- [ ] 能够进行 Code Review
- [ ] 能够合并 PR

**操作步骤**:

```powershell
# ========== 场景 1: 推送分支到远程 ==========
# 1. 创建功能分支
git checkout -b feature-remote

# 2. 开发功能
echo "# 远程协作笔记" > "02-GitHub 操作/远程协作.md"
git add .
git commit -m "新增：远程协作笔记"

# 3. 推送到远程
git push -u origin feature-remote

# 4. 查看远程分支
git branch -r


# ========== 场景 2: 创建 Pull Request ==========
# 1. 访问 GitHub 仓库
# https://github.com/你的用户名/Git-Practice-2026

# 2. 点击 "New pull request"

# 3. 选择：
# base: main
# compare: feature-remote

# 4. 填写 PR 信息：
# 标题：新增：远程协作笔记
# 描述：添加了远程协作的学习笔记

# 5. 点击 "Create pull request"


# ========== 场景 3: Code Review ==========
# 1. 在 GitHub 网页查看 PR
# 2. 点击 "Files changed" 查看变更
# 3. 点击行号添加评论
# 4. 点击 "Review changes" 提交审查


# ========== 场景 4: 合并 PR ==========
# 1. 在 GitHub 网页点击 "Merge pull request"
# 2. 确认合并
# 3. 点击 "Confirm merge"

# 4. 本地同步
git checkout main
git pull
git branch -d feature-remote


# ========== 场景 5: 拉取远程更新 ==========
# 1. 拉取并合并
git pull

# 2. 拉取并变基（推荐）
git pull --rebase

# 3. 仅拉取，不合并
git fetch origin
git branch -r
```

---

### Task 8: 综合实战

**目标**: 模拟真实的开发流程，综合运用所有技能。

**验收标准**:
- [ ] 完整的开发流程
- [ ] 正确的分支管理
- [ ] 规范的提交信息
- [ ] 成功的代码合并
- [ ] 清理工作分支

**操作步骤**:

```powershell
# ========== 阶段 1: 准备 ==========
# 1. 切换到 main 分支
git checkout main

# 2. 拉取最新代码
git pull

# 3. 创建功能分支
git checkout -b feature-final-project


# ========== 阶段 2: 开发功能 ==========
# 1. 创建项目文档
echo "# Git 实战项目总结" > "项目总结.md"
echo "## 学习内容" >> "项目总结.md"
echo "1. Git 基础概念" >> "项目总结.md"
echo "2. 分支管理" >> "项目总结.md"
echo "3. 冲突解决" >> "项目总结.md"

# 2. 第一次提交
git add .
git commit -m "新增：项目总结文档初稿"

# 3. 继续完善
echo "4. 远程协作" >> "项目总结.md"
echo "5. 最佳实践" >> "项目总结.md"

# 4. 第二次提交
git add .
git commit -m "更新：补充项目总结内容"

# 5. 创建学习笔记
echo "# 学习心得" > "03-分支管理/学习心得.md"
echo "通过今天的练习，我掌握了..." >> "03-分支管理/学习心得.md"

# 6. 第三次提交
git add .
git commit -m "新增：学习心得笔记"


# ========== 阶段 3: 推送到远程 ==========
# 1. 推送到 GitHub
git push -u origin feature-final-project

# 2. 查看提交历史
git log --oneline


# ========== 阶段 4: 创建 PR ==========
# 1. 访问 GitHub 创建 PR
# 2. 填写 PR 信息
# 3. 请求审查


# ========== 阶段 5: 合并与清理 ==========
# 1. 在 GitHub 合并 PR
# 2. 本地同步
git checkout main
git pull

# 3. 删除本地分支
git branch -d feature-final-project

# 4. 查看最终状态
git status
git lg

# 5. 验证 GitHub 仓库
# 访问 GitHub 确认所有文件已合并
```

---

### Task 9: 分支管理进阶 ⭐

**目标**: 掌握分支推送、upstream 关联、远程同步等高级操作。

**验收标准**:
- [ ] 理解 upstream 概念
- [ ] 能够推送分支到远程
- [ ] 能够查看分支关联
- [ ] 能够同步远程分支
- [ ] 能够处理推送失败

**操作步骤**:

```powershell
# ========== 阶段 1: 创建功能分支并开发 ==========
# 1. 切换到 main 分支
git checkout main
git pull

# 2. 创建功能分支
git checkout -b feature-advanced-branch

# 3. 创建新功能文件
echo "# 高级分支管理技巧" > "01-Git 基础/高级分支管理.md"
echo "## upstream 关联" >> "01-Git 基础/高级分支管理.md"
echo "upstream 是上游分支的关联关系" >> "01-Git 基础/高级分支管理.md"

# 4. 提交
git add .
git commit -m "新增：高级分支管理技巧"


# ========== 阶段 2: 首次推送到远程 ==========
# 1. 推送到远程并建立 upstream 关联
git push -u origin feature-advanced-branch

# 预期输出：
# Branch 'feature-advanced-branch' set up to track remote branch 'feature-advanced-branch' from 'origin'.

# 2. 查看分支关联
git branch -vv

# 预期输出：
# * feature-advanced-branch    abc1234 [origin/feature-advanced-branch] 新增：高级分支管理技巧
#   main                       def5678 [origin/main] 更新 README


# ========== 阶段 3: 继续开发并推送 ==========
# 1. 继续完善文档
echo "## 远程同步策略" >> "01-Git 基础/高级分支管理.md"
echo "git pull = git fetch + git merge" >> "01-Git 基础/高级分支管理.md"

# 2. 提交
git add .
git commit -m "更新：补充远程同步策略"

# 3. 推送（已建立关联，直接 git push）
git push


# ========== 阶段 4: 查看和管理 upstream ==========
# 1. 查看所有分支的 upstream
git branch -vv

# 2. 查看远程分支
git branch -r

# 3. 查看所有分支（本地 + 远程）
git branch -a

# 4. 手动设置 upstream（如果分支已存在但没有关联）
# git branch --set-upstream-to=origin/feature-advanced-branch feature-advanced-branch


# ========== 阶段 5: 同步远程变更 ==========
# 1. 拉取远程更新
git pull

# 2. 或者使用 rebase（推荐，保持历史整洁）
git pull --rebase

# 3. 仅拉取，不合并
git fetch origin
git status


# ========== 阶段 6: 处理推送冲突 ==========
# 1. 如果推送失败，提示非快进更新
# ! [rejected]        feature-advanced-branch -> feature-advanced-branch (non-fast-forward)

# 2. 先拉取远程变更
git pull --rebase

# 3. 解决冲突（如果有）
# git status 查看冲突文件
# 手动编辑解决冲突
# git add 冲突文件
# git rebase --continue

# 4. 推送
git push


# ========== 阶段 7: 合并回 main 并清理 ==========
# 1. 切换回 main
git checkout main

# 2. 合并功能分支
git merge feature-advanced-branch

# 3. 推送到远程
git push

# 4. 删除本地分支
git branch -d feature-advanced-branch

# 5. 删除远程分支
git push origin --delete feature-advanced-branch

# 6. 查看最终状态
git branch -a
git lg
```

---

### Task 10: 完整协作流程模拟 ⭐⭐⭐

**目标**: 模拟真实的团队协怍场景，包括 PR 流程、Code Review、冲突解决。

**场景设定**:
- 你和你的同学协作一个项目
- 你们同时修改了同一个文件
- 需要创建 PR、审查代码、解决冲突

**验收标准**:
- [ ] 创建功能分支
- [ ] 推送到远程
- [ ] 创建 Pull Request
- [ ] 进行 Code Review
- [ ] 解决合并冲突
- [ ] 完成合并

**操作步骤**:

```powershell
# ========== 步骤 1: 准备 ==========
# 1. 确保在 main 分支
git checkout main
git pull

# 2. 创建功能分支
git checkout -b feature-collaboration


# ========== 步骤 2: 开发功能 ==========
# 1. 修改 README.md
echo "## 协作开发流程" >> README.md
echo "1. 创建功能分支" >> README.md
echo "2. 开发功能" >> README.md
echo "3. 创建 PR" >> README.md

# 2. 提交
git add .
git commit -m "新增：协作开发流程说明"

# 3. 推送
git push -u origin feature-collaboration


# ========== 步骤 3: 创建 Pull Request ==========
# 1. 访问 GitHub 仓库
# https://github.com/你的用户名/Git-Practice-2026

# 2. 点击 "New pull request"

# 3. 选择：
# base: main
# compare: feature-collaboration

# 4. 填写 PR 信息：
# 标题：新增：协作开发流程说明
# 描述：
# - 添加了协作开发流程的说明
# - 包含分支创建、PR 流程、Code Review 步骤


# ========== 步骤 4: Code Review ==========
# 1. 在 GitHub 网页查看 PR
# 2. 点击 "Files changed" 查看变更
# 3. 点击行号添加评论
# 4. 点击 "Review changes" 提交审查
# 5. 选择 "Approve" 批准


# ========== 步骤 5: 合并 PR ==========
# 1. 在 GitHub 网页点击 "Merge pull request"
# 2. 确认合并
# 3. 点击 "Confirm merge"


# ========== 步骤 6: 本地同步 ==========
# 1. 切换回 main
git checkout main

# 2. 拉取最新代码
git pull

# 3. 查看历史
git lg

# 4. 删除本地分支
git branch -d feature-collaboration


# ========== 步骤 7: 验证 ==========
# 1. 查看 GitHub 仓库
# 2. 确认 PR 已合并
# 3. 确认文件已更新
```

---

### Task 10: 命令对比训练 ⭐⭐⭐⭐⭐

**目标**: 掌握 Git 易混淆命令的区别，能够根据场景选择正确的命令。

**核心技能**: git restore / git reset / git checkout / git switch / git merge / git rebase

**场景说明**: 本任务通过 6 个具体场景，全面训练你对 Git 命令的理解。

---

#### 场景 1：撤销工作区修改

**任务**: 修改一个文件后，想撤销修改

**操作步骤**:
```powershell
# 1. 创建测试文件
echo "原始内容" > test-undo.md
git add test-undo.md
git commit -m "新增：测试文件"

# 2. 修改文件
echo "新内容" >> test-undo.md

# 3. 查看状态
git status
# 输出：Changes not staged for commit:
#   modified: test-undo.md

# 4. 撤销工作区修改（选择正确的命令）
git restore test-undo.md

# 5. 验证
git status
# 输出：nothing to commit, working tree clean
cat test-undo.md
# 输出：原始内容
```

**关键点**:
- `git restore <文件>` 用于撤销**工作区**的修改
- `git checkout -- <文件>` 是旧语法，作用相同

**❌ 错误做法**:
```powershell
# 错误！git reset 是操作暂存区的
git reset HEAD test-undo.md
# 这个命令对工作区修改无效！
```

---

#### 场景 2：撤销 git add（取消暂存）

**任务**: 执行了 git add 后，想取消暂存

**操作步骤**:
```powershell
# 1. 创建测试文件
echo "测试内容" > test-staged.md
git add test-staged.md

# 2. 查看状态
git status
# 输出：Changes to be committed:
#   new file:   test-staged.md

# 3. 撤销暂存（选择正确的命令）
git restore --staged test-staged.md

# 或者使用旧语法
git reset HEAD test-staged.md

# 4. 验证
git status
# 输出：Changes not staged for commit:
#   new file:   test-staged.md
# 注意：文件内容还在，只是从暂存区移除了
```

**关键点**:
- `git restore --staged <文件>` 撤销**暂存区**的操作
- 文件的修改还在，只是移除了暂存状态

---

#### 场景 3：撤销提交

**任务**: 提交后发现有问题，想撤销提交

**操作步骤**:
```powershell
# 1. 创建文件并提交
echo "内容A" > test-commit.md
git add test-commit.md
git commit -m "新增：测试提交"

# 2. 查看提交历史
git log --oneline
# 输出：abc1234 新增：测试提交

# 3. 撤销提交（保留修改）
git reset --soft HEAD^

# 4. 验证
git status
# 输出：Changes to be committed:
#   new file:   test-commit.md
# 注意：修改还在暂存区！

# 5. 如果想完全丢弃修改
git reset --hard HEAD^
# ⚠️ 危险！修改会丢失！
```

**命令对比**:
| 命令 | 修改位置 | 效果 |
|------|----------|------|
| `git reset --soft HEAD^` | 暂存区 | 修改在暂存区 |
| `git reset --mixed HEAD^` | 暂存区+工作区 | 修改在工作区（默认） |
| `git reset --hard HEAD^` | 全部 | 完全丢弃（危险！） |

---

#### 场景 4：切换分支

**任务**: 在分支之间切换，体验不同命令

**操作步骤**:
```powershell
# 1. 确保在 main 分支
git checkout main

# 2. 创建新分支并切换（方法对比）
# 方法 A：git checkout -b（老语法）
git checkout -b branch-A

# 切换回 main 并删除
git checkout main
git branch -d branch-A

# 方法 B：git switch -c（新版推荐）
git switch -c branch-B

# 切换回 main 并删除
git switch main
git branch -d branch-B

# 3. 对比输出
git switch -c branch-test
# 输出：Switched to a new branch 'branch-test'

git checkout -b branch-test2
# 输出：Switched to a new branch 'branch-test2'
```

**推荐**:
- 使用 `git switch` 更清晰（不会和文件操作混淆）
- `git checkout` 功能太多，容易混淆

---

#### 场景 5：merge vs rebase

**任务**: 体验两种合并方式的区别

**操作步骤**:
```powershell
# ========== 准备：创建场景 ==========
# 1. 在 main 创建初始提交
git checkout main
echo "初始内容" > merge-test.md
git add merge-test.md
git commit -m "初始提交"

# 2. 创建功能分支
git checkout -b feature-merge
echo "功能A" >> merge-test.md
git add merge-test.md
git commit -m "新增：功能A"

# ========== 场景 5a: 使用 merge ==========
# 3. 切回 main，制造一个"干扰"提交
git checkout main
echo "干扰提交" >> merge-test.md
git add merge-test.md
git commit -m "更新：main更新"

# 4. 使用 merge 合并
git merge feature-merge

# 5. 查看历史
git log --oneline --graph
# 会看到分叉历史

# ========== 场景 5b: 使用 rebase（重新开始）==========
# 1. 切回 main，删除之前的分支
git checkout main
git branch -D feature-merge
git reset --hard HEAD~2  # 撤销前面的测试

# 2. 重新创建功能分支
git checkout -b feature-rebase
echo "功能B" >> merge-test.md
git add merge-test.md
git commit -m "新增：功能B"

# 3. 切回 main，制造"干扰"提交
git checkout main
echo "干扰提交2" >> merge-test.md
git add merge-test.md
git commit -m "更新：main更新2"

# 4. 使用 rebase 合并
git checkout feature-rebase
git rebase main

# 5. 查看历史
git log --oneline --graph
# 会看到线性历史！

# ========== 清理 ==========
git checkout main
git branch -D feature-rebase
git reset --hard HEAD~1
```

**关键区别**:
| 特性 | merge | rebase |
|------|-------|--------|
| 历史 | 分叉（有合并提交） | 线性（无合并提交） |
| 安全性 | 安全 | ⚠️ 不要对公共分支用 |
| 适用 | 公共分支、团队协作 | 个人分支整理 |

---

#### 场景 6：git rm 的三种模式

**任务**: 掌握不同的文件删除方式

**操作步骤**:
```powershell
# ========== 场景 6a: git rm（彻底删除）==========
# 1. 创建并提交文件
echo "重要内容" > important.txt
git add important.txt
git commit -m "新增：重要文件"

# 2. 使用 git rm 删除
git rm important.txt
# 效果：工作区删除 + 暂存区删除操作

git status
# 输出：Changes to be committed:
#   deleted:    important.txt

git commit -m "删除：重要文件"

# ========== 场景 6b: git rm --cached（仅停止跟踪）==========
# 1. 创建一个被跟踪的大文件
echo "大文件内容" > large.bin
git add large.bin
git commit -m "新增：大文件"

# 2. 使用 git rm --cached（停止跟踪但不删除本地）
git rm --cached large.bin
# 效果：仅从 Git 移除，本地文件保留

git status
# 输出：Changes to be committed:
#   deleted:    large.bin

# 查看 .gitignore
echo "large.bin" >> .gitignore
git add .gitignore
git commit -m "更新：.gitignore，移除大文件跟踪"

# ========== 场景 6c: git rm -f（强制删除）==========
# 1. 创建并修改文件
echo "修改过的内容" > force-delete.txt
git add force-delete.txt
git commit -m "新增：强制删除测试"

# 2. 修改文件
echo "新内容" >> force-delete.txt

# 3. 尝试普通删除（会失败）
git rm force-delete.txt
# 输出：error: the following file has local modifications:
# force-delete.txt

# 4. 使用 -f 强制删除
git rm -f force-delete.txt

# ========== 清理 ==========
git checkout main
git branch -D test-rm
```

---

#### 验收标准

- [ ] 能够正确使用 git restore 撤销工作区修改
- [ ] 能够正确使用 git restore --staged 撤销 git add
- [ ] 能够正确使用 git reset --soft / --hard 撤销提交
- [ ] 能够区分 git checkout 和 git switch 的用途
- [ ] 能够区分 git merge 和 git rebase 的适用场景
- [ ] 能够正确使用 git rm 的三种模式

---

## 10. 提交规范速查

### 最简单的提交格式

```powershell
git commit -m "类型：简短描述"
```

### 6 个常用类型

| 类型 | 使用场景 | 示例 |
|------|----------|------|
| **新增** | 添加新功能、新文件 | `新增：STM32 LED 控制示例` |
| **修复** | 修复 Bug、错误 | `修复：串口通信波特率错误` |
| **更新** | 更新现有内容 | `更新：README 添加安装说明` |
| **优化** | 性能优化、代码改进 | `优化：提升查询速度 50%` |
| **文档** | 文档相关修改 | `文档：补充 API 使用说明` |
| **删除** | 删除文件、功能 | `删除：废弃的配置文件` |

### 好 vs 坏的提交信息

**❌ 不好**:
```powershell
git commit -m "update"           # 太模糊
git commit -m "fix bug"          # 不知道修复了什么
git commit -m "修改了一些代码"    # 没有信息量
git commit -m "今天的学习"        # 不知道学了什么
```

**✅ 好**:
```powershell
git commit -m "新增：STM32 LED 控制示例"
git commit -m "修复：串口通信波特率错误"
git commit -m "更新：README 添加使用说明"
git commit -m "优化：减少延时函数执行时间"
git commit -m "文档：补充 GPIO 配置说明"
```

---

## 11. 实战问题解析 ⭐

### 11.1 git restore vs git reset 详解

**核心区别**：
- **`git restore`**: 恢复**文件内容**（工作区或暂存区）
- **`git reset`**: 移动**分支指针**（撤销提交或暂存）

**一句话记忆**：
> restore 恢复文件，reset 重置指针

#### 详细对比表

| 场景 | 使用命令 | 作用区域 | 示例 |
|------|----------|----------|------|
| **撤销工作区修改** | `git restore <文件>` | 仓库 → 工作区 | 文件写错了，恢复到上次提交 |
| **撤销暂存** | `git restore --staged <文件>` | 暂存区 → 工作区 | 误加了文件，从暂存区移除 |
| **完全恢复** | `git restore --staged <文件>` + `git restore <文件>` | 暂存区 + 工作区 | 完全撤销所有修改 |
| **撤销提交** | `git reset --hard HEAD~1` | 分支指针后退 | 提交错了，撤销这次提交 |
| **撤销暂存（旧方法）** | `git reset HEAD <文件>` | 暂存区 → 工作区 | 同 `git restore --staged` |

#### 状态转换图

```
┌─────────────────────────────────────────────────────────┐
│                    Git 三区域模型                        │
└─────────────────────────────────────────────────────────┘

工作区 (Working Directory)  ←→  暂存区 (Staging Area)  ←→  仓库区 (Repository)
      ↑                              ↑                          ↑
      │                              │                          │
  git restore                    git restore                git reset
  git checkout                   git reset HEAD             git reset --hard
      │                              │                          │
      ▼                              ▼                          ▼
  恢复文件内容                   从暂存区移除                移动分支指针
```

#### 实战场景演示

**场景 1: 修改文件后反悔**
```powershell
# 1. 修改文件
echo "新内容" >> file.txt

# 2. 查看状态
git status
# 输出：Changes not staged for commit (工作区修改)

# 3. 撤销修改（恢复到上次提交）
git restore file.txt

# 4. 验证
cat file.txt  # 修改消失
```

**场景 2: 误加文件到暂存区**
```powershell
# 1. 添加文件到暂存区
git add file.txt

# 2. 查看状态
git status
# 输出：Changes to be committed (已暂存)

# 3. 从暂存区移除（但保留工作区修改）
git restore --staged file.txt
# 或旧方法：git reset HEAD file.txt

# 4. 查看状态
git status
# 输出：Changes not staged for commit (回到工作区)
```

**场景 3: 完全撤销（工作区 + 暂存区）**
```powershell
# 1. 已暂存的修改
git add file.txt
git commit -m "错误提交"

# 2. 完全撤销
git reset --hard HEAD~1
# 这条命令会：
# - 移动 HEAD 指针到上一次提交
# - 清空暂存区
# - 恢复工作区到上次提交状态

# ⚠️ 警告：这会永久删除工作区的修改！
```

---

### 11.2 Git 输出信息解读

#### 输出 1: "Your branch is ahead of 'origin/main' by 1 commit"
```
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)
```

**含义**：
- 你的本地 `main` 分支比远程 `origin/main` 多 1 个提交
- 这个提交还没有推送到远程
- Git 建议你执行 `git push`

**示意图**：
```
本地：A ← B ← C ← D (main)
                ↑
              多出的提交

远程：A ← B ← C (origin/main)
```

**解决方案**：
```powershell
git push
```

---

#### 输出 2: "Changes to be committed"
```
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
    new file:   src/edm.md
```

**含义**：
- `src/edm.md` 已经添加到暂存区
- 下次提交时会包含这个文件
- 如果想移除，使用 `git restore --staged src/edm.md`

**状态**：
```
工作区：src/edm.md (已创建)
  ↓ git add
暂存区：src/edm.md (已暂存) ← 当前状态
  ↓ git commit
仓库区：(待提交)
```

---

#### 输出 3: "fatal: The current branch has no upstream branch"
```
fatal: The current branch user-login has no upstream branch.
To push the current branch and set the remote as upstream, use
    git push --set-upstream origin user-login
```

**含义**：
- `user-login` 是本地新建的分支
- 远程仓库还没有这个分支
- Git 不知道要推送到哪里

**解决方案**：
```powershell
# 方法 1: 完整写法
git push --set-upstream origin user-login

# 方法 2: 简写（推荐）
git push -u origin user-login

# ✅ 推送成功后，Git 会输出：
# Branch 'user-login' set up to track remote branch 'user-login' from 'origin'.
```

**建立关联后**：
```
本地：user-login ─────┐
                      ├─→ 关联 (upstream)
远程：origin/user-login ─┘

之后可以直接：git push
```

---

#### 输出 4: 推送过程
```
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 12 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (4/4), 313 bytes | 313.00 KiB/s, done.
```

**含义**：
- **Enumerating objects**: 统计要推送的对象（文件、提交等）
- **Counting objects**: 计算对象数量
- **Delta compression**: 压缩差异（只推送变化的部分）
- **Compressing objects**: 压缩数据
- **Writing objects**: 写入远程仓库
- ✅ **推送成功！**

---

### 11.3 PowerShell 命令速查

#### 目录操作
```powershell
# 创建目录
mkdir src
New-Item -ItemType Directory -Force -Path "src"

# 创建多级目录
mkdir src\components\utils
New-Item -ItemType Directory -Force -Path "src\components\utils"

# 查看目录内容
ls
dir
Get-ChildItem

# 进入目录
cd src
Set-Location src

# 返回上级
cd ..

# 删除目录（空）
rmdir empty_folder

# 删除目录及内容（谨慎！）
Remove-Item -Recurse -Force folder_name
ri folder_name -r -fo
```

#### 文件操作
```powershell
# 创建文件
echo "内容" > file.txt
"内容" | Out-File -FilePath file.txt

# 追加内容
echo "新内容" >> file.txt
"新内容" | Out-File -FilePath file.txt -Append

# 查看文件内容
cat file.txt
Get-Content file.txt
type file.txt

# 复制文件
Copy-Item source.txt destination.txt
cp source.txt dest.txt
cpi source.txt dest.txt

# 移动文件
Move-Item old.txt new.txt
mv old.txt new.txt

# 删除文件
Remove-Item file.txt
del file.txt
rm file.txt
```

#### 路径检查
```powershell
# 检查文件/目录是否存在
Test-Path src
Test-Path file.txt

# 检查后创建（推荐模式）
if (!(Test-Path src)) { mkdir src }
```

---

### 11.4 实战问题解析（v4.0 内容）

### 11.1 今日实战问题回顾

今天在练习过程中，遇到了以下关键问题：

#### 问题 1: git rm 失败

**现象**:
```powershell
git rm Git-Practice-2026\01-学习笔记\Git 基础.md 
fatal: pathspec 'Git-Practice-2026\01-学习笔记\Git' did not match any files
```

**分析**:
- PowerSHell 将路径中的空格解析为分隔符
- `Git-Practice-2026\01-学习笔记\Git` 被当作一个参数
- `基础.md` 被当作另一个参数

**解决方案**:
```powershell
# 1. 使用引号包裹完整路径
git rm "Git-Practice-2026\01-学习笔记\Git 基础.md"

# 2. 或使用正斜杠
git rm "Git-Practice-2026/01-学习笔记/Git 基础.md"

# 3. 或使用相对路径
git rm "01-学习笔记/Git 基础.md"
```

---

#### 问题 2: git reset HEAD 与 git restore --staged 的区别

**现象**: 两个命令似乎都能撤销暂存，但结果不同

**分析**:

| 命令 | 作用 | 结果 |
|------|------|------|
| `git restore --staged <文件>` | 从暂存区移除 | 文件回到工作区状态 |
| `git reset HEAD <文件>` | 从暂存区移除 | 与 `git restore --staged` 完全相同 |

**示例**:
```powershell
# 初始状态：文件在暂存区（Changes to be committed）
git status
# Changes to be committed:
#   modified: 01-学习笔记/Git 基础.md

# 执行命令
git restore --staged "01-学习笔记/Git 基础.md"

# 结果：文件在工作区（Changes not staged）
git status
# Changes not staged for commit:
#   modified: 01-学习笔记/Git 基础.md
```

---

#### 问题 3: git rm 后的状态变化

**现象**: 执行 `git rm` 后，文件在暂存区显示为 deleted

**分析**:
```
执行前:
工作区: 文件存在
暂存区: (空)
仓库: 文件存在

执行 git rm "文件":
工作区: 文件被删除
暂存区: 删除操作被暂存
仓库: 文件仍存在

提交后:
工作区: 文件不存在
暂存区: (空)
仓库: 文件被删除
```

**示例**:
```powershell
# 删除文件
git rm "01-学习笔记/Git 基础.md"
# 输出: rm '01-学习笔记/Git 基础.md'

# 查看状态
git status
# Changes to be committed:
#   deleted: 01-学习笔记/Git 基础.md

# 提交删除
git commit -m "删除：Git 基础学习笔记"

# 推送
git push
```

---

#### 问题 4: git restore --staged 与 git restore 的区别

**现象**: 两个命令都很相似，但作用不同

**分析**:

| 命令 | 作用对象 | 作用区域 | 结果 |
|------|----------|----------|------|
| `git restore --staged <文件>` | 暂存区 | 暂存区 → 工作区 | 从暂存区移除，不影响工作区 |
| `git restore <文件>` | 工作区 | 仓库 → 工作区 | 从仓库恢复到工作区 |
| `git restore --staged <文件>` + `git restore <文件>` | 暂存区 + 工作区 | 完全恢复 | 恢复到上次提交状态 |

**示例**:
```powershell
# ========== 场景 1: 撤销暂存 ==========
# 文件已添加到暂存区
git add "文件.md"
git status
# Changes to be committed:
#   modified: 文件.md

# 撤销暂存
git restore --staged "文件.md"
git status
# Changes not staged for commit:
#   modified: 文件.md

# ========== 场景 2: 恢复文件 ==========
# 工作区文件被修改
# 恢复到上次提交的状态
git restore "文件.md"

# ========== 场景 3: 完全恢复 ==========
# 撤销暂存并恢复文件
git restore --staged "文件.md"  # 从暂存区移除
git restore "文件.md"           # 从仓库恢复
```

---

#### 问题 5: 已删除文件的恢复

**现象**: 文件被 `git rm` 删除后，如何恢复

**分析**: 需要区分两种情况

**情况 1: 删除操作在暂存区（未提交）**
```powershell
# 状态：Changes to be committed: deleted: 文件.md
# 恢复方法：
git restore --staged "文件.md"  # 从暂存区移除删除操作
git restore "文件.md"           # 从仓库恢复文件
```

**情况 2: 删除操作已提交**
```powershell
# 状态：文件已从仓库删除
# 恢复方法：
# 从上一个提交恢复文件
git checkout HEAD~ -- "文件.md"
# 或
git restore --source HEAD~ "文件.md"

# 提交恢复
git add "文件.md"
git commit -m "恢复：文件.md"
```

**情况 3: 删除操作已推送**
```powershell
# 从远程仓库恢复
git checkout HEAD~ -- "文件.md"
git add "文件.md"
git commit -m "恢复：文件.md"
git push
```

---

### 11.2 实战练习：文件删除与恢复全流程

让我们通过一个完整的练习来理解这些概念：

```powershell
# ========== 练习 1: 创建测试文件 ==========
# 1. 创建文件
echo "原始内容" > "测试文件.md"
git add "测试文件.md"
git commit -m "新增：测试文件"

# 2. 查看状态
git status
# nothing to commit, working tree clean

# ========== 练习 2: 删除文件（未提交） ==========
# 1. 删除文件
git rm "测试文件.md"

# 2. 查看状态
git status
# Changes to be committed:
#   deleted: 测试文件.md

# 3. 恢复文件（未提交状态下的恢复）
git restore --staged "测试文件.md"  # 撤销暂存的删除操作
git restore "测试文件.md"           # 从仓库恢复文件

# 4. 查看状态
git status
# nothing to commit, working tree clean

# ========== 练习 3: 删除文件（已提交） ==========
# 1. 删除文件
git rm "测试文件.md"
git commit -m "删除：测试文件"

# 2. 查看状态
git status
# nothing to commit, working tree clean

# 3. 恢复文件（已提交状态下的恢复）
git checkout HEAD~ -- "测试文件.md"

# 4. 查看文件内容
cat "测试文件.md"
# 应该显示：原始内容

# 5. 提交恢复
git add "测试文件.md"
git commit -m "恢复：测试文件"
```

---

### 11.3 实战练习：撤销操作全流程

```powershell
# ========== 练习 1: 撤销工作区修改 ==========
# 1. 修改文件
echo "新内容" >> "测试文件.md"

# 2. 查看状态
git status
# Changes not staged for commit:
#   modified: 测试文件.md

# 3. 撤销修改
git restore "测试文件.md"

# 4. 查看文件（回到上次提交状态）
cat "测试文件.md"


# ========== 练习 2: 撤销暂存区修改 ==========
# 1. 修改文件并添加到暂存区
echo "新内容" >> "测试文件.md"
git add "测试文件.md"

# 2. 查看状态
git status
# Changes to be committed:
#   modified: 测试文件.md

# 3. 撤销暂存
git restore --staged "测试文件.md"

# 4. 查看状态
git status
# Changes not staged for commit:
#   modified: 测试文件.md


# ========== 练习 3: 撤销提交（保留修改） ==========
# 1. 提交修改
git add "测试文件.md"
git commit -m "更新：测试文件"

# 2. 撤销提交（保留修改）
git reset --soft HEAD~

# 3. 查看状态
git status
# Changes to be committed:
#   modified: 测试文件.md


# ========== 练习 4: 撤销提交（丢弃修改） ==========
# 1. 撤销提交并丢弃修改（危险！）
git reset --hard HEAD~
# 注意：这会完全丢弃修改，无法恢复！
```

---

## 附录：快速参考卡

### 最常用命令 TOP 10

```powershell
git status              # 1. 查看状态（最常用！）
git add .              # 2. 添加所有文件
git commit -m "信息"    # 3. 提交
git push               # 4. 推送
git pull               # 5. 拉取
git log --oneline      # 6. 查看历史
git branch             # 7. 查看分支
git checkout -b 分支名  # 8. 创建并切换分支
git merge 分支名        # 9. 合并分支
git diff               # 10. 查看差异
```

### 撤销操作速查

```powershell
git restore <文件>           # 撤销工作区修改
git restore --staged <文件>  # 撤销暂存
git reset --soft HEAD^       # 撤销提交（保留修改）
git stash                    # 暂存当前工作
git stash pop                # 恢复暂存
```

### 分支操作速查

```powershell
git branch                    # 查看分支
git checkout -b <分支名>      # 创建并切换
git merge <分支名>            # 合并分支
git branch -d <分支名>        # 删除分支
```

---

**祝你学习愉快！** 🚀

**最后更新**: 2026-03-11  
**版本**: v4.0（实战问题解决版）