# Windows 相关

## 修改最大系统暂停更新时间

注册表位置 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UX\Settings`

新建/修改 `FlightSettingsMaxPauseDays` `DWORD` `3650` 约 10 年

删除该值即可恢复默认策略

使用管理员权限执行 CMD
```bash
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UX\Settings" /v FlightSettingsMaxPauseDays /t REG_DWORD /d 3650 /f

reg delete "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UX\Settings" /v FlightSettingsMaxPauseDays /f
```
需手动去设置中调整你的最大暂停更新时间
