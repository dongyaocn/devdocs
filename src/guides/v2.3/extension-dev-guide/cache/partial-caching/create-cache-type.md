---
group: php-developer-guide
title: 创建缓存类型
---

  *缓存类型*允许您指定缓存的内容，并允许商家使用 [Magento 管理后台](https://glossary.magento.com/magento-admin)中的 [缓存](https://glossary.magento.com/cache) 管理页面清除该[缓存类型](https://glossary.magento.com/cache-type).

标记*作用域*为缓存类型提供了一种机制。

## 缓存类型配置 {#m2devgde-cache-type-configuration}

在 `etc/cache.xml` 文件中声明具有以下属性的新缓存类型:

| 属性 | 必须? | 描述 |
| --- | --- | --- |
| `name` | 是 | 唯一的缓存类型ID |
| `translate` | 否 | 将在"缓存管理"页上转换的参数 |
| `instance` | 是 | 缓存类型模型类 |

此外，缓存类型配置具有以下必需参数：

| 参数 | 描述 |
| --- | --- |
| `label` | "缓存类型"字段将显示在 `System` > `Tools` > `Cache Management` 页面. |
| `description` | "说明"字段将显示在 `System` > `Tools` > `Cache Management` 页面. |

例如:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Cache/etc/cache.xsd">
    <type name="%cache_type_id%" translate="label,description" instance="VendorName\ModuleName\Model\Cache\Type\CacheType">
        <label>Cache Type Label</label>
        <description>Cache Type Description</description>
    </type>
</config>
```

可以声明多个缓存类型。

## 缓存类型模型 {#m2devgde-cache-type-model}

```php
<?php
namespace VendorName\ModuleName\Model\Cache\Type;

use Magento\Framework\App\Cache\Type\FrontendPool;
use Magento\Framework\Cache\Frontend\Decorator\TagScope;

/**
 * System / Cache Management / Cache type "Your Cache Type Label"
 */
class CacheType extends TagScope
{
    /**
     * Cache type code unique among all cache types
     */
    const TYPE_IDENTIFIER = '%cache_type_id%';

    /**
     * The tag name that that limits the cache cleaning scope within a particular tag
     */
    const CACHE_TAG = '%CACHE_TYPE_TAG%';

    /**
     * @param FrontendPool $cacheFrontendPool
     */
    public function __construct(FrontendPool $cacheFrontendPool)
    {
        parent::__construct(
            $cacheFrontendPool->get(self::TYPE_IDENTIFIER),
            self::CACHE_TAG
        );
    }
}
```

必须指定以下参数：

*  `VendorName\ModuleName` 定义使用缓存类型的[模块](https://glossary.magento.com/module)的名称。一个模块可以使用多个缓存类型，一个缓存类型可以在多个模块中使用。
*  `%cache_type_id%` 定义缓存类型的唯一标识符。
*  `%CACHE_TYPE_TAG%` 定义要在缓存类型作用域中使用的唯一标记。

[tagscope]: {{ site.mage2bloburl }}/{{ page.guide_version }}/lib/internal/Magento/Framework/Cache/Frontend/Decorator/TagScope.php
[type]: {{ site.mage2bloburl }}/{{ page.guide_version }}/app/code/Magento/Customer/Model/Cache/Type/Notification.php
