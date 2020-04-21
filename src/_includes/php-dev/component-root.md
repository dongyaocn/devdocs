### 根目录位置

组件的根目录是该组件的顶级目录，其文件夹和文件位于该目录下。根据Magento开发环境的安装方式，组件的根目录可以位于两个位置：

*  `<Magento install directory>/app`: 这是组件开发的*推荐*位置。您可以通过[克隆Magento 2 GitHub仓库]({{ page.baseurl }}/install-gde/prereq/dev_install.html)轻松地设置此类环境。

   *  对于模块开发，使用 `app/code`.
   *  对于店铺主题，使用 `app/design/frontend`.
   *  对于管理后台，使用 `app/design/adminhtml`.
   *  对于语言包，使用 `app/i18n`.

*  `<Magento install directory>/vendor`: 对于使用 {% if page.guide_version == "2.0" %} [`composer create-project`]({{page.baseurl}}/install-gde/prereq/integrator_install.html) {% else %} [`composer create-project`]({{page.baseurl}}/install-gde/composer.html). {% endif %}命令安装的Magento 2 元包(下载 CE 或者 EE 代码)的安装，您将找到此位置。  或者是提取了 [Magento2程序压缩文档]({{ page.baseurl }}/install-gde/prereq/zip_install.html) 安装的Magento。

   任何第三方组件（以及Magento应用程序本身）都被下载并存储在 `<Magento install directory>/vendor` 目录。如果你使用 [Git](https://git-scm.com/docs) 管理你的项目，此目录通常添加到 `<Magento install directory>/.gitignore` 文件中。 因此，我们建议您在 `<Magento install directory>/app/code`，不推荐在 `<Magento install directory>/vendor`.
