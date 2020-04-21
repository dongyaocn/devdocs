下表讨论了Magento Marketplace支持的组件类型。下表中的composer`type`列指定必须添加到该类型组件的`composer.json`中的`type`字段的值。

|名称|composer.json 类型|描述|
|--- |--- |:-- |
|元包|metapackage|从技术上来说，这是一个Composer包类型，而不是Magento组件类型。 元包仅由特定的组件及其依赖项列表组成的 `composer.json` 文件。例如， {{site.data.var.ce}} 和 {{site.data.var.ee}} 都是元包.|
|模块|magento2-module|修改Magento应用程序行为的代码。您可以将单个模块上载到Magento Marketplace，或者您的模块可以依赖于某些父包。|
|主题|magento2-theme|修改店面或者Magento管理后台的外观视觉.|
|语言包|magento2-language|Translations for the storefront or Admin.|
|库|magento2-library|支持位于`lib/internal`而不是`vendor`目录中的库。|
|组件|magento2-component|由必须位于根目录（index.php、.htaccess、etc）中的文件组成的包。目前还包括`dev/tests`和`setup`。|

