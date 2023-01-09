[English](README.md) | [中文](README-zh.md)

# Brand | 布兰德
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

# 参考资料
#### 1 VPN

[Set up Ubuntu Server 20.04 (or 18.04) as an IKEv2 VPN server](https://github.com/jawj/IKEv2-setup)

[Build your own IPsec VPN server](https://github.com/hwdsl2/setup-ipsec-vpn)

[一键搭建适用于Ubuntu/CentOS的IKEV2/L2TP的VPN](https://github.com/quericy/one-key-ikev2-vpn)

#### 2 Proxy


##### Trojan Pc
使用 Qv2ray

For Windwos - Linux - Macos

[Qv2ray](https://github.com/Qv2ray/Qv2ray) + [QPlugin-Trojan](https://github.com/Qv2ray/QvPlugin-Trojan) + [V2rayCore](https://github.com/v2ray/v2ray-core)

 Android 👉 [Igniter](https://github.com/trojan-gfw/igniter)

iPhone 👉 Shadowrocket


















