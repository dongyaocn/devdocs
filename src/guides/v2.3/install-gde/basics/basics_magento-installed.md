---
group: installation-guide
subgroup: 开始
title: Magento软件已经安装了吗?
menu_title: Magento软件已经安装了吗?
menu_node:
menu_order: 101
level3_menu_node: level3child
level3_subgroup: basics
functional_areas:
  - Install
  - System
  - Setup
---

要确定Magento软件是否已经安装，可以使用web浏览器访问[Magento Admin](https://glossary.magento.com/magento-admin)(管理控制台)或[店铺前端](https://glossary.magento.com/storefront)。

**先决条件**:您必须知道Magento服务器的主机名或IP地址，以及[URL](https://glossary.magento.com/url)才能访问Magento安装。如果您不确定，请从系统管理员或主机提供商处查找信息。

然后打开web浏览器并转到提供给您的URL。一些例子:

```http
http://www.example.com/magento2/admin
https://www.example.com/admin
http://www.example.com
```

如果显示404 (Not Found)错误，Magento可能没有安装。您应该与系统管理员或主机提供商确认这一点。

如果安装了Magento，在登录后应该会看到如下内容:

Magento Admin（管理控制台）:

![Magento Admin (管理控制台)，验证安装成功]({{ site.baseurl }}/common/images/install_success_admin.png)

Magento storefront（店铺前端）:

![Magento storefront（店铺前端）, 验证安装成功]({{ site.baseurl }}/common/images/install-success_store.png)

## 如果安装了Magento呢?

如果Magento已经安装，您希望管理或升级组件，请参阅以下指南:

*  [Component Manager Guide(组件管理器指南)]({{ page.baseurl }}/comp-mgr/bk-compman-upgrade-guide.html)

   Magento (component )*组件*是扩展、语言包或主题。组件管理器安装、卸载、更新、启用或禁用组件。

*  [Upgrade Guide(升级指南)]({{ page.baseurl }}/comp-mgr/upgrader/upgrade-start.html)

   升级Magento软件或组件。

