---
group: frontend-developer-guide
title: 前端开发人员指南
landing-page: 前端开发人员指南
functional_areas:
  - 前端
---

## 介绍 {#overview-introduction}

本文档提供了为Magento应用程序创建和安装定制[店面主题](https://glossary.magento.com/storefront)的说明。它描述了Magento的内容呈现过程，并解释了系统的视图层，以便有效地构建[主题](https://glossary.magento.com/theme) 。该文档还介绍了[前端](https://glossary.magento.com/frontend)开发人员的日常任务。

开发自定义[模块](https://glossary.magento.com/module)和自定义[Magento Admin](https://glossary.magento.com/magento-admin)面板设计超出了本指南的范围。

前端开发人员可以使用此指南创建自定义主题，为特定客户定制Magento店面。

你可以将这些定制级别应用到你的网站，这些级别需要不同的开发技能:

*  您可以使用层叠样式表(CSS)对站点进行相对简单的更改，以更改各种界面组件的颜色和外观，替换图像，以及其他相对美观的更改。对于更高级的样式，熟悉LESS (Leaner Style Sheets)和XML (Extensible Markup Language)会有帮助。

    不需要对页面进行结构更改—您可以接受站点上加载的模块默认提供的站点结构。

    这可能是一个不错的起点，因为它需要较少的工作量和知识。

*  除了更改[CSS](https://glossary.magento.com/css)和站点上的图片之外，还有一小步要做，那就是更改由现有模块生成的[HTML](https://glossary.magento.com/html)。

    这需要基本的[PHP](https://glossary.magento.com/php)技能来调整[PHTML](https://glossary.magento.com/phtml)模板文件。

    虽然涉及到PHP编码，但这通常是从现有模板文件复制和粘贴一小段PHP代码到具有不同结构的HTML的新模板文件中。

    如果生成的现有HTML没有足够的CSS类名或HTML元素来实现您希望实现的表示更改，那么这将非常有用。

*  下一个复杂的层次是通过在页面上的不同位置之间移动功能或移动到完全不同的页面来对您的站点进行结构更改。

    这是使用Magento [layout](https://glossary.magento.com/layout)引擎实现的。布局更改不需要PHP代码，但是布局引擎相当复杂。

*  最后，您可以开发新的模块来添加新的自定义功能到您的站点，或者扩展现有的Magento或第三方模块提供的功能。

    这第三层定制在本指南中没有提到。

    有关如何开发新模块的详细信息，请参阅开发人员指南。

    这不仅需要了解前面所有领域的知识，还需要了解PHP编程知识。

## Frontend development prerequisites {#fedg-prereqs}

To implement what is discussed in this guide, you need a working Magento installation and the following browser versions installed on your device:

{% include browsers/supported-browsers.md %}

To use this guide, you must be familiar with:

*  [CSS, CSS 3](https://glossary.magento.com/css)
*  [LESS](https://glossary.magento.com/less)
*  [HTML and HTML 5](https://glossary.magento.com/html)
*  [XML](https://glossary.magento.com/xml)
*  [JavaScript](https://glossary.magento.com/javascript)
*  [PHTML](https://glossary.magento.com/phtml)
*  [PHP (Basic)](https://glossary.magento.com/php)
*  [Responsive Web Design (RWD)](https://devdocs.magento.com/guides/v2.3/frontend-dev-guide/responsive-web-design/rwd_overview.html)

{:.ref-header}
Related topics

*  [Themes]({{ page.baseurl }}/frontend-dev-guide/themes/theme-overview.html)
*  [Magento UI library]({{ page.baseurl }}/frontend-dev-guide/css-topics/theme-ui-lib.html)
*  [Cascading style sheets (CSS)]({{ page.baseurl }}/frontend-dev-guide/css-topics/css-overview.html)
*  [JavaScript coding standard]({{ page.baseurl }}/coding-standards/code-standard-javascript.html)
*  [Responsive web design]({{ page.baseurl }}/frontend-dev-guide/responsive-web-design/rwd_overview.html)
*  [Translations]({{ page.baseurl }}/frontend-dev-guide/translations/xlate.html)

