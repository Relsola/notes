# WSL 中使用 Linux

这里以 `Debian` 为例。

1. 安装发行版

```bash
# 查看可供下载的发行版
wsl --list --online

# 安装
wsl --install Debian

# 查看已安装的版本
wsl --list --verbose
```

2. 迁移到D盘

```bash
# 导出分发版为tar文件到d盘
wsl --export Debian d:\wsl-debian.tar

# 注销当前分发版
wsl --unregister Debian

# 重新导入并安装在指定目录
wsl --import Debian d:\WSL\Debian d:\wsl-debian.tar --version 2

# 删除tar文件
del d:\wsl-debian.tar
```

3. WSL 常用命令

```bash
# 关闭wsl
wsl --shutdown

# 更新wsl
wsl --update

# 启动发行版
wsl -d Debian

# 终止发行版进程
wsl -t Debian         
```
