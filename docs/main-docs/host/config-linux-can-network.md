---
sidebar_position: 1
description: Config linux CAN Network (ifupdown)
---

# 配置 Linux CAN Network (ifupdown)

:::info[在开始之前]

需要安装 `ifupdown`

```shell
sudo apt update
sudo apt install ifupdown
```

:::

编辑 `/etc/network/interfaces.d/can0`

```shell
sudo nano /etc/network/interfaces.d/can0
```

然后添加以下配置

```systemd
allow-hotplug can0
iface can0 can static
    bitrate 1000000
    up ifconfig $IFACE txqueuelen 1024
```

然后使用以下命令重启

```shell
sudo systemctl restart networking
```
