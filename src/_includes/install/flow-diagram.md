![How Magento installation works]({{ site.baseurl }}/common/images/install_diagram.png){:width="1100px"}

上图显示了以下内容:

1. 设置服务器环境。

   安装必备软件，包括PHP、Apache和MySQL。查阅[系统要求]({{ page.baseurl }}/install-gde/system-requirements-tech.html) 。

1. 获取 Magento 软件.

   *  为简单起见，获取一个 {{site.data.var.ce}} 或 {{site.data.var.ee}} [压缩文件包]({{ page.baseurl }}/install-gde/prereq/zip_install.html)，将其解压缩到Magento服务器上，然后开始安装。

   *  如果你更专业，并且熟悉 Composer，那就选择一个 {{site.data.var.ce}} 或 {{site.data.var.ee}} {% if page.guide_version == "2.0" %} [metapackage]({{page.baseurl}}/install-gde/prereq/integrator_install.html) {% else %} [metapackage]({{page.baseurl}}/install-gde/composer.html). {% endif %}

   *  如果你想为 {{site.data.var.ce}} 代码库做贡献或者定制Magento应用程序， [克隆]({{ page.baseurl }}/install-gde/prereq/dev_install.html) Magento 2 GitHub 仓库. (这种方法需要熟悉GitHub和Composer。)

   {:.bs-callout-info}
   要使用 Web Setup Wizard（Web安装向导） 安装或升级Magento软件，或者管理从 Magento Marketplace（Magento市场）中获得的扩展，那就必须用Magento程序压缩包或者 Composer metapackage。如果从 GitHub 仓库克隆， 你便不能使用 Web Setup Wizard 来升级Magento软件和扩展。必须使用 [Composer and Git 命令行]({{ page.baseurl }}/install-gde/install/cli/dev_options.html)进行升级。

1. 使用Web安装向导或命令行安装Magento软件。

   为了简单起见，图中只显示了Web设置向导。

   在每个步骤中，Web安装向导将验证您输入的信息。如上图所示，如果验证失败，您必须在继续之前手动修复问题。

   如果由于先决条件软件没有正确设置而导致步骤失败，请查看我们的 [先决条件]({{ page.baseurl }}/install-gde/prereq/prereq-overview.html)。

1. 通过查看您的店面和Magento管理员来验证安装。
