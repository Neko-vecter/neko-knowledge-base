---
sidebar_position: 2
description: m328p Fuse Bit 配置说明
---

# m328p Fuse Bit 设置

## Fuse 基本概念

### Low Fuse

ATmega328P 的 Low Fuse Byte（低位熔丝字节）一共有 8 个 bit（bit7 - bit0），主要控制时钟源，启动时间以及是否输出时钟等功能。

| Bit           | bit7   | bit6  | bit5 | bit4 | bit3   | bit2   | bit1   | bit0   |
| ------------- | ------ | ----- | ---- | ---- | ------ | ------ | ------ | ------ |
| Fuse Bit Name | CKDIV8 | CKOUT | SUT1 | SUT0 | CKSEL3 | CKSEL2 | CKSEL1 | CKSEL0 |
| Default Value | 0      | 1     | 1    | 0    | 0      | 0      | 1      | 0      |

`0x62` 1 MHz 8 分频 `默认Hex`

`0xe2` 8 MHz 不分频

`0xff` 16MHz 外部晶振

### High Fuse

ATmega328P 的 High Fuse Byte（高位熔丝字节）一共有 8 个 bit（bit7 - bit0），主要控制 Bootloader 大小 / 启动方式 / SPI 烧录使能 / EEPROM 保存等功能。

| Bit           | bit7     | bit6 | bit5  | bit4  | bit3   | bit2    | bit1    | bit0    |
| ------------- | -------- | ---- | ----- | ----- | ------ | ------- | ------- | ------- |
| Fuse Bit Name | RSTDISBL | DWEN | SPIEN | WDTON | EESAVE | BOOTSZ1 | BOOTSZ0 | BOOTRST |
| Default Value | 1        | 1    | 0     | 1     | 1      | 1       | 1       | 1       |

:::warning

错误的配置 `SPIEN` 会导致无法写入

:::

### Extended Fuse

TODO

## 读取 Fuse Bit

### 使用 usbasp

```shell
avrdude -c usbasp -p m328p -U lfuse:r:-:h -U hfuse:r:-:h -U efuse:r:-:h
```

### 使用 arduino as isp

```shell
avrdude -c avrisp -P /dev/serial/by-id/xxx -b 19200 -p m328p -U lfuse:r:-:h -U hfuse:r:-:h -U efuse:r:-:h
```

## 写入 Fuse Bit 

使用 `0xe2` 作为 example。内部RC 振荡器 8 MHz 不分频。

### 使用 usbasp

```shell title="配置Low Fuse"
avrdude -c usbasp -p m328p -U lfuse:w:0xe2:m
```

### 使用 arduino as isp

```shell title="配置Low Fuse"
avrdude -c avrisp -P /dev/serial/by-id/xxx -b 19200 -p m328p -U lfuse:w:0xe2:m
```
