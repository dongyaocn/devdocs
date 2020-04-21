---
group: php-developer-guide
subgroup: 01_Introduction
title: 开发人员路线图
menu_title: 开发人员路线图
menu_order: 2
---

本主题介绍要创建或自定义Magento应用程序的开发人员的高级工作流。开发人员还可以打包和分发他们的定制给商家。
要满足创建或自定义Magento应用程序所需的最少元素，请执行以下操作：

*  [声明组件依赖关系]({{ page.baseurl }}/extension-dev-guide/build/composer-integration.html) in `composer.json`.

   {:.bs-callout-tip}
   虽然您可以自己管理依赖项，但建议并强烈建议使用`composer.json`文件。

*  使用 `registration.php` 文件注册组件.
*  使用下面的组件指定的XML定义文件:
   *  模块: [`module.xml`]({{ page.baseurl }}/extension-dev-guide/build/create_component.html)
   *  主题: [`theme.xml`]({{ page.baseurl }}/frontend-dev-guide/themes/theme-create.html#fedg_create_theme_how-to_declare)
   *  语言包: [`language.xml`]({{ page.baseurl }}/config-guide/cli/config-cli-subcommands-i18n.html#config-cli-subcommands-xlate-pack-meta-xml)

*  分发组件:
   *  使用 `.zip`格式[打包组件]({{ page.baseurl }}/extension-dev-guide/package/package_module.html) 。
   *  如果您要将组件发布到Magento Marketplace，则组件打包文件应小于30MB。

