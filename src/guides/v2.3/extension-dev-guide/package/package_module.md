---
group: php-developer-guide
subgroup: 05_Package
title: 打包组件
menu_title: 打包组件
menu_order: 2
---

## 打包概述 {#package-over}

Magento 程序使用 [Composer](https://glossary.magento.com/composer) 包在应用程序实例中分发, 安装, 升级组件。

要打包组件，必须：

*  创建 Magento Composer 文件 (`composer.json`).
*  使用 `registration.php` 文件注册组件。
*  打包并发布组件。

## 创建 Magento Composer 文件 {#composer}

Magento`composer.json`文件定义了组件的名称、需求、版本和其他基本信息。 此文件必须放在 [模块](https://glossary.magento.com/module)的根目录中。

`composer.json` 使用 [Composer的一般结构](https://getcomposer.org/doc/04-schema.md)， 有以下限制：

Element | Description
--- | ---
`name` | 完全限定的组件名称，格式为 `<vendor-name>/<component-name>`. 所有字母必须小写。使用破折号分隔词组`<component-name>` . 主题必须使用如下格式 `<vendor-name>/theme-<area>-<theme-name>`. 
`type` | 对于模块, 这个值必须设置为 `magento2-module`. 其他可能的类型是 `metapackage`, `magento2-theme`, 和 `magento2-language`。 
`autoload` | 指定要加载的必要信息, 像 [registration.php]({{ page.baseurl }}/extension-dev-guide/build/component-registration.html)，更多详细信息， 参考 Composer [自动加载](https://getcomposer.org/doc/01-basic-usage.md#autoloading) 。 

{% include php-dev/composer-types.md %}

### 使用 元包 {#package-metapackage}

元包 允许你把多个包组成的 [扩展](https://glossary.magento.com/extension)分组成一个聚合单元。它的工作原理与标准的[composer.json 文档](https://getcomposer.org/doc/04-schema.md#type)描述相同。如果您的扩展使用了多个包，则必须使用 [元包](https://glossary.magento.com/metapackage) 作为 *根包(root package)*。否则不应使用元包。提交给Magento Marketplace的元包应该是一个.zip文件，其中只包含元包 `composer.json` 文件.

 {:.bs-callout-info}
我们建议元包引用特定的组件版本。不要使用通配符来表示版本范围。

#### 元包 示例

下面是一个元包示例 `composer.json` :

```json

{
    "name": "magento/product-community-edition",
    "description": "A sample metapackage",
    "version": "2.0.0",
    "type": "metapackage",
    "require": {
        "php": "~7.1.3|~7.2.0",
        "zendframework/zend-stdlib": "~2.4.6",
        "zendframework/zend-code": "~2.4.6",
        "zendframework/zend-server": "~2.4.6",
        "zendframework/zend-soap": "~2.4.6",
        "zendframework/zend-uri": "~2.4.6",
        "zendframework/zend-validator": "~2.4.6",
        "zendframework/zend-crypt": "~2.4.6",
        "zendframework/zend-console": "~2.4.6",
        "zendframework/zend-modulemanager": "~2.4.6",
        "zendframework/zend-mvc": "~2.4.6",
        "zendframework/zend-text": "~2.4.6",
        "zendframework/zend-i18n": "~2.4.6",
        "ext-ctype": "*",
        "ext-gd": "*",
        "ext-spl": "*",
        "ext-dom": "*",
        "ext-simplexml": "*",
        "ext-mcrypt": "*",
        "ext-hash": "*",
        "ext-curl": "*",
        "ext-iconv": "*",
        "ext-intl": "*",
        "ext-xsl": "*",
        "ext-mbstring": "*",
        "ext-openssl": "*"
        },
    "license": [
        "OSL-3.0",
        "AFL-3.0"
    ]
}

```

###  composer.json 文件样本 {#sample-composerjson-file}

以下示例是模块的 `composer.json`文件

```json
{
  "name": "magento/sample-module-newpage",
  "description": "A Magento 2 module that creates a new page",
  "type": "magento2-module",
  "version": "1.0.0",
  "license": [
    "OSL-3.0",
    "AFL-3.0"
  ],
  "require": {
    "php": "~7.1.3|~7.2.0",
    "magento/framework": "~100.0.4"
  },
  "autoload": {
    "files": [ "registration.php" ],
    "psr-4": {
      "Magento\\SampleNewPage\\": ""
    }
  }
}

```

## 打包和发布扩展 {#packaging}

通过对带有扩展名的目录（不包括不必要的目录）执行zip操作，创建扩展名的包。例如：

    zip -r vendor-name_package-name-1.0.0.zip package-path/ -x 'package-path/.git/*'

对带有破折号的包文件名使用字母数字字符来分隔单词。不要使用空格。
Magento可以从任何有效的GitHub [URL](https://glossary.magento.com/url) 检索扩展包

<!-- After you have created the module's `composer.json` file in the root directory of the module, Composer can recognize your package as compatible with its deployment strategy. Such packages can be published to a code repository (GitHub, SVN, etc.), packagist.org, or on your own private package repository. -->

 {:.bs-callout-info}
支持第三方存储库。

### 在GitHub和Packagist上托管{#hosting}

前提条件: 必须在您的计算机上设置Git.

1. 导航到组件目录，根目录中有`composer.json`文件，并使其成为新的Git存储库. 详细信息查阅 [GitHub 文档](https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/) 。
1. 当您提交组件并将其推送到GitHub仓库时，您可以：

   *  使用 [Composer 直接引用](https://getcomposer.org/doc/05-repositories.md#vcs), 或者
   *  使用以下步骤通过Packagist引用包。

      1. 在 [packagist.org](https://packagist.org/)注册一个账户。
      1. 点击Submit Package 按钮并粘贴GitHub仓库链接。Packagist自动从组件的 `composer.json`文件收集信息并将其链接到GitHub仓库，允许您将包引用为 `vendor/module` ，而无需任何其他仓库信息，因为这仅需要使用GitHub。

### 托管在私有仓库上 {#private_repos}

 {:.bs-callout-info}
如果使用安装向导，则必须使用Magento Marketplace仓库。私有存储库可用于开发或私有代码，但安装必须使用命令行界面完成（您可以安装仅使用命令行安装指定私有仓库的包）。

1. 使用[Satis](https://getcomposer.org/doc/articles/handling-private-packages-with-satis.md) 或者 [Private Packagist](https://packagist.com/)等系统设置自己的Composer包仓库。
1. 以类似于上述的方式创建包。
1. 在仓库提交/注册包。例如，它可以作为代码存储库的引用托管，也可以作为zip存档提交。
1. 要在项目中使用私有打包仓库，请将以下内容添加到`composer.json`文件中：

   ```json
   {
       "repositories": [
           {
               "type": "composer",
               "url": [repository url here]
           }
       ]
   }
   ```

现在可以在 `require` 字段中引用私有仓库中的所有包。.

参考 [官方文档](https://packagist.com/features/private-vcs-packages) 有关如何将项目配置为使用私有Packagist的详细信息。
<!-- ##Submitting your module to Marketplace -->

