# HUSTESROBO 组织主页

组织展示正文位于 [profile/README.md](profile/README.md)，用于 https://github.com/HUSTESROBO 的 Overview。

平台仓库为 [HUSTESROBO/ESROBO](https://github.com/HUSTESROBO/ESROBO)。应用项目在实际发布后更新 profile 中的链接；保留原仓库入口，未发布项目不使用占位链接。

2026-10-26：建立 ESROBO 平台介绍、驱动／文档／通信导航，以及 PICO 实机遥操作和现有 IsaacLab 项目入口。

## 2026-10-26 主页内容整理

- 按“平台定位、硬件组成、基础开发资源、分布式架构、应用项目、开始使用”组织内容，合并重复介绍和导航。
- 明确本机负责采集／运算／目标下发，机器人主机负责底层执行与反馈；模型入口直接链接 URDF 和资源清单。
- PICO 项目更新为已发布的 `refactor/unified-teleoperation-20261026/teleoperation` 统一目录，补充操作文档入口；仿真项目链接既有仓库及复现资料。
- 应用与平台分别说明版本，不把目录重构分支或历史试验写成新的实机验收结果。主页未增加尚不存在的项目仓库或占位媒体。
- 本次只更新组织展示内容；14 个不同目标链接已通过 GitHub 连接器读取验证，`git diff --check` 通过；发布后再核验远程 main 与组织首页实际展示。

## 2026-10-26 平台与遥操作内容分离

- 平台仓库移除遥操作副本，主页继续在应用项目区提供其外部入口。
- 模型导航改为平台 `model/`：独立 URDF、全部 70 个网格及来源清单，网格由 Git LFS 管理。
- 平台基础资源与遥操作代码的边界在资源区明确说明。

## 2026-10-26 轻量视觉调整

- 增加仓库内维护的 SVG 页首横幅，以深蓝和青绿色配色展示平台名称；图形为抽象连接节点，不使用替代机器人照片。
- 导航与主要章节增加少量图标，使用分隔线区分基础资源和应用项目；架构图按计算、执行与设备着色。
- 现有说明、应用边界和目标链接保持不变。SVG 无脚本、外部字体或外部图片依赖，支持缩放。

- 参考 [XR-Robotics](https://github.com/XR-Robotics) 的资源／样例分组，以及 [Unitree Robotics](https://github.com/unitreerobotics)、[ROBOTIS](https://github.com/robotis-git) 的分类仓库导航，将平台资源和应用入口前置；两个应用以并排卡片展示，硬件与控制架构放入可展开区。
- 只借鉴导航结构，保留 ESROBO 自有文案和原创横幅，不复用其他组织的标识或产品素材。
