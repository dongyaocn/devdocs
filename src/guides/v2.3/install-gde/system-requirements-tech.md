---
group: 安装指南
title: Magento 2.3技术堆栈要求
functional_areas:
  - Install
  - System
  - Setup
---

## 操作系统（Linux x86-64）

Linux发行版，如RedHat Enterprise Linux（RHEL）、CentOS、Ubuntu、Debian等。
Magento不支持：

*  Windows OS
*  Mac OS

## 内存要求

升级从Magento Marketplaces和其他来源获得的Magento应用程序和扩展可能需要高达2GB的RAM。如果您使用的系统的RAM小于2GB，建议您创建一个[swap file](https://support.magento.com/hc/en-us/articles/360032980432)；否则，您的升级可能会失败。

## Composer (最新稳定版本)

对于希望为Magento 2代码库或任何希望开发Magento扩展的开发人员，都需要 [Composer][]。

## Web 服务器

* [Apache 2.4][]

   此外，必须启用Apache `mod_rewrite` 和 `mod_version` 模块。[`mod_rewrite`][]模块使服务器能够执行URL重写。[`mod'version][]模块为不同的“httpd”版本提供灵活的版本检查。有关更多信息，请参阅[我们的Apache文档][]。

*  [nginx 1.x][]

## 数据库

MySQL 5.6，5.7版本

Magento还兼容MySQL NDB Cluster 7.4.*、MariaDB 10.0、10.1、10.2、Percona 5.7和其他二进制兼容的MySQL技术。

{:.bs-callout-info}
Magento只使用与MariaDB兼容的MySQL特性。然而，MariaDB可能不兼容所有MySQL特性，因此在使用Magento模块中的特性之前，请务必研究兼容性问题。

## PHP

{:.bs-callout-warning}
PHP7.1已经提达到了它的[尽头](https://www.php.net/supported-versions.php)。为了保持PCI兼容性，不应在不受支持的软件上运行Magento。
从GitHub安装将不再适用于Magento 2.3.4/PHP 7.1。
使用PHP 7.1.x安装2.3.4的唯一方法是使用Composer。
Magento建议使用PHP7.3

<!--{% assign supported_php_versions = site.data.codebase.v2_3.open-source.composer_lock.platform.php | split: "||" %}-->
{% include install/php-versions-template.md %}

### 所需的PHP扩展

{:.bs-callout-info}
[PHP安装说明][]包含安装这些扩展的步骤。

{:.bs-callout-warning}
如果您通过从[github](https://github.com/magento/magento2)存储库克隆安装Magento，那么请确保您的实例上安装了[ext sockets](https://github.com/php-amqplib/php-amqplib/blob/master/CHANGELOG.md#281---2018-11-13)。

<!--{% assign platform-req = site.data.codebase.v2_3.open-source.composer_lock.platform %}-->
{% include install/php-extensions-template.md %}

有关安装的详细信息，请参阅[官方PHP文档][]。

### PHP OPcache

我们强烈建议您验证[PHP OPcache][]是否因性能原因而启用。OPcache在许多PHP发行版中都启用了。要验证它是否已安装，请参阅我们的[PHP文档][]。
如果必须单独安装，请参阅[PHP OPcache文档][]。

### PHP settings

我们建议使用特定的PHP配置设置，例如 `memory_limit`，这样可以避免在使用Magento时出现常见问题。
有关更多信息，请参阅[必需的PHP设置][]。

## SSL

*  HTTPS需要有效的[安全证书][]。
*  不支持自签名SSL证书。
*  传输层安全（TLS）要求 - PayPal 和 `repo.magento.com` 都要求TLS 1.2或更高版本：

   *  [关于PayPal的更多信息 ][]

### 所需的系统依赖项 {#required-system-dependencies}

Magento的某些操作需要以下系统工具:

*  [bash][]
*  [gzip][]
*  [lsof][]
*  [mysql][]
*  [mysqldump][]
*  [nice][]
*  [php][]
*  [sed][]
*  [tar][]

### 邮件服务器

邮件传输代理（MTA）或SMTP服务器

## Magento可以使用的技术 {#technologies-magento-can-use}

*  [Redis][] 用于页面缓存和会话存储的redis版本3.2、4.0、5.0（兼容2.4+）。强烈建议使用5.0版.
*  [Varnish]({{page.baseurl}}/config-guide/varnish/config-varnish.html) 版本 4.x, 5.2 或 6.2
*  [Elasticsearch]({{page.baseurl}}/config-guide/elasticsearch/es-overview.html)

   {{site.data.var.ee}} 版本2.3.x支持以下Elasticsearch版本:

   *  Elasticsearch [6.x][]{:target="_blank"}

      Magento 2.3使用[Elasticsearch PHP客户端][]{:target="_blank"} 版本 6.1.

      {:.bs-callout-warning}
      Magento仍然支持Elasticsearch，但不推荐 [2.x and 5.x][].

      如果必须使用Magento 2.3.1运行Elasticsearch 2.x或5.x，则必须更改Elasticsearch客户端版本。

      按照更改 Elasticsearch 搜索模块中的说明操作。

*  RabbitMQ 3.8.x (compatible with 2.0 and later)

   [RabbitMQ][]{:target="_blank"} 可用于将消息发布到队列并定义异步接收消息的使用者。

### 仅 {{site.data.var.ee}} 

*  三个主数据库

   这些[主数据库][]为Magento应用程序的不同功能区域（如签出、订单和所有剩余的Magento应用程序表）提供了可伸缩性优势。

### 推荐（可选）

*  [php_xdebug 2.5.x][]{:target="_blank"} 或更高版本（仅限于开发环境；可能对性能产生不利影响）

{:.bs-callout-info}
`xdebug`存在一个已知问题，可能会影响Magento安装，或在安装后访问店面或Magento管理员。有关详细信息，请参阅[xdebug的已知问题][]。

*  [`mcrypt`](http://php.net/manual/en/book.mcrypt.php){:target="_blank"} (for PHP < 7.2)
*  PHPUnit (作为命令行工具) 6.2.0

<!-- Link Definitions -->
[`mcrypt`]: http://php.net/manual/en/book.mcrypt.php
[Known issue with xdebug]: https://support.magento.com/hc/en-us/articles/360034242212
[php_xdebug 2.5.x]: http://xdebug.org/download.php
[master databases]: {{page.baseurl}}/config-guide/multi-master/multi-master.html
[bash]: https://www.gnu.org/software/bash/
[gzip]: https://www.gzip.org/
[lsof]: https://linux.die.net/man/8/lsof
[mysql]: https://www.mysql.com/
[mysqldump]: https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html
[nice]: https://linux.die.net/man/1/nice
[php]: http://www.php.net/
[sed]: https://www.gnu.org/software/sed/manual/sed.html
[tar]: https://linux.die.net/man/1/tar
[Change Elasticsearch Module]: {{ page.baseurl }}/config-guide/elasticsearch/es-downgrade.html
[Composer]: https://glossary.magento.com/composer
[Apache 2.4]: http://httpd.apache.org/download.cgi
[`mod_rewrite`]: https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html
[`mod_version`]: https://httpd.apache.org/docs/2.4/mod/mod_version.html
[our Apache documentation]: {{page.baseurl}}/install-gde/prereq/apache.html
[nginx 1.x]: https://nginx.org/en/download.html
[ZenHub board]: https://app.zenhub.com/workspace/o/magento-engcom/php-7.2-support/boards?repos=116423356,116426364,115111902
[PHP installation instructions]: prereq/php-settings.html
[official PHP documentation]: http://php.net/manual/en/extensions.php
[PHP OPcache]: http://php.net/manual/en/intro.opcache.php
[PHP documentation]: prereq/php-settings.html
[PHP OPcache documentation]: http://php.net/manual/en/opcache.setup.php
[Required PHP settings]: {{ page.baseurl }}/install-gde/prereq/php-settings.html
[security certificate]: https://glossary.magento.com/security-certificate
[More information about PayPal]: {{page.baseurl}}/install-gde/system-requirements_tls1-2.html
[Redis]: {{page.baseurl}}/config-guide/redis/config-redis.html
[Varnish]: {{page.baseurl}}/config-guide/varnish/config-varnish.html
[Elasticsearch]: {{page.baseurl}}/config-guide/elasticsearch/es-overview.html
[6.x]: https://www.elastic.co/downloads/past-releases/elasticsearch-6-6-1
[Elasticsearch PHP client]: https://github.com/elastic/elasticsearch-php
[2.x and 5.x]: https://www.elastic.co/support/eol
[RabbitMQ]: {{page.baseurl}}/config-guide/mq/rabbitmq-overview.html
