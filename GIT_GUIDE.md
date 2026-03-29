# Git 常用命令速查

> 每天写完笔记后，照着下面的流程操作即可

---

## 每日工作流（最常用）

```bash
# 1. 查看当前改动
git status

# 2. 添加所有改动到暂存区
git add .

# 3. 提交改动（引号里写今天的主题）
git commit -m "学习: 两数之和"

# 4. 推送到 GitHub
git push

# ===== 一键完成 =====
git add . && git commit -m "学习: 今日LeetCode" && git push
```

---

## 查看信息

| 命令 | 作用 |
|------|------|
| `git status` | 查看当前改动状态 |
| `git log --oneline` | 查看提交历史（简洁版） |
| `git log` | 查看完整提交历史 |
| `git diff` | 查看未暂存的改动内容 |
| `git remote -v` | 查看远程仓库地址 |

---

## 撤销操作

| 命令 | 作用 |
|------|------|
| `git restore <文件>` | 撤销工作区改动（未 add 前） |
| `git restore --staged <文件>` | 取消暂存（已 add，但想撤回） |
| `git commit --amend` | 修改上一次提交信息 |

---

## 分支操作

| 命令 | 作用 |
|------|------|
| `git branch` | 查看所有分支 |
| `git branch <分支名>` | 创建新分支 |
| `git checkout <分支名>` | 切换分支 |
| `git checkout -b <分支名>` | 创建并切换到新分支 |
| `git merge <分支名>` | 合并指定分支到当前分支 |

---

## 同步远程

| 命令 | 作用 |
|------|------|
| `git pull` | 拉取远程最新代码 |
| `git push` | 推送到远程 |
| `git clone <仓库地址>` | 克隆远程仓库到本地 |

---

## 常见问题

### 提示 "fatal: not a git repository"
说明当前目录没有初始化 git，运行：
```bash
git init
```

### 推送时提示输入用户名密码
可以使用 SSH 或配置 token。简单方案：
```bash
# 配置记住密码（缓存15分钟）
git config --global credential.helper cache

# 或缓存1小时
git config --global credential.helper 'cache --timeout=3600'
```

### 不想提交某个文件
创建 `.gitignore` 文件，写入要忽略的文件名或模式：
```
.DS_Store
*.tmp
node_modules/
```

### 提交后发现写错了
```bash
# 修改上一次提交信息
git commit --amend -m "正确的提交信息"

# 如果已经 push 了，需要强制推送（慎用）
git push --force
```

---

## 推荐学习资源

- [Git 官方文档](https://git-scm.com/doc)
- [Pro Git 电子书](https://git-scm.com/book/zh/v2)（中文版免费）
- [Learn Git Branching](https://learngitbranching.js.org/)（可视化学习）
