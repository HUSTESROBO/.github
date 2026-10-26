<div align="center">

<img src="https://raw.githubusercontent.com/HUSTESROBO/.github/main/profile/assets/header.svg" alt="ESROBO · HUSTESROBO robotics platform" width="100%" />

**移动双臂灵巧手机器人平台**

硬件开发 · 分布式控制 · 实机遥操作 · 仿真与回放

<code>Ubuntu 22.04</code> &nbsp; <code>ROS 2 Humble</code> &nbsp; <code>Python / C++</code>

[🏠 平台仓库](https://github.com/HUSTESROBO/ESROBO) · [📖 开发文档](https://github.com/HUSTESROBO/ESROBO/blob/main/document/README.md) · [⚙️ 驱动与 SDK](https://github.com/HUSTESROBO/ESROBO/blob/main/src/README.md) · [🔗 通信协议](https://github.com/HUSTESROBO/ESROBO/blob/main/robot_link/PROTOCOL.md)

</div>

**ESROBO** 是一套移动双臂灵巧手机器人平台。HUSTESROBO 汇集设备驱动、开发文档、独立机器人模型与通信接口，为基于该平台的遥操作和仿真研究提供入口。

---

## 🧰 平台资源

基础资源统一维护在 **[HUSTESROBO/ESROBO](https://github.com/HUSTESROBO/ESROBO)**，包含设备驱动、开发文档、独立模型和通信接口；遥操作代码由下方应用项目单独维护。

| 资源 | 内容 | 文档入口 |
| --- | --- | --- |
| **硬件文档** | 整机与部件手册、CAN／串口连接、设备命名和逐部件调试 | [手册索引](https://github.com/HUSTESROBO/ESROBO/blob/main/document/README.md) · [硬件接入](https://github.com/HUSTESROBO/ESROBO/blob/main/HARDWARE_BRINGUP.md) |
| **驱动与 SDK** | 机械臂、灵巧手、底盘、腰部、头部、相机、雷达及力传感器的 ROS 2 驱动与底层库 | [驱动索引](https://github.com/HUSTESROBO/ESROBO/blob/main/src/README.md) |
| **机器人模型** | 独立整机 URDF、70 个视觉／碰撞网格、灵巧手联动及逐文件来源校验 | [URDF](https://github.com/HUSTESROBO/ESROBO/tree/main/model/esrobo_waist_with_head/urdf) · [资源清单](https://github.com/HUSTESROBO/ESROBO/blob/main/model/esrobo_waist_with_head/SOURCE.json) |
| **通信与执行** | `robot_link` Python 客户端、认证 UDP、目标与反馈格式、执行网关和状态管理 | [接入指南](https://github.com/HUSTESROBO/ESROBO/blob/main/robot_link/README.md) · [协议](https://github.com/HUSTESROBO/ESROBO/blob/main/robot_link/PROTOCOL.md) · [执行流程](https://github.com/HUSTESROBO/ESROBO/blob/main/robot_link/ROBOT_EXECUTION.md) |

---

## 🧪 应用项目

<table>
<tr>
<td width="50%" valign="top">
<h3>🥽 PICO 实机遥操作</h3>
<p>PICO Body / Hand 输入、人体标定、双臂与灵巧手重定向、IK 和网页控制台。</p>
<p><strong>本机采集与运算 → 机器人网关执行</strong></p>
<p><a href="https://github.com/SaluteYan/esrobo/tree/refactor/unified-teleoperation-20261026/teleoperation">查看代码 →</a> &nbsp; · &nbsp; <a href="https://github.com/SaluteYan/esrobo/blob/refactor/unified-teleoperation-20261026/teleoperation/docs/01_README.md">操作文档</a></p>
</td>
<td width="50%" valign="top">
<h3>🧊 IsaacLab 仿真与回放</h3>
<p>ESROBO 仿真资产、PICO / SenseGlove 输入、遥操作基线与录制数据回放。</p>
<p><strong>仿真环境 → 算法验证与实验复现</strong></p>
<p><a href="https://github.com/SaluteYan/Dual-arm-teleoperation">查看仓库 →</a> &nbsp; · &nbsp; <a href="https://github.com/SaluteYan/Dual-arm-teleoperation/tree/main/reproducibility">复现说明</a></p>
</td>
</tr>
</table>

<sub>应用由原作者账号下的仓库维护。实机入口指向 <code>refactor/unified-teleoperation-20261026</code> 目录整合分支；各项目分别记录运行环境和验证范围。</sub>

<details>
<summary><strong>🤖 了解硬件组成与控制架构</strong></summary>

### 硬件组成

| 子系统 | 硬件组成 |
| --- | --- |
| 双臂与双手 | 两台 NERO 七轴机械臂、双 LinkerHand L20Lite 灵巧手 |
| 移动与姿态 | Ranger Mini 3 底盘、三轴腰部、头部云台舵机 |
| 视觉与测距 | Orbbec 头部 RGB-D 相机、RealSense 腕部 RGB-D 相机、RoboSense 激光雷达 |
| 力觉感知 | 双六维力／力矩传感器 |

主要部署环境为 **Ubuntu 22.04 / ROS 2 Humble**。具体设备接口、接线和启动顺序见平台开发文档。

### 分布式控制架构

```mermaid
flowchart LR
    A["输入设备"] --> B["本机计算端<br/>数据采集、重定向与 IK"]
    B -->|关节目标| C["机器人主机<br/>网关、运动约束与底层控制"]
    C -->|实测反馈| B
    C <--> D["CAN / ROS 2 驱动"]
    D <--> E["ESROBO"]
    classDef compute fill:#e0f2fe,stroke:#0284c7,color:#0c4a6e
    classDef control fill:#ccfbf1,stroke:#0d9488,color:#134e4a
    classDef device fill:#f1f5f9,stroke:#64748b,color:#0f172a
    class B compute
    class C control
    class A,D,E device
```

本机计算端负责输入处理、算法运算和运动目标下发；机器人主机负责目标校验、轨迹执行、设备通信及反馈。当前网络关节接口主要面向机械臂与灵巧手，具体控制能力以通信合同和项目说明为准。

</details>

---

## 🚀 开始使用

- **部署机器人**：阅读整机手册，按硬件接入指南逐项检查设备，再配置相应驱动。
- **开发控制应用**：从 `robot_link` 接入指南开始，先使用 mock 网关验证通信，再完成实机联调。
- **运行遥操作或仿真**：进入对应项目，按其说明安装环境、准备模型与输入设备。

平台硬件、驱动和协议问题请提交到 [ESROBO Issues](https://github.com/HUSTESROBO/ESROBO/issues)；算法与运行问题请在对应项目反馈，并提供代码版本、环境和复现步骤。
