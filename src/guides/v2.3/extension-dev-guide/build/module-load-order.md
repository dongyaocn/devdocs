---
group: php-developer-guide
subgroup: 03_Build
title: 组件加载顺序
menu_title: 组件加载顺序
menu_order: 7000
---

你可能需要使用组件的 [composer.json]({{ page.baseurl }}/extension-dev-guide/build/create_component.html#add-component-xml)指定组件对其他组件或来自其他组件文件的依赖性。 进一步，你可以使用 `module.xml`文件中的`<sequence>` 标签确保在加载组件时，已经加载了其他组件中需要的文件。

`<sequence>` 声明在加载当前组件之前必须加载的组件列表。它用于加载不同类型的文件：配置文件、视图文件（包括CSS、Less和模板文件）或安装类。请注意 `<sequence>` 不影响常规类（非设置类）的加载。
*Setup* 类是组件中创建或更新 [数据库结构](https://glossary.magento.com/database-schema) 或数据的的类。

如果您知道组件的逻辑依赖于另一个组件中的某些内容，那么应该将此组件添加到 `module.xml` 的 `<sequence>` 中和 `composer.json` 的`require`中 。

成功设置Magento后，在`<magento_root>/app/etc/config.php` 文件中检查模块的加载顺序。 这个文件在运行时动态设置创建。

 {:.bs-callout-info}
如果使用 `<sequence>`改变了组件的加载顺序，必须在  `config.php`文件中重新生成组件列表; 否则，加载顺序不会生效。 目前，唯一的方法是通过[`magento module:enable`]({{ page.baseurl}}/install-gde/install/cli/install-cli-subcommands-enable.html#instgde-cli-subcommands-enable-disable)启用组件，其中 `<module-list>` 是 `<sequence>`添加了的一个或多个组件。

### 例如

假设您有一个组件需要来自另一个组件的配置文件：

__组件 B__ 引入了 `gadgetlayout.xml`，它从 __组件 A__更新块`gadgetBlock` 。在这个案例中， __组件 A__的布局文件应该在在 __组件 B__之前加载， 因此应该  [module](https://glossary.magento.com/module).xml文件中的组件B的`<sequence>` 条目中指定。 换句话说， __组件 B__ 依赖于 __组件 A__. 也就是说:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="Vendor_ComponentB" setup_version="0.0.1">
        <sequence>
        <!-- Vendor_ComponentB is dependent on Vendor_ComponentA: -->
            <module name="Vendor_ComponentA" />
        </sequence>
    </module>
</config>
```

对于每个特定的场景，从不同的组件加载相同类型的文件，同时考虑到每个组件的`module.xml`文件中提供的序列信息。

在另一种场景下，要加载名为 `default.xml`的所有的 [布局](https://glossary.magento.com/layout) 文件。 __组件 A__ 在`<sequence>`指定 __组件 B__ . 文件按以下顺序加载：

1. `component X/view/frontend/layout/default.xml`---或者我们不关心组件X何时加载，或者组件B要求在加载之前加载它。
1. `component B/view/frontend/layout/default.xml`
1. `component A/view/frontend/layout/default.xml`---在 __组件 B__ 之后加载，因为 __组件 B__ 列入了__组件 A的__ `<sequence>` 标记中。
1. `component Z/view/frontend/layout/default.xml`---或者我们不关心组件Z的顺序，或者组件Z可能需要先加载组件A文件。

没有限制---你可以在 `<sequence>`中指定任何有效的组件。

如果在 `<sequence>`中指定了组件， 确保还将其添加到组件的  `composer.json` 文件的`require` 部分中。

{:.bs-callout-info}
在 多个组件中`<sequence>`要谨慎些，因为可能会定义循环的依赖项。 如果这样做，Magento会在检测到循环依赖项时中止安装。



{:.ref-header}
下一步

[禁用/启用组件]({{ page.baseurl }}/extension-dev-guide/build/enable-module.html)
