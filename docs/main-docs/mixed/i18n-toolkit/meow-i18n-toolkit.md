---
sidebar_position: 2
description: i18n toolkit AST 拆分合并工具
---

# Meow i18n toolkit

针对 docusaurus 设计的持续本地化工具。

## 初始化工具 venv

TODO

## 构建中间格式

```shell
<path_to_venv>/python3 <path_to_tool>/src/build_middleware.py
```

这会在项目目录中创建缓存文件以及toml格式的中间文件。

## 构建翻译后的 mdx 文件

当翻译完成后使用以下命令构建翻译文件

```shell
<path_to_venv>/python3 <path_to_tool>/src/sync_to_i18n.py
```

## TODO

- [ ] 增加启动参数
- [ ] 增加初始化 venv 工具
