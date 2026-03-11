# 发现：Git 分支管理与协作

## 核心概念

### 分支的本质
- 分支 = 指向提交的指针
- HEAD = 当前所在分支的指针
- 切换分支 = 移动 HEAD 指针
- 每次提交 = 移动当前分支指针到新提交

### 分支命名规范
```
功能分支：feature/功能名称
修复分支：fix/问题描述
热修复：hotfix/紧急修复
发布分支：release/版本号
实验分支：experiment/实验内容
```

## Git Flow vs GitHub Flow vs Trunk Based

### Git Flow（传统）
```
main (生产)
  └── develop (开发)
        ├── feature/*
        ├── hotfix/*
        └── release/*
```
- 适合：长期项目、多版本维护
- 优点：结构清晰、版本管理严格
- 缺点：流程复杂、合并频繁

### GitHub Flow（轻量）
```
main (唯一长期分支)
  └── feature/* (短期分支，PR 后删除)
```
- 适合：持续部署、快速迭代
- 优点：简单高效、代码快速上线
- 缺点：不适合多版本并行

### Trunk Based（现代）
```
main (主干，所有人直接提交)
  └── 短期分支 (< 2 天)
```
- 适合：成熟团队、高测试覆盖率
- 优点：合并冲突少、集成快
- 缺点：需要强文化约束

## 远程协作流程

### 标准 PR 流程
1. 从 main 创建功能分支
2. 本地开发并提交
3. 推送分支到远程
4. 创建 Pull Request
5. Code Review
6. 解决评论/冲突
7. 合并到 main
8. 删除功能分支

### 同步远程变更
```bash
# 方式 1: rebase（推荐，保持历史整洁）
git fetch origin
git rebase origin/main

# 方式 2: merge（保留完整历史）
git fetch origin
git merge origin/main

# 方式 3: pull（=fetch+merge）
git pull origin main
```

## 冲突解决策略

### 冲突产生原因
- 同一文件的同一区域被不同分支修改
- 一个分支修改文件，另一个分支删除该文件
- 文件重命名冲突

### 解决步骤
1. `git status` 查看冲突文件
2. 打开文件，找到冲突标记 `<<<<<<<`, `=======`, `>>>>>>>`
3. 手动编辑，保留需要的代码
4. `git add <文件>` 标记为解决
5. `git commit` 完成合并

### 预防冲突
- 频繁同步远程变更
- 小步提交，快速合并
- 明确代码所有权
- 使用 Code Owners 文件

## 相关资源
- [Git 分支模型 (A successful Git branching model)](https://nvie.com/posts/a-successful-git-branching-model/)
- [GitHub Flow](https://docs.github.com/en/get-started/using-github/github-flow)
- [Git 官方文档 - 分支](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E7%AE%80%E4%BB%8B)

## 待验证假设
- [ ] 用户能够独立完成完整的 PR 流程
- [ ] 用户能够理解 rebase 和 merge 的区别
- [ ] 用户能够解决至少 3 种类型的合并冲突

## 参考资料
- `Git 实战使用指南.md` v4.0
- `Git 和 GitHub 完整使用指南.md` v1.0
