Magento软件和组件存储库`repo.Magento.com`最近开始要求传输层安全（TLS）1.1或更高版本。

[PCI安全标准委员会](https://en.wikipedia.org/wiki/Payment_Card_Industry_Security_Standards_Council)删除了SSL/TLS 1.0作为[PCI数据安全标准(PCI DSS)](https://www.pcisecuritystandards.org/pci_security) 版本3.1，声明在2016年6月30日之后不再用作安全控制。

有关详细信息，请参阅[从SSL和早期TLS迁移的更改日期](http://blog.pcisecuritystandards.org/migrating-from-ssl-and-early-tls).

### 症状

如果您有早期版本的TLS，您将看到本节中讨论的错误。

#### 下载Magento元包，

如果试图运行`composer create project`以获取Magento元包，将显示以下错误：

```terminal
[Composer\Downloader\TransportException]
The "https://repo.magento.com/packages.json" file could not be downloaded: Failed to enable crypto
failed to open stream: operation failed
```

### 使用Web安装向导

保存身份验证凭据或与Magento Marketplace同步等操作失败，错误如下：

![SSL connect error]({{ site.baseurl }}/common/images/install_ssl-connect-error.png)
