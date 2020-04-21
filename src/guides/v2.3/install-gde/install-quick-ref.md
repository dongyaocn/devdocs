---
group: installation-guide
subgroup: 01_resource
title: 安装快速参考(教程)
menu_title: 安装快速参考(教程)
menu_node:
menu_order: 2
functional_areas:
  - Install
  - System
  - Setup
---

我们知道安装Magento软件很有挑战性。我们想帮助你尽可能简化这个过程。

这个主题的假设:

*  您有自己的Magento服务器（您没有使用共享宿主提供程序）。
*  您正在使用`composer create project`启动安装，这使您能够获取最新的Magento软件，并在需要时向其中添加您自己的自定义设置。
*  所有内容都安装在一台主机上（数据库、web服务器等）。
*  您要安装的主机是Ubuntu或CentOS。

   （您可以使用相同的指令在其他UNIX发行版（如RedHat Enterprise Linux或Debian）上安装，但Mac或Windows不支持Magento。）

*  你主机的IP地址是 `192.0.2.5`.

  这只是一个示例IP地址，您将在本主题的详细示例中看到它。您可以用与服务器匹配的任何内部/外部IP地址替换它。

*  您正在安装到web服务器docroot下的“magento 2”子目录（完整路径为`/var/www/html/magento 2`）

   您可以选择设置静态路由或虚拟主机以安装到主机名而不是IP，但这超出了本主题的范围。

我们将安装过程分为三个主要部分：开始、安装和安装后。我们希望下面的内容对您有所帮助；如果您希望提出改进建议，请单击此页顶部的**在GitHub上编辑此页**，然后通知我们。

## 先决条件：你有多牛逼？

你知道什么是`终端`应用程序吗？你知道你的服务器运行什么操作系统吗？你知道Apache 是什么吗？

如果没有，请参阅 (安装概述)[]。

## 安装第1部分：入门

1. 参见[系统要求][]。
1. 如果您的系统缺少任何要求，请参阅必备文档：

   *  [Apache][]
   *  [PHP][]
   *  [MySQL][]

1. 同样重要的是，在服务器上设置[Magento文件系统所有者][]。
1. 切换到[Magento文件系统所有者][]。

### 获取Magento软件

满足所有先决条件后，使用[Composer][]获取Magento软件，如下所示：

```bash
cd <web server docroot directory>
```

```bash
composer create-project --repository=https://repo.magento.com/ magento/project-community-edition magento2
```

您需要进行身份验证；有关详细信息，请参见[获取身份验证密钥][]。这只下载Magento代码；它不为您安装软件。

{:.bs-callout-tip}
或者，您也可以下载[Magento软件存档][]。

{% include install/file-system-perms-before_22.md %}

## 安装第2部分：安装Magento软件

您可以选择使用[基于web的安装向导][]或使用[命令行][]安装Magento软件。

### 命令行安装

{% collapsible Click to view the command-line installation %}

下面的示例演示如何使用带有以下选项的命令行进行安装：

* Magento软件安装在`/var/www/html/Magento 2`目录中，这意味着您的店面URL是`http://192.0.2.5/magento2/`

*  数据库服务器与web服务器位于同一主机上。
数据库名是'magento'，用户名和密码都是'magento'`
  
* 使用服务器重写

*  Magento管理员具有以下属性：

   *  第一个和最后的名称是`Magento User`
   *  用户名  `admin` 和 密码 `admin123`
   *  E-mail 地址是 `user@example.com`

* 默认语言是 `en_US` (美国英语)

* 默认货币为美元

*  默认时区为美国中部（美洲/芝加哥）Central (America/Chicago)

    ```bash
    bin/magento setup:install --base-url=http://192.0.2.5/magento2/ \
    --db-host=localhost --db-name=magento --db-user=magento --db-password=magento \
    --admin-firstname=Magento --admin-lastname=User --admin-email=user@example.com \
    --admin-user=admin --admin-password=admin123 --language=en_US \
    --currency=USD --timezone=America/Chicago --use-rewrites=1
   ```

（可选）切换到[开发人员模式]({{page.baseurl}}/config-guide/cli/config-cli-subcommands-mode.html)。

```bash
cd <magento_root>/bin
```

```bash
php magento deploy:mode:set developer
```

{% endcollapsible %}

### Web安装向导

{% collapsible Click to view the Web Setup Wizard installation %}

下面的示例演示如何使用具有以下选项的Web安装向导进行安装：

*  Magento软件安装在相对于web服务器docroot的`magento2`目录中，这意味着您的店面URL是`http://192.0.2.5/magento2
*  数据库服务器与web服务器位于同一主机上。
数据库名是`magento`，用户名和密码都是`magento`
*  Magento管理员具有以下属性:

   *  用户名是 `admin` 并且密码是 `admin123`
   *  E-mail 地址是 `user@example.com`
*  默认语言为`en_US`（美国英语）
*  默认货币为美元
*  默认时区为美国中部（美洲/芝加哥）Central (America/Chicago)

要运行Web安装向导，请执行以下操作：

1. 在浏览器的地址或位置字段中输入以下URL：

    http://192.0.2.5/magento2/setup

1. 在欢迎页面上，单击**同意并设置Magento**。

   [您必须接受许可协议才能安装Magento软件]({{ site.baseurl }}/common/images/install_qr_wizard-welcome.png){:width="200px"}

1. 准备就绪检查确认系统已准备好安装Magento软件。

   单击**开始就绪检查**

   ![准备就绪检查确保您的系统已准备好使用Magento软件]({{ site.baseurl }}/common/images/install_qr_readiness.png){:width="400px"}

   *  如果就绪检查通过，请单击**下一步**，然后继续下一步。
   *  如果就绪检查失败，请参阅[就绪检查问题][]
   *  如果就绪检查通过，请单击**下一步**，然后继续下一步。
   *  如果就绪检查失败，请参阅 [准备检查问题]({{ page.baseurl }}/install-gde/trouble/readiness/tshoot_rc_main.html)

1. 第2步：添加数据库使您能够设置Magento数据库。

   ![设置Magento数据库]({{ site.baseurl }}/common/images/install_qr_database.png){:width="400px"}

1. Web配置使您能够输入店面和Magento Admin url。

   ![输入店面和Magento管理url]({{ site.baseurl }}/common/images/install_qr_web.png){:width="400px"}

1. 自定义存储使您能够输入默认存储货币、时区和语言。

   ![自定义存储使您能够输入默认存储货币、时区和语言。]({{ site.baseurl }}/common/images/install_qr_store.png){:width="400px"}

1. 创建管理帐户允许您设置Magento管理员。此用户可以在Magento管理中执行所有操作。

   ![创建Magento管理员帐户]({{ site.baseurl }}/common/images/install_qr_admin.png){:width="400px"}

1. 当您单击**立即安装**时，安装将开始安装。

   您可以选择展开**控制台日志**，在安装过程中查看安装消息。

{% endcollapsible %}

## 安装第3部分：安装后

*  [验证安装][]成功。
*  了解[组件管理器和系统升级][]以备将来更新。

<!-- Link Definitions -->
[安装概述]:{{page.baseurl }}/install-gde/bk-install-guide.html
[系统要求]:{{page.baseurl }}/install-gde/system-requirements.html
[Apache]:{{page.baseurl }}/install-gde/prereq/Apache.html
[PHP]:{{page.baseurl }}/install-gde/prereq/PHP-settings.html
[MySQL]:{{page.baseurl }}/install-gde/prereq/MySQL.html
[Magento文件系统所有者]:{{page.baseurl }}/install-gde/prereq/file-sys-perms-over.html

[Composer]: https://glossary.magento.com/composer

[命令行]:{{page.baseurl }}/install-gde/install/cli/install-cli.html
[获取身份验证密钥]:{{page.baseurl }}/install-gde/prereq/connect-auth.html
[Magento软件存档]:{{page.baseurl }}/install-gde/install/get-software.html
[基于web的安装向导]:{{page.baseurl }}/install-gde/install/web/install-web.html
[就绪检查问题]:{{page.baseurl }}/install gde/trouble/Readiness/tshoot_rc_main.html
[验证安装]:{{page.baseurl }}/install-gde/install/Verify.html
[组件管理器和系统升级]:{{page.baseurl }}/comp-mgr/bk-compman-Upgrade-guide.html