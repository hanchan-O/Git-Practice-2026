# 🎯 Git 实战使用指南

> 从零开始掌握 Git 和 GitHub，包含完整流程、命令详解和简单的提交规范

**版本**: v2.0（简化实用版）  
**最后更新**: 2026-03-10

---

## 📚 目录

1. [Git 基础概念](#git-基础概念)
2. [完整工作流程](#完整工作流程)
3. [核心命令详解](#核心命令详解)
4. [实战训练任务](#实战训练任务)
5. [简单的提交规范](#简单的提交规范) ⭐
6. [常见问题解决](#常见问题解决)

---

## Git 基础概念

### 什么是 Git？

**Git** 是一个**分布式版本控制系统**，就像一个"时光机"：
- ✅ 记录文件的每次修改历史
- ✅ 可以回退到任意历史版本
- ✅ 多人协作开发
- ✅ 创建分支进行并行开发

### 什么是 GitHub？

**GitHub** 是一个**代码托管平台**，就像一个"云端仓库"：
- ✅ 存储你的代码（远程仓库）
- ✅ 展示你的项目
- ✅ 与他人协作
- ✅ 构建技术身份

### 核心概念图解

```
工作区 (Working Directory)     你电脑上的文件
    ↓ git add
暂存区 (Staging Area)          准备提交的文件
    ↓ git commit
本地仓库 (Local Repository)    本地的 Git 数据库
    ↓ git push
远程仓库 (Remote Repository)   GitHub 上的仓库
```

**详细说明**：
1. **工作区**：你电脑上实际编辑文件的目录
2. **暂存区**：准备提交的文件临时存放区
3. **本地仓库**：本地的 Git 数据库（.git 文件夹）
4. **远程仓库**：GitHub 上的仓库

---

## 完整工作流程

### 🎯 从零开始的完整流程

#### 第一步：在 GitHub 创建仓库

1. **访问 GitHub**：https://github.com
2. **登录账号**
3. **创建新仓库**：
   - 点击右上角 "+" → "New repository"
   - Repository name: `你的仓库名`
   - 选择 **Public**（公开）
   - ✅ 勾选 "Add a README file"
   - 点击 "Create repository"

---

#### 第二步：克隆到本地

```powershell
# 1. 进入工作目录
cd d:\AIcode\Github

# 2. 克隆远程仓库
git clone https://github.com/你的用户名/仓库名.git

# 3. 进入项目目录
cd 仓库名

# 4. 查看当前状态
git status
```

**预期输出**:
```
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

> 💡 **说明**: GitHub 从 2020 年起默认分支名从 `master` 改为 `main`，如果你看到的是 `master` 也没关系，操作方式完全相同！

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

# 3. 查看状态
git status

# 4. 添加所有文件
git add .

# 5. 提交到本地仓库
git commit -m "初始化：创建项目目录结构和学习笔记"

# 6. 查看提交历史
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

### 📅 每日工作流程

```powershell
# 早上开始工作
# 1. 拉取最新代码
git pull

# 2. 编辑文件...

# 3. 查看修改
git status

# 4. 添加修改
git add .

# 5. 提交
git commit -m "完成：今天的学习任务"

# 6. 推送
git push
```

---

## 核心命令详解

### 🔧 基础命令（必须掌握）

#### 1. 初始化和配置

```powershell
# 初始化 Git 仓库
git init

# 配置用户名（必须，只需配置一次）
git config --global user.name "你的用户名"

# 配置邮箱（必须，只需配置一次）
git config --global user.email "你的邮箱"

# 查看配置
git config --global --list
```

---

#### 2. 查看状态（最常用！）

```powershell
# 查看当前状态（最常用）
git status

# 查看提交历史
git log

# 查看简洁历史（推荐）
git log --oneline

# 查看图形化历史
git log --oneline --graph --all

# 查看文件差异
git diff
```

**git status 输出说明**:
```
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   README.md
        modified:   src/index.js

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
        modified:   package.json

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .env
```

**关键信息**:
- `new file`: 新文件，已添加到暂存区
- `modified`: 修改的文件
- `Changes to be committed`: 已暂存，准备提交
- `Changes not staged for commit`: 未暂存，需要 git add
- `Untracked files`: 未跟踪文件

---

#### 3. 添加和提交

```powershell
# 添加单个文件
git add README.md

# 添加所有文件（最常用）
git add .

# 添加整个目录
git add 目录名/

# 提交到本地仓库
git commit -m "提交信息"

# 提交所有已跟踪的文件
git commit -a -m "提交信息"
```

**提交信息规范**:
```
新增：添加用户登录功能
修复：解决内存泄漏问题
更新：修改 README 文档
优化：提升查询性能
```

---

#### 4. 推送和拉取

```powershell
# 首次推送，设置上游分支
git push -u origin main

# 后续推送（简化）
git push

# 拉取并合并（最常用）
git pull

# 仅拉取，不合并
git fetch origin
```

---

#### 5. 分支管理

```powershell
# 查看所有分支
git branch

# 创建新分支
git branch feature-login

# 切换分支
git checkout feature-login

# 创建并切换分支（推荐）
git checkout -b feature-login

# 合并分支
git checkout main
git merge feature-login

# 删除分支
git branch -d feature-login
```

---

### 🚀 高级命令（进阶使用）

#### 1. 撤销操作

```powershell
# 撤销工作区修改
git checkout -- README.md

# 撤销暂存区
git reset HEAD README.md

# 撤销最后一次提交（保留修改）
git reset --soft HEAD^

# 撤销最后一次提交（丢弃修改）
git reset --hard HEAD^
```

---

#### 2. 暂存工作

```powershell
# 暂存当前工作
git stash

# 查看暂存列表
git stash list

# 恢复暂存
git stash pop
```

---

#### 3. 远程仓库管理

```powershell
# 查看远程仓库
git remote -v

# 添加远程仓库
git remote add origin https://github.com/用户名/仓库名.git

# 移除远程仓库
git remote remove origin

# 修改远程仓库地址
git remote set-url origin https://github.com/用户名/新仓库名.git
```

---

## 实战训练任务

### 📋 任务概览

| 任务 | 主题 | 核心技能 | 预计时间 | 难度 |
|------|------|----------|----------|------|
| **Task 1** | 从零创建项目 | 初始化、提交、推送 | 15 分钟 | ⭐ |
| **Task 2** | 分支管理与功能开发 | 分支、合并、冲突解决 | 20 分钟 | ⭐⭐ |
| **Task 3** | 完整协作流程 | PR、Code Review、合并 | 25 分钟 | ⭐⭐⭐ |

---

### Task 1: 从零创建项目

**目标**: 创建一个练习项目，包含完整的目录结构，并成功推送到 GitHub。

**验收标准**:
- [ ] GitHub 仓库创建成功
- [ ] 本地仓库有完整的目录结构
- [ ] 所有文件成功推送到 GitHub
- [ ] 能够查看提交历史

**操作步骤**: 参考上方的"完整工作流程"部分。

---

### Task 2: 分支管理与功能开发

**目标**: 使用分支开发新功能，学习分支管理、合并和冲突解决。

**验收标准**:
- [ ] 创建并切换到新分支
- [ ] 在分支上开发功能
- [ ] 合并分支到主分支
- [ ] 解决可能的冲突

**操作步骤**:

```powershell
# 1. 创建并切换到新分支
git checkout -b feature-advanced-git

# 2. 在分支上开发功能
echo "# 高级 Git 技巧" > "01-学习笔记/高级 Git 技巧.md"
git add .
git commit -m "新增：高级 Git 技巧笔记"

# 3. 切换回主分支
git checkout main

# 4. 合并分支
git merge feature-advanced-git

# 5. 推送
git push

# 6. 删除已合并的分支
git branch -d feature-advanced-git
```

---

### Task 3: 完整协作流程模拟

**目标**: 模拟真实的团队协作流程，使用 Pull Request 进行代码审查和合并。

**验收标准**:
- [ ] 创建功能分支并开发
- [ ] 推送分支到 GitHub
- [ ] 创建 Pull Request
- [ ] 进行 Code Review
- [ ] 合并 PR

**操作步骤**:

```powershell
# 1. 创建功能分支
git checkout -b feature-collaboration

# 2. 开发功能
# ... 编辑文件 ...
git add .
git commit -m "新增：团队协作规范文档"

# 3. 推送分支
git push -u origin feature-collaboration

# 4. 在 GitHub 创建 Pull Request（手动操作）
# 访问：https://github.com/你的用户名/仓库名/pulls
# 点击 "New pull request"
# 选择 base: main, compare: feature-collaboration
# 填写 PR 信息并创建

# 5. Code Review（在 GitHub 网页）
# 查看文件变更，添加评论

# 6. 合并 PR（在 GitHub 网页）
# 点击 "Merge pull request"

# 7. 本地同步
git checkout main
git pull
git branch -d feature-collaboration
```

---

## 简单的提交规范 ⭐

> 这是你最关心的部分！每次任务产出后，按照下面的模板编写提交信息。

### 最简单的提交格式

```powershell
git commit -m "类型：简短描述"
```

### 6 个常用类型（记住这个就够了！）

| 类型 | 使用场景 | 示例 |
|------|----------|------|
| **新增** | 添加新功能、新文件 | `新增：STM32 LED 控制示例` |
| **修复** | 修复 Bug、错误 | `修复：串口通信波特率错误` |
| **更新** | 更新现有内容 | `更新：README 添加安装说明` |
| **优化** | 性能优化、代码改进 | `优化：提升查询速度 50%` |
| **文档** | 文档相关修改 | `文档：补充 API 使用说明` |
| **删除** | 删除文件、功能 | `删除：废弃的配置文件` |

---

### 实际应用场景

#### 场景 1: 完成一个学习任务后

```powershell
# 学习了 STM32 GPIO 控制 LED
git add .
git commit -m "新增：STM32 GPIO 控制 LED 示例"
git push
```

#### 场景 2: 修复了一个 Bug

```powershell
# 修复了串口通信的问题
git add .
git commit -m "修复：串口通信波特率配置错误"
git push
```

#### 场景 3: 更新了文档

```powershell
# 修改了 README 文件
git add .
git commit -m "更新：README 添加项目说明"
git push
```

#### 场景 4: 优化了代码

```powershell
# 改进了代码性能
git add .
git commit -m "优化：减少内存占用 30%"
git push
```

#### 场景 5: 添加了学习笔记

```powershell
# 整理了今天的学习笔记
git add .
git commit -m "新增：FreeRTOS 任务调度学习笔记"
git push
```

#### 场景 6: 删除了不需要的文件

```powershell
# 清理临时文件
git add .
git commit -m "删除：临时测试文件"
git push
```

---

### 提交信息模板（直接套用！）

**模板 1: 新增功能**
```powershell
git commit -m "新增：[具体功能名称]"
# 示例
git commit -m "新增：STM32 串口通信示例"
git commit -m "新增：FreeRTOS 传感器数据采集"
```

**模板 2: 修复问题**
```powershell
git commit -m "修复：[具体问题]"
# 示例
git commit -m "修复：LED 闪烁频率错误"
git commit -m "修复：内存泄漏问题"
```

**模板 3: 更新内容**
```powershell
git commit -m "更新：[更新的内容]"
# 示例
git commit -m "更新：项目依赖版本升级"
git commit -m "更新：配置文件参数调整"
```

**模板 4: 文档相关**
```powershell
git commit -m "文档：[文档内容]"
# 示例
git commit -m "文档：添加 API 接口说明"
git commit -m "文档：补充安装步骤"
```

---

### 每日提交流程示例

```powershell
# 早上开始学习
git pull

# 学习 STM32 GPIO...
# 编写代码...
# 测试通过...

# 提交第一次
git status
git add .
git commit -m "新增：STM32 GPIO 控制 LED 示例"
git push

# 继续学习串口通信...
# 发现问题并修复...

# 提交第二次
git status
git add .
git commit -m "修复：串口通信初始化顺序错误"
git push

# 整理学习笔记...

# 提交第三次
git status
git add .
git commit -m "新增：STM32 基础知识学习笔记"
git push
```

---

### 常见错误示例

**❌ 不好的提交信息**:
```powershell
git commit -m "update"           # 太模糊
git commit -m "fix bug"          # 不知道修复了什么
git commit -m "修改了一些代码"    # 没有信息量
git commit -m "今天的学习"        # 不知道学了什么
git commit -m "asdfasdf"         # 乱写
```

**✅ 好的提交信息**:
```powershell
git commit -m "新增：STM32 LED 控制示例"
git commit -m "修复：串口通信波特率错误"
git commit -m "更新：README 添加使用说明"
git commit -m "优化：减少延时函数执行时间"
git commit -m "文档：补充 GPIO 配置说明"
```

---

### 提交频率建议

**推荐**:
- ✅ 完成一个小功能就提交一次
- ✅ 修复一个 Bug 就提交一次
- ✅ 学习完一个知识点就提交一次
- ✅ 每天至少提交一次

**不推荐**:
- ❌ 几天才提交一次（容易丢失）
- ❌ 一次提交太多内容（难以回退）
- ❌ 提交信息模糊（不知道改了什么）

---

## 常见问题解决

### ❌ 问题 1: 推送时提示需要 Token

**解决方案**:
1. 访问 https://github.com/settings/tokens
2. 点击 "Generate new token (classic)"
3. 配置：
   - Note: `我的第一个 Token`
   - Expiration: `90 days`
   - 勾选：✅ repo
4. 点击 "Generate token"
5. 复制 Token（只显示一次！）
6. 推送时粘贴 Token（不是密码）

---

### ❌ 问题 2: GitHub 返回 502 错误

**错误信息**:
```
fatal: unable to access 'https://github.com/...': The requested URL returned error: 502
```

**解决方案**:
- 等待几分钟后重试
- 检查 GitHub 状态：https://www.githubstatus.com/

---

### ❌ 问题 3: 合并冲突

**解决方案**:
```powershell
# 1. 查看冲突文件
git status

# 2. 打开冲突文件，找到冲突标记
# <<<<<<< HEAD
# 你的修改
# =======
# 其他人的修改
# >>>>>>>

# 3. 手动编辑，保留需要的内容，删除冲突标记

# 4. 标记冲突已解决
git add 冲突文件.md

# 5. 完成合并
git commit -m "合并：解决冲突"
```

---

### ❌ 问题 4: 忘记切换分支

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

## 快速参考卡

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

---

### 提交信息速查

```
新增：添加新功能
修复：修复 Bug
更新：更新现有功能
优化：性能优化
文档：文档更新
删除：删除文件
```

---

### 每日工作流

```powershell
# 早上开始
git pull

# 编辑文件...

# 晚上结束
git add .
git commit -m "完成：今天的学习任务"
git push
```

---

**祝你学习愉快！** 🚀

**最后更新**: 2026-03-10  
**版本**: v2.0（简化实用版）
