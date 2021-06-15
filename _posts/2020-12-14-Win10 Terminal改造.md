---
layout: post
title: Win10 Terminal 改造
tags: 
 - PHP
---

我心中一款完美的终端工作台

1、脱离鼠标

2、摆脱多任务频繁切换

3、高颜值、高性能、流畅体验好



![img](https://mmbiz.qlogo.cn/sz_mmbiz_png/eibiaibEerNQsG9rZIFfnxxt8Y6dhGZbkp2FY7Km9FNHnxaVPpdJdgoicbNL8XcpBusufEXZKmZicPv4Wf9ZZgm5oXQ/0?wx_fmt=png)

↑ 配置完成之后的 Terminal



## 摆脱鼠标

剥离了图形化的界面之后，不用离开键盘去操作鼠标，在熟练掌握之后，成倍提升编码效率。

### 内置快捷键

- Alt + Shilft + - (新建平行窗格)
- Alt + Shilft + + (新建垂直窗格)
- Alt + 方向键 (移动到指定窗格)
- Alt + Shift + 方向键 （可进行上下左右调整窗格大小）
- Ctrl + Shift + w (关闭当前窗格)
- ctrl+shift+f (搜索)
- ctrl+shift+p (快捷调出)
- Win + 方向键 （改变窗口格式）
- Ctrl + Tab  (切换下一个标签)



![img](https://mmbiz.qpic.cn/sz_mmbiz_gif/eibiaibEerNQsG9rZIFfnxxt8Y6dhGZbkp2rCYOVwBhxLoFhR2AS2J7uAcnI2YgiaZKahficXicibMsia6E1vxK71agq1A/0?wx_fmt=gif)



![img](https://mmbiz.qlogo.cn/sz_mmbiz_gif/eibiaibEerNQsG9rZIFfnxxt8Y6dhGZbkp2gttdCeVorCo95mCT7sEECF7KPYAFbk5qtRbl7eF2RS5kqx1YsNvtGQ/0?wx_fmt=gif)

### 自定义快捷键

```json
// 添加窗格
{ "command": { "action": "splitPane", "split": "vertical" }, "keys": "alt+shift+plus" },
{ "command": { "action": "splitPane", "split": "horizontal" }, "keys": "alt+shift+-" },
{ "command": { "action": "splitPane", "split": "auto" }, "keys": "alt+shift+|" },
// 切换窗格
{ "command": { "action": "moveFocus", "direction": "down" }, "keys": "alt+down" },
{ "command": { "action": "moveFocus", "direction": "left" }, "keys": "alt+left" },
{ "command": { "action": "moveFocus", "direction": "right" }, "keys": "alt+right" },
{ "command": { "action": "moveFocus", "direction": "up" }, "keys": "alt+up" },
// 调整窗格大小
{ "command": { "action": "resizePane", "direction": "down" }, "keys": "alt+shift+down" },
{ "command": { "action": "resizePane", "direction": "left" }, "keys": "alt+shift+left" },
{ "command": { "action": "resizePane", "direction": "right" }, "keys": "alt+shift+right" },
{ "command": { "action": "resizePane", "direction": "up" }, "keys": "alt+shift+up" }
// 关闭窗格
{ "command": "closePane", "keys": "ctrl+shift+w" }
// 复制窗格
{ "command": { "action": "splitPane", "split": "auto", "splitMode": "duplicate" }, "keys": "alt+shift+d" }
```

## 主题

### 内置的配色方案

Windows 终端将这些配色方案包含在 `defaults.json` 文件中，可按住 alt 并选择设置按钮来访问该文件。 如果要在一个命令行配置文件中设置配色方案，请添加 `colorScheme` 属性，并将配色方案的 `name` 作为值。

```json
"colorScheme": "配置主题名称"
```

#### Campbell

![Windows 终端 Campbell 配色方案](https://docs.microsoft.com/zh-cn/windows/terminal/images/campbell-color-scheme.png)

#### Campbell Powershell

![Windows 终端 Campbell Powershell 配色方案](https://docs.microsoft.com/zh-cn/windows/terminal/images/campbell-powershell-color-scheme.png)

#### Vintage

![Windows 终端 Vintage 配色方案](https://docs.microsoft.com/zh-cn/windows/terminal/images/vintage-color-scheme.png)

#### One Half Dark

![Windows 终端 One Half Dark 配色方案](https://docs.microsoft.com/zh-cn/windows/terminal/images/one-half-dark-color-scheme.png)

#### One Half Light

![Windows 终端 One Half Light 配色方案](https://docs.microsoft.com/zh-cn/windows/terminal/images/one-half-light-color-scheme.png)

#### Solarized Dark

![Windows 终端 Solarized Dark 配色方案](https://docs.microsoft.com/zh-cn/windows/terminal/images/solarized-dark-color-scheme.png)

#### Solarized Light

![Windows 终端 Solarized Light 配色方案](https://docs.microsoft.com/zh-cn/windows/terminal/images/solarized-light-color-scheme.png)

#### Tango Dark

![Windows 终端 Tango Dark 配色方案](https://docs.microsoft.com/zh-cn/windows/terminal/images/tango-dark-color-scheme.png)

#### Tango Light

![Windows 终端 Tango Light 配色方案](https://docs.microsoft.com/zh-cn/windows/terminal/images/tango-light-color-scheme.png)

### 自定义配色

打开配置文件 `settings.json`，找到 `schemes`写入以下格式，包含了所有的颜色格式

```json
{
    // 配色名称
    "name" : "Campbell",

    // 可选
    "cursorColor": "#FFFFFF",
    // 可选
    "selectionBackground": "#FFFFFF",

    "background" : "#0C0C0C",
    "foreground" : "#CCCCCC",

    "black" : "#0C0C0C",
    "blue" : "#0037DA",
    "cyan" : "#3A96DD",
    "green" : "#13A10E",
    "purple" : "#881798",
    "red" : "#C50F1F",
    "white" : "#CCCCCC",
    "yellow" : "#C19C00",
    "brightBlack" : "#767676",
    "brightBlue" : "#3B78FF",
    "brightCyan" : "#61D6D6",
    "brightGreen" : "#16C60C",
    "brightPurple" : "#B4009E",
    "brightRed" : "#E74856",
    "brightWhite" : "#F2F2F2",
    "brightYellow" : "#F9F1A5"
},
```

### 更多配置字段和信息

把一下内容写入到对应的 profile 中

```json
// 字体
"fontFace": "Fira Code",
// 字体大小
"fontSize": 11,
"historySize": 9001,
// 显示在标签和菜单中的图标。
"icon":"111",
"padding": "5, 5, 20, 25",
// 设置为 true ，输入时窗口会自动跳转到输入行；设置为 false ，输入时窗口不会自动跳转。
"snapOnInput": true,
// 使用亚克力
"useAcrylic": true,
// 透明度
"acrylicOpacity": 0.7
```

[Windows 终端全局设置 | Microsoft Docs](https://docs.microsoft.com/zh-cn/windows/terminal/customize-settings/global-settings)

