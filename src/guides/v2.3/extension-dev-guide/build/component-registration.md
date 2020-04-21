---
group: php-developer-guide
title: 注册组件
---

Magento组件，包括模块、主题和语言包，必须通过Magento`componentregistrator`类在Magento系统中注册。

在每个组件的根目录都有一个名为 `registration.php` 的文件。例如这里是[AdminNotification module]({{ site.mage2bloburl }}/{{ page.guide_version }}/app/code/Magento/AdminNotification/registration.php)的`registration.php`文件. 根据组件的类型，可以通过 `registration.php` 进行注册，方法如下：

## 注册模块 {#register-modules}

将模块注册到：

```php
ComponentRegistrar::register(ComponentRegistrar::MODULE, '<VendorName_ModuleName>', __DIR__);
```

这里的 `<VendorName>` 是提供 [模块](https://glossary.magento.com/module) 的公司名称， `<ModuleName>` 是模块的名称。

避免对自定义模块名使用`Ui`，因为指定路径时需要使用<code>%Vendor%_Ui</code>符号，这可能会导致问题。

### 示例

```php
use Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(ComponentRegistrar::MODULE, 'Magento_AdminNotification', __DIR__);
```

## 注册主题 {#register-themes}

注册主题：

```php
ComponentRegistrar::register(ComponentRegistrar::THEME, '<area>/<vendor>/<theme name>', __DIR__);
```

这里 `<area>`是模块的功能区 (frontend, controller, 等等.)，`<vendor>` 是提供主题的公司的名称， `<theme name>` 是 [主题](https://glossary.magento.com/theme)名称。

### 示例

```php
use Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(ComponentRegistrar::THEME, 'frontend/Magento/luma', __DIR__);
```

## 注册语言包 {#register-langpacks}

注册语言包：

```php
ComponentRegistrar::register(ComponentRegistrar::LANGUAGE, '<VendorName>_<packageName>', __DIR__);
```

这里 `<VendorName>` 提供语言包公司的名称， `<packageName>`是语言包的名称。

### 示例

```php
use Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(ComponentRegistrar::LANGUAGE, 'magento_de_de', __DIR__);
```

## 注册库 {#register-libraries}

库是这样注册的

```php
ComponentRegistrar::register(ComponentRegistrar::LIBRARY, '<vendor>/<library_name>', __DIR__);
```

这里 `<vendor>` 是提供库的公司的名称。 `<library_name>` 是库的名称。

### 示例

```php
use Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(ComponentRegistrar::LIBRARY, 'magento/framework', __DIR__);
```

## 调用 `registration.php` 在 `composer.json` 自动加载 {#register-autoload}

创建 `registration.php` 文件后，并创建 [组件的 composer.json 文件]({{page.baseurl}}/extension-dev-guide/build/composer-integration.html)后，在`composer.json`文件的`autoload` 部分调用 `registration.php` :

```json
{
 "name": "Acme-vendor/bar-component",
 "autoload": {
    "psr-4": { "AcmeVendor\\BarComponent\\": "" },
    "files": [ "registration.php" ]
 }
}
```

### 简单的 `registration.php` 文件 {#register-sample}

```php
use Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(ComponentRegistrar::MODULE, 'Magento_AdminNotification', __DIR__);
```

{:.ref-header}
下一步

[URN schema 验证]({{ page.baseurl }}/extension-dev-guide/build/XSD-XML-validation.html)
