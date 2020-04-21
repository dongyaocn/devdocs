---
group: php-developer-guide
title: composer.json文件
---

## 概述

Magento 2 使用 [Composer][0]{:target="_blank"}, 这是一个 [PHP](https://glossary.magento.com/php) 依赖管理器，用来打包组件和产品版本。

Composer读取Magento根目录中的`Composer.json`文件，以下载该文件中列出的第三方依赖项。

[组件管理器][1] 在扩展根目录中 使用 `composer.json` 文件执行以下操作:

*  如果使用Composer 安装(包含 来自 [Packagist][2]{:target="_blank"}, [Magento Marketplace][6]{:target="_blank"}, 或者其他源) *和* 包含一个 `composer.json` 文件组件，则组件管理器可以更新、卸载、启用或禁用扩展。
*  *没有*使用Composer（例如自定义代码）安装扩展。但如果组件包含了`composer.json`文件，组件管理器依然可以启用/禁用这个扩展。

我们建议您在组件的根目录中包含`composer.json`，即使您不打算使用Magento将其分发给其他商家。

 {:.bs-callout-info}
Magento 不支持 [`path`][3] 仓库。

## composer.json

这是一个 composer.json 示例文件

{% collapsible composer.json 文件内容 %}
 ```json
  {
    "name": "mycompany/sample-module-minimal",
    "description": "A module that creates a page in the Magento admin area",
    "type": "magento2-module",
    "version": "1.0.0",
    "license": [
      "OSL-3.0",
      "AFL-3.0"
    ],
    "require": {
      "php": "~7.1.3||~7.2.0||~7.3.0"
    },
    "autoload": {
      "files": [ "registration.php" ],
      "psr-4": {
        "MyCompany\\ExampleAdminNewPage\\": ""
      }
    }
  }
 ```
{% endcollapsible %}

## Composer 二进制文件位置 {#composer-binary}

Magento 使用 `<Magento root>/vendor/composer` 目录下的composer二进制文件，而不是全局安装的[composer](https://glossary.magento.com/composer).

在使用Magento 2自定义、更新或排除composer故障时，请记住这一点。

## 项目与产品

在Composer中， "project" 包是 [`composer create-project`][9]{:target="_blank"} 用来设置项目结构的模板.
[系统集成程序的安装说明][10] 使用 {{site.data.var.ce}} 和 {{site.data.var.ee}} 项目包来设置 Magento 目录结构。

"product" 包是使用`composer create-project`下载并安装项目包之后由 `composer.json`指向实际的应用程序。

## 不同composer.json文件的说明 {#composerjson-overview}

下面的Magento组件和产品版本使用一个`composer.json` 文件。

### Magento Root

**位置:** `composer.json`

**名称:** `magento/magento2ce`

**类型:** `project`

这是Magento的主`composer.json`文件，它声明依赖项和第三方组件。

其他root`composer.json`文件将此文件用作模板。

---

### {{site.data.var.ce}} 项目
**位置:** `composer.json`

**名称:** `magento/project-community-edition`

**类型:** `project`

Magento 系统集成者使用 `composer.json` 文件来部署{{site.data.var.ce}}产品及其依赖。

---

### {{site.data.var.ee}} 项目
**位置:** `composer.json`

**名称:** `magento/product-enterprise-edition`

**类型:** `metapackage`

Magento 系统集成者使用 `composer.json` 文件来部署{{site.data.var.ce}}产品及其依赖。

---

### Magento 框架

**位置:** `lib/internal/Magento/Framework/composer.json`

**名称:** `magento/framework`

**类型:** `magento2-library`

Magento 应用程序使用这个 `composer.json` 文件作为其框架包.

---

### 模块

**位置:**

*  `app/code/<vendor-name>/<module-name>/composer.json`
*  `vendor/<vendor-name>/<module-name>/composer.json`

**名称:** `<vendor-name>/<package-name>`

**类型:** `magento2-module`

[模块](https://glossary.magento.com/module)使用这个`composer.json`文件声明了扩展运行需要的依赖项。

---

### 主题

**位置:**

*  `app/design/frontend/<vendor-name>/<theme-name>/composer.json`
*  `app/design/adminhtml/<vendor-name>/<theme-name>/composer.json`

**名称:** `<vendor-name>/<package-name>`

**类型:** `magento2-theme`

[主题](https://glossary.magento.com/theme) 组件的`composer.json`文件 包含和继承了父主题的扩展和依赖项。

---

### 语言包

**位置:**
`app/i18n/<vendor-name>/<language-code>/composer.json`

**名称:** `<vendor-name>/<package-name>`

**类型:** `magento2-language`

对于语言包, 你必须对`composer.json`文件中的语言代码使用正确的[ISO 代码][4]{:target="_blank"}

---

## Magento-特定的包类型

Magento扩展可以是以下任何类型：

*  `magento2-module` 模块
*  `magento2-theme` 主题
*  `magento2-language` 语言包
*  `magento2-component` 表示不适合任何其他类型的通用扩展

扩展类型告诉系统在Magento目录结构中安装每个扩展的目录和文件的位置。

## 命名约定

由于Composer包的命名空间在包仓库中是全局的命名空间 [packagist.org][2], 因此在命名包时候请使用以下格式：

`<vendor-name>/<package-name>`

使用Composer命名约定有助于将软件包与不同的供应商区分开来，从而降低冲突的风险。

### vendor-name

供应商名称中的所有字母都必须小写。
例如，Magento Inc发布的扩展名的供应商名称格式是`magento`。

#### Magento扩展市场

Magento Marketplace在扩展提交过程中使用 `vendor-name` 将扩展与供应商匹配。
如果您计划将您的扩展提交到 [Magento Marketplace][7]{:target="_blank"}, 则您*必须*使用创建Marketplace帐户时创建或分配给您的唯一供应商名称。

在`composer.json`文件中，将配置文件中的'Vendor Name'值用作扩展名的`vendor-name`部分。

有关您的唯一供应商名称的详细信息，请参见 [Marketplace Documentation][5]{:target="_blank"}.

### package-name

`package-name` 中的所有字母必须是小写。

如果名称包含多个单词，则编写器规范建议使用破折号分隔它们。

Magento包名称的约定如下：

`magento/<type-prefix>-<suffix>[-<suffix>]...`

在这里:

:`type-prefix` 是Magento的任何扩展类型:

*  `module-` 是对于模块的
*  `theme-` 是对于扩展的
*  `language-` 是对于语言包的
*  `product-` 是对于[元包][8] 例如 {{site.data.var.ce}} 或者 {{site.data.var.ee}}

: `suffix` 是该类型扩展的唯一标识符。

## 版本管理 {#component-version}
{% include php-dev/component-versioning.md %}

---

**下一步:**
[定义配置文件]({{ page.baseurl }}/extension-dev-guide/build/required-configuration-files.html)

[0]: https://getcomposer.org/
[1]: {{ page.baseurl }}/comp-mgr/module-man/compman-start.html
[2]: https://packagist.org/
[3]: https://getcomposer.org/doc/05-repositories.md#path
[4]: https://www.iso.org/iso-639-language-codes.html
[5]: https://devdocs.magento.com/marketplace/sellers/profile-company.html
[6]: https://marketplace.magento.com/
[7]: https://marketplace.magento.com
[8]: {{ page.baseurl }}/extension-dev-guide/package/package_module.html#package-metapackage
[9]: https://getcomposer.org/doc/03-cli.md#create-project
[10]: {{ page.baseurl }}/install-gde/composer.html
