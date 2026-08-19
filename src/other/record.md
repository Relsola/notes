# Relsola‘s Blog

不要过度设计

## 架构设计

```text
┌──────────────────────────────────────────────────────────┐
│                   访客浏览器 (Client)                    │
│   - HTML / Classless CSS 排版                            │
│   - Marked.js 动态解析 Markdown                          │
│   - Highlight.js 代码高亮 & 交互 (暗黑模式/复制等)        │
└─────────────────────────────▲────────────────────────────┘
                              │ HTTP (HTML/JSON)
┌─────────────────────────────▼────────────────────────────┐
│              Relsola C++ Server (Crow + Asio)            │
│                                                          │
│  ┌────────────────────────────────────────────────────┐  │
│  │ 路由转发器 (Routes Handler)                       │  │
│  │  - GET /               -> 返回首页与文章列表 JSON   │  │
│  │  - GET /posts/<title>  -> 读取 .md 文件并拼装模板   │  │
│  └──────────────────────────┬─────────────────────────┘  │
│                             │ 读文件 (std::filesystem)   │
│  ┌──────────────────────────▼─────────────────────────┐  │
│  │ 本地文件系统 (./posts/*.md)                        │  │
│  │  - 纯 Markdown 存储，版本控制跟随 Git               │  │
│  └────────────────────────────────────────────────────┘  │
└──────────────────────────────────────────────────────────┘
```

## 配置 Linux

下载 Nginx

```bash
sudo apt update

sudo apt install nginx -y

# 进入默认配置目录
cd /etc/nginx/sites-enabled/

# 备份默认文件
mv default default.bak

# 软链接自己的配置 [源文件绝对路径] [目标软链接路径]
ln -s /home/code/Relsola/config/nginx.conf /etc/nginx/sites-enabled/nginx.conf

# 验证配置文件是否正确
nginx -t

# 平滑重载（Reload）让配置生效
nginx -s reload
```
