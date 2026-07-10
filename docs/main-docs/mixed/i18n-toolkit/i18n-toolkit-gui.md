---
sidebar_position: 2
description: i18n toolkit GUI
---

# Neko i18n toolkit GUI

:::info

[Neko-vecter/i18n-toolkit-gui](https://github.com/Neko-vecter/i18n-toolkit-gui)

:::

## 在开始之前

i18n toolkit GUI 为翻译项目提供了可视化的编辑和管理界面，适合查看原文 / 编辑译文 / 切换语言 / 管理翻译文件。

i18n toolkit GUI 可以用于以下两类项目：

- 使用 Docusaurus 框架搭建的文档项目
- 单独的 i18n-project 翻译项目

## Docusaurus

如果使用 Docusaurus 框架。你可以使用 GUI 直接生成对应的翻译中间文件在i18n目录中。这个文件会把原始的文档拆分成一个一个的小段落。当原始文档段落修改或者添加之后。只需要点击rebuild。并且重新翻译修改过的部分。这样可以大幅减少原始文档更新。但是翻译没有更新的问题。

:::note

rebuild workflow 中默认会自动引用原始文档的图片。

:::

## i18n-project

当前版本没有完善转换目录或者打开目录为 i18n-project。可以通过以下方法手动创建。

### 美好的项目从新建文件夹开始

首先在项目目录下新建需要翻译的文件夹。比如 `en`。

并且创建 `i18n-project.toml` 的文件。

### toml 文件定义

:::info

- `[metadata]` 暂时无定义实际内容

:::

```toml
[metadata]

[[block]] 
key = "sha256 for origin"
origin = '''
This is the original source text that needs translation.
It can span multiple lines comfortably.
'''
translate = '''
This is the translated text in the target language.
The extension makes these blocks easy to distinguish.
'''
```

### 目录结构

```
<lang_1>
    folder
        file_1.toml
    file_2.toml
<lang_2>
    folder
        file_1.toml
    file_2.toml
i18n-project.toml
```
