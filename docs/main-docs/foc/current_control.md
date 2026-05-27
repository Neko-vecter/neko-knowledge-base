---
sidebar_position: 2
description: FOC 电流计算
---

# FOC 电流计算

在以下内容中使用 MIT Mini Cheetah PD Feed-Forward

## 基本概念

在传统的 FOC 设计中使用 Cascaded PI 作为 Position loop 和 Velocity loop 的反馈控制器。这样的设计固然符合控制论的直觉但是不可避免的在高速控制中引入一定的动态响应延迟。

在此基础上 PD Feed-Forward 的控制架构的速度位置上没有使用之前的 Cascaded PI 作为 Position loop 和 Velocity loop 的反馈控制器。而是从力矩层面出发通过把 Position 和 Velocity 作为参数传入。并且作为 Torque 计算的一部分。最终直接输出 $I_q$ 给 Current loop。

## Torque calculation

在有期望目标 Position / Velocity / Torque 的时候想要计算出电流环 $I_q$。首先我们需要计算需要的力矩 $\tau$

$\tau = K_p \cdot (p_{input} - p_{meas}) + K_d \cdot (v_{input} - v_{meas}) + \tau_{ff}$

变量定义

### 调节参数

- $K_p$ Proportional Gain
- $K_d$ Derivative Gain

### 输入参数

- $p_{input}$ Target Position
- $v_{input}$ Target Velocity
- $\tau_{ff}$ Feedforward Torque

### 测量参数

- $p_{meas}$ Measured Position
- $v_{meas}$ Measured Velocity

## Calculation of q-axis Current Reference Using Torque Constant

随后使用电机力矩常数 $K_t$ 把输出力矩 $\tau$ 转换成 q 轴电流参考值 $I_{q\_ref}$

$I_{q\_ref} = \frac{\tau}{K_t}$
