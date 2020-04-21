### 必需的文件

所有组件都需要以下文件：

*  `registration.php`: 默认情况下，Composer会自动在 `<Magento root dir>/vendor` 目录中安装组件。除此之外，此文件指定生产环境中供应商安装组件的目录。详细信息，查阅 [组件注册]({{ page.baseurl }}/extension-dev-guide/build/component-registration.html).
*  `composer.json`: 指定组件依赖项和其他元数据。了解更多信息，查阅 [Composer 集成]({{ page.baseurl }}/extension-dev-guide/build/composer-integration.html).

每个组件都有一个特定于组件的附加必需文件：

| 组件类型 | 必须的文件 | 描述 |
| --- | --- | --- |
| `magento2-module` | [module.xml]({{page.baseurl}}/architecture/archi_perspectives/components/modules/mod_depend.html#managing-module-dependencies) | 此文件定义有关组件的基本信息，例如组件依赖项和版本号。当执行`bin/magento setup:upgrade`时，Magento使用版本号来确定要更新的架构和数据。 |
| `magento2-theme` | [theme.xml]({{page.baseurl}}/frontend-dev-guide/themes/theme-create.html#fedg_create_theme_how-to_declare) | 描述Magento 主题。文件在`title`节点中指定主题名称, 父主题 (可选), 和在`media/preview_image` 节点指定主题预览图 (可选) 。 |
| `magento2-language` | [language.xml]({{page.baseurl}}/config-guide/cli/config-cli-subcommands-i18n.html#m2devgde-xlate-files) | 声明语言翻译包。 |
