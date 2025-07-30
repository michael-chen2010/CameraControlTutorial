# UE5 交互式相机系统教程 | UE5 Interactive Camera System Tutorial

[![UE Version](https://img.shields.io/badge/UE-5.x-blue.svg)](https://www.unrealengine.com/)
[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Mac%20%7C%20Linux-green.svg)](https://www.unrealengine.com/)
[![License](https://img.shields.io/badge/License-MIT-lightgrey.svg)](https://opensource.org/licenses/MIT)

本仓库是视频教程 **《UE5蓝图实战：从零打造一个交互式产品展示器》** 的完整项目源码。

This repository contains the complete source code for the tutorial: **"UE5 Blueprint Practice: Building an Interactive Product Presenter from Scratch"**.

---

## 成果演示 (Final Result)

<!-- 请将此处的 GIF 路径替换为你的实际演示动图 -->
<!-- Please replace the GIF path below with your actual demo GIF -->
![Camera Control Demo GIF](https://media.githubusercontent.com/media/michael-chen2010/CameraControlTutorial/refs/heads/main/pics/CameraControl.gif)

## 功能亮点 (Features)

这个项目使用 **100% 纯蓝图** 实现了一个功能强大、可复用的交互式相机系统，类似于 Sketchfab 或其他产品在线展示应用。

✅ **丝滑的轨道模式 (Smooth Orbit Mode)**
-   鼠标拖拽即可围绕焦点进行轨道旋转。
-   鼠标中键或右键拖拽可平移相机。
-   支持俯仰角限制，防止相机翻转。

✅ **平滑的视野缩放 (Smooth FOV Zoom)**
-   使用鼠标滚轮实现电影镜头般的平滑视野（FOV）变焦，而非生硬的跳跃式变化。

✅ **第一人称漫游 (First-Person Mode)**
-   通过 `WASD` 键在场景中自由漫游和探索。

✅ **精准的交互与聚焦 (Precise Interaction & Focusing)**
-   **双击** 场景中的任意位置，相机会平滑地移动过去并将其设为新的旋转中心。
-   **点击天空** 或空白区域，相机将自动重置到初始状态。
-   （可扩展）点击场景中的特定标签，镜头会自动聚焦并环绕该物体。

## 核心技术与设计模式 (Core Concepts & Design Patterns)

本教程的核心目标不仅是实现功能，更是讲解其背后的 **专业设计模式**，帮助你构建稳定、可扩展的蓝图系统。

### 1. 健壮的蓝图架构 (Robust Blueprint Architecture)
-   **组件化设计 (Component-based Design)**: 通过 `SceneComponent` (作为旋转中心)、`SpringArm` (控制距离) 和 `Camera` 的巧妙父子关系，轻松实现复杂的轨道运动。
-   **状态管理 (State Management with Enums)**: 使用枚举 (`ECameraMode`) 清晰地管理相机是在 `轨道模式` 还是 `第一人称模式`，让逻辑分支一目了然。
-   **参数集 (Parameter Sets)**: 将所有可调参数（如旋转速度、缩放速度、FOV范围等）整合到蓝图中，方便统一传递和修改。

### 2. 专业的交互实现 (Professional Interaction Implementation)
-   **安全的轨道旋转 (Gimbal-Lock-Safe Orbiting)**: 我们不直接旋转相机！而是旋转作为父级的 `CameraTarget`，并在世界空间中对其旋转值进行钳制 (Clamp)，从根源上避免了万向节死锁问题，确保控制永远顺滑。
-   **电影级平滑动画 (Cinematic Smoothing Techniques)**:
    -   **Timeline + Lerp**: 用于有明确起止的动画（如双击聚焦），在指定时间内按缓动曲线完成位移和旋转。
觉变化。
-   **优雅的模式切换 (Elegant Mode Switching)**: 通过 `Attach To Component` 和 `Detach From Component` 节点，动态改变相机的“父亲”，在“被束缚”的轨道模式和“自由”的第一人称模式间无缝切换。
-   **高效的持续输入 (Efficient Continuous Input)**: 使用 `Gate` 节点配合 `Event Tick` 来处理需要按住鼠标持续生效的操作（如拖拽旋转），比在输入事件里直接写逻辑更加高效和规范。

## 如何使用 (How to Use)

1.  **克隆或下载** 本仓库。
    ```bash
    git clone https://github.com/michael-chen2010/CameraControlTutorial.git
    ```
2.  使用 Unreal Engine 5.6 打开项目根目录下的 `.uproject` 文件。
3.  在内容浏览器中，找到并打开主场景地图（例如 `Maps/MainDemo`）。
4.  点击 **Play** 即可体验所有功能。
5.  主要的蓝图逻辑都封装在 `/CameraControl/CameraModule/BP_CameraController` 中，你可以打开它进行学习和修改。

## 许可协议 (License)

本项目采用 [MIT License](LICENSE) 许可。
