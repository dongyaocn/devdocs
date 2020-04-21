### 语言包文件结构

三种语言包的典型目录结构如下：

```tree
├── de_DE
│   ├── composer.json
│   ├── language.xml
│   ├── LICENSE_AFL.txt
│   ├── LICENSE.txt
│   └── registration.php
├── en_US
│   ├── composer.json
│   ├── language.xml
│   ├── LICENSE_AFL.txt
│   ├── LICENSE.txt
│   └── registration.php
├── pt_BR
│   ├── composer.json
│   ├── language.xml
│   ├── LICENSE_AFL.txt
│   ├── LICENSE.txt
│   └── registration.php
```

语言包的唯一需要是顶级目录。虽然不是必需的，但我们建议目录名与 [ISO](http://www.iso.org/iso/home/standards/language_codes.htm) 代码匹配以标识区域设置。



有关语言包的详细信息，请参见 [翻译词典和语言包]({{ page.baseurl }}/config-guide/cli/config-cli-subcommands-i18n.html).