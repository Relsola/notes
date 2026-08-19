# 使用 ArchiSteamFarm 挂卡

记录下在服务器上使用 ArchiSteamFarm 挂卡

> 这里参考的配置文件注释最后需要删除

项目主页：[https://github.com/JustArchiNET/ArchiSteamFarm](https://github.com/JustArchiNET/ArchiSteamFarm)

中文WIKI文档：[https://github.com/JustArchiNET/ArchiSteamFarm/wiki/Setting-up-zh-CN](https://github.com/JustArchiNET/ArchiSteamFarm/wiki/Setting-up-zh-CN)

请先耐心看完文档几乎就能解决大部分问题

## 下载配置环境

```bash
# 环境配置， Debian 稳定版仅需再手动安装 libicu76
apt update && apt install -y libicu76

# 创建并进入 ASF 相关目录
mkdir -p /opt/asf && cd /opt/asf

# 查看服务器架构
uname -m

# 下载相应的文件
wget https://github.com/JustArchiNET/ArchiSteamFarm/releases/download/6.3.9.5/ASF-linux-x64.zip

# 下载解压程序
apt install -y unzip

# 解压到 core 路径
unzip ASF-linux-x64.zip -d core
```

## 配置及调试

### BOT 配置

路径： core/config/Relsola.json

一个 xxx.json 就代表一个挂卡机器人

```json
{
    // 启用机器人
	"Enabled": true,
    // 跳过挂卡直接挂时长
	"FarmingPreferences": 1,
    // 不处理交易
    "BotBehaviour": 64,
    // 挂时长游戏ID，游戏商店页面url上有
	"GamesPlayedWhileIdle": [
		730,
		570
	],
	"SteamLogin": "账号",
	"SteamPassword": "密码"
}
```

### ASF 配置

```json
{
    // 性能选项
    "OptimizationMode": 1
}
```

### 首次登录授权调试

```bash
# 可以下载 tmux 用于 web 调试（可选）
apt install -y tmux

# 文件路径
cd /opt/asf/core

# 给可执行文件授权
chmod +x ArchiSteamFarm

# 启动服务
./ArchiSteamFarm
```

执行后等待登录然后使用 steam 令牌验证，然后在程序终端输入 Y 确认就行

正常运行后后你可以打开一个本地 web 界面调试，例如 http://localhost:1242/bot/relsola

其余操作可以参考 wiki， 比如按 c 可用进入指令交互

## 设置服务后台永久运行

### 创建配置文件 /etc/systemd/system/asf.service

```ini
[Unit]
Description=ArchiSteamFarm Service
# 在网络服务启动成功后再启动 ASF
After=network.target

[Service]
Type=simple
User=root
# ASF 可执行文件目录
WorkingDirectory=/opt/asf/core
# 启动命令：--no-ui 会在后台运行期间强制关闭 Web 界面以降低资源占用
ExecStart=/opt/asf/core/ArchiSteamFarm --no-ui

# 进程异常退出/崩溃后总是自动重启
Restart=always
# 崩溃后等待 10 秒再重新启动，防止频繁重试
RestartSec=10

# 硬限制最大内存150MB
MemoryMax=150M
# 软限制130MB调度触发.NET垃圾回收
MemoryHigh=125M

[Install]
# 随系统多用户模式开机自启
WantedBy=multi-user.target
```

配置下日志防止磁盘被刷爆

位置：/etc/systemd/journald.conf

```ini
[Journal]
# 限制任意服务 30 秒内最多只能写 500 条日志
RateLimitBurst=500
# 设置200M日志上限
SystemMaxUse=200M
# 强制日志文件最多只保留 1 个月
MaxFileSec=1month
```

### 首次加载与启动

```bash
# 重新加载 systemd 配置文件
sudo systemctl daemon-reload

# 设置开机自启
sudo systemctl enable asf

# 启动 ASF
sudo systemctl start asf
```

### 日常运维与监控

```bash
# 查看服务运行状态（运行中 / 停止 / 异常）
systemctl status asf

# 查看实时运行日志（替代终端控制台输出，按 Ctrl+C 退出查看）
journalctl -u asf -f

# 重新启动 ASF 服务
sudo systemctl restart asf

# 停止 ASF 服务
sudo systemctl stop asf
```

### 临时调试

如果后续需要进行调优或登录验证，无需修改配置文件，直接运行

```bash
# 暂停后台托管服务
sudo systemctl stop asf

# 切到 ASF 目录并手动启动
cd /opt/asf/core && ./ArchiSteamFarm

# 调试结束后重新启动后台服务
sudo systemctl start asf
```
