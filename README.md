# MaGen-STM32-Web

MaGen-STM32-Web 是一个 STM32 工程生成器项目，同时包含经典 C# Windows 桌面版和网页版。

MaGen-STM32-Web is an STM32 project generator that contains both a classic C# Windows desktop application and a web-based version.

项目当前全面支持 `STM32 F0-F4 系列` 以及 `L1 系列` 的所有单片机开发板（共计涵盖 543 款芯片）与 `Keil` 工程生成场景，能够生成全系列引脚配置与传感器配置、常用外设初始化代码、维护工程结构，并支持对已有项目继续编辑。

The project currently fully supports all microcontroller development boards from the `STM32 F0-F4 series` and `L1 series` (covering a total of 543 chips) for `Keil`-based project generation. It can generate comprehensive pin and sensor configurations across the entire series, peripheral initialization code, maintain project structure, and continue editing existing projects.

## 项目概览 | Overview

- `MaGen`：基于 `.NET Framework 4.8` 的 C# Windows Forms 桌面程序
- `MaGen.Web`：基于 `.NET 9` 的 ASP.NET Core Web 应用
- 目标流程：配置外设 -> 生成或更新工程 -> 打开 Keil

- `MaGen`: C# Windows Forms desktop application based on `.NET Framework 4.8`
- `MaGen.Web`: ASP.NET Core web application based on `.NET 9`
- Target workflow: configure peripherals -> generate or update project -> open in Keil

## 功能特性 | Features

- **全面支持 STM32 F0、F1、F2、F3、F4 及 L1 系列（共计 543 款芯片）的引脚与传感器配置**
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

- **Fully supports pin and sensor configurations for 543 chips across the STM32 F0, F1, F2, F3, F4, and L1 series**
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
|- MaGen/          桌面版项目 / Desktop application (C#)
|- MaGen.Web/      网页版项目 / Web application
|- packages/       本地 NuGet 依赖 / Local NuGet package dependencies
|- MaGen.sln       Visual Studio 解决方案 / Visual Studio solution
