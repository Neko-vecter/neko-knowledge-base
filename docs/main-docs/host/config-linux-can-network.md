---
sidebar_position: 1
description: Config linux CAN Network (ifupdown)
---

# Config Linux CAN Network

Add the config to `/etc/network/interfaces.d/can0`

```shell
sudo nano /etc/network/interfaces.d/can0
```

Add the config below. `use control + x to exit`

```
allow-hotplug can0
iface can0 can static
    bitrate 1000000
    up ifconfig $IFACE txqueuelen 1024
```
