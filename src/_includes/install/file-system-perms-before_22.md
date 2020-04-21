## 设置预安装文件系统的所有权和权限{#perms-over}

本主题讨论如何在安装Magento软件之前设置web服务器组的读写权限。这是必需的，以便安装向导或命令行可以将文件写入Magento文件系统。

您使用的过程不同，具体取决于您是使用[共享主机](#perms-shared)并有一个用户，还是使用[专用服务器](#perms-private)并有两个用户。

{:.bs-callout-info}
如果您使用的是早于*2.0.6的Magento版本*，请参见[附录---Magento文件系统所有权和附录（旧版)][{{page.baseurl }}/install-gde/install/legacy-fil-system-perms.html]。

## 设置共享宿主的权限（一个用户） {#perms-shared}

本节讨论如果您以同样运行web服务器的用户身份登录到Magento服务器，如何设置安装前权限。这种类型的设置在共享宿主环境中很常见。

{% collapsible 为单用户系统设置所有权和权限: %}
{% include install/file-system-perms-oneuser_22.md %}
{% endcollapsible %}

## 为两个用户设置所有权和权限 {#perms-private}

本节讨论如何为您自己的服务器或专用主机设置设置所有权和权限。在这种类型的设置中，您通常*无法*以web服务器用户的身份登录或切换到web服务器用户。您通常以一个用户的身份登录，并以其他用户的身份运行web服务器。

{% collapsible 设置双用户系统的所有权和权限: %}
{% include install/file-system-perms-twouser_22.md %}
{% endcollapsible %}

## 切换到Magento文件系统所有者 {#install-update-depend-user-switch}

执行完本主题中的其他任务后，输入以下命令之一切换到该用户：

*  Ubuntu: `su <username>`
*  CentOS: `su - <username>`

例如，

```bash
su magento_user
```
