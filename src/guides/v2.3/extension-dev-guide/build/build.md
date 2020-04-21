---
group: php-developer-guide
subgroup: 03_Build
title: 构建
menu_title: 构建
menu_order: 1
menu_node: parent
---

构建组件包含布局文件结构，创建必要的配置文件，构建接口和服务所属的任何 [API](https://glossary.magento.com/api)，以及添加组件所需的[店面](https://glossary.magento.com/frontend) 任何部分。

## 先决条件 {#create-component-basics}

在开始构建新组件之前，请确保 Magento 2,和Magento [系统要求]({{ page.baseurl }}/install-gde/system-requirements.html)安装正常.

此外，Magento建议在设置组件文件结构和添加配置文件时禁用缓存。

以下详细说明了组件构建过程：

*  [创建 composer.json]({{ page.baseurl }}/extension-dev-guide/build/composer-integration.html)
*  [定义配置文件]({{ page.baseurl }}/extension-dev-guide/build/required-configuration-files.html)
*  [创建组件文件结构]({{ page.baseurl }}/extension-dev-guide/build/module-file-structure.html)
*  [注册组件]({{ page.baseurl }}/extension-dev-guide/build/component-registration.html)
*  [URN schema 验证]({{ page.baseurl }}/extension-dev-guide/build/XSD-XML-validation.html)
*  [命名组件]({{ page.baseurl }}/extension-dev-guide/build/create_component.html)
*  [组件加载顺序]({{ page.baseurl }}/extension-dev-guide/build/module-load-order.html)
*  [启用组件]({{ page.baseurl }}/extension-dev-guide/build/enable-module.html)
