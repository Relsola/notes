# Windows 相关

## 修改最大系统暂停更新时间

注册表位置 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UX\Settings`

新建/修改 `FlightSettingsMaxPauseDays`， 类型 `DWORD`， 值十进制 `3650`， 约 10 年

删除该值即可恢复默认策略

使用管理员权限执行 cmd 脚本快速设置
```bash
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UX\Settings" /v FlightSettingsMaxPauseDays /t REG_DWORD /d 3650 /f

reg delete "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UX\Settings" /v FlightSettingsMaxPauseDays /f
```
改完后需手动去设置中调整你的最大暂停更新时间

## 修改注册表来让文件支持右键打开方式

注册表位置

`HKEY_CLASSES_ROOT\*\shell` 在所有文件的右键菜单中显示

`HKEY_CLASSES_ROOT\Directory\shell` 在所有文件夹的右键菜单中显示

`HKEY_CLASSES_ROOT\Directory\Background\shell` 在文件夹背景的右键菜单中显示

新建值 `Icon` 图标路径

创建命令项 `command` 
- `"C:\Program Files\Typora\Typora.exe" "%1"` , `%1` 代表被右键的文件  
- `"C:\Program Files\Typora\Typora.exe" "%V"` , `%V` 代表被右键的文件夹

这里以我配置 emacs 为例

在文本中设置好以 `reg` 格式文件点击执行即可

```text
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\*\shell\Edit with Emacs]
@="Edit with Emacs"
"Icon"="D:\\app\\Emacs\\emacs-30.2\\bin\\emacs.exe"

[HKEY_CLASSES_ROOT\*\shell\Edit with Emacs\command]
@="\"D:\\app\\Emacs\\emacs-30.2\\bin\\emacsclient.exe\" -n -a \"\" \"%1\""

```
