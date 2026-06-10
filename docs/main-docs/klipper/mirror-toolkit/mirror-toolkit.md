---
sidebar_position: 10
description: Moonraker Mirror Toolkit
---

# Moonraker Mirror Toolkit

:::info

[Neko-vecter/moonraker-mirror-toolkit](https://github.com/Neko-vecter/moonraker-mirror-toolkit)

:::

## 什么是 Moonraker Mirror Toolkit

Moonraker Mirror Toolkit 是一个基于 tunasync 框架构建的本地镜像服务器工具，主要用于为 Moonraker 与 Klipper 生态提供本地 Mirror 服务。

可以镜像的内容包括:

- Moonraker
- Klipper
- Mainsail
- Fluidd

在多台打印机同时更新时，设备通常会直接访问 GitHub 或其它远端仓库。这会带来几个比较常见的问题:

- GitHub API Rate Limit
- 更新速度缓慢
- 网络超时
- 重复下载占用大量带宽
- 批量更新时容易失败

以上情况在大规模部署的情况下更容易触发:

- Printer Farm
- 局域网批量部署

## 部署 Moonraker Mirror Toolkit

在部署之前你需要有一个配置好 tunasync 的服务器

### clone 仓库

clone git 仓库

```shell
git clone https://github.com/Neko-vecter/moonraker-mirror-toolkit.git
```

进入 repo 文件夹

```shell
cd moonraker-mirror-toolkit
```

### 配置 webui 部分

初始化 python venv

```shell
make init
```

添加 webui 部分需要的同步配置

```json title="example-release.json"
{
    "repo": "owner/repo",
    "keep_versions": 10,
    "base_mirror_url": "<mirrors>/repo-release"
}
```

在 `worker` 配置文件中添加以下配置以添加 webui 镜像

:::info

需要修改其中的 python venv 路径 / 同步工具路径 / 同步工具的配置文件位置

:::

```toml title="worker.conf"
[[mirrors]]
name = "mainsail-release"
provider = "command"
upstream = ""
command = "/path-venv/python3 /path/sync-webui-release.py --workers 5 --config /path/example-release.json"
size_pattern = "Total size is ([0-9\\.]+[KMGTP]?)"
interval = 720
```

#### Sync mirror

在开始 mirror 后会在 tunasync 的 working-dir 下创建以下结构的目录

```
LatestRelease/
v2.16.1/
v2.17.0/
```

并且在每个版本中包含了 `release` 文件

```json title="release"
{
    "name": "v2.17.0",
    "tag_name": "v2.17.0",
    "assets": [
        {
            "name": "mainsail.zip",
            "content_type": "application/zip",
            "browser_download_url": "<mirrors>/mainsail-release/v2.17.0/mainsail.zip",
            "size": 3001860
        }
    ],
    "sync_at": ""
}
```

### 配置 git repo 部分

在 tunasync worker 配置文件添加以下部分

```toml title="worker.conf"
[[mirrors]]
name = "klipper.git"
provider = "command"
command = "/path/mmt/git-repo.sh -b master"
upstream = "https://github.com/Klipper3d/klipper.git"
size_pattern = "Total size is ([0-9.]+[KMGTP]?)"
interval = 720

[[mirrors]]
name = "moonraker.git"
provider = "command"
command = "/path/mmt/git-repo.sh -b master"
upstream = "https://github.com/Neko-vecter/moonraker.git"
size_pattern = "Total size is ([0-9.]+[KMGTP]?)"
interval = 720
```

## 使用镜像更新

:::info

在使用镜像更新需要使用可以使用镜像版本的 moonraker

[Neko-vecter/moonraker](https://github.com/Neko-vecter/moonraker)

:::

配置 git repo 的上游同步地址

:::info

在第一次配置的时候需要使用 ssh 手动设置 moonraker 的 origin 为可以使用 mirror 的版本

后续在 mirror 之间切换可以直接使用配置文件进行更改。保存后会自动检查 origin 并且自动 `git remote set-url origin` 到配置文件的地址

:::

```
[update_manager klipper]
dev_mode: True
origin: https://<mirror>/klipper.git

[update_manager moonraker]
dev_mode: True
origin: https://<mirror>/moonraker.git
```

配置 webui 的上游同步地址

```
[update_manager mainsail]
type: web
channel: stable
repo: mainsail-crew/mainsail
path: ~/mainsail

enable_mirror: True
mirror_url: https://<mirror>/mainsail-release/
mirror_latest_template: {base_url}/LatestRelease/release
mirror_tag_template: {base_url}/{tag}/release
```

## TODO

- [x] 增加 Moonraker / Klipper 等 git 仓库的镜像
