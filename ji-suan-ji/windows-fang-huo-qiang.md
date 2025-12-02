---
description: Windows 防火墙
---

## Windows 防火墙 cmd 批处理文件

1. 批处理文件

```cmd
chcp 65001

netsh advfirewall firewall add rule name="DxO PureRAW 5" dir=in program="C:\Program Files\DxO\DxO PureRAW 5\PureRawv5.exe" action=block
netsh advfirewall firewall add rule name="DxO PureRAW 5" dir=out program="C:\Program Files\DxO\DxO PureRAW 5\PureRawv5.exe" action=block

netsh advfirewall firewall add rule name="Luminar Neo" dir=in program="C:\Program Files\Skylum\Luminar Neo\Luminar Neo.exe" action=block
netsh advfirewall firewall add rule name="Luminar Neo" dir=out program="C:\Program Files\Skylum\Luminar Neo\Luminar Neo.exe" action=block

netsh advfirewall firewall add rule name="OpenJDK Platform binary" dir=in program="C:\program files (x86)\yozosoft\yozo_office\jre\bin\java.exe" action=block
netsh advfirewall firewall add rule name="OpenJDK Platform binary" dir=out program="C:\program files (x86)\yozosoft\yozo_office\jre\bin\java.exe" action=block

netsh advfirewall firewall add rule name="photoshop" dir=in program="C:\Program Files\Adobe\Adobe Photoshop 2026\Photoshop.exe" action=block
netsh advfirewall firewall add rule name="photoshop" dir=out program="C:\Program Files\Adobe\Adobe Photoshop 2026\Photoshop.exe" action=block

netsh advfirewall firewall add rule name="ucloudservice" dir=in program="C:\program files (x86)\yozosoft\yozo_office\third\ucloudservice-full\ucloudservice.exe" action=block
netsh advfirewall firewall add rule name="ucloudservice" dir=out program="C:\program files (x86)\yozosoft\yozo_office\third\ucloudservice-full\ucloudservice.exe" action=block

netsh advfirewall firewall add rule name="Yozo Engine" dir=in program="C:\program files (x86)\yozosoft\yozo_office\yozo_engine.exe" action=block
netsh advfirewall firewall add rule name="Yozo Engine" dir=out program="C:\program files (x86)\yozosoft\yozo_office\yozo_engine.exe" action=block

netsh advfirewall firewall add rule name="会声会影" dir=in program="C:\Program Files\Corel\Corel VideoStudio 2023\vstudio.exe" action=block
netsh advfirewall firewall add rule name="会声会影" dir=out program="C:\Program Files\Corel\Corel VideoStudio 2023\vstudio.exe" action=block

netsh advfirewall firewall add rule name="永中表格" dir=in program="C:\program files (x86)\yozosoft\yozo_office\yozo_calc.exe" action=block
netsh advfirewall firewall add rule name="永中表格" dir=out program="C:\program files (x86)\yozosoft\yozo_office\yozo_calc.exe" action=block

netsh advfirewall firewall add rule name="永中简报" dir=in program="C:\program files (x86)\yozosoft\yozo_office\yozo_impress.exe" action=block
netsh advfirewall firewall add rule name="永中简报" dir=out program="C:\program files (x86)\yozosoft\yozo_office\yozo_impress.exe" action=block

netsh advfirewall firewall add rule name="永中文字" dir=in program="C:\program files (x86)\yozosoft\yozo_office\yozo_writer.exe" action=block
netsh advfirewall firewall add rule name="永中文字" dir=out program="C:\program files (x86)\yozosoft\yozo_office\yozo_writer.exe" action=block

REM netsh advfirewall firewall add rule name="禁止QQ联网" dir=in program="C:\Program Files (x86)\Tencent\QQ\Bin\QQ.exe" action=block
REM netsh advfirewall firewall add rule name="禁止QQ联网" dir=out program="C:\Program Files (x86)\Tencent\QQ\Bin\QQ.exe" action=block
```

