[//] 注释
[--] email  relsola1018@gmail.com
[--] author Alice Relsola
[--] title  Git 详解

## 设置 git

```bash
# 1. 设置用户名（建议填你的 GitHub 账号用户名）
git config --global user.name "你的GitHub用户名"

# 2. 设置邮箱（必须是你在 GitHub 上绑定的那个邮箱）
git config --global user.email "你的GitHub邮箱@example.com"

# 生成新的 SSH 密钥
ssh-keygen -t ed25519 -C "你的GitHub邮箱@example.com"

# 打印密钥
cat ~/.ssh/id_ed25519.pub

## 绑定密钥后测试连接
ssh -T git@github.com
```

## git 简单命令

```bash
# 1. 初始化本地仓库（如果之前没初始化过）
git init

# 2. 将所有文件添加到暂存区（它会自动读取你的 .gitignore 忽略 build 等文件）
git add .

# 3. 提交代码到本地
git commit -m "feat: initial commit with Crow, Asio and README"

# 4. 设置默认分支名为 main
git branch -M main

# 5. 关联 GitHub 远程仓库 (注意将下面的地址换成你自己的 SSH 仓库地址)
git remote add origin git@github.com:Relsola/Relsola.git

# 6. 推送到 GitHub
git push -u origin main
```

