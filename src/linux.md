# Linux

## PowerShell + Oh my posh

配置 PowerShell 别名适应 bash

```bash
bash -c "which oh-my-posh"
```

windows
```bash
# 编辑 PowerShell 配置文件
notepad $PROFILE

# 确保先创建配置文件
New-Item -Path $PROFILE -Type File -Force

# oh-my-posh init pwsh --config 'D:/configs/ohmyposh/half-life.omp.json' | Invoke-Expression
```

linux
```bash
curl -s https://ohmyposh.dev/install.sh | bash -s -- -d /usr/local/bin

# /mnt/d/<PATH>
```

## WSL2

```bash
wsl --shutdown         # 关闭wsl
wsl --update           # 更新wsl
wsl -l -v              # 查看发行版
wsl --unregister Arch  # 卸载发行版
wsl -d Arch            # 启动发行版
wsl -t Arch            # 终止发行版进程
```

## WSL2 安装 Arch


1. 下载 https://github.com/yuk7/ArchWSL 解压并使用 arch.exe 安装  

2. 初始化 Arch

```bash
# 初始化pacman密钥
pacman-key --init

# 填充Arch Linux密钥
pacman-key --populate archlinux

# 刷新密钥
pacman-key --refresh-keys

# 清理损坏的包缓存
pacman -Scc

# 更新数据库
pacman -Syy

# 更新 archlinux-keyring
pacman -S archlinux-keyring

# 只更新密钥环包
pacman -S archlinux-keyring --noconfirm

# 然后更新系统
pacman -Syu
```

3. WSL2 上安装 KDE Plasma

```bash
# 安装 Xorg 显示服务器
pacman -S xorg-server

# 安装 KDE Plasma 桌面环境（精简版）
pacman -S plasma-desktop

# 或者安装完整版（包含更多KDE组件，推荐）
# qt6-multimedia-ffmpeg | pipewire-jack | noto-fonts
pacman -S plasma

# 终端模拟器
pacman -S konsole

# 文件管理器
pacman -S dolphin

# 文本编辑器
pacman -S kate

# 系统设置
pacman -S systemsettings

# 中文字体
pacman -S noto-fonts-cjk wqy-microhei wqy-zenhei

# Fcitx5 输入法框架
pacman -S fcitx5-im fcitx5-chinese-addons
```

4. 配置输入法环境变量

```bash
# 1. 设置环境变量
cat >> ~/.bashrc << 'EOF'
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
export INPUT_METHOD=fcitx
export SDL_IM_MODULE=fcitx
export GLFW_IM_MODULE=ibus
EOF

# 2. 使环境变量生效
source ~/.bashrc

# 3. 启动输入法（在KDE启动后运行）
fcitx5 &

# 4. 配置输入法（图形界面）
fcitx5-configtool
```


5. 启动 KDE

```bash
startplasma-x11
```

6. 切换 power shell

```bash
# 安装一些依赖
pacman -S curl tar

# 下载最新版PowerShell
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v7.4.2/powershell-7.4.2-linux-x64.tar.gz

# 创建目标目录
mkdir -p /opt/microsoft/powershell/7

# 解压
tar -xzf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/7

# 创建符号链接
ln -sf /opt/microsoft/powershell/7/pwsh /usr/bin/pwsh

# 清理
rm /tmp/powershell.tar.gz

# 给pwsh文件添加执行权限
sudo chmod +x /opt/microsoft/powershell/7/pwsh
sudo chmod +x /usr/bin/pwsh

# 查看/etc/shells中列出的所有合法shell
cat /etc/shells

# 查看当前shell
echo $SHELL
echo $0

# 设置为默认shell
chsh -s /usr/bin/pwsh
```

## Arch 自定义
