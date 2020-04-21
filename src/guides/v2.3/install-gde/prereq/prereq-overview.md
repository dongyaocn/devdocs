---
group: 安装指南
subgroup: 先决条件
title: 先决条件
menu_node: parent
menu_title: 先决条件
menu_order: 1
functional_areas:
  - Install
  - System
  - Setup
---

## 在你开始之前 {#instgde-prereq-overview}

在安装Magento之前，必须执行以下所有操作：

*  设置一个或多个满足[Magento系统要求]({{page.baseurl}}/install-gde/system-requirements.html)的主机.
*  如果要使用负载平衡设置多个web节点，请在安装Magento之前设置并测试系统的该部分。
*  确保您可以在安装过程中的不同点备份整个系统，以便在[事件](https://glossary.magento.com/event) 中回滚.

{:.bs-callout-info}
我们假设您正在**开发环境**中安装Magento 2软件，这意味着您拥有对计算机具有访问权限的[root 用户](http://www.linfo.org/root.html)  **并且**计算机不需要高度安全。如果要设置更安全的计算机，强烈建议您咨询网络管理员以获得其他帮助。

强烈建议您更新和升级操作系统软件。这些升级可以提供安全性和软件修复，防止将来出现问题。不知道这是什么意思？查看我们的[安装概述页]({{page.baseurl}}/install-gde/bk-install-guide.html).

以具有`root`权限的用户身份输入以下命令：

*  Ubuntu

```bash
apt-get update
```

```bash
apt-get upgrade
```

*  CentOS

```bash
yum -y update
```

```bash
yum -y upgrade
```

## 先决条件检查 {#instgde-prereq-check}

要检查系统的先决条件，请输入以下命令：

### Apache

CentOS: `httpd -v`

Ubuntu: `apache2 -v`

Magento支持Apache2.4版本，结果如下：

```terminal
Server version: Apache/2.4.0 (Unix)
Server built:   Jul 23 2017 14:17:29
```

要安装或升级Apache，请参阅[Apache]({{page.baseurl}}/install-gde/prereq/apache.html).

### PHP

{:.bs-callout-info}
Magento 2.3.3支持PHP7.2。
所有第三方库现在都支持PHP7.2。
如果您有兴趣参与马金托社区项目，我们欢迎您的帮助！请参阅我们的[ZenHub board](https://app.zenhub.com/workspace/o/magento-engcom/php-7.2-support/boards?repos=116423356,116426364,115111902) 以获取未解决问题的完整列表。

```bash
php -v
```

{% include install/php-versions-template.md %}

必须运行[PHP]（https://glossary.magento.com/PHP）7.2或7.3版：

```terminal
PHP 7.2.0 (cli) (built: Jan  9 2018 09:23:16) ( NTS )
Copyright (c) 1997-2017 The PHP Group
Zend Engine v3.1.0, Copyright (c) 1998-2018 Zend Technologies with Zend OPcache v7.1.6, Copyright (c) 1999-2018, by Zend Technologies
```

有关PHP需求的信息，请参见[PHP](/guides/v2.3/install-gde/prereq/php-settings.html) 。

### MySQL

```bash
mysql -u <database root user or database owner name> -p
```

For example:

```bash
mysql -u magento -p
```

请参阅[PHP]您必须运行MySQL 5.6版或更高版本，因为以下结果表明：有关PHP需求的信息。

```terminal
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 871
Server version: 5.6.21 MySQL Community Server (GPL)

Copyright (c) 2000, 2014, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.
```

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

Enter `exit` at the `mysql>` prompt to exit.

要安装或升级MySQL，请参见[MySQL]({{page.baseurl}}/install-gde/prereq/mysql.html).

{:.ref-header}
下一步

[选择如何安装Magento软件]({{page.baseurl}}/install-gde/bk-install-guide.html)

{:.ref-header}
相关主题

*  [MySQL]({{page.baseurl}}/install-gde/prereq/mysql.html)
*  [Apache]({{page.baseurl}}/install-gde/prereq/apache.html)
*  [PHP]({{page.baseurl}}/install-gde/prereq/php-settings.html)
*  [安装可选软件]({{page.baseurl}}/install-gde/prereq/optional.html)
*  [如何获得Magento软件]({{ page.baseurl }}/install-gde/bk-install-guide.html)
