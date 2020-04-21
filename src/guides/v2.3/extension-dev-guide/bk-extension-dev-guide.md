---
group: php-developer-guide
title: PHP开发人员指南
---

[PHP](https://glossary.magento.com/php)开发人员指南包含了一些信息，供希望了解有关开发或修改magento组件的更多信息的开发人员使用。利用这些知识，您可以扩展或自定义Magento应用程序中的任何现有组件。您还可以创建引入新功能并将其分发给商家的组件。

## Magento组件

Magento应用程序由*模块*、*主题*和*语言包*组成：

*  [**模块**]({{ page.baseurl }}/architecture/archi_perspectives/components/modules/mod_intro.html) 与应用程序的其他部分交互，以完成特定的业务功能或提供功能。[模块](https://glossary.magento.com/module)可以包含用于显示信息或与用户交互的用户界面。它还可以包含另一个Magento模块或代码块可能调用的应用程序接口。

*  [**主题**]({{ page.baseurl }}/frontend-dev-guide/themes/theme-overview.html)通过改变[店面](https://glossary.magento.com/storefront)或[管理后台](https://glossary.magento.com/admin)的外观和感觉，为每个Magento安装提供了个性化的触感。默认的Magento 2.x代码结构中已经有两个主题：Blank主题和Luma主题。创建自定义主题时，请参考这些默认主题。

*  [**语言包**]({{ page.baseurl }}/frontend-dev-guide/translations/xlate.html)通过为显示在店面和管理器上的字符串提供翻译，帮助实现国际化（i18n）和本地化。

 {:.bs-callout-info}
在构建模块时，必须遵循[PSR-4 compliant](http://www.php-fig.org/psr/psr-4/) 结构。

{:.ref-header}
相关主题

*  [开发人员路线图]({{ page.baseurl }}/extension-dev-guide/intro/developers_roadmap.html)
*  [Composer 介绍]({{ page.baseurl }}/extension-dev-guide/intro/intro-composer.html)
*  [通用术语表]({{ page.baseurl }}/extension-dev-guide/intro/intro-composer-gloss.html)
