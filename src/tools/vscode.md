# VScode

## 快捷键操作

### 编辑与操作

`Ctrl+X` 删除整行

`Ctrl+C / Ctrl+V ` 复制/粘贴

`Shift+Alt+Up/Down` 复制到上方/下方

`Alt+Up/Down` 上移/下移

`Ctrl+/` 行注释开关

`Shift+Alt+A` 块注释开关

`Ctrl+L` 选中整行

### 手动触发补全

```json
{
	// 禁用输入时自动弹出的建议列表
  "editor.quickSuggestions": false,
	// 禁用输入触发字符时自动补全
  "editor.suggestOnTriggerCharacters": false,
	// 禁用行内灰色幽灵文本补全
  "editor.inlineSuggest.enabled": false,
	// 禁用函数参数提示气泡
  "editor.parameterHints.enabled": false
}
```

`Ctrl+Space` 通用补全

`Ctrl+Shift+Space` 参数提示

### 多光标操作

`Alt+Click` 在点击位置新增一个光标

`Ctrl+Alt+Up/Down` 在上方或下方新增光标

`Ctrl+D` 选中当前词，再按一次会选中下一个相同词并新增光标

`Ctrl+K Ctrl+D` 最后一个光标移动到下一个匹配项

`Ctrl+Alt+D` 选中当前词，再按一次会选中上一个相同词并新增光标 `addSelectionToPreviousFindMatch`

`Ctrl+K Ctrl+Alt+D` 最前一个光标移动到上一个匹配项 `moveSelectionToPreviousFindMatch`

`Ctrl+U` 撤销上一次光标选择操作

`Ctrl+Shift+L` 把当前选中的文本为所有匹配项添加光标

`Ctrl+F2` 基于当前词为所有匹配项添加光标

`Alt+Shift+I` 给当前已选中的多行文本每一行末尾添加一个光标

`Shift+Alt+Drag` 框选一个矩形区域，形成一列多光标

`Esc` 退出多光标模式

### 查询和跳转

`Ctrl+F` 在当前打开文件里找文本，区分大小写、全词匹配、正则

`Ctrl+H` 当前文件查找并替换

`Ctrl+Shift+F` 工作区全局查找，支持 include/exclude 路径过滤

`Ctrl+Shift+H` 工作区全局替换

> 在查找框中 `Enter / Shift+Enter` 查找上一个/下一个

`Ctrl+P` 按文件名快速跳转打开文件

`Ctrl+Tab` 最近文件切换

`Ctrl+Shift+P` 命令面板查找命令

`Ctrl+Shift+O` 在当前文件跳到符号

`Ctrl+T` 在工作区查找符号

`F12 / Shift+F12` 跳转到定义/引用

`Ctrl+F12` 查找实现

`Ctrl+G` 跳转到行

`Alt+Left/Right` 跳转到上/下一个位置

### 窗口与面板

`` Ctrl+` `` 打开或聚焦终端

`` Ctrl+Shift+` `` 新建终端

`Ctrl+K Z` 专注模式

`Ctrl+B / Ctrl+J` 切换侧边栏 / 切换底部面板

### 调试

`F5` 启动调试

`F9` 切换断点

`F10` 单步调试

`F11` 单步进入

`Shift+F11` 单步返回

`Ctrl+F5` 重启调试
