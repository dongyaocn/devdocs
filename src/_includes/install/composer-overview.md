我们使用 [Composer](https://getcomposer.org/){:target="_blank"} 来管理 Magento 组件和依赖。 使用 Composer 获取 Magento 软件 [元包](https://glossary.magento.com/metapackage) 具有以下优点:

-  重用第三方库，而不将它们与源代码捆绑在一起
-  通过使用基于组件的体系结构和健壮的依赖管理减少扩展冲突和兼容性问题
-  遵守 [PHP-Framework Interoperability Group (FIG)](https://www.php-fig.org/) 标准
-  将Magento与其他组件重新打包为开放源码
-  在生产环境中使用Magento软件

{:.bs-callout-warning}
如果要使用Magento Web安装向导升级Magento软件和第三方扩展，必须从我们的元包创建一个Composer项目。
