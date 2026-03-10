# 🎯 Git 和 GitHub 完整使用指南

> 从零开始，手把手教你使用 Git 和 GitHub，包含所有常见问题解决方案

**版本**: v1.0（完整整合版）  
**最后更新**: 2026-03-10

---

## 📚 目录

1. [Git 基础概念](#git-基础概念)
2. [完整工作流程](#完整工作流程)
3. [核心命令教学](#核心命令教学)
4. [GitHub 使用方法](#github-使用方法)
5. [常见问题解决](#常见问题解决)
6. [最佳实践](#最佳实践)
7. [学习资源](#学习资源)

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

#### 第二步：在本地创建项目

**方法 A：克隆远程仓库（推荐）**

```powershell
# 1. 进入工作目录
cd d:\AIcode\Github

# 2. 克隆远程仓库
git clone https://github.com/你的用户名/仓库名.git

# 3. 进入项目目录
cd 仓库名
```

**方法 B：本地创建后推送**

```powershell
# 1. 创建项目目录
mkdir Embedded-Automotive-2026
cd Embedded-Automotive-2026

# 2. 创建文件和文件夹
New-Item -ItemType Directory -Force -Path "0-Learning-Notes"
New-Item -ItemType Directory -Force -Path "1-STM32-Basics"
echo "# Embedded-Automotive-2026" > README.md

# 3. 初始化 Git 仓库
git init

# 4. 添加远程仓库
git remote add origin https://github.com/你的用户名/仓库名.git
```

---

#### 第三步：提交代码到本地仓库

```powershell
# 1. 查看当前状态
git status

# 2. 添加文件到暂存区
git add .              # 添加所有文件
# 或
git add README.md      # 添加单个文件

# 3. 提交到本地仓库
git commit -m "初始化：创建项目目录结构"
```

---

#### 第四步：推送到 GitHub

```powershell
# 首次推送
git push -u origin master

# 后续推送
git push
```

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

## 核心命令教学

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

#### 2. 查看状态

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

**提交信息规范**：
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
git push -u origin master

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
git checkout master
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

## GitHub 使用方法

### 🌐 GitHub 核心功能

#### 1. 创建仓库

**步骤**：
1. 登录 https://github.com
2. 点击右上角 "+" → "New repository"
3. 填写信息：
   - Repository name: 仓库名
   - Description: 描述（可选）
   - Public/Private: 公开/私有
   - ✅ Add a README file
4. 点击 "Create repository"

---

#### 2. 查看仓库

**访问仓库**：
- 直接访问：`https://github.com/用户名/仓库名`

**查看内容**：
- 点击文件名查看文件内容
- 点击目录名进入目录
- 点击分支选择器切换分支

---

#### 3. 创建 Personal Access Token

**为什么需要 Token**：
GitHub 已不再支持密码认证，推送时需要 Token。

**创建步骤**：
1. 访问 https://github.com/settings/tokens
2. 点击 "Generate new token (classic)"
3. 配置：
   - Note: `Embedded-Automotive-2026`
   - Expiration: `90 days` 或 `No expiration`
   - 勾选：✅ repo（完整仓库权限）
4. 点击 "Generate token"
5. **立即复制 Token**（只显示一次！）

**使用 Token**：
```powershell
git push
# Username: 输入 GitHub 用户名
# Password: 粘贴 Token（不是密码）
```

---

#### 4. 配置凭证管理器（推荐）

**配置一次，永久自动保存密码**：

```powershell
# 配置凭证管理器
git config --global credential.helper manager
```

**作用**：
- 第一次推送时输入 GitHub 用户名和 Token
- 之后自动保存凭证，无需重复输入

---

#### 5. 配置 SSH 密钥（可选）

**生成 SSH 密钥**：
```powershell
ssh-keygen -t rsa -b 4096 -C "你的邮箱"
# 按三次回车
```

**添加到 GitHub**：
1. 查看公钥：`cat ~/.ssh/id_rsa.pub`
2. 复制公钥内容
3. 访问 https://github.com/settings/keys
4. 点击 "New SSH key"
5. 粘贴公钥内容
6. 点击 "Add SSH key"

**测试连接**：
```powershell
ssh -T git@github.com
# 成功输出：Hi 用户名！You've successfully authenticated...
```

---

## 常见问题解决

### ❌ 问题 1：SSH 端口 22 被阻止

**错误信息**：
```
ssh: connect to host github.com port 22: Connection refused
```

**原因**：
- 防火墙或网络环境阻止了 SSH 端口 22
- 常见于公司网络、校园网、某些地区网络

**解决方案 1：使用 HTTPS + 凭证管理器（推荐）**

```powershell
# 1. 配置凭证管理器
git config --global credential.helper manager

# 2. 切换到 HTTPS 地址
git remote remove origin
git remote add origin https://github.com/用户名/仓库名.git

# 3. 推送（首次需要输入 Token）
git push -u origin master
```

**优势**：
- ✅ 无需配置 SSH 密钥
- ✅ 通过 HTTPS 端口（443）连接，不会被阻止
- ✅ 配置凭证管理器后，无需每次输入密码
- ✅ 简单快速，立即可用

**解决方案 2：SSH 通过 443 端口连接**

手动创建 SSH 配置文件（Windows）：
1. 打开记事本
2. 输入以下内容：
   ```
   Host github.com
     Hostname ssh.github.com
     Port 443
     User git
   ```
3. 保存到：`C:\Users\你的用户名\.ssh\config`
4. 测试连接：`ssh -T git@github.com`

---

### ❌ 问题 2：GitHub 仓库没有完整目录结构

**现象**：
- 本地仓库有完整的目录结构 ✅
- GitHub 仓库只有 README.md ❌

**原因**：
- 本地分支是 `master`
- GitHub 仓库的默认分支是 `main`
- 两个分支不同步

**解决方案**：

**方法 1：切换到 master 分支查看**
1. 访问 GitHub 仓库
2. 点击分支选择器（显示 `main`）
3. 切换到 `master` 分支
4. 应该有完整目录结构

**方法 2：设置 master 为默认分支**
1. 访问仓库设置：`https://github.com/用户名/仓库名/settings`
2. 向下滚动到 "Default branch"
3. 点击 "Switch default branch"
4. 选择 `master`
5. 确认切换

**方法 3：强制推送到 master 分支**
```powershell
cd d:\AIcode\Github\Embedded-Automotive-2026
git push -u origin master --force
```

---

### ❌ 问题 3：git push 失败，提示"非快进更新"

**错误信息**：
```
! [rejected]        master -> master (non-fast-forward)
```

**原因**：远程仓库有新的提交，本地未拉取

**解决方案**：
```powershell
# 方法 1：拉取并合并
git pull --rebase origin master
git push

# 方法 2：强制推送（谨慎使用！会覆盖远程修改）
git push -f
```

---

### ❌ 问题 4：忘记切换分支，在 master 上修改了

**解决方案**：
```powershell
# 1. 暂存当前修改
git stash

# 2. 创建并切换到新分支
git checkout -b feature-new

# 3. 恢复修改
git stash pop

# 4. 提交到新分支
git add .
git commit -m "新增：新功能"
git push -u origin feature-new
```

---

### ❌ 问题 5：提交了错误的文件

**解决方案**：
```powershell
# 情况 1：还未 push
# 撤销最后一次提交（保留修改）
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

### ❌ 问题 6：推送时提示"Authentication failed"

**原因**：
1. Token 不正确
2. Token 已过期
3. 用户名错误

**解决方案**：
1. 检查 Token 是否正确复制
2. 重新创建 Token
3. 确认用户名是 GitHub 用户名（不是邮箱）
4. 清除已保存的凭证：
   - 控制面板 → 用户账户 → 凭据管理器
   - Windows 凭据 → 普通凭据
   - 删除 `git:https://github.com`

---

### ❌ 问题 7：GitHub 返回 502 错误

**错误信息**：
```
fatal: unable to access 'https://github.com/...': The requested URL returned error: 502
```

**原因**：GitHub 服务器临时故障

**解决方案**：
- 等待几分钟后重试
- 检查 GitHub 状态：https://www.githubstatus.com/
- 通常很快会自动恢复

---

## 最佳实践

### 1. Commit 信息规范

**推荐格式**：
```
<类型>: <简短描述>

<详细描述>（可选）
```

**类型说明**：
- `新增`：添加新功能
- `修复`：修复 Bug
- `更新`：更新现有功能
- `优化`：性能优化或代码重构
- `文档`：文档更新
- `测试`：添加测试

**示例**：
```powershell
git commit -m "新增：添加用户登录功能"
git commit -m "修复：解决内存泄漏问题"
git commit -m "优化：提升查询性能 50%"
git commit -m "文档：更新 README 使用说明"
```

---

### 2. .gitignore 文件

创建`.gitignore` 文件，忽略不需要提交的文件：

```
# 编译输出
*.o
*.obj
*.exe
*.out

# 调试文件
*.log
*.dSYM/

# IDE 配置
.vscode/
.idea/
*.swp

# 系统文件
.DS_Store
Thumbs.db

# 临时文件
*.tmp
*.bak
*~

# 依赖目录
node_modules/
vendor/
```

---

### 3. 分支命名规范

```
master/main     - 主分支（生产环境）
develop         - 开发分支
feature-xxx     - 功能分支
bugfix-xxx      - Bug 修复分支
release-x.x.x   - 发布分支
hotfix-xxx      - 紧急修复分支
```

**示例**：
```powershell
git checkout -b feature-freertos
git checkout -b bugfix-memory-leak
git checkout -b release-1.0.0
```

---

### 4. 定期提交

**建议频率**：
- ✅ 每完成一个小功能就提交
- ✅ 每天至少提交一次
- ✅ 提交前先 `git status` 检查
- ✅ 提交信息要清晰明了

**不要**：
- ❌ 几天才提交一次
- ❌ 提交信息模糊（"update"、"fix bug"）
- ❌ 一次提交太多文件

---

### 5. 推送前先拉取

```powershell
# 养成好习惯
git pull
git push

# 或者使用组合命令
git pull && git push
```

---

### 6. 使用别名简化命令

```powershell
# 设置常用别名
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.lg "log --oneline --graph --all"

# 使用别名
git st
git co master
git br
git ci -m "提交信息"
git lg
```

---

## 学习资源

### 官方资源
- **Git 官方文档**: https://git-scm.com/doc
- **Pro Git 书籍**: https://git-scm.com/book/zh/v2（免费）
- **GitHub 官方文档**: https://docs.github.com/cn

### 交互式学习
- **Learn Git Branching**: https://learngitbranching.js.org/?locale=zh_CN
- **GitHub Skills**: https://skills.github.com/

### 视频教程
- B 站搜索："Git 教程"、"GitHub 教程"

---

## 快速参考卡

### 最常用命令

```powershell
git status              # 查看状态
git add .              # 添加所有文件
git commit -m "信息"    # 提交
git push               # 推送
git pull               # 拉取
git log --oneline      # 查看历史
git branch             # 查看分支
git checkout -b 分支名  # 创建并切换分支
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

### 方案对比

| 方案 | 优点 | 缺点 | 推荐度 |
|------|------|------|--------|
| **HTTPS + 凭证管理器** | 简单快速<br>不会被阻止<br>自动保存密码 | 首次需输入 Token | ⭐⭐⭐⭐⭐ |
| **SSH + 443 端口** | 无需输入密码<br>更安全 | 需配置 SSH 密钥<br>需修改配置文件 | ⭐⭐⭐⭐ |
| **SSH + 端口 22** | 标准方式 | 端口 22 被阻止<br>无法使用 | ⭐ |

---

## 🎯 推荐工作流程

### 对于新手

1. **先使用 HTTPS**（快速开始）
2. **配置凭证管理器**（自动保存密码）
3. **熟悉 Git 后配置 SSH**（长期便利）

### 对于长期使用

1. **配置 SSH 密钥**（一劳永逸）
2. **配置 Git 凭证管理器**（HTTPS 自动保存）
3. **使用别名简化命令**（提高效率）

---

**最后更新**: 2026-03-10  
**版本**: v1.0（完整整合版）  
**状态**: ✅ 已解决所有常见问题
