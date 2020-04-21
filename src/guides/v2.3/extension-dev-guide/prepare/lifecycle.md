---
group: php-developer-guide
title: 扩展生命周期
menu_title: 扩展生命周期
---

本主题描述模块的生命周期，以及如何在初始化、升级或卸载模块时创建执行代码的类。
这些可执行类可以执行设置数据库、更新数据和清理数据的任务。

*注意：*主题和语言包扩展不需要初始化或卸载任务，因为它们不安装数据库架构或更新数据。

## 生命周期指南

在开发可执行类以使其在特定生命周期阶段运行时，请遵循以下准则：

*  将可执行类放在模块根目录中的`Setup`目录中。
*  为类(Class)的目标生命周期阶段使用特定的文件和类名。
*  为类(Class)的目标阶段实现特定的类接口和函数。
*  更改模块版本时，请遵循Magento的[版本控制策略]。

## Schema 初始化阶段

Schema初始化阶段是指安装、重新安装或升级模块时Magento运行的第一组进程。

### Schema 安装

在模块的初始安装期间，Magento执行schema安装类。
如果在`setup_module`表中找到模块的`schema_version`，则Magento将跳过此阶段并进入[schema upgrade]阶段。

| **类名:** | `InstallSchema`            |
| **接口:**  | [`InstallSchemaInterface`] |
| **方法:**     | `install()`                |

**示例:** InstallSchema.php

```php
class VendorName\ModuleName\Setup\InstallSchema implements \Magento\Framework\Setup\InstallSchemaInterface
{
    /**
     * {@inheritdoc}
     */
    public function install(SchemaSetupInterface $setup, ModuleContextInterface $context)
    {
        //Install schema logic
    }
}
```

### Schema 升级 {#schema-upgrade}

当检测到早期安装时，Magento将执行模块的schema upgrade类。
此类的目的是更新数据库结构或应用修补程序。

| **类名** | `UpgradeSchema`            |
| **接口**  | [`UpgradeSchemaInterface`] |
| **方法**     | `upgrade()`                |

**示例:** UpgradeSchema.php

```php
class \VendorName\ModuleName\Setup\UpgradeSchema implements \Magento\Framework\Setup\UpgradeSchemaInterface
{
    /**
     * {@inheritdoc}
     */
    public function upgrade(SchemaSetupInterface $setup, ModuleContextInterface $context)
    {
        //Upgrade schema logic
    }
}
```

### 重复 schema 事件

Magento在每个schema安装或升级阶段之后执行模块的定期schema事件类。
此类在安装或更新 database schema后对其进行最终修改。

| **类名** | `Recurring`                |
| **接口**  | [`InstallSchemaInterface`] |
| **方法**     | `install()`                |

**Example:** Recurring.php

```php
class \VendorName\ModuleName\Setup\Recurring implements \Magento\Framework\Setup\InstallSchemaInterface
{
    /**
     * {@inheritdoc}
     */
    public function install(SchemaSetupInterface $setup, ModuleContextInterface $context)
    {
        //Recurring schema event logic
    }
}
```

## 数据初始化

在schema初始化过程完成后，Magento将遍历模块的数据初始化阶段。

### 数据安装

除非在数据库中找到现有版本条目，否则在模块的初始安装期间，Magento将执行数据安装类。
此类的目的是用初始数据填充数据库。

| **类名** | `InstallData`            |
| **接口**  | [`InstallDataInterface`] |
| **方法**     | `install()`              |

**示例:** InstallData.php

```php
class \VendorName\ModuleName\Setup\InstallData implements \Magento\Framework\Setup\InstallDataInterface
{
    /**
     * {@inheritdoc}
     */
    public function install(ModuleDataSetupInterface $setup, ModuleContextInterface $context)
    {
        // Data install logic
    }
}
```

### 数据升级

当Magento在`setup_module`表中模块的`data_version`字段中检测到早期版本时，它将执行数据升级类。
此类的目的是修复损坏的数据或在架构更改后填充新的数据字段。

| **类名** | `UpgradeData`            |
| **接口**  | [`UpgradeDataInterface`] |
| **方法**     | `upgrade()`              |

**示例:** UpgradeData.php

```php
class \VendorName\ModuleName\Setup\UpgradeData implements \Magento\Framework\Setup\UpgradeDataInterface
{
    /**
     * {@inheritdoc}
     */
    public function upgrade(ModuleDataSetupInterface $setup, ModuleContextInterface $context)
    {
        // Data upgrade logic
    }
}
```

### Recurring data 事件

Magento在每个数据安装或升级阶段之后执行模块的重复数据事件类。
此类在安装或更新数据后对数据库存储区进行最终修改。

| **类名** | `RecurringData`          |
| **接口**  | [`InstallDataInterface`] |
| **方法**     | `install()`              |

**示例:** RecurringData.php

```php
class \VendorName\ModuleName\Setup\RecurringData implements \Magento\Framework\Setup\InstallDataInterface
{
    /**
     * {@inheritdoc}
     */
    public function install(ModuleDataSetupInterface $setup, ModuleContextInterface $context)
    {
        // Recurring data event logic
    }
}
```

## 数据库接口

需要进行数据库操作时，请使用[`ModuleDataSetupInterface`]。
如果安装或升级逻辑跨越多个类，请将此资源传递给需要修改数据库的其他类。

**示例:** [客户模块的 DefaultCustomerGroupsAndAttributes.php]

```php
class DefaultCustomerGroupsAndAttributes implements DataPatchInterface, PatchVersionInterface
{
    /**
     * @var CustomerSetupFactory
     */
    private $customerSetupFactory;
    /**
     * @var ModuleDataSetupInterface
     */
    private $moduleDataSetup;
    /**
     * DefaultCustomerGroupsAndAttributes constructor.
     * @param CustomerSetupFactory $customerSetupFactory
     * @param ModuleDataSetupInterface $moduleDataSetup
     */
    public function __construct(
        CustomerSetupFactory $customerSetupFactory,
        \Magento\Framework\Setup\ModuleDataSetupInterface $moduleDataSetup
    ) {
        $this->customerSetupFactory = $customerSetupFactory;
        $this->moduleDataSetup = $moduleDataSetup;
    }
    /**
     * {@inheritdoc}
     * @SuppressWarnings(PHPMD.ExcessiveMethodLength)
     */
    public function apply()
    {
        /** @var CustomerSetup $customerSetup */
        $customerSetup = $this->customerSetupFactory->create(['setup' => $this->moduleDataSetup]);
        ...
        $customerSetup->installEntities();
        $customerSetup->installCustomerForms();
        $disableAGCAttribute = $customerSetup->getEavConfig()->getAttribute('customer', 'disable_auto_group_change');
        ...
        $migrationSetup = $this->moduleDataSetup->createMigrationSetup();
        $migrationSetup->appendClassAliasReplace(
            'customer_eav_attribute',
            'data_model',
            Migration::ENTITY_TYPE_MODEL,
            Migration::FIELD_CONTENT_TYPE_PLAIN,
            ['attribute_id']
        );
        $migrationSetup->doUpdateClassAliases();
    }
    ...
}
```

## 模块版本

使用[`ModuleContextInterface`]获取当前模块版本并根据版本执行逻辑。

**示例:** [用户模块 UpgradeData.php]

```php
namespace Magento\User\Setup;

use Magento\Framework\Encryption\Encryptor;
use Magento\Framework\Setup\ModuleContextInterface;
use Magento\Framework\Setup\ModuleDataSetupInterface;
use Magento\Framework\Setup\UpgradeDataInterface;

class UpgradeData implements UpgradeDataInterface
{
    /**
     * @inheritdoc
     */
    public function upgrade(ModuleDataSetupInterface $setup, ModuleContextInterface $context)
    {
        $setup->startSetup();
        if (version_compare($context->getVersion(), '2.0.1', '<')) {
            $this->upgradeHash($setup);
        }
        $setup->endSetup();
    }

    ...

}
```

## 卸载事件

使用[Component Manager]或使用以下命令行命令卸载模块时，Magento将执行卸载事件类：

```bash
bin/magento module:uninstall --remove-data <module_name>
```

在此阶段，您的模块应通过删除表、删除数据或还原数据来删除数据库中存在的所有跟踪。

| **类名** | `Uninstall`            |
| **接口**  | [`UninstallInterface`] |
| **方法**     | `uninstall()`          |

**示例:** Uninstall.php

```php
class \VendorName\ModuleName\Setup\Uninstall implements \Magento\Framework\Setup\UninstallInterface
{
    /**
     * {@inheritdoc}
     */
    public function uninstall(SchemaSetupInterface $setup, ModuleContextInterface $context)
    {
        //Uninstall logic
    }
}
```

### 禁用模块

禁用的模块仍可以执行其卸载事件。
但是，特定于模块的配置（如依赖注入和事件/观察者配置）将不可用，并将导致问题。
通过在卸载事件类中不包含依赖项来避免这种情况

**相关主题:**

*  Magento的[版本控制策略]

[versioning policy]: {{ page.baseurl }}/extension-dev-guide/versioning/

[schema upgrade]: #schema-upgrade

[`InstallSchemaInterface`]: {{ site.mage2bloburl }}/{{page.guide_version}}/lib/internal/Magento/Framework/Setup/InstallSchemaInterface.php
[`UpgradeSchemaInterface`]: {{ site.mage2bloburl }}/{{page.guide_version}}/lib/internal/Magento/Framework/Setup/UpgradeSchemaInterface.php
[`InstallDataInterface`]: {{ site.mage2bloburl }}/{{page.guide_version}}/lib/internal/Magento/Framework/Setup/InstallDataInterface.php
[`UpgradeDataInterface`]: {{ site.mage2bloburl }}/{{page.guide_version}}/lib/internal/Magento/Framework/Setup/UpgradeDataInterface.php
[`ModuleDataSetupInterface`]: {{ site.mage2bloburl }}/{{page.guide_version}}/lib/internal/Magento/Framework/Setup/ModuleDataSetupInterface.php
[Customer module's DefaultCustomerGroupsAndAttributes.php]: {{ site.mage2bloburl }}/{{page.guide_version}}/app/code/Magento/Customer/Setup/Patch/Data/DefaultCustomerGroupsAndAttributes.php
[`ModuleContextInterface`]: {{ site.mage2bloburl }}/{{page.guide_version}}/lib/internal/Magento/Framework/Setup/ModuleContextInterface.php
[Component Manager]: {{ page.baseurl }}/comp-mgr/extens-man/extensman-uninst-final.html
[`UninstallInterface`]: {{ site.mage2bloburl }}/{{page.guide_version}}/lib/internal/Magento/Framework/Setup/UninstallInterface.php