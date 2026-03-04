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


```
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


## Emacs 常用键位操作

Emacs 键位表示 `C Ctrl` `M Alt` `S shift`

`C-g` 表示同时按下 `Ctrl` 和 `g`

`C-x C-s` 表示先同时按下 `Ctrl` 和 `x` 再同时按下 `Ctrl` 和 `s`

| 快捷键    | 操作           | fun |
| --------- | -------------- | --- |
| `C-g`     | 取消操作       |     |
| ---       | ---            |     |
| `C-x C-f` | 打开/创建文件  |     |
| `C-x C-s` | 保存文件       |     |
| ---       | ---            |     |
| `M-w`     | 剪切           |     |
| `C-w`     | 复制           |     |
| `C-y`     | 粘贴           |     |
| `C-/`     | undo           |     |
| -----     | --------       |     |
| `C-x o`   | 切换窗口       |     |
| `C-x 0`   | 关闭当前窗口   |     |
| `C-x 1`   | 只保留当前窗口 |     |
| `C-x 2`   | 横向分屏       |     |
| `C-x 3`   | 纵向分屏       |     |
| `C-x k`   | kill buffer    |     |
| -----     | --------       |     |
| `C-f`     | 前进           |     |
| `C-b`     | 后退           |     |
| `C-n`     | 下一行         |     |
| `C-p`     | 上一行         |     |
| `M-f`     | 前进一个词     |     |
| `M-b`     | 后退一个词     |     |
| `C-a`     | 行首           |     |
| `C-e`     | 行尾           |     |
| `M-a`     | 句首           |     |
| `M-e`     | 句尾           |     |
| `M-<`     | 页头           |     |
| `M->`     | 页尾           |     |

## 光标移动


C-v 向上翻页  M-v 向下翻页

C-s 正向搜索  M-s 逆向搜素

## Emacs-shell

M-p 上一条历史命令
M-n 下一条历史命令


## Emacs 扩展...

1. 自动格式化
2. vterm
3. 标签页
4. 变量重构



## Emacs 功能操作

### 操作宏录制

`C-x (` 开始录制宏， `C-x )` 结束录制宏

`C-x e` 执行一次刚才录制的宏，连续按 e 会重复执行上次宏操作

### 搜索

C-s 正向增量搜素，重复使用 C-s 跳转到下一个匹配项
C-y 反向增量搜素，重复使用 C-y 跳转到下一个匹配项

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

M-x compile 输入编译命令进行编译，在报错/警告位置按回车可跳转到源文件位置

M-x dired 浏览和管理当前目录

M-x grep | rgrep 搜索

## 自定义配置

| 全局快捷键    | 功能                            | fun                     |
| ------------- | ------------------------------- | ----------------------- |
| `C-x C-g`     | 打开光标处的文件路径            |                         |
| `C-c i m`     | 打开当前文件的函数/符号索引菜单 |                         |
| ---           | ---                             |                         |
| `C-x p s`     | 对选中内容执行 rgrep            |                         |
| ---           | ---                             |                         |
| `C-S-c C-S-c` | 对选中的每行添加光标            |                         |
| `C->`         | 向下寻找并标记匹配项            |                         |
| `C-<`         | 向上寻找并标记匹配项            |                         |
| `C-c C-<`     | 选中当前 Buffer 中所有匹配项    |                         |
| `C-"`         | 跳过下一个匹配项                |                         |
| `C-:`         | 跳过上一个匹配项                |                         |
| ---           | ---                             |                         |
| `M-p`         | 移动到上一行                    |                         |
| `M-n`         | 移动到下一行                    |                         |
| `C-,`         | 复制到下一行                    |                         |
| ---           | ---                             |                         |
| `M-.`         | 跳到定义                        | `xref-find-definitions` |
| `M-,`         | 返回上一个位置                  | `xref-go-back`          |
| `M-?`         | 查找引用                        | `xref-find-references`  |
| ---           | ---                             |                         |
| -             | 折叠当前块                      | `hs-hide-block`         |
| -             | 展开当前块                      | `hs-show-block`         |
| -             | 当前块折叠/展开切换             | `hs-toggle-hiding`      |
| -             | 折叠所有块                      | `hs-hide-all`           |
| -             | 展开所有块                      | `hs-show-all`           |


## 其他

### windows 下 Ctrl+SPC 与 Emacs 标记快捷键冲突

安装 AutoHotkey  
创建脚本更改映射为 Ctrl+@  
``` ahk
^Space::
        if WinActive("ahk_class Emacs")
	   Send ^{@}
Return
```
双击运行
