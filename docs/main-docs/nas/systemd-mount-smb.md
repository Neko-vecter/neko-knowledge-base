---
sidebar_position: 1
description: 使用 systemd 挂载 smb 目录
---

# systemd 挂载 smb 目录

由于使用 fstab 可能会导致无法启动。比如 smb 无法加载。

### 配置 mount

```shell
sudo nano /etc/systemd/system/mnt-media.mount
```

```systemd
[Unit]
Description=SMB Media Mount
After=network-online.target
Wants=network-online.target

[Mount]
What=//<nas-ip>/<path>
Where=/mnt/<mount_path>
Type=cifs
Options=credentials=/home/username/.smbcredentials,iocharset=utf8,vers=3.0

[Install]
WantedBy=multi-user.target
```

```shell
sudo systemctl daemon-reexec
sudo systemctl daemon-reload
sudo systemctl enable --now mnt-media.mount
```

### 配置 automount 可选

```shell
sudo nano /etc/systemd/system/mnt-media.automount
```

```systemd
[Unit]
Description=Automount SMB Media

[Automount]
Where=/mnt/<mount_path>

[Install]
WantedBy=multi-user.target
```

### 启用 automount 可选

```shell
sudo systemctl daemon-reexec
sudo systemctl daemon-reload
sudo systemctl enable --now mnt-media.automount
```
