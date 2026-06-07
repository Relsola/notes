# Emacs

## Emacs Lisp
```lisp
(add-to-list 'package-archives
             '("melpa" . "https://melpa.org/packages/") t)
```
' 是引用(`quote`)的简写。

`'package-archives` => `(quote package-archives)`

`"..."` 表示 字符串(`string`)字面量。

`t` 是 `Emacs Lisp` 里的一个特殊符号，代表 `true`，并且它的值永远是它自己。

`cons cell` 语法，表示一个二元结构 `(A . B)`, 也就是一个`键值对`风格的数据结构。


```
(defvar rc/package-contents-refreshed nil)
```

`defvar` 定义变量


``` lisp
(defun rc/require-theme (theme)
	(let ((theme-package (->> theme
														(symbol-name)
														(funcall (-flip #'concat) "-theme")
														(intern))))
		(rc/require theme-package)
		(load-theme theme t)))
```

`defun` 定义函数

`let` 用来创建局部变量

`funcall` 调用一个函数对象

`#'concat` 函数对象写法(`function quoting`)，表示 `concat` 这个函数本身

`->>` 线程宏(`thread-last`) 把上一步的结果插入到下一步表达式的最后一个参数位置

1. `theme`输入通常是个符号
2. `symbol-name` 把符号转成字符串
3. `-flip` `dash.el` 提供的高阶函数，作用是把一个二元/多元函数的参数顺序交换（“翻转参数”


## 基础操作

Emacs 键位表示 `C Ctrl` `M Alt` `S shift`

`C-g` 表示同时按下 `Ctrl` 和 `g`

`C-x C-s` 表示先同时按下 `Ctrl` 和 `x` 再同时按下 `Ctrl` 和 `s`

| 快捷键    | 操作                             | fun                              |
| --------- | -------------------------------- | -------------------------------- |
| `C-g`     | 取消操作                         | `keyboard-quit`                  |
| `M-x`     | 输入命令                         | `execute-extended-command`       |
| `C-x C-=` | 放大字号                         | `text-scale-adjust`              |
| `C-x C--` | 缩小字号                         | `text-scale-adjust`              |
| `C-x C-0` | 重置字号                         | `text-scale-adjust`              |
| `C-x C-c` | 退出程序                         | `save-buffers-kill-terminal`     |
| `C-h C-h` | 打开帮助窗口                     |                                  |
| `C-h c`   | 简要描述快捷键功能               | `describe-key-briefly`           |
| `C-h f`   | 描述函数功能                     | `describe-function`              |
| `C-h v`   | 描述变量                         | `describe-variable`              |
| `C-h ?`   | 帮助的帮助                       | `help-for-help`                  |
| ---       | ---                              |                                  |
| `C-x C-f` | 打开/创建文件                    | `find-file`                      |
| `C-x C-s` | 保存文件                         |                                  |
| ---       | ---                              | ---                              |
| `C-x h`   | 全选                             |                                  |
| `C-w`     | 剪切选区                         |                                  |
| `M-w`     | 复制选区                         |                                  |
| `C-y`     | 粘贴                             | `yank`                           |
| `C-/`     | 撤销                             | `undo`                           |
| ---       | ---                              | ---                              |
| `C-x o`   | 切换窗口                         |                                  |
| `C-x 0`   | 关闭当前窗口                     |                                  |
| `C-x 1`   | 只保留当前窗口                   |                                  |
| `C-x 2`   | 横向分屏                         |                                  |
| `C-x 3`   | 纵向分屏                         |                                  |
| `C-x k`   | 关闭缓冲区                       | `kill-buffer`                    |
| ---       | ---                              | ---                              |
| `C-f`     | 光标向左一个字符（方向键左）     | `backward-char`                  |
| `C-b`     | 光标向右一个字符（方向键右）     | `forward-char`                   |
| `C-p`     | 光标向上一行（方向键上）         | `previous-line`                  |
| `C-n`     | 光标向下一行（方向键下）         | `next-line`                      |
| `M-f`     | 光标向右移动一个词               | `forward-word`                   |
| `M-b`     | 光标向左移动一个词               | `backward-word`                  |
| `C-a`     | 光标移至行首                     | `move-beginning-of-line`         |
| `C-e`     | 光标移至行尾                     | `move-end-of-line`               |
| `M-a`     | 光标移至句首                     | `backward-sentence`              |
| `M-e`     | 光标移至句尾                     | `forward-sentence`               |
| `M-<`     | 光标移至缓冲区首                 | `beginning-of-buffer`            |
| `M->`     | 光标移至缓冲区尾                 | `end-of-buffer`                  |
| `M-r`     | 光标移动至窗口的中间、最上、最下 | `move-to-window-line-top-bottom` |
| `C-v`     | 向上翻页                         | `next-page`                      |
| `M-v`     | 向下翻页                         | `previous-page`                  |
| ---       | ---                              | ---                              |
| `C-x C-;` | 注释                             | `comment-line`                   |

`eval-buffer`


## 常用命令

| 命令                | 操作                |
| ------------------- | ------------------- |
| `M-x revert-buffer` | 手动刷新当前 buffer |
| `M-x text-mode`     | 切换模式            |

## 自定义

| 快捷键    | 操作                       | fun              |
| --------- | -------------------------- | ---------------- |
| `C-x C-g` | 打开光标处的文件路径       |                  |
| `C-c i m` | 打开当前文件的符号索引菜单 |                  |
| ---       | ---                        | ---              |
| `M-w`     | 剪切                       | `kill-region`    |
| `C-w`     | 复制                       | `kill-ring-save` |


## 功能扩展

### 终端操作

Emacs 下打开终端

`M-x shell` 打开 Emacs 内置的 shell-model

`M-x compile` 输入编译命令进行编译，在报错/警告位置按回车可跳转到源文件位置

`M-x term` 打开原生终端

`M-x vterm` 性能更好的终端体验，需安装第三方插件


终端中通常支持如下操作

`TAB` 自动补全命令和文件名

`M-p` 上一条历史命令、编译错误

`M-n` 下一条历史命令、编译错误

`C-c C-j` Emacs 键位生效

`C-c C-k`  终端键位生效

### 文件管理

## Emacs 功能操作

Emacs 会自动识别 .git | Makefile | .project 为工作目录

`project-dired` 打开历史项目目录

`M-x comint-clear-buffer` 清除 buffer 内容  

### 扩展操作

#### 录制宏操作

`C-x (`  开始录制宏

`C-x )`  结束录制宏

 `C-x e`  执行一次刚才录制的宏，连续按 `e` 会重复执行 

#### 批量处理

`C-u` 先按数字，再按命令快捷键，进行重复执行

例如 `C-u 5 C-n` 下移 5 行

`M-num` 等效于 `C-u num`

#### 多光标编辑

**安装插件  multiple-cursors**

| 自定义全局快捷键 | 功能                         | fun                             |
| ---------------- | ---------------------------- | ------------------------------- |
| `C-S-c C-S-c`    | 对选中的每行添加光标         | `mc/edit-lines`                 |
| `C->`            | 向下寻找并标记匹配项         | `mc/mark-next-like-this`        |
| `C-<`            | 向上寻找并标记匹配项         | `mc/mark-previous-like-this`    |
| `C-c C-<`        | 选中当前 Buffer 中所有匹配项 | `mc/mark-all-like-this`         |
| `C-"`            | 跳过下一个匹配项             | `mc/skip-to-next-like-this`     |
| `C-:`            | 跳过上一个匹配项             | `mc/skip-to-previous-like-this` |

### 文本搜索

`C-s` 正向增量搜素，重复使用 `C-s` 跳转到下一个匹配项

`C-y` 反向增量搜素，重复使用 `C-y` 跳转到下一个匹配项

`RET` 退出搜索模式，光标保持在当前结果上


`M-x grep` 当前目录搜索，显示列表结果

`M-x rgrep` 递归子目录搜素，显示列表结果

`M-x occur` 当前缓冲区内查找并跳转

**安装插件 ripgrep**


C-u + 数字 | M + 数字  进行重复指令操作

M-% 搜素并替换  
    - y 替换本次出现
    - n 跳过本次出现
    - ! 替换所有剩下的匹配点
    - q 退出替换
    - . 只替换当前这个然后退出
    - ^ 跳回上一个匹配
    - e 修改这次替换的替换内容
    - C-r 进入递归编辑

C-M-% 正则替换

M-x dired 浏览和管理当前目录

M-x grep | rgrep 搜索

### buffer

tab-bar

### dired

### magit

## 自定义常用配置快捷键

| 全局快捷键    | 功能                         | fun                     |
| ------------- | ---------------------------- | ----------------------- |
| `C-x p s`     | 对选中内容执行 rgrep         |                         |
| ---           | ---                          |                         |
| `C-S-c C-S-c` | 对选中的每行添加光标         |                         |
| `C->`         | 向下寻找并标记匹配项         |                         |
| `C-<`         | 向上寻找并标记匹配项         |                         |
| `C-c C-<`     | 选中当前 Buffer 中所有匹配项 |                         |
| `C-"`         | 跳过下一个匹配项             |                         |
| `C-:`         | 跳过上一个匹配项             |                         |
| ---           | ---                          |                         |
| `M-p`         | 移动到上一行                 |                         |
| `M-n`         | 移动到下一行                 |                         |
| `C-,`         | 复制到下一行                 |                         |
| ---           | ---                          |                         |
| `M-.`         | 跳到定义                     | `xref-find-definitions` |
| `M-,`         | 返回上一个位置               | `xref-go-back`          |
| `M-?`         | 查找引用                     | `xref-find-references`  |
| ---           | ---                          |                         |
| -             | 折叠当前块                   | `hs-hide-block`         |
| -             | 展开当前块                   | `hs-show-block`         |
| -             | 当前块折叠/展开切换          | `hs-toggle-hiding`      |
| -             | 折叠所有块                   | `hs-hide-all`           |
| -             | 展开所有块                   | `hs-show-all`           |

## 其他

### 更改键位映射

解决 `windows` 下 `Ctrl+SPC` 与 `Emacs` 标记快捷键冲突

将 `Ctrl` 与 `Caps` 映射互换

安装 `AutoHotkey`  创建脚本并双击运行

``` ahk
#IfWinActive ahk_class Emacs

Capslock::Control
Control::Capslock

^Space::
    Send ^{@}
Return

#IfWinActive; 
```
