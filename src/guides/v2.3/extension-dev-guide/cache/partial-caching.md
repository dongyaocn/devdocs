---
group: php-developer-guide
subgroup: 08_Partial caching
title: 局部缓存
menu_title: 局部缓存
menu_order: 1
menu_node: parent
---

Magento 使用 [Zend_Cache](http://framework.zend.com/manual/1.12/en/zend.cache.html){:target="_blank"}与缓存存储交互. 但是，Magento也有用于实现Magento特定缓存的 [Magento\Cache]({{ site.mage2bloburl }}/{{ page.guide_version }}/lib/internal/Magento/Framework/Cache){:target="_blank"} [库](https://glossary.magento.com/library) 。 这些主题讨论如何配置缓存和 [缓存](https://glossary.magento.com/cache) 类型.

 {:.bs-callout-info}
默认情况下，文件系统缓存已启用；无需配置即可使用它。这意味着缓存位于`<magento_root>/var`之下。

要更改缓存配置，请编辑 `<magento_root>/app/etc/env.php`.

缓存配置是一个关联数组，类似于以下内容：

```php
'cache_types' =>
   array (
      'config' => 1,
      'layout' => 1,
      'block_html' => 1,
      'collections' => 1,
      'db_ddl' => 1,
      'eav' => 1,
      'full_page' => 1,
      'translate' => 1,
      'config_integration' => 1,
      'config_webservice' => 1,
      'config_integration_api' => 1,
   ),
);
```

前面列出了所有缓存类型，并显示它们都已启用。

## 有关缓存的详细信息

以下主题讨论如何设置缓存：

*  [创建缓存类型]({{ page.baseurl }}/extension-dev-guide/cache/partial-caching/create-cache-type.html)
*  [创建或扩展配置类型]({{ page.baseurl }}/config-guide/config/config-create.html)
*  [将缓存前端与缓存类型关联]({{ page.baseurl }}/config-guide/cache/cache-types.html)
*  [低级别缓存选项]({{ page.baseurl }}/config-guide/cache/cache-options.html)
*  [配置和使用 Varnish]({{ page.baseurl }}/config-guide/varnish/config-varnish.html)
*  [配置 Redis]({{ page.baseurl }}/config-guide/redis/config-redis.html)

