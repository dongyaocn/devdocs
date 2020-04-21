---
group: installation-guide
title: 如何获得Magento软件
landing-page: 安装指南
functional_areas:
  - Install
  - System
  - Setup
---

您是全球24万信任我们电子商务软件的商家之一。我们收集了一些信息，以帮助您开始与Magento和您的Magento安装。

我们这里有一些资源，可以帮助你开始使用未来的电子商务平台——Magento 2。

我们就是这么做的。

## 如何获得Magento软件 {#install-get-software}

在我们的[Magento 2.3产品可用性页面](https://devdocs.magento.com/release/#availability)上查看令人兴奋的新功能和版本的可用性，并了解如何获得它们。

要开始安装，请参考下表

{{site.data.var.ce}} 或 {{site.data.var.ee}}.

<table>
    <tbody>
        <tr>
            <th>用户需求</th>
            <th>描述</th>
            <th>高级安装和升级步骤</th>
            <th>相关链接</th>
        </tr>
    <tr>
        <td><p>易于安装，命令行，有自己的服务器</p></td>
        <td><p>懂一些专业技术，会使用命令行访问Magento服务器。</p>
            <p>允许使用 <a href="{{ page.baseurl }}/install-gde/install/web/install-web.html">Web安装向导</a> 或 <a href="{{ page.baseurl }}/install-gde/install/cli/install-cli.html">命令行</a>安装Magento软件和扩展.</p>
        <p>你<em>不能</em> 使用 Web安装向导来升级Magento 软件和扩展。 你必须使用 <a href="{{ page.baseurl }}/install-gde/install/cli/dev_reinstall.html">Composer</a> 和 the <a href="{{ page.baseurl }}/install-gde/install/cli/install-cli.html">命令行</a>进行升级.</p></td>
        <td><ol><li>下载包含Magento软件的压缩文件。</li>
            <li>将其解压到Magento服务器上，或者要求网络管理员这样做。</li>
            <li>使用Web安装向导或命令行安装Magento软件。</li>
            <li>使用Composer和命令行升级Magento应用程序和扩展。</li></ol>
        </td>
        <td><p><a href="{{ page.baseurl }}/install-gde/prereq/zip_install.html">Easy installation (拥有自己的服务器)</a></p></td>
    </tr>
    <tr>
        <td><p>整合, 包管理器</p></td>
        <td><p>想要完全控制安装的所有组件，可以访问Magento服务器，技术含量高，可以将{{site.data.var.ce}}与其他组件重新打包。</p>
        <p>使您能够使用 <a href="{{ page.baseurl }}/install-gde/install/web/install-web.html">Web安装向导</a> 或者 <a href="{{ page.baseurl }}/install-gde/install/cli/install-cli.html">命令行</a>安装Magento软件和扩展。</p>
        <p>您还可以使用 <a href="{{ page.baseurl }}/comp-mgr/bk-compman-upgrade-guide.html">Web安装向导（Web Setup Wizard）</a> 或者 <a href="{{ page.baseurl }}/comp-mgr/cli/cli-upgrade.html">命令行</a>升级Magento应用程序和扩展。</p></td>
        <td><ol><li>创建一个Composer<em>项目</em> ，其中要包含使用的组件列表.</li>
            <li>使用 Composer 更新包依赖项; 使用 <code>composer create-project</code> 获取 Magento metapackage.</li>
            <li>使用命令行或安装向导安装Magento软件。</li>
        <li>使用Web安装向导或命令行升级Magento应用程序和扩展。</li></ol></td>
        <td><p><a href="{{ page.baseurl }}/install-gde/composer.html">获取 Magento metapackage</a></p></td>
    </tr>
    <tr>
        <td><p>开发人员的贡献</p></td>
        <td><p>为Magento代码库、文件错误和自定义Magento软件作出贡献。高技术，有自己的Magento开发服务器，懂Composer和GitHub。</p>
            <p>能够使用 <a href="{{ page.baseurl }}/install-gde/install/web/install-web.html">Web安装向导（Web Setup Wizard）</a> 或 <a href="{{ page.baseurl }}/install-gde/install/cli/install-cli.html">命令行</a>其中之一安装Magento软件和扩展</p>
            <p>您 <em>不能</em> 在生产环境中使用Magento。</p>
      <p>您 <em>不能</em> 使用 Web Setup Wizard 来升级Magento软件和扩展. 您必须使用 <a href="{{ page.baseurl }}/install-gde/install/cli/dev_options.html">Composer 和 Git 命令行</a>进行升级.</p></td>
        <td><ol><li>在 GitHub 仓库克隆 Magento 2.</li>
            <li>使用 Composer 更新包依赖项</li>
            <li>使用命令行或安装向导安装Magento软件。</li>
            <li>使用Composer和GitHub命令升级Magento软件。</li>
            <li>在目录<code>app/code</code> 下编写自定义代码.</li></ol></td>
        <td><p><a href="{{ page.baseurl }}/install-gde/prereq/dev_install.html">克隆 Magento 仓库</a></p></td>
    </tr>
    </tbody>
</table>
## 有用的信息

在您安装过程中的任何时候，利用我们的[安装快速参考(教程)]或[安装路线图(参考)]。它们非常容易使用;本教程将带您完成一个示例安装。路线图提供了整个指南中常见任务的链接。

使用页面左侧的链接在安装的每个部分中导航主题。

## 需要服务器权限

UNIX系统需要 `root` 权限来安装和配置软件，如web服务器、PHP等。如果你需要安装这个软件，请确保你有 `root` 访问权限.

你不应该以 `root` 用户的身份在Web服务器docroot中安装Magento软件，因为Web服务器可能无法与这些文件进行交互.

您还需要`root`权限来创建[Magento文件系统所有者]并将该所有者添加到web服务器的用户组中。您将使用[Magento文件系统所有者](https://glossary.magento.com/magento-file-system-owner)从命令行运行任何命令，并设置Magento cron作业，它为您安排任务。

<!-- 链接定义 -->

[安装快速参考(教程)]: {{ page.baseurl }}/install-gde/install-quick-ref.html
[安装路线图(参考)]: {{ page.baseurl }}/install-gde/install-roadmap_part1.html
[Magento文件系统所有者]: {{ page.baseurl }}/install-gde/prereq/file-sys-perms-over.html