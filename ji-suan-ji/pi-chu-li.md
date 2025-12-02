---
description: 批处理编辑知识
---

##  批处理编辑知识

### 1.  cmd

```cmd
chcp 65001

rd /s /q "C:\Program Files (x86)\Kingsoft\office6"
REM 删除指定文件夹

xcopy 模板.xls 1月\朱凯.xls*
xcopy 模板.xls 1月\刘涛.xls*



xcopy 1月 2月\
xcopy 1月 3月\
xcopy 1月 4月\
xcopy 1月 5月\
xcopy 1月 6月\
xcopy 1月 7月\
xcopy 1月 8月\
xcopy 1月 9月\
xcopy 1月 10月\
xcopy 1月 11月\
xcopy 1月 12月\
```

chcp 解决中文问题，windows系统编码会出现中文错误。

xcopy 文件后面`\ 和 *`用来确认文件夹和文件

### 2. 关机重启


```cmd
shutdown -p
REM 关机
```
```cmd
shutdown -r -t 0
REM 重启
```
```cmd
rundll32.exe powrprof.dll,SetSuspendState 0,1,0 
REM 睡眠
```