---
group: php-developer-guide
title: 命名组件
---

在`composer.json`和`module.xml`文件中为组件命名。这些文件还包含其他必需的配置参数，例如模块的架构版本。

## 先决条件 {#prereq}

继续之前，请确保已完成以下所有任务：

*  创建  [文件结构]({{page.baseurl}}/extension-dev-guide/build/module-file-structure.html)。
*  创建需要的 [配置文件]({{page.baseurl}}/extension-dev-guide/build/required-configuration-files.html) 。
*  [注册]({{page.baseurl}}/extension-dev-guide/build/component-registration.html) 组件。

## 添加组件的 `module.xml` 文件 {#add-component-xml}

通过在组件目录下的`/etc`目录中添加一个 `module.xml`来声明组件本身。

组件在`module.xml`文件中声明自己 (即定义名称和存在) , 位于Magento安装目录 `<ComponentName>/etc/`中。

工作最简单的`module.xml` 文件如下:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
        <module name="Vendor_ComponentName"/>
</config>
```

`name` 参数定义了组件的名称。所有组件都需要。 如果不使用 [Declarative Schema]({{ page.baseurl }}/extension-dev-guide/declarative-schema/index.html) 来辅助管理处理组件的安装和升级，则还必须添加  `setup_version` 参数在 `module` 这一行中。 将`setup_version` 值设置为模块 [database schema](https://glossary.magento.com/database-schema) 的版本。 如果不使用[Declarative Schema]({{ page.baseurl }}/extension-dev-guide/declarative-schema/index.html)，请忽略`setup_version`参数。

 {:.bs-callout-info}
避免使用 "Ui" 在你的模块名称中，因为 `%Vendor%_Ui` 指定的路径中包含符号, 可能会导致问题.

## 添加组件的 `composer.json` 文件 {#add-composer-json}
`composer.json`指定组件名称并提供组件依赖项。

此外,  [组件管理器]({{ page.baseurl }}/comp-mgr/module-man/compman-start.html) 在组件根目录中查找`composer.json` ，并可以对组件及其依赖项执行操作：

*  如果组件具有 `composer.json` *并且* 组件使用 [Composer](https://glossary.magento.com/composer) (包含自 packagist,  Magento Marketplace, 或者其他源)安装组件，Component 管理器可以更新，删除，启用，禁用组件。
*  组件具有 `composer.json` 但 *不是* 通过 Composer (例如, 开发人员编写的自定义代码)安装，, Component 管理器仍然可以启用或者禁用组件。
*  我们强烈推荐在你的组件根目录中包含 `composer.json`不管你是否打算将它分发给其他的Magento商家。

参考 [模块版本依赖项]({{ page.baseurl }}/extension-dev-guide/versioning/dependencies.html) 以确定版本控制需求。

### 示例 `composer.json` 文件

```json
{
    "name": "your-name/module-Acme",
    "description": "Test component for Magento 2",
    "require": {
        "php": "~7.1.3||~7.2.0",
        "magento/module-store": "102.1",
        "magento/module-catalog": "102.1",
        "magento/module-catalog-inventory": "102.1",
        "magento/module-ui": "self.version",
        "magento/magento-composer-installer": "*"
    },
    "suggest": {
      "magento/module-webapi": "102.1"
    },
    "type": "magento2-module",
    "version": "102.1",
    "license": [
        "OSL-3.0",
        "AFL-3.0"
    ],
    "autoload": {
        "files": [ "registration.php" ],
        "psr-4": {
            "Magento\\CatalogImportExport\\": ""
        }
    }
}
```

在这个示例中：

*  `name` 是组件的名称
*  `description` 是对组件用途的简明说明。
*  `require` 列出组件所依赖的任何组件。
*  `suggest` 列出软依赖项。组件可以在没有它们的情况下运行，但是如果组件处于活动状态，则此组件可能会影响它们的功能。`Suggest`不影响组件加载顺序。
*  `type` 确定 [Magento 组件](https://glossary.magento.com/magento-component) 类型。 在这些类型 *magento2-theme*, *magento2-language*, 或者 *magento2-module*中选择一个。
*  `version` 列出组件的版本。
*  `license` 列出适用于组件的适用许可证。
*  `autoload` 指示 Composer 加载指定的文件。

 {:.bs-callout-info}
Magento 当前不支持 [`path`](https://getcomposer.org/doc/05-repositories.md#path) 仓库.

#### 下一步

[组件加载顺序]({{ page.baseurl }}/extension-dev-guide/build/module-load-order.html)