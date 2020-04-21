---
group: php-developer-guide
title: 通用术语表
---

### 组件 {#gloss-component}

我们将您编写的代码称之为 *组件*. (Composer 称之为 <a href="https://getcomposer.org/doc/05-repositories.md#packages" target="_blank">*包*</a>;  这里的组件和包是一样的意思。)  

[Magento 组件](https://glossary.magento.com/magento-component) 可以分为以下几种*类型*:

*  [模块](https://glossary.magento.com/module) (扩展 Magento 功能)
*  [主题](https://glossary.magento.com/theme) (改变 [店面](https://glossary.magento.com/storefront) 和 管理后台 的视觉感官)
*  [语言包](https://glossary.magento.com/language-package) (本地化 店面 和 管理后台)

你可以把你的组件打包如下:

* 单独的

*  如果您开发的产品有多个组件，可以作为一个 [元包](https://getcomposer.org/doc/04-schema.md#type)。这是Magento Marketplace的要求。

   元包由*共享包*组成。例如：由模块和主题、两个模块、两个主题等组成的元包。
有关元包的更多信息可以在下一节中找到。

 {:.bs-callout-info}
Magento Marketplace把综合产品叫做组件或[元包](https://glossary.magento.com/metapackage).

### 元包 {#gloss-meta}

Magento Marketplace要求将多个组件打包为*元包*，该组件仅由指定单个组件及其依赖项的`composer.json`组成。（Magento Marketplace还将元包称为*扩展*）

元包需要或建议我们称为*共享包*的组件。如果愿意，可以在多个元包中使用共享包。（如果使用共享包，Marketplace要求元包中的*所有*组件都是共享包。）

例如，您可能希望在Magento Marketplace中列出两个元软件包：标准软件包和高级软件包。所有的标准包组件都可以是高级包使用的共享包。除此之外，这使商家能够使用<a href="#gloss-compman">Magento组件管理器</a>轻松地从您的标准包升级到您的高级包。

商家不需要明白，在封装下，有些包是共享的。

{:.bs-callout-warning}
您可以上传到Magento Marketplace，只要您想，但您必须明确地给予组件访问它们的权限。否则，您的组件在被商家安装后将无法正常工作。有关更多信息，请参见 [Magento Marketplace 用户指南](http://docs.magento.com/marketplace/user_guide/getting-started.html){:target="_blank"}.

{:.ref-header}
相关主题

*  [元包]({{ page.baseurl }}/extension-dev-guide/package/package_module.html#package-metapackage)
*  [`composer.json`中的组件类型]({{ page.baseurl }}/extension-dev-guide/build/composer-integration.html).

### 组件管理器 {#gloss-compman}

商家使用 [组件管理器]({{ page.baseurl }}/comp-mgr/module-man/compman-start.html) (Magento 管理后台的一部分) 执行以下任何操作:

*  安装, 卸载
*  更新
*  启用, 禁用

如果您按照本指南和<em>市场用户指南</em>中的说明打包和上载组件，则商家可以在您发布组件后轻松更新它们。

详细情况， 查看 [运行扩展管理器]({{ page.baseurl }}/comp-mgr/extens-man/extensman-checklist.html)
