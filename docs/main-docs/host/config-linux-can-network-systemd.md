---
sidebar_position: 1
description: Config linux CAN Network (systemd)
---

# 使用 systemd-networkd 管理 CAN Network

:::info

Debian 13 之前的版本建议使用 [配置 Linux CAN Network (ifupdown)](./config-linux-can-network.md)

:::

### 添加 `can.network` 配置文件

``` shell
sudo nano /etc/systemd/network/80-can.network
```

`/etc/systemd/network/80-can.network` 

``` systemd
[Match]
Name=can*

[CAN]
BitRate=1000000

[Link]
RequiredForOnline=no
```

### 添加 `can.link` 配置文件

``` shell 
sudo nano /etc/systemd/network/80-can.link
```

`/etc/systemd/network/80-can.link` 

``` systemd
[Match]
Type=can

[Link]
TransmitQueueLength=1000
```

### 开启 `systemd-networkd`

``` shell
sudo systemctl enable --now systemd-networkd.service 
```
