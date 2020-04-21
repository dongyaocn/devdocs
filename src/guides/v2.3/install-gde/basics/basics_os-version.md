---
group: installation-guide
title: 我的服务器运行什么操作系统?
functional_areas:
  - Install
  - System
  - Setup
---

如何判断Magento服务器运行的操作系统和版本?

**先决条件**:您必须使用命令提示符(一个允许您直接输入命令的应用程序)访问服务器。

如果您可以直接登录到计算机，应用程序通常称为终端。

如果不能直接登录,可以 [远程登录]({{ page.baseurl }}/install-gde/basics/basics_login.html).

## 准确的命令 或者 使用排除法获取命令?

如果你已经知道你在运行Ubuntu或者CentOS，但是你不知道它的版本，请看下面的章节。如果您不知道那么多，只需使用排除法—运行两个命令，直到您找到一个工作环境。

### CentOS

要找到CentOS版本，请在终端中输入以下命令:

```bash
cat /etc/*release*
```

下面的示例输出显示您正在运行CentOS 6.5(您可以忽略大部分输出):

```terminal
CentOS release 6.5 (Final)
LSB_VERSION=base-4.0-amd64:base-4.0-noarch:core-4.0-amd64:core-4.0-noarch:graphics-4.0-amd64:graphics-4.0-noarch:printing-4.0-amd64:printing-4.0-noarch
cat: /etc/lsb-release.d: Is a directory
CentOS release 6.5 (Final)
CentOS release 6.5 (Final)
```

### Ubuntu

要找到Ubuntu版本，在终端输入以下命令:

```bash
lsb_release -a
```

下面的示例输出显示您正在运行Ubuntu 14:

```terminal
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 14.04.1 LTS
Release:        14.04
Codename:       trusty
```
