要有选择地在一行中输入所有命令，请假定Magento安装在`/var/www/html/magento2`中，并且web服务器组名为`apache`：

```bash
cd /var/www/html/magento2 && find var generated vendor pub/static pub/media app/etc -type f -exec chmod g+w {} + && find var generated vendor pub/static pub/media app/etc -type d -exec chmod g+ws {} + && chown -R :apache . && chmod u+x bin/magento
```

如果文件系统权限设置不正确且Magento文件系统所有者无法更改，则可以以具有`root`权限的用户身份输入命令：

```bash
cd /var/www/html/magento2 && sudo find var generated vendor pub/static pub/media app/etc -type f -exec chmod g+w {} + && sudo find var generated vendor pub/static pub/media app/etc -type d -exec chmod g+ws {} + && sudo chown -R :apache . && sudo chmod u+x bin/magento
```

