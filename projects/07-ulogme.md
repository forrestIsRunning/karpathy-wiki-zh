# ulogme

**GitHub:** https://github.com/karpathy/ulogme
**Stars:** 1.2k | **Forks:** 206 | **Language:** Python
**License:** MIT

## 项目介绍

在 Ubuntu/OSX 环境下自动收集和可视化使用统计信息。记录全天的电脑活动：以漂亮的 HTML 时间线展示活动窗口标题和按键次数。

**今天你有多高效？写了多少代码？时间都去哪儿了？**

### 功能特性

- 记录全天的**活动窗口**标题
- 记录全天**按键频率**
- 为特定时间或全天记录自定义**备注**
- 一切**完全在本地运行**：你的数据不会上传到任何地方
- **漂亮、可定制的 HTML/CSS/JS 界面**（使用 d3.js）

目前仅支持 Ubuntu 和 OSX，使用新的 ECMAScript 6 Promises 功能。

ulogme 是一个"时间小侦探"，默默记下你今天在电脑上都做了什么。它知道你在哪个窗口工作，打了多少字，还能画成漂亮的图给你看。一切都存在你自己的电脑里，别人看不到，就像你的秘密日记本。

## 快速上手

### 记录

```bash
$ git clone https://github.com/karpathy/ulogme.git
# Ubuntu 上：sudo apt-get install xdotool wmctrl
$ cd ulogme
$ ./ulogme.sh  # 启动记录脚本
```

**OSX 用户：** 前往 系统偏好设置 > 安全性与隐私 > 辅助功能，允许 Terminal/iTerm2。

### 用户界面

复制示例配置：
```bash
$ cp render/render_settings_example.js render/render_settings.js
```
编辑 `render_settings.js` 配置标题映射（基于正则表达式的活动类型分类）。

启动 Web 服务器：
```bash
$ python ulogme_serve.py
```
在浏览器中访问 `http://localhost:8123`。

### 视图

- **单日页面：** 输入每日备注/提醒。在条形码视图中点击任意条形，添加带时间戳的备注。
- **概览页面：** 点击窗口标题切换可见性。点击竖条查看完整日统计信息。

## 已知问题

- 部分 Ubuntu 用户报告日志中出现含异常字符的时间戳
- 地址已被占用？使用不同的端口：`python ulogme_serve.py 8124`
- 概览页面在 Firefox 上可能无法正常显示（需要 ES6 支持）

## 相关项目

- [selfspy](https://github.com/gurgeh/selfspy) - 记录你在电脑上的一切操作
- [arbtt](http://freecode.com/projects/arbtt) - 基于规则的自动时间追踪器

---

*数据获取自 https://github.com/karpathy/ulogme (2026-05-09)*