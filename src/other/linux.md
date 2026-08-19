# Linux 服务器使用记录

## 个人常用环境搭建

`htop` : Linux 终端里的任务管理器

## 与 Windows 主机互操作

### 使用 SSH 连接远程主机

-  `-p` 222 指定端口，默认是 22 端口
-  `-i` "C:\path\key.pem" 指定密钥路径

```bat
ssh -i "C:\Users\30890\.ssh\Relsola.pem" root@12.34.56.78
```

### 配置简洁登录

```bat
@REM 上传公钥并设置权限
type %USERPROFILE%\.ssh\id_ed25519.pub | ssh -i "C:\Users\30890\.ssh\Relsola.pem" root@12.34.56.78 "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys && chmod 700 ~/.ssh"

@REM 配置别名登录
code %USERPROFILE%\.ssh\config

@REM
ssh relsola
```

追加打开的 config

```txt
Host relsola
    HostName 12.34.56.78
    User root
    IdentityFile C:\Users\30890\.ssh\id_ed25519
    # 每隔 30 秒自动发送一次心跳包到服务器
    ServerAliveInterval 30
    # 连续发送 3 次都没有收到服务器的响应自主断开
    ServerAliveCountMax 3
```

### 其它操作


```bat
@REM 下载文件 [-r] 传递文件夹
scp relsola:"/home/blog/posts/asf.md" "%USERPROFILE%\Desktop\"

@REM 上传文件
scp "%USERPROFILE%\Desktop\new.md" relsola:"/home/blog/posts/"
```

## 系统服务

现代 Linux 系统基本都使用 systemctl 来管理系统后台服务

```bash
# 列出所有正在运行的服务
systemctl list-units --type=service --state=running

# 查看服务如 nginx
systemctl status nginx

# 停止服务如 nginx
systemctl stop nginx

# 启动服务如 nginx
systemctl start nginx
```

## 文件操作
