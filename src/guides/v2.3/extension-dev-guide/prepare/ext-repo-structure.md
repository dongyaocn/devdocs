---
group: php-developer-guide
title: 扩展仓库结构
---

## 扩展仓库结构

对于Magento 2.3模块、主题和语言包扩展仓库，我们推荐五种最佳实践：

*  等级制度扁平化
*  每个仓库一个*扩展类型*（模块、主题或语言包）
*  每个仓库有多个组件
*  每个仓库有一个组件
*  每个模块组件一个功能测试套件

### 等级制度扁平化

仓库结构不在包含 `app/code/<Vendor>/` 目录。

*Before:*

```tree
<extension_repo_root\>
└── app/code/<Vendor>/
    └── <Module1>
```

*After:*

```tree
<extension_repo_root>/
└── <Module1>
```

### 每个仓库一个扩展类型

不能在同一扩展仓库中混合扩展类型（模块、主题和语言包）。每个组件类型都必须有自己的仓库。例如，*你不能这样做*：

```tree
// 不支持此操作
<extension_repo_root>
├── <Module1>
├── <theme1>
└── <language1>
```

### 每个仓库有多个组件

如果扩展很复杂并且需要几个组件，则可以将这些组件保存在同一个仓库中，以使扩展易于打包和维护：

```tree
<extension_repo_root>
├── <Module1>
├── <Module2>
├── <Module1SampleData>
└── <Module2SampleData>
```

您可以对主题和语言包扩展执行相同的操作：

```tree
<extension_repo_root>/
├── <theme1>
└── <theme2>
```
```tree
<extension_repo_root>/
├── <language1>
└── <language2>
```
### 每个仓库有一个组件

如果您的扩展只需要一个组件，那么您的`<component_root>`目录和`<repo_root>`目录将相同，以减少目录结构中不必要的层次结构：

```tree
<MyModule_repo_root>
├── Api
├── Block
├── Controller
├── Console
├── etc
├── Helper
├── i18n
├── Model
├── Plugin
├── Test
├── view
├── composer.json
├── LICENSE.txt
└── ...
```

### 测试套件

函数测试可以添加到扩展的每个模块中的`Test`目录中。
注意：目前，只有单元和MFTF测试可以从`<Module>`目录中运行。

```tree
<extension_repo_root>
├── <Module1>
│   ├── ...
│   ├── Test
│   │   ├── Unit
│   │   ├── Integration
│   │   └── Mftf
│   │       ├── TestSuite
│   │       └── composer.json
│   └── ...
├── <Module2>
├── <Module1SampleData>
└── <Module2SampleData>
```