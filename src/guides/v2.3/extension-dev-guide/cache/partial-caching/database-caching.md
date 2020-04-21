---
group: php-developer-guide
title: 创建自定义缓存引擎
redirect_from:
  -  /guides/v2.3/config-guide/database/database.html
  -  /guides/v2.3/config-guide/cache/caching-database.html
---

## 数据库缓存概述 {#mage-cache-db-over}

本主题讨论如何使用Magento 2数据库进行缓存。完成这些任务后，缓存对象将存储在 `cache` 和 `cache_tag` Magento 2数据库表中。并非存储在 `var/cache` 或者 `var/page_cache`.

本主题讨论如何设置数据库缓存以及如何验证数据库缓存是否正常工作。我们讨论以下选项：

*  使用 `default` 缓存前端,，在这种情况下只能修改`di.xml` 。
*  使用自定义 [缓存](https://glossary.magento.com/cache) 前端，在这种情况下只能修改`env.php` 。	 

{:.bs-callout-warning}
数据库缓存---类似于基于文件的缓存--- 在开发环境中运行良好，但我们强烈建议您在生产中使用 [Varnish][]
Varnish被设计用来加速HTTP协议。

## 先决条件 {#mage-cache-db-prereq}

继续之前，如果正在使用自己的前端缓存，请确保 [将缓存前端与缓存类型关联]。如果使用 `default` [前端](https://glossary.magento.com/frontend) 缓存，则不必这样做。

我们在本主题的最后提供[示例配置]。

## 数据库缓存使用 `default` 缓存前端 {#mage-cache-db-di}

要使用 `default` 前端启用数据库缓存，必须修改 `<magento_root>/app/etc/di.xml`，这是magento应用程序的全局部署注入配置。

修改 `di.xml`:

1. 以[Magento文件系统所有者]的身份登录到Magento服务器，或切换到该服务器。
1. 输入一下命令复制 `di.xml`:

   ```bash
   cd <magento_root>/app/etc
   ```

   ```bash
   cp di.xml di.xml.bak
   ```

1. 在文档编辑器中打开 `di.xml` 并定位到一下代码块:

   ```xml
   <type name="Magento\Framework\App\Cache\Frontend\Pool">
       <arguments>
           <argument name="frontendSettings" xsi:type="array">
               <item name="page_cache" xsi:type="array">
                   <item name="backend_options" xsi:type="array">
                       <item name="cache_dir" xsi:type="string">page_cache</item>
                   </item>
               </item>
           </argument>
       </arguments>
   </type>
   <type name="Magento\Framework\App\Cache\Type\FrontendPool">
       <arguments>
           <argument name="typeFrontendMap" xsi:type="array">
               <item name="full_page" xsi:type="string">page_cache</item>
           </argument>
       </arguments>
   </type>
   ```

   `<type name="Magento\Framework\App\Cache\Frontend\Pool">` 节点为所有前端缓存实例的内存池配置选项。

   `<type name="Magento\Framework\App\Cache\Type\FrontendPool">` 节点配置特定于每种缓存类型的缓存前端选项。

1. 用以下内容替换整个块:

   ```xml
   <type name="Magento\Framework\App\Cache\Frontend\Pool">
       <arguments>
           <argument name="frontendSettings" xsi:type="array">
               <item name="page_cache" xsi:type="array">
                   <item name="backend" xsi:type="string">database</item>
               </item>
               <item name="<your cache id>" xsi:type="array">
                   <item name="backend" xsi:type="string">database</item>
               </item>
           </argument>
       </arguments>
   </type>
   <type name="Magento\Framework\App\Cache\Type\FrontendPool">
       <arguments>
           <argument name="typeFrontendMap" xsi:type="array">
               <item name="backend" xsi:type="string">database</item>
           </argument>
       </arguments>
   </type>
   ```

   where `<your cache id>` is your unique cache identifier.

1. Save your changes to `di.xml` and exit the text editor.

1. Continue with [Verify database caching is working].

## Database caching using a custom cache frontend {#mage-cache-db-env}

This section discusses how to set up database caching with a custom [cache frontend](https://glossary.magento.com/cache-frontend).

{:.bs-callout-info}
Due to a known issue, a custom cache frontend still results in some objects being cached to the file system; however, fewer assets are cached compared to file system caching.

To enable database caching using a custom cache frontend, you must modify `<magento_root>/app/etc/env.php` as follows:

1. Log in to the Magento server as, or switch to, the [Magento file system owner].
1. Enter the following commands to make a copy of `env.php`:

   ```bash
   cd <magento_root>/app/etc
   ```

   ```bash
   cp env.php env.php.bak
   ```

1. Open `env.php` in a text editor and add the following anywhere, such as before `'cache_types' =>`:

   ```php
   'cache' => [
       'frontend' => [
           '<unique frontend id>' => [
                <cache options>
           ],
       ],
       'type' => [
            <cache type 1> => [
                'frontend' => '<unique frontend id>'
           ],
       ],
       'type' => [
            <cache type 2> => [
               'frontend' => '<unique frontend id>'
           ],
       ],
   ],
   ```

   An example is shown in [Configuration examples].

1. Save your changes to `env.php` and exit the text editor.
1. Continue with the next section.

## Verify database caching is working {#mage-cache-db-verify}

To verify database caching is working, clear the current cache directories, go to any cacheable page in a web browser, and verify that data is written to the database and not to the file system.

Use the following steps:

1. If you haven't done so already, log in to the Magento server as, or switch to, the [Magento file system owner].
1. Clear the current cache directories:

   ```bash
   rm -rf <magento_root>/var/cache/* <magento_root>/var/page_cache/* <magento_root>/generated/metadata/* <magento_root>/generated/code/*
   ```

1. In a web browser, go to any cacheable page (such as the [storefront](https://glossary.magento.com/storefront) front door page).

 If exceptions display, verify `di.xml` syntax and try again. (To see exceptions in the browser, you must [enable developer mode].)
1. Enter the following commands:

   ```bash
   ls <magento_root>/var/cache/*
   ```

   ```bash
   ls <magento_root>/var/page_cache/*
   ```

   {:.bs-callout-info}
   Due to a known issue, a custom cache frontend still results in some objects being cached to the file system; however, fewer assets are cached compared to file system caching. If you use the `default` cache frontend, you don't have this issue.

1. Verify both directories are empty; if not, edit `di.xml` again and correct any issues.
1. Use a database tool such as [phpMyAdmin] to verify there is data in the `cache` and `cache_tag` tables.

   The following figures show examples. The important thing is that there are rows in the tables. *The data in your tables will be different than the following*.

   `cache` table example.

   ![Sample contents of the cache table with database caching enabled]

   `cache_tag` table example.

   ![Sample contents of the cache tag table with database caching enabled]

## Configuration examples {#mage-cache-db-config}

This section contains code sample snippets to refer to when configuring database caching.

### Sample `di.xml` for the default cache frontend {#mage-cache-db-config-default}

`di.xml` snippet:

```xml
<type name="Magento\Framework\App\Cache\Frontend\Pool">
    <arguments>
        <argument name="frontendSettings" xsi:type="array">
            <item name="page_cache" xsi:type="array">
                <item name="backend" xsi:type="string">database</item>
            </item>
            <item name="default" xsi:type="array">
                <item name="backend" xsi:type="string">database</item>
            </item>
        </argument>
    </arguments>
</type>
<type name="Magento\Framework\App\Cache\Type\FrontendPool">
    <arguments>
        <argument name="typeFrontendMap" xsi:type="array">
            <item name="backend" xsi:type="string">database</item>
        </argument>
    </arguments>
</type>
```

### Sample `env.php` for a custom cache frontend {#mage-cache-db-config-custom}
`env.php` snippet that enables all cache types with a custom frontend named `magento_cache`:

```php
'cache' => [
    'frontend' => [
        'magento_cache' => [
            'backend' => 'database'
        ],
    ],
    'type' => [
        'config' => [
            'frontend' => 'magento_cache'
        ],
        'layout' => [
            'frontend' => 'magento_cache'
        ],
        'block_html' => [
            'frontend' => 'magento_cache'
        ],
        'view_files_fallback' => [
            'frontend' => 'magento_cache'
        ],
        'view_files_preprocessing' => [
            'frontend' => 'magento_cache'
        ],
        'collections' => [
            'frontend' => 'magento_cache'
        ],
        'db_ddl' => [
            'frontend' => 'magento_cache'
        ],
        'eav' => [
            'frontend' => 'magento_cache'
        ],
        'full_page' => [
            'frontend' => 'magento_cache'
        ],
        'translate' => [
            'frontend' => 'magento_cache'
        ],
        'config_integration' => [
            'frontend' => 'magento_cache'
        ],
        'config_integration_api' => [
            'frontend' => 'magento_cache'
        ],
        'config_webservice' => [
            'frontend' => 'magento_cache'
        ],
    ],
],
```

<!-- Link references -->
[Varnish]: {{ page.baseurl }}/config-guide/varnish/config-varnish.html
[associate cache frontends with cache types]: {{ page.baseurl }}/config-guide/cache/cache-types.html
[sample configurations]: #mage-cache-db-config
[Magento file system owner]: {{ page.baseurl }}/install-gde/prereq/file-sys-perms-over.html
[Verify database caching is working]: #mage-cache-db-verify
[Configuration examples]: #mage-cache-db-config
[enable developer mode]: {{ page.baseurl }}/config-guide/cli/config-cli-subcommands-mode.html#change-to-developer-mode
[phpMyAdmin]: {{ page.baseurl }}/install-gde/prereq/optional.html#install-optional-phpmyadmin

<!-- Image references -->
[Sample contents of the cache table with database caching enabled]: {{ site.baseurl }}/common/images/config-db_cache-table.png
[Sample contents of the cache tag table with database caching enabled]: {{ site.baseurl }}/common/images/config-db_cache-tag-table.png
