---
title: Windows11安装WSL2
date: 2021/9/18
description: Windows11安装WSL2
tag: 解决方案
author: shiyd
---

## 开始准备

第一步是打开主板BIOS的虚拟化选项，如果你是这几年新买的电脑，默认这项是打开的。注意这一项每个电脑主板型号的不同，设置的方法也不同。所以最好的方法，是你根据自己主板的型号，去百度或者Google去搜索一下开启虚拟话的方法。

- Windows平台 ：Intel（VMX）Virtuallzation Technology 需要到主板中进行开启
- AMD平台：AMD-V

## 安装WSL2

- **第一步**：启动WSL。用管理员身份打开`PowerShell`.(打开方法见视频)，然后在PowerShell中，输入下面的命令。

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

- **第二步**：启动虚拟机给功能。同样在PoweShell中输入下面的命令。输入完命令后，要重启一下电脑，然后再进行第三步。

```powshell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

- **第三步**：将 WSL2 设置为默认版本。打开 PowerShell，然后在安装新的 Linux 发行版时运行以下命令，将 WSL 2 设置为默认版本，命令如下。

```powershell
wsl --set-default-version 2
```

完成上面步骤后，就可以去安装对应的 Linux 发行版了，这里我们拿Ubuntu举例。

## 安装 Ubuntu 发行版

- **第一步：**打开`Microsoft Store`，并选择你偏好的 Linux 分发版。我这里选择`Ubuntu`进行安装。下安装完成后，先不要打开
- **第二步：**下载一下 Linux 内核更新包，下载链接如下，下载完成后并安装，默认安装即可，到这里就可以使用了。

https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi

- **第三步：**如果是首次进入，需要设置用户名和密码。当进入系统后，可以使用下面的命令来查看当前Ubuntu的版本。

```bash
lsb_release -a
```

##  报错误

如果安装完成后打开 ubuntu 报错 WslRegisterDistribution failed with error: 0x8007019e 的错误，解决方法如下：

1. win+x，选择 PowerShell（管理员）
2. 输入如下命令，回车，输入Y，系统重启后打开 Ubuntu 再试试。

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

如果还是不行，可以重新安装一下 Linux 内核更新包，按照安装 Ubuntu发行版第二步。

## 参考目录

[1] : https://blog.csdn.net/weixin_46211269/article/details/115466326 (报错解决方法)

[2] : https://jspang.com/article/80 (Windows11 中安装Linux 教程 | WSL2的使用)

[3] : https://learn.microsoft.com/zh-cn/windows/wsl/install-manual (中文官网安装教程)
