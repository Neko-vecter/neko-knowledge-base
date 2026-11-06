---
sidebar_position: 2
description: i18n toolkit AST CLI Command
---

# Neko i18n toolkit CLI

:::info

[Neko-vecter/neko-i18n-toolkit](https://github.com/Neko-vecter/neko-i18n-toolkit)

[npm package @neko_vecter/i18n-toolkit](https://www.npmjs.com/package/@neko_vecter/i18n-toolkit)

:::

## Add Package

```shell
pnpm add -D @neko_vecter/i18n-toolkit
```

## CLI

### 构建 middleware 文件

```shell
pnpm i18n-toolkit extract --lang <lang> -i docs/<path_to_file_1> docs/<path_to_file_2>
```

### 构建 mdx 文件

```shell
pnpm i18n-toolkit build --lang <lang> -i docs/<path_to_file_1> docs/<path_to_file_2>
```

### Sync

`sync` command 会先 `extract` 然后 `build` 文件

```shell
pnpm i18n-toolkit sync --lang <lang> -i docs/<path_to_file_1> docs/<path_to_file_2>
```
