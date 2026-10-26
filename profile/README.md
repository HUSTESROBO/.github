<div align="center">

# ESROBO

**移动双臂灵巧手机器人平台**

硬件开发 · 分布式控制 · 实机遥操作 · 仿真与回放

[平台仓库](https://github.com/HUSTESROBO/ESROBO) · [开发文档](https://github.com/HUSTESROBO/ESROBO/blob/main/document/README.md) · [驱动与 SDK](https://github.com/HUSTESROBO/ESROBO/blob/main/src/README.md) · [通信协议](https://github.com/HUSTESROBO/ESROBO/blob/main/robot_link/PROTOCOL.md)

</div>

## 关于 ESROBO

ESROBO 是一套集成移动底盘、双七轴机械臂和双五指灵巧手的机器人平台。**HUSTESROBO** 汇集该平台的硬件资料、设备驱动、机器人模型和通信接口，并提供基于平台开发的遥操作与仿真项目入口。

平台仓库负责通用的硬件接入与控制基础，各应用项目维护自己的输入设备、算法、运行环境和实验说明。

## 硬件平台

| 子系统 | 硬件组成 |
| --- | --- |
| 双臂与双手 | 两台 NERO 七轴机械臂、双 LinkerHand L20Lite 灵巧手 |
| 移动与姿态 | Ranger Mini 3 底盘、三轴腰部、头部云台舵机 |
| 视觉与测距 | Orbbec 头部 RGB-D 相机、RealSense 腕部 RGB-D 相机、RoboSense 激光雷达 |
| 力觉感知 | 双六维力／力矩传感器 |

主要部署环境为 **Ubuntu 22.04 / ROS 2 Humble**。具体设备接口、接线和启动顺序见平台开发文档。

## 平台开发资源

基础资源统一维护在 **[HUSTESROBO/ESROBO](https://github.com/HUSTESROBO/ESROBO)**。

| 资源 | 内容 | 文档入口 |
| --- | --- | --- |
| **硬件文档** | 整机与部件手册、CAN／串口连接、设备命名和逐部件调试 | [手册索引](https://github.com/HUSTESROBO/ESROBO/blob/main/document/README.md) · [硬件接入](https://github.com/HUSTESROBO/ESROBO/blob/main/HARDWARE_BRINGUP.md) |
| **驱动与 SDK** | 机械臂、灵巧手、底盘、腰部、头部、相机、雷达及力传感器的 ROS 2 驱动与底层库 | [驱动索引](https://github.com/HUSTESROBO/ESROBO/blob/main/src/README.md) |
| **机器人模型** | 整机 URDF、关节连接与限位、灵巧手联动关系，以及模型资源来源 | [URDF](https://github.com/HUSTESROBO/ESROBO/tree/main/teleoperation/urdf) · [资源清单](https://github.com/HUSTESROBO/ESROBO/blob/main/teleoperation/assets/esrobo_waist_with_head/SOURCE.json) |
| **通信与执行** | `robot_link` Python 客户端、认证 UDP、目标与反馈格式、执行网关和状态管理 | [接入指南](https://github.com/HUSTESROBO/ESROBO/blob/main/robot_link/README.md) · [协议](https://github.com/HUSTESROBO/ESROBO/blob/main/robot_link/PROTOCOL.md) · [执行流程](https://github.com/HUSTESROBO/ESROBO/blob/main/robot_link/ROBOT_EXECUTION.md) |

### 分布式控制架构

```mermaid
flowchart LR
    A["输入设备"] --> B["本机计算端<br/>数据采集、重定向与 IK"]
    B -->|关节目标| C["机器人主机<br/>网关、运动约束与底层控制"]
    C -->|实测反馈| B
    C <--> D["CAN / ROS 2 驱动"]
    D <--> E["ESROBO"]
```

本机计算端负责输入处理、算法运算和运动目标下发；机器人主机负责目标校验、轨迹执行、设备通信及反馈。当前网络关节接口主要面向机械臂与灵巧手，具体控制能力以通信合同和项目说明为准。

## 基于平台的项目

| 项目 | 主要内容 | 代码与文档 |
| --- | --- | --- |
| **PICO 实机遥操作** | PICO Body／Hand 采集、人体标定、双臂与灵巧手重定向、IK、网页控制台和机器人网关接入 | [统一遥操作目录](https://github.com/SaluteYan/esrobo/tree/refactor/unified-teleoperation-20261026/teleoperation) · [操作文档](https://github.com/SaluteYan/esrobo/blob/refactor/unified-teleoperation-20261026/teleoperation/docs/01_README.md) |
| **IsaacLab 仿真与回放** | ESROBO 仿真资产、PICO／SenseGlove 输入、遥操作基线、录制回放及复现资料 | [Dual-arm-teleoperation](https://github.com/SaluteYan/Dual-arm-teleoperation) · [复现说明](https://github.com/SaluteYan/Dual-arm-teleoperation/tree/main/reproducibility) |

实机项目入口指向已完成目录整合的 `refactor/unified-teleoperation-20261026` 分支，采集与控制组件集中在 `teleoperation/`。上述应用目前由原作者账号下的仓库维护；平台与应用分别记录版本和验证范围。

## 开始使用

- **部署机器人**：阅读整机手册，按硬件接入指南逐项检查设备，再配置相应驱动。
- **开发控制应用**：从 `robot_link` 接入指南开始，先使用 mock 网关验证通信，再完成实机联调。
- **运行遥操作或仿真**：进入对应项目，按其说明安装环境、准备模型与输入设备。

平台硬件、驱动和协议问题请提交到 [ESROBO Issues](https://github.com/HUSTESROBO/ESROBO/issues)；算法与运行问题请在对应项目反馈，并提供代码版本、环境和复现步骤。
