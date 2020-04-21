要在安装Magento软件之前设置权限，请执行以下操作：

1. 登录到您的Magento服务器。
1. 使用共享宿主提供程序提供的文件管理器应用程序验证是否在以下目录上设置了写入权限：

   *  `vendor` (Composer 或者压缩档案安装)
   *  `app/etc`
   *  `pub/static`
   *  `var`
   *  `generated`
   *  任何其他静态资源

1. 如果具有命令行访问权限，请按所示顺序输入以下命令：

   ```bash
   cd <magento_root>
   ```

   ```bash
   find var generated vendor pub/static pub/media app/etc -type f -exec chmod u+w {} +
   ```

   ```bash
   find var generated vendor pub/static pub/media app/etc -type d -exec chmod u+w {} +
   ```

   ```bash
   chmod u+x bin/magento
   ```

要选择在一行中输入所有命令，请在假定Magento安装在 `/var/www/html/magento2`:

```bash
cd /var/www/html/magento2 && find var generated vendor pub/static pub/media app/etc -type f -exec chmod u+w {} + && find var generated vendor pub/static pub/media app/etc -type d -exec chmod u+w {} + && chmod u+x bin/magento
```

1. 如果您还没有这样做，请使用以下方法之一获取Magento软件：

   *  [压缩存档]({{ page.baseurl }}/install-gde/prereq/zip_install.html)
   *  [Composer 元包]({{ page.baseurl }}/install-gde/composer.html)
   *  [克隆仓库 (仅贡献开发者)]({{ page.baseurl }}/install-gde/prereq/dev_install.html)

1. 设置文件系统所有权和权限后，请继续执行下列任一操作:

   *  [命令行安装]({{ page.baseurl }}/install-gde/install/cli/install-cli.html)
   *  [安装向导]({{ page.baseurl }}/install-gde/install/web/install-web.html)

{:.bs-callout-info}
要在安装Magento软件后进一步限制权限，请[配置Magento umask]({{ page.baseurl }}/install-gde/install/post-install-umask.html).

*[贡献开发者]: 为Magento 2 CE 代码库贡献代码的开发人员

