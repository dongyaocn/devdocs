---
group: installation-guide
subgroup: Getting Started
title: 登录到Magento服务器
functional_areas:
  - Install
  - System
  - Setup
---

<!-- This topic is referred to from Magento 2 code! Don't change the URL without informing engineering! -->
<!-- Referring file: README.md owned by core -->

要完成本指南中几乎所有的任务，您必须远程登录到Magento服务器。

**先决条件:**你必须具备:

*  一个终端应用程序

   Windows和Mac OS通常使用不同的终端应用程序。

   *  Windows: 部分列表: [putty][], [Cygwin][]
   *  Mac OS: 你可以使用内置的 [Terminal][] 程序 或者使用以下任何一种: [iTerm][], or [these][]
   *  Linux: 如果使用 [桌面环境][] 你可以使用桌面环境提供的CLI应用程序，如 [Konsole (KDE)][], [GNOME Shell][]  或 [Xfce Terminal][]。您还可以安装和使用桌面环境独立的终端应用程序，如 [Xterm][].

*  Magento服务器的用户名和密码

   在托管系统中，这可能是一个对服务器没有管理权限的用户;只要用户可以安装系统软件、停止和启动web服务器等服务，就可以。

   如果您有自己的服务器，您或您的系统管理员通常可以作为[root][]用户登录，在Linux上，该用户是对整个服务器具有完全管理权限的用户。

使用终端应用程序远程访问Magento服务器:

1. 根据提供的文档设置终端应用程序。
1. 启动终端应用程序。
1. 当提示时，输入Magento服务器的主机名或IP地址。
1. 使用提供的用户名或密码登录到服务器。

下面是您作为Windows上Cygwin的`root`用户登录到服务器时的情况。

![Logging in with Cygwin on Windows]({{ site.baseurl }}/common/images/install_cygwin.png)

 {:.bs-callout-info}
[Secure Shell (ssh)][] 是一种协议，您可以使用它安全地连接到远程服务器，而无需通过网络发送用户名或密码。

<!-- Link definitions -->
[putty]: http://www.putty.org/
[Cygwin]: https://www.cygwin.com/
[Terminal]: http://en.wikipedia.org/wiki/Terminal_(OS_X)
[iTerm]: http://iterm2.com/
[these]: http://computers.tutsplus.com/tutorials/beyond-terminal-4-os-x-terminal-alternatives--mac-56217
[Desktop Environment]: https://en.wikipedia.org/wiki/Desktop_environment
[Konsole (KDE)]: https://en.wikipedia.org/wiki/Konsole
[GNOME Shell]: https://en.wikipedia.org/wiki/GNOME_Shell
[Xfce Terminal]: https://en.wikipedia.org/wiki/Xfce#Xfce_Terminal
[Xterm]: https://en.wikipedia.org/wiki/Xterm
[root]: http://www.linfo.org/root.html
[Secure Shell (ssh)]: http://en.wikipedia.org/wiki/Secure_Shell

