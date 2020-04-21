按所示顺序完成以下任务：

*  [关于共享组](#mage-owner-about-group)
*  [步骤1：创建Magento文件系统所有者并给用户一个强密码](#mage-owner-create-user)
*  [步骤2:查找web服务器组](#install-update-depend-user-findgroup)
*  [步骤3：将Magento文件系统所有者放入web服务器的组中](#install-update-depend-user-add2group)
*  [步骤4：获取Magento软件](#perms-get-software)
*  [步骤5:设置共享组的所有权和权限](#perms-set-two-users)

### 关于共享组 {#mage-owner-about-group}

若要使web服务器能够在Magento文件系统中写入文件和目录，但同时维护Magento文件系统所有者的*所有权*，两个用户必须位于同一组中。这是必要的，这样两个用户都可以共享对Magento文件的访问权限（包括使用Magento管理或其他基于web的实用程序创建的文件）。

本节讨论如何创建新的Magento文件系统所有者并将该用户放入web服务器的组中。如果愿意，可以使用现有用户帐户；出于安全原因，我们建议用户使用强密码。

{:.bs-callout-info}
如果计划使用现有用户帐户，请跳到 [步骤2](#install-update-depend-user-findgroup) 。

### 步骤1：创建Magento文件系统所有者并给用户一个强密码 {#mage-owner-create-user}

本节讨论如何创建Magento文件系统所有者。（Magento文件系统所有者是*命令行用户*的另一个术语）

要在CentOS或Ubuntu上创建用户，请以具有`root`权限的用户身份输入以下命令：

```bash
adduser <username>
```

要向用户提供密码，请以具有“root”权限的用户身份输入以下命令：

```bash
passwd <username>
```

按照屏幕上的提示为用户创建密码。

{:.bs-callout-warning}
如果您在Magento服务器上没有`root`权限，则可以使用其他本地用户帐户。确保用户具有强密码，然后继续执行[将Magento文件系统所有者放入web服务器组](#install-update-depend-user-add2group)。

例如，要创建名为`magento_user`的用户并为该用户提供密码，请输入：

```bash
sudo adduser magento_user
```

```bash
sudo passwd magento_user
```

{:.bs-callout-warning}
因为创建此用户的目的是提供附加的安全性，所以请确保创建一个 [强密码](https://en.wikipedia.org/wiki/Password_strength).

### Step 2: 查找web服务器用户组 {#install-update-depend-user-findgroup}

要查找web服务器用户组，请执行以下操作：

*  CentOS:

   ```bash
   grep -E -i '^user|^group' /etc/httpd/conf/httpd.conf
   ```

   or

   ```bash
   grep -Ei '^user|^group' /etc/httpd/conf/httpd.conf
   
   # 通常，用户名和组名都是 `apache`.
   ```

*  Ubuntu: `ps aux | grep apache` 找到apache用户，然后 `groups <apache user>` 找到组。通常，用户名和组名都是 `www-data`。

### 步骤3：将Magento文件系统所有者放入web服务器的组中 {#install-update-depend-user-add2group}

要将Magento文件系统所有者放入web服务器的主组（假定CentOS和Ubuntu的典型Apache组名），请以具有`root`权限的用户身份输入以下命令：

*  CentOS: `usermod -a -G apache <username>`
*  Ubuntu: `usermod -a -G www-data <username>`

{:.bs-callout-info}
`-a -G`选项很重要，因为它们将`apache` 或`www-data`作为_辅助组_添加到用户帐户中，从而保留用户的主组。将_辅助组_添加到用户帐户有助于[限制文件所有权和权限](#perms-set-two-users) ，以确保共享组的成员只能访问某些文件。

例如，要将用户`magento_user`添加到CentOS上的`apache`主组，请执行以下操作：

```bash
sudo usermod -a -G apache magento_user
```

要确认Magento用户是web服务器组的成员，请输入以下命令：

```bash
groups magento_user
```

下面的示例结果显示了用户的主要（`magento`）组和次要（`apache`）组。

```bash
magento_user : magento_user apache
```

{:.bs-callout-info}
通常，用户名和主组名是相同的。

要完成此任务，请重新启动web服务器：

*  Ubuntu: `service apache2 restart`
*  CentOS: `service httpd restart`

### 步骤4：获取Magento软件 {#perms-get-software}

如果您还没有这样做，请使用以下方法之一获取Magento软件：

*  [压缩文档]({{ page.baseurl }}/install-gde/prereq/zip_install.html)
*  [Composer 元包]({{ page.baseurl }}/install-gde/composer.html)
*  [克隆仓库 (仅贡献开发者)]({{ page.baseurl }}/install-gde/prereq/dev_install.html)

### 步骤5:设置共享组的所有权和权限  {#perms-set-two-users}

要在安装Magento软件之前设置所有权和权限，请执行以下操作：

1. 以Magento文件系统所有者的身份登录或切换到Magento服务器。
1. 按所示顺序输入以下命令：

   ```bash
   cd <magento_root>
   ```

   ```bash
   find var generated vendor pub/static pub/media app/etc -type f -exec chmod g+w {} +
   ```

   ```bash
   find var generated vendor pub/static pub/media app/etc -type d -exec chmod g+ws {} +
   ```

   ```bash
   chown -R :<web server group> .
   ```

   ```bash
   chmod u+x bin/magento
   ```

{% include install/file-system-perms-twouser_cmds-only_22.md %}

###下一步

设置文件系统所有权和权限后，请继续执行下列任一操作：

*  [命令行安装]({{ page.baseurl }}/install-gde/install/cli/install-cli.html)
*  [安装向导]({{ page.baseurl }}/install-gde/install/web/install-web.html)
