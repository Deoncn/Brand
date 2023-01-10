# IEKv2 配置和使用指南

* [导言](#导言)
* [配置-ikev2-vpn-客户端](#配置-ikev2-vpn-客户端)
* [ikev2-故障排除](#ikev2-故障排除)

## 导言

现代操作系统支持 IKEv2 协议标准。因特网密钥交换（英语：Internet Key Exchange，简称 IKE 或 IKEv2）是一种网络协议，归属于 IPsec 协议族之下，用以创建安全关联 (Security Association, SA)。与 IKE 版本 1 相比较，IKEv2 的 [功能改进](https://en.wikipedia.org/wiki/Internet_Key_Exchange#Improvements_with_IKEv2) 包括比如通过 MOBIKE 实现 Standard Mobility 支持，以及更高的可靠性。

Libreswan 支持通过使用 RSA 签名算法的 X.509 Machine Certificates 来对 IKEv2 客户端进行身份验证。该方法无需 IPsec PSK, 用户名或密码。它可以用于 Windows, macOS, iOS, Android, Chrome OS, Linux 和 RouterOS。


## 配置-ikev2-vpn-客户端

* [Windows 7, 8, 10 和 11](#windows-7-8-10-和-11)
* [OS X (macOS)](#os-x-macos)
* [iOS (iPhone/iPad)](#ios)
* [Android](#android)
* [Chrome OS (Chromebook)](#chrome-os)
* [Linux](#linux)
* [Mikrotik RouterOS](#routeros)


### Windows 7, 8, 10 和 11

#### 自动导入配置

[**屏幕录影：** 在 Windows 上自动导入 IKEv2 配置](https://ko-fi.com/post/IKEv2-Auto-Import-Configuration-on-Windows-8-10-a-K3K1DQCHW)

**Windows 8, 10 和 11** 用户可以自动导入 IKEv2 配置：

1. 将生成的 `.p12` 文件安全地传送到你的计算机。
1. 右键单击 [ikev2_config_import.cmd](https://github.com/hwdsl2/vpn-extras/releases/latest/download/ikev2_config_import.cmd) 并保存这个辅助脚本到与 `.p12` 文件 **相同的文件夹**。
1. 右键单击保存的脚本，选择 **属性**。单击对话框下方的 **解除锁定**，然后单击 **确定**。
1. 右键单击保存的脚本，选择 **以管理员身份运行** 并按提示操作。

要连接到 VPN：单击系统托盘中的无线/网络图标，选择新的 VPN 连接，然后单击 **连接**。连接成功后，你可以到 [这里](https://www.ipchicken.com) 检测你的 IP 地址，应该显示为`你的 VPN 服务器 IP`。

如果在连接过程中遇到错误，请参见 [故障排除](#ikev2-故障排除)。







### OS X (macOS)

[[支持者] **屏幕录影：** 在 macOS 上导入 IKEv2 配置并连接](https://ko-fi.com/post/Support-this-project-and-get-access-to-supporter-o-X8X5FVFZC)

首先，将生成的 `.mobileconfig` 文件安全地传送到你的 Mac，然后双击并按提示操作，以导入为 macOS 配置描述文件。如果你的 Mac 运行 macOS Big Sur 或更新版本，打开系统偏好设置并转到描述文件部分以完成导入。在完成之后，检查并确保 "IKEv2 VPN" 显示在系统偏好设置 -> 描述文件中。

要连接到 VPN：

1. 打开系统偏好设置并转到网络部分。
1. 选择与 `你的 VPN 服务器 IP`（或者域名）对应的 VPN 连接。
1. 选中 **在菜单栏中显示 VPN 状态** 复选框。
1. 单击 **连接**。

（可选功能）启用 **VPN On Demand（按需连接）** 以在你的 Mac 连接到 Wi-Fi 时自动启动 VPN 连接。要启用它，选中 VPN 连接的 **按需连接** 复选框，然后单击 **应用**。你可以自定义按需连接规则，以排除某些 Wi-Fi 网络（例如你的家庭网络）。参见 [:book: 电子书：搭建自己的 IPsec VPN, OpenVPN 和 WireGuard 服务器](https://mybook.to/vpnzhs) 中的 "指南：为 macOS 和 iOS 自定义 IKEv2 VPN On Demand 规则"。

<details>
<summary>
如果你手动配置 IKEv2 而不是使用辅助脚本，点这里查看步骤。
</summary>

首先，将生成的 `.p12` 文件安全地传送到你的 Mac，然后双击以导入到 **钥匙串访问** 中的 **登录** 钥匙串。下一步，双击导入的 `IKEv2 VPN CA` 证书，展开 **信任** 并从 **IP 安全 (IPsec)** 下拉菜单中选择 **始终信任**。单击左上角的红色 "X" 关闭窗口。根据提示使用触控 ID，或者输入密码并单击 "更新设置"。

在完成之后，检查并确保新的客户端证书和 `IKEv2 VPN CA` 都显示在 **登录** 钥匙串 的 **证书** 类别中。

1. 打开系统偏好设置并转到网络部分。
1. 在窗口左下角单击 **+** 按钮。
1. 从 **接口** 下拉菜单选择 **VPN**。
1. 从 **VPN 类型** 下拉菜单选择 **IKEv2**。
1. 在 **服务名称** 字段中输入任意内容。
1. 单击 **创建**。
1. 在 **服务器地址** 字段中输入 `你的 VPN 服务器 IP` （或者域名）。   
   **注：** 如果你在配置 IKEv2 时指定了服务器的域名（而不是 IP 地址），则必须在 **服务器地址** 和 **远程 ID** 字段中输入该域名。
1. 在 **远程 ID** 字段中输入 `你的 VPN 服务器 IP` （或者域名）。
1. 在 **本地 ID** 字段中输入 `你的 VPN 客户端名称`。   
   **注：** 该名称必须和你在 IKEv2 配置过程中指定的客户端名称一致。它与你的 `.p12` 文件名的第一部分相同。
1. 单击 **认证设置** 按钮。
1. 从 **认证设置** 下拉菜单中选择 **无**。
1. 选择 **证书** 单选按钮，然后选择新的客户端证书。
1. 单击 **好**。
1. 选中 **在菜单栏中显示 VPN 状态** 复选框。
1. 单击 **应用** 保存VPN连接信息。
1. 单击 **连接**。
</details>

连接成功后，你可以到 [这里](https://www.ipchicken.com) 检测你的 IP 地址，应该显示为`你的 VPN 服务器 IP`。

如果在连接过程中遇到错误，请参见 [故障排除](#ikev2-故障排除)。

<details>
<summary>
删除 IKEv2 VPN 连接。
</summary>

要删除 IKEv2 VPN 连接，打开系统偏好设置 -> 描述文件并移除你添加的 IKEv2 VPN 描述文件。
</details>

### iOS

[[支持者] **屏幕录影：** 在 iOS (iPhone & iPad) 上导入 IKEv2 配置并连接](https://ko-fi.com/post/Support-this-project-and-get-access-to-supporter-o-X8X5FVFZC)

首先，将生成的 `.mobileconfig` 文件安全地传送到你的 iOS 设备，并且导入为 iOS 配置描述文件。要传送文件，你可以使用：

1. AirDrop（隔空投送），或者
1. 使用 [文件共享](https://support.apple.com/zh-cn/HT210598) 功能上传到设备（任何 App 目录），然后打开 iOS 设备上的 "文件" App，将上传的文件移动到 "On My iPhone" 目录下。然后单击它并到 "设置" App 中导入，或者
1. 将文件放在一个你的安全的托管网站上，然后在 Mobile Safari 中下载并导入它们。

在完成之后，检查并确保 "IKEv2 VPN" 显示在设置 -> 通用 -> VPN 与设备管理（或者描述文件）中。

要连接到 VPN：

1. 进入设置 -> VPN。选择与 `你的 VPN 服务器 IP`（或者域名）对应的 VPN 连接。
1. 启用 **VPN** 连接。

（可选功能）启用 **VPN On Demand（按需连接）** 以在你的 iOS 设备连接到 Wi-Fi 时自动启动 VPN 连接。要启用它，单击 VPN 连接右边的 "i" 图标，然后启用 **按需连接**。你可以自定义按需连接规则，以排除某些 Wi-Fi 网络（例如你的家庭网络），或者在 Wi-Fi 和蜂窝网络上都启动 VPN 连接。参见 [:book: 电子书：搭建自己的 IPsec VPN, OpenVPN 和 WireGuard 服务器](https://mybook.to/vpnzhs) 中的 "指南：为 macOS 和 iOS 自定义 IKEv2 VPN On Demand 规则"。

<details>
<summary>
如果你手动配置 IKEv2 而不是使用辅助脚本，点这里查看步骤。
</summary>

首先，将生成的 `ca.cer` 和 `.p12` 文件安全地传送到你的 iOS 设备，并且逐个导入为 iOS 配置描述文件。要传送文件，你可以使用：

1. AirDrop（隔空投送），或者
1. 使用 [文件共享](https://support.apple.com/zh-cn/HT210598) 功能上传到设备（任何 App 目录），然后打开 iOS 设备上的 "文件" App，将上传的文件移动到 "On My iPhone" 目录下。然后逐个单击它们并到 "设置" App 中导入，或者
1. 将文件放在一个你的安全的托管网站上，然后在 Mobile Safari 中下载并导入它们。

在完成之后，检查并确保新的客户端证书和 `IKEv2 VPN CA` 都显示在设置 -> 通用 -> VPN 与设备管理（或者描述文件）中。

1. 进入设置 -> 通用 -> VPN 与设备管理 -> VPN。
1. 单击 **添加VPN配置...**。
1. 单击 **类型** 。选择 **IKEv2** 并返回。
1. 在 **描述** 字段中输入任意内容。
1. 在 **服务器** 字段中输入 `你的 VPN 服务器 IP` （或者域名）。   
   **注：** 如果你在配置 IKEv2 时指定了服务器的域名（而不是 IP 地址），则必须在 **服务器** 和 **远程 ID** 字段中输入该域名。
1. 在 **远程 ID** 字段中输入 `你的 VPN 服务器 IP` （或者域名）。
1. 在 **本地 ID** 字段中输入 `你的 VPN 客户端名称`。   
   **注：** 该名称必须和你在 IKEv2 配置过程中指定的客户端名称一致。它与你的 `.p12` 文件名的第一部分相同。
1. 单击 **用户鉴定** 。选择 **无** 并返回。
1. 启用 **使用证书** 选项。
1. 单击 **证书** 。选择新的客户端证书并返回。
1. 单击右上角的 **完成**。
1. 启用 **VPN** 连接。
</details>

连接成功后，你可以到 [这里](https://www.ipchicken.com) 检测你的 IP 地址，应该显示为`你的 VPN 服务器 IP`。

如果在连接过程中遇到错误，请参见 [故障排除](#ikev2-故障排除)。

<details>
<summary>
删除 IKEv2 VPN 连接。
</summary>

要删除 IKEv2 VPN 连接，打开设置 -> 通用 -> VPN 与设备管理（或者描述文件）并移除你添加的 IKEv2 VPN 描述文件。
</details>

### Android

[[支持者] **屏幕录影：** 使用 Android strongSwan VPN 客户端连接](https://ko-fi.com/post/Support-this-project-and-get-access-to-supporter-o-X8X5FVFZC)

1. 将生成的 `.sswan` 文件安全地传送到你的 Android 设备。
1. 从 [**Google Play**](https://play.google.com/store/apps/details?id=org.strongswan.android)，[**F-Droid**](https://f-droid.org/en/packages/org.strongswan.android/) 或 [**strongSwan 下载网站**](https://download.strongswan.org/Android/)下载并安装 strongSwan VPN 客户端。
1. 启动 strongSwan VPN 客户端。
1. 单击右上角的 "更多选项" 菜单，然后单击 **导入VPN配置**。
1. 选择你从服务器传送过来的 `.sswan` 文件。   
   **注：** 要查找 `.sswan` 文件，单击左上角的抽拉式菜单，然后浏览到你保存文件的目录。
1. 在 "导入VPN配置" 屏幕上，单击 **从VPN配置导入证书**，并按提示操作。
1. 在 "选择证书" 屏幕上，选择新的客户端证书并单击 **选择**。
1. 单击 **导入**。
1. 单击新的 VPN 配置文件以开始连接。

<details open>
<summary>
或者，Android 11+ 用户也可以使用系统自带的 IKEv2 客户端连接。
</summary>

[[支持者] **屏幕录影：** 使用 Android 11+ 系统自带的 VPN 客户端连接](https://ko-fi.com/post/Support-this-project-and-get-access-to-supporter-o-X8X5FVFZC)

1. 将生成的 `.p12` 文件安全地传送到你的 Android 设备。
1. 启动 **设置** App。
1. 进入 安全 -> 高级 -> 加密与凭据。
1. 单击 **安装证书**。
1. 单击 **VPN 和应用用户证书**。
1. 选择你从服务器传送过来的 `.p12` 文件。   
   **注：** 要查找 `.p12` 文件，单击左上角的抽拉式菜单，然后浏览到你保存文件的目录。
1. 为证书输入名称，然后单击 **确定**。
1. 进入 设置 -> 网络和互联网 -> VPN，然后单击 "+" 按钮。
1. 为 VPN 配置文件输入名称。
1. 在 **类型** 下拉菜单选择 **IKEv2/IPSec RSA**。
1. 在 **服务器地址** 字段中输入 `你的 VPN 服务器 IP` （或者域名）。   
   **注：** 它必须与 IKEv2 辅助脚本输出中的服务器地址 **完全一致**。
1. 在 **IPSec 标识符** 字段中输入任意内容（例如 `empty`）。   
   **注：** 该字段不应该为必填。它是 Android 的一个 bug。
1. 在 **IPSec 用户证书** 下拉菜单选择你导入的证书。
1. 在 **IPSec CA 证书** 下拉菜单选择你导入的证书。
1. 在 **IPSec 服务器证书** 下拉菜单选择 **(来自服务器)**。
1. 单击 **保存**。然后单击新的 VPN 连接并单击 **连接**。
</details>

<details>
<summary>
如果你的设备运行 Android 6.0 或更早版本，点这里查看额外的步骤。
</summary>

如果你的设备运行 Android 6.0 (Marshmallow) 或更早版本，要使用 strongSwan VPN 客户端连接，你必须更改 VPN 服务器上的以下设置：编辑服务器上的 `/etc/ipsec.d/ikev2.conf`。在 `conn ikev2-cp` 小节的末尾添加 `authby=rsa-sha1`，开头必须空两格。保存文件并运行 `service ipsec restart`。
</details>

（可选功能）你可以选择启用 Android 上的 "始终开启的 VPN" 功能。启动 **设置** App，进入 网络和互联网 -> 高级 -> VPN，单击 "strongSwan VPN 客户端" 右边的设置图标，然后启用 **始终开启的 VPN** 以及 **屏蔽未使用 VPN 的所有连接** 选项。

<details>
<summary>
如果你手动配置 IKEv2 而不是使用辅助脚本，点这里查看步骤。
</summary>

**Android 10 和更新版本:**

1. 将生成的 `.p12` 文件安全地传送到你的 Android 设备。
1. 从 [**Google Play**](https://play.google.com/store/apps/details?id=org.strongswan.android)，[**F-Droid**](https://f-droid.org/en/packages/org.strongswan.android/) 或 [**strongSwan 下载网站**](https://download.strongswan.org/Android/)下载并安装 strongSwan VPN 客户端。
1. 启动 **设置** App。
1. 进入 安全 -> 高级 -> 加密与凭据。
1. 单击 **安装证书**。
1. 单击 **VPN 和应用用户证书**。
1. 选择你从服务器传送过来的 `.p12` 文件，并按提示操作。   
   **注：** 要查找 `.p12` 文件，单击左上角的抽拉式菜单，然后浏览到你保存文件的目录。
1. 启动 strongSwan VPN 客户端，然后单击 **添加VPN配置**。
1. 在 **服务器地址** 字段中输入 `你的 VPN 服务器 IP` （或者域名）。   
   **注：** 如果你在配置 IKEv2 时指定了服务器的域名（而不是 IP 地址），则必须在 **服务器地址** 字段中输入该域名。
1. 在 **VPN 类型** 下拉菜单选择 **IKEv2 证书**。
1. 单击 **选择用户证书**，选择新的客户端证书并单击 **选择**。
1. **（重要）** 单击 **显示高级设置**。向下滚动，找到并启用 **Use RSA/PSS signatures** 选项。
1. 保存新的 VPN 连接，然后单击它以开始连接。

**Android 4 to 9:**

1. 将生成的 `.p12` 文件安全地传送到你的 Android 设备。
1. 从 [**Google Play**](https://play.google.com/store/apps/details?id=org.strongswan.android)，[**F-Droid**](https://f-droid.org/en/packages/org.strongswan.android/) 或 [**strongSwan 下载网站**](https://download.strongswan.org/Android/)下载并安装 strongSwan VPN 客户端。
1. 启动 strongSwan VPN 客户端，然后单击 **添加VPN配置**。
1. 在 **服务器地址** 字段中输入 `你的 VPN 服务器 IP` （或者域名）。   
   **注：** 如果你在配置 IKEv2 时指定了服务器的域名（而不是 IP 地址），则必须在 **服务器地址** 字段中输入该域名。
1. 在 **VPN 类型** 下拉菜单选择 **IKEv2 证书**。
1. 单击 **选择用户证书**，然后单击 **安装证书**。
1. 选择你从服务器传送过来的 `.p12` 文件，并按提示操作。   
   **注：** 要查找 `.p12` 文件，单击左上角的抽拉式菜单，然后浏览到你保存文件的目录。
1. **（重要）** 单击 **显示高级设置**。向下滚动，找到并启用 **Use RSA/PSS signatures** 选项。
1. 保存新的 VPN 连接，然后单击它以开始连接。
</details>

连接成功后，你可以到 [这里](https://www.ipchicken.com) 检测你的 IP 地址，应该显示为`你的 VPN 服务器 IP`。

如果在连接过程中遇到错误，请参见 [故障排除](#ikev2-故障排除)。

### Chrome OS

首先，在 VPN 服务器上导出 CA 证书到 `ca.cer`：

```bash
sudo certutil -L -d sql:/etc/ipsec.d -n "IKEv2 VPN CA" -a -o ca.cer
```

将生成的 `.p12` 文件和 `ca.cer` 文件安全地传送到你的 Chrome OS 设备。

安装用户证书和 CA 证书：

1. 在 Google Chrome 中打开新标签页。
1. 在地址栏中输入 **chrome://settings/certificates**
1. **（重要）** 单击 **导入并绑定** 而不是 **导入**。
1. 在对话框中选择你从服务器传送过来的 `.p12` 文件并选择 **打开**。
1. 如果证书没有密码，单击 **确定**。否则输入该证书的密码。
1. 单击上面的 **授权机构** 选项卡，然后单击 **导入**。
1. 在对话框中左下角的下拉菜单选择 **所有文件**。
1. 选择你从服务器传送过来的 `ca.cer` 文件并选择 **打开**。
1. 保持默认选项并单击 **确定**。

添加 VPN 连接：

1. 进入设置 -> 网络。
1. 单击 **添加连接**，然后单击 **添加内置 VPN**。
1. 在 **服务名称** 字段中输入任意内容。
1. 在 **提供商类型** 下拉菜单选择 **IPsec (IKEv2)**。
1. 在 **服务器主机名** 字段中输入 `你的 VPN 服务器 IP`（或者域名）。
1. 在 **身份验证类型** 下拉菜单选择 **用户证书**。
1. 在 **服务器 CA 证书** 下拉菜单选择 **IKEv2 VPN CA [IKEv2 VPN CA]**。
1. 在 **用户证书** 下拉菜单选择 **IKEv2 VPN CA [客户端名称]**。
1. 保持其他字段空白。
1. 启用 **保存身份信息和密码**。
1. 单击 **连接**。

连接成功后，网络状态图标上会出现 VPN 指示。你可以到 [这里](https://www.ipchicken.com) 检测你的 IP 地址，应该显示为`你的 VPN 服务器 IP`。

（可选功能）你可以选择启用 Chrome OS 上的 "始终开启的 VPN" 功能。要管理该设置，进入设置 -> 网络，然后单击 **VPN**。

如果在连接过程中遇到错误，请参见 [故障排除](#ikev2-故障排除)。

### Linux

在配置 Linux 客户端之前，你必须更改 VPN 服务器上的以下设置：编辑服务器上的 `/etc/ipsec.d/ikev2.conf`。在 `conn ikev2-cp` 小节的末尾添加 `authby=rsa-sha1`，开头必须空两格。保存文件并运行 `service ipsec restart`。

要配置你的 Linux 计算机以作为客户端连接到 IKEv2，首先安装 NetworkManager 的 strongSwan 插件：

```bash
# Ubuntu and Debian
sudo apt-get update
sudo apt-get install network-manager-strongswan

# Arch Linux
sudo pacman -Syu  # 升级所有软件包
sudo pacman -S networkmanager-strongswan

# Fedora
sudo yum install NetworkManager-strongswan-gnome

# CentOS
sudo yum install epel-release
sudo yum --enablerepo=epel install NetworkManager-strongswan-gnome
```

下一步，将生成的 `.p12` 文件安全地从 VPN 服务器传送到你的 Linux 计算机。然后提取 CA 证书，客户端证书和私钥。将下面示例中的 `vpnclient.p12` 换成你的 `.p12` 文件名。

```bash
# 示例：提取 CA 证书，客户端证书和私钥。在完成后可以删除 .p12 文件。
# 注：你可能需要输入 import password，它可以在 IKEv2 辅助脚本的输出中找到。
#    如果在脚本的输出中没有 import password，请按回车键继续。
# 注：如果使用 OpenSSL 3.x (运行 "openssl version" 进行检查)，
#    请将 "-legacy" 附加到下面的 3 个命令。
openssl pkcs12 -in vpnclient.p12 -cacerts -nokeys -out ca.cer
openssl pkcs12 -in vpnclient.p12 -clcerts -nokeys -out client.cer
openssl pkcs12 -in vpnclient.p12 -nocerts -nodes  -out client.key
rm vpnclient.p12

# （重要）保护证书和私钥文件
# 注：这一步是可选的，但强烈推荐。
sudo chown root.root ca.cer client.cer client.key
sudo chmod 600 ca.cer client.cer client.key
```

然后你可以创建并启用 VPN 连接：

1. 进入 Settings -> Network -> VPN。单击 **+** 按钮。
1. 选择 **IPsec/IKEv2 (strongswan)**。
1. 在 **Name** 字段中输入任意内容。
1. 在 **Gateway (Server)** 部分的 **Address** 字段中输入 `你的 VPN 服务器 IP`（或者域名）。
1. 为 **Certificate** 字段选择 `ca.cer` 文件。
1. 在 **Client** 部分的 **Authentication** 下拉菜单选择 **Certificate(/private key)**。
1. 在 **Certificate** 下拉菜单（如果存在）选择 **Certificate/private key**。
1. 为 **Certificate (file)** 字段选择 `client.cer` 文件。
1. 为 **Private key** 字段选择 `client.key` 文件。
1. 在 **Options** 部分，选中 **Request an inner IP address** 复选框。
1. 在 **Cipher proposals (Algorithms)** 部分，选中 **Enable custom proposals** 复选框。
1. 保持 **IKE** 字段空白。
1. 在 **ESP** 字段中输入 `aes128gcm16`.
1. 单击 **Add** 保存 VPN 连接信息。
1. 启用 **VPN** 连接。

连接成功后，你可以到 [这里](https://www.ipchicken.com) 检测你的 IP 地址，应该显示为`你的 VPN 服务器 IP`。

如果在连接过程中遇到错误，请参见 [故障排除](#ikev2-故障排除)。

### RouterOS

**注：** 这些步骤由 [@Unix-User](https://github.com/Unix-User) 提供。建议通过 SSH 连接运行终端命令，例如通过 Putty。

1. 将生成的 `.p12` 文件安全地传送到你的计算机。

   <details>
   <summary>
   单击查看屏幕录影。
   </summary>

   ![routeros get certificate](images/routeros-get-cert.gif)
   </details>

2. 在 WinBox 中，转到 System > certificates > import. 将 `.p12` 证书文件导入两次（是的，导入同一个文件两次）。检查你的 certificates panel。你应该看到 2 个文件，其中标注 KT 的是密钥。

   <details>
   <summary>
   单击查看屏幕录影。
   </summary>

   ![routeros import certificate](images/routeros-import-cert.gif)
   </details>

   或者，你也可以使用终端命令 (empty passphrase):

   ```bash
   [admin@MikroTik] > /certificate/import file-name=mikrotik.p12
   passphrase:

     certificates-imported: 2
     private-keys-imported: 0
            files-imported: 1
       decryption-failures: 0
     keys-with-no-certificate: 0

   [admin@MikroTik] > /certificate/import file-name=mikrotik.p12
   passphrase:

        certificates-imported: 0
        private-keys-imported: 1
               files-imported: 1
          decryption-failures: 0
     keys-with-no-certificate: 0

   ```

3. 在 terminal 中运行以下命令。将以下内容替换为你自己的值。
`YOUR_VPN_SERVER_IP_OR_DNS_NAME` 是你的 VPN 服务器 IP 或域名。
`IMPORTED_CERTIFICATE` 是上面第 2 步中的证书名称，例如 `vpnclient.p12_0`
（标记为 KT 的行 - Priv. Key Trusted - 如果未标记为 KT，请再次导入证书）。
`THESE_ADDRESSES_GO_THROUGH_VPN` 是你想要通过 VPN 浏览因特网的本地网络地址。
假设 RouterOS 后面的本地网络是 `192.168.0.0/24`，你可以使用 `192.168.0.0/24`
来指定整个网络，或者使用 `192.168.0.10` 来指定仅用于一个设备，依此类推。

   ```bash
   /ip firewall address-list add address=THESE_ADDRESSES_GO_THROUGH_VPN list=local
   /ip ipsec mode-config add name=ike2-rw responder=no src-address-list=local
   /ip ipsec policy group add name=ike2-rw
   /ip ipsec profile add name=ike2-rw
   /ip ipsec peer add address=YOUR_VPN_SERVER_IP_OR_DNS_NAME exchange-mode=ike2 \
       name=ike2-rw-client profile=ike2-rw
   /ip ipsec proposal add name=ike2-rw pfs-group=none
   /ip ipsec identity add auth-method=digital-signature certificate=IMPORTED_CERTIFICATE \
       generate-policy=port-strict mode-config=ike2-rw \
       peer=ike2-rw-client policy-template-group=ike2-rw
   /ip ipsec policy add group=ike2-rw proposal=ike2-rw template=yes
   ```
4. 更多信息请参见 [#1112](https://github.com/hwdsl2/setup-ipsec-vpn/issues/1112#issuecomment-1059628623)。

> 已在以下系统测试   
> mar/02/2022 12:52:57 by RouterOS 6.48   
> RouterBOARD 941-2nD








## ikev2-故障排除

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


