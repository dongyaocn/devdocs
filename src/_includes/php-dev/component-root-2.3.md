### 根目录位置

组件的根目录与组件的名称匹配，并包含其所有子目录和文件。根据安装Magento的方式，可以将组件的根目录放在以下两个位置之一：

*  `<Magento install directory>/app`: 这是组件开发的*推荐*位置。您可以通过[克隆Magento 2 GitHub仓库]({{ page.baseurl }}/install-gde/prereq/dev_install.html)轻松地设置此类环境

   *  对于模块开发，使用 `app/code`.
   *  对于店铺主题，使用 `app/design/frontend`.
   *  对于管理后台，使用 `app/design/adminhtml`.
   *  对于语言包，使用 `app/i18n`.

*  `<Magento install directory>/vendor`: 对于使用 [`composer create-project`]({{page.baseurl}}/install-gde/composer.html) 安装的Magento 2 元包(下载 CE 或者 EE 代码)的安装，您将找到此位置。 如果您通过提取[Magento 2程序压缩文档]({{page.baseurl}}/install-gde/prereq/zip_install.html)安装的Magento，也会找到这个位置。

   Magento 在 `<Magento install directory>/vendor` 目录中安装第三方组件。但我们建议将组件添加到`<Magento install directory>/app/code` 目录。如果将组件添加到 `<Magento install directory>/vendor` 目录， [Git](https://git-scm.com/docs) 将忽略它，因为Magento将 `vendor` 目录添加到了 `<Magento install directory>/.gitignore` 文件。
