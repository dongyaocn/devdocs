---
group: php-developer-guide
subgroup: 03_Build
title: 启用或禁用组件
menu_title: 启用或禁用组件
menu_order: 8000
---

构建组件并准备在Magento环境中启用它之后，请执行以下操作：

1. 在 System->Cache Management`下 禁用 [缓存](https://glossary.magento.com/cache)
1. 在命令行中输入以下命令：

   ```bash
   bin/magento module:enable --clear-static-content Component_Name
   ```

   ```bash
   bin/magento setup:upgrade
   ```

   ```bash
   bin/magento cache:clean
   ```

   其中 `Component_Name` 是要启用的组件的名称。

1. 在 **System** > **Tools** > **Web Setup Wizard** > **Module Manager** 检查组件是否存在。

## 操作顺序

 `setup:upgrade` 一般的操作顺序：

1. **架构 安装/升级.**
1. **架构 升级后**— 处理任何其他更新。这些定期升级是独立进行的，与架构的任何更改无关。
1. **数据 安装/升级** — 安装数据。来自 `setup/InstallData.php`.

## 禁用组件

要禁用组件，请在命令行中输入以下命令：

```bash
bin/magento module:disable --clear-static-content Component_Name
```

有关启用和禁用组件的详细信息，请参见 [启用或禁用模块]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-enable.html#instgde-cli-subcommands-enable-disable).
