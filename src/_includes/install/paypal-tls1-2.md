## PayPal对TLS 1.2的要求

PayPal最近宣布，他们将要求传输层安全（TLS）1.2版在实时环境中处理支付。（PayPal已经在沙盒中要求TLS 1.2。）
更多信息：

*  [详细信息（PayPal安全公告）](https://www.paypal.com/uk/webapps/mpp/ssl-security-update)
*  [2016年6月PayPal在线支付切换（PayPal技术博客）](https://medium.com/paypal-engineering/security-related-changes-required-to-avoid-service-disruption-82caf7778328#0422)

### 症状

根据PayPal的说法，问题的症状包括错误日志中的以下消息：

```text
*Unknown SSL protocol error* in connection to api-3t.sandbox.paypal.com:-9824
```

or

```text
140062736746144:error:1408F10B:SSL routines:SSL3_GET_RECORD:wrong version number:s3_pkt.c:337:

... (more messages) ...

New, (NONE), Cipher is (NONE)
Secure Renegotiation IS NOT supported*
Compression: NONE
Expansion: NONE
SSL-Session:
Protocol: SSLv3*

... (more messages) ...
```

### 说明

问题的根源是您的[`libcurl`](https://curl.haxx.se/libcurl/c/CURLOPT_SSLVERSION.html)版本。`libcurl` 7.34之前的版本默认使用TLS 1.1或更早版本。
要确定正在运行的 `libcurl` 的版本，请在处理PayPal事务的服务器上输入以下命令：

```bash
curl --version
```

如果版本早于7.34，请继续下一节。如果您已经运行7.34或更高版本，则无需执行任何操作。

### 解决方案

问题的根源是，[`libcurl`](https://curl.haxx.se/libcurl/c/CURLOPT_SSLVERSION.html)与CentOS 6.6和更早版本一起打包的库默认使用TLS 1.1或更早版本。
要确定服务器运行的CentOS版本，请输入以下命令：

```bash
cat /etc/*release*
```

如果您已经在运行CentOS 6.8或更高版本，则无需执行任何操作。根据[CentOS 6.8变更日志](https://wiki.CentOS.org/Manuals/ReleaseNotes/CentOS6.8)，“现在各种应用程序都支持TLS 1.2，即OpenLDAP、yum、stunnel、vsftpd、git、postfix和其他。此外，TLS 1.2在默认情况下已在各种软件包中启用”。
（CentOS 7有一个新版本的`libcurl`，默认为TLS 1.2。）
您有以下选项：

*  （推荐）将Magento服务器升级到CentOS 6.8或更高版本。
    它推荐的存储库支持当前版本的带有`libcurl`的TLS。使用CentOS 6.8或更高版本是继续操作商店和接受PayPal的最安全方法。
    CentOS 6.8的`libcurl`版本默认为TLS 1.2。
    
*  （不太安全，*不推荐*）。使用非推荐的第三方存储库在CentOS 6上升级至`libcurl`7.34或更高版本。
    一种可能的解决方案是使用[serverfault](http://serverfault.com/questions/321321/upgrade-curl-to-latest-on-centos)上的信息。
    
    {:.bs-callout-info}
    不推荐从存储库安装软件，这可能会更改其他系统包并有可能导致问题产生。我们强烈建议您在开发环境中升级`libcurl`，并在将其投入生产之前*彻底测试*您使用的所有支付处理器以及任何其他关键软件。