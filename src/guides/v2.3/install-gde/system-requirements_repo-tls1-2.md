---
group: 安装指南
title: repo.magento.com对TLS的要求
functional_areas:
  - Install
  - System
  - Setup
---

{% include install/tls-repo.md %}

### 解决方案

此问题的解决方案取决于操作系统如何打包TLS。有关详细信息，请参阅以下部分之一：

*  [Ubuntu](#solution-ubuntu)
*  [CentOS](#solution-centos)
*  [Mac OS](#solution-macos)

#### Ubuntu {#solution-ubuntu}

确保您使用的是[`libcurl`](https://curl.haxx.se/libcurl/c/CURLOPT_SSLVERSION.html){:target="_blank"}。`libcurl'versions 7.34`或更高版本；这些版本默认使用TLS 1.2。
要确定`libcurl`版本，请输入以下命令：

```bash
curl --version
```

#### CentOS {#solution-centos}

问题的根源是，[`libcurl`](https://curl.haxx.se/libcurl/c/CURLOPT_SSLVERSION.html){:target="_blank"}[库]（https://glossary.magento.com/library）与CentOS 6.6及更早版本一起打包，默认使用TLS 1.1或更早版本。
要确定服务器运行的CentOS版本，请输入以下命令：

```bash
cat /etc/*release*
```

如果您已经在运行CentOS 6.8或更高版本，则无需执行任何操作。根据[CentOS 6.8 changelog](https://wiki.CentOS.org/Manuals/ReleaseNotes/CentOS6.8){:target="blank"}，现在各种应用程序都支持TLS 1.2，即OpenLDAP、yum、stunnel、vsftpd、git、postfix等。此外，TLS 1.2在默认情况下已在各种软件包中启用。
（CentOS 7有一个新版本的`libcurl`，默认为TLS 1.2。）

#### Mac OS {#solution-macos}

最近对[OS X liip包](http://php-osx.liip.ch){:target="_blank"}的更新应该可以解决这个问题。

