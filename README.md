# MaGen-STM32-Web

MaGen-STM32-Web 是一个 STM32 工程生成器项目，同时包含经典 Windows 桌面版和网页版。

MaGen-STM32-Web is an STM32 project generator that contains both a classic Windows desktop application and a web-based version.

项目当前主要面向 `STM32F103C8T6` 与 `Keil` 工程生成场景，能够生成常用外设初始化代码、维护工程结构，并支持对已有项目继续编辑。

The project is currently focused on `STM32F103C8T6` and `Keil`-based project generation. It can generate peripheral initialization code, maintain project structure, and continue editing existing projects.

## 项目概览 | Overview

- `MaGen`：基于 `.NET Framework 4.8` 的 Windows Forms 桌面程序
- `MaGen.Web`：基于 `.NET 9` 的 ASP.NET Core Web 应用
- 目标流程：配置外设 -> 生成或更新工程 -> 打开 Keil

- `MaGen`: Windows Forms desktop application based on `.NET Framework 4.8`
- `MaGen.Web`: ASP.NET Core web application based on `.NET 9`
- Target workflow: configure peripherals -> generate or update project -> open in Keil

## 功能特性 | Features

- GPIO 配置
- ADC 配置
- USART 配置
- PWM 配置
- TIM 配置
- EXTI / NVIC 中断配置
- 常用模块与传感器配置
- 基于模板资源生成 Keil 工程结构
- 支持对已生成项目继续编辑
- 自动识别 `USER\*.uvprojx` 并打开 Keil 工程
- 网页版支持 Windows 原生目录选择器

- GPIO configuration
- ADC configuration
- USART configuration
- PWM configuration
- TIM configuration
- EXTI / NVIC interrupt configuration
- Module configuration for common peripherals and sensors
- Generate Keil project structure from embedded template resources
- Continue editing existing generated projects
- Automatically detect `USER\*.uvprojx` and open Keil project
- Native Windows folder picker in the web version

## 支持的模块模板 | Supported Module Templates

- DHT11
- OLED
- ESP-01S
- HC-SR04
- BH1750
- DS18B20
- HX711
- DS3231
- DS1302
- MPU6050
- MAX30102
- AS608
- BMP280

## 仓库结构 | Repository Structure

```text
MaGen_C#源码/
|- MaGen/          桌面版项目 / Desktop application
|- MaGen.Web/      网页版项目 / Web application
|- packages/       本地 NuGet 依赖 / Local NuGet package dependencies
|- MaGen.sln       Visual Studio 解决方案 / Visual Studio solution
```

## 桌面版 | Desktop Version

路径 / Path: `MaGen\`

- 框架 / Framework: `.NET Framework 4.8`
- UI 库 / UI libraries: `AntdUI`, `SunnyUI.Common`
- 主入口 / Main entry: `MaGen\Form1.cs`
- 构建输出 / Build output: `MaGen\bin\Debug\MaGen.exe`

当前桌面版已同步支持完整 EXTI 中断配置，包括：

- 中断引脚选择
- 输入模式选择
- 触发边沿选择
- 抢占优先级与子优先级
- 自动生成 `EXTI.c` 与 `EXTI.h`
- 自动向 Keil 工程注入 `stm32f10x_exti.c`

The current desktop version supports synchronized full EXTI interrupt configuration, including:

- interrupt pin selection
- input mode selection
- trigger edge selection
- preemption priority and sub priority
- generation of `EXTI.c` and `EXTI.h`
- automatic injection of `stm32f10x_exti.c` into the Keil project

## 网页版 | Web Version

路径 / Path: `MaGen.Web\`

- 框架 / Framework: ASP.NET Core on `.NET 9`
- 前端 / Frontend: 原生 HTML、CSS、JavaScript
- 后端形式 / Backend style: Minimal API
- 主要文件 / Main files:
- `MaGen.Web\Program.cs`
- `MaGen.Web\ProjectGenerator.cs`
- `MaGen.Web\ProjectModels.cs`
- `MaGen.Web\wwwroot\index.html`
- `MaGen.Web\wwwroot\app.js`

当前网页版支持：

- 项目保存与重新打开
- 对本地已生成项目继续编辑
- Windows 原生目录选择
- 自动识别 Keil 工程路径
- 直接打开已识别到的 Keil 工程
- 独立 EXTI / NVIC 中断配置

The current web version supports:

- project save and reopen
- continue editing local generated projects
- native Windows directory selection
- automatic recognition of Keil project paths
- direct opening of detected Keil projects
- independent EXTI / NVIC interrupt configuration

## 构建与运行 | Build And Run

### 桌面版 | Desktop Application

使用 Visual Studio 2022 打开 `MaGen.sln`，构建 `MaGen` 项目即可。

Open `MaGen.sln` with Visual Studio 2022 and build the `MaGen` project.

也可以使用 MSBuild：

You can also build with MSBuild:

```powershell
& "C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Current\Bin\MSBuild.exe" ".\MaGen.sln" /t:Build /p:Configuration=Debug /m:1
```

### 网页版 | Web Application

在 `MaGen.Web\` 目录中运行：

Run in `MaGen.Web\`:

```powershell
dotnet build /p:UseAppHost=false
dotnet run
```

默认本地访问地址 / Default local URL:

```text
http://localhost:5078/
```

## 环境要求 | Environment

- Windows
- 推荐使用 Visual Studio 2022
- 桌面版需要 `.NET Framework 4.8`
- 网页版需要 `.NET 9 SDK`
- 生成的 STM32 工程建议使用 `Keil5`

- Windows
- Visual Studio 2022 recommended
- `.NET Framework 4.8` for desktop version
- `.NET 9 SDK` for web version
- `Keil5` recommended for generated STM32 projects

## 说明 | Notes

- 该项目当前以 Windows 环境为主，因为网页版使用了 Windows 原生文件夹与文件选择能力
- 生成工程依赖仓库内嵌入的 STM32 标准外设库风格模板
- 当前 `MaGen.sln` 仅包含桌面版项目，`MaGen.Web` 可独立打开和构建

- This project is currently Windows-oriented because the web version uses native Windows dialogs for folder and file selection
- Generated projects are based on STM32 standard peripheral library style templates embedded in the repository
- The current `MaGen.sln` only includes the desktop project, and `MaGen.Web` can be opened and built independently

## 当前状态 | Status

项目仍在持续开发中。网页版已经扩展到接近原桌面版的工作流，桌面版也已经同步补充了最新的 EXTI 中断配置支持。

This repository is under active development. The web version has been extended to align with the original desktop workflow, and the desktop version has also been synchronized with the latest EXTI interrupt configuration support.
