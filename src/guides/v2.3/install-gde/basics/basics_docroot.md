---
group: installation-guide
subgroup: Getting Started
title: 什么是docroot?
menu_title: 什么是docroot?
menu_node:
menu_order: 200
level3_menu_node: level3child
level3_subgroup: basics
functional_areas:
  - Install
  - System
  - Setup
---

web服务器文档根目录(通常称为_docroot_)是放置网站运行所需的所有文件的地方。您可以使用您的web服务器的默认docroot或[修改它以增强安全性]({{ page.baseurl }}/install-gde/tutorials/change-docroot-to-pub.html)。例如，您应该在安装之后限制浏览器对特定于magento的文件的访问。

到您的web服务器的默认docroot的路径取决于以下内容:

-  操作系统
-  Web服务器软件
-  虚拟主机提供商 (如果你使用其中一个的话)

{:.bs-callout-warning}
作为Magento 2安装过程的一部分，需要在docroot下指定一个子目录(通常是` magento2 `)。特定于magento的文件安装在这个子目录中，因此知道在哪里找到默认的docroot是至关重要的。

## 联系您的主机提供商

如果您使用一个，请联系您的主机提供商来定位web服务器docroot。例如，[cPanel](http://support.hostgator.com/articles/cpanel/what-a-document-root -folder){:target="_blank"}通常使用`public_html `作为其docroot，但是您应该联系您的提供商进行确认。

## 自己去找docroot

本节假设您已经使用以下命令设置了一个简单的web服务器[Apache virtual hosts](https://httpd.apache.org/docs/2.4/vhosts/){:target="_blank"} or [nginx server blocks](https://www.nginx.com/resources/wiki/start/topics/examples/server_blocks/){:target="_blank"}.

{:.bs-callout-info}
您可以使用_virtual hosts_和_server blocks_在一台机器上运行多个网站 (e.g., `company1.example.com` and `company2.example.com`) ，或者在不更改的情况下覆盖web服务器的默认docroot。

要找到你的服务器上的docroot:

1. 在文本编辑器中打开下列文件之一:

   -  **Ubuntu**

      ```text
      /etc/apache2/sites-available/000-default.conf (Apache)
      /etc/nginx/sites-available/default (nginx)
      ```

   -  **CentOS**

      ```text
      /etc/httpd/conf/httpd.conf (Apache)
      /etc/nginx/nginx.conf (nginx)
      ```

1. 在文件中搜索 `DocumentRoot` or `root`.

   通常，Ubuntu _and_ CentOS上的默认Apache docroot是`/var/www/html` 而CentOS上的默认nginx docroot是`/usr/share/nginx/html`。例如:

   -  **Apache + Ubuntu/CentOS**

      ```conf
      DocumentRoot "/var/www/html"
      ```

   -  **nginx + CentOS**

       ```conf
       root      /usr/share/nginx/html
       ```

