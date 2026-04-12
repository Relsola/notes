# 环境配置

这里以 `Debian` 为例。

### 安装基础下载工具

```bash
sudo apt update
sudo apt install wget curl -y
```

### 安装最新版 LLVM

```bash
# 从官方仓库下载安装脚本
wget https://apt.llvm.org/llvm.sh

# 加执行权限
chmod +x llvm.sh

# 执行脚本
sudo ./llvm.sh
```
