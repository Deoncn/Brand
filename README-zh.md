[English](README.md) | [中文](README-zh.md)

# Brand
proxy ,vpn ,something.

萨尔瓦多 = Salvador


问题：1 Windows 10 IKEv2 拨号产生13868策略匹配错误的处理

解决方案：
```
在 HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Rasman\Parameters 
底下新增：

名称："NegotiateDH2048_AES256"
类型："REG_DWORD"
值："1"
```
保存退出即可。
标签: none
