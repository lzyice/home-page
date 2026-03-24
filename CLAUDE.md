# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

基于 HTML5 UP "Dimension" 模板的静态个人主页，通过 GitHub Pages 部署到 www.uuid.win。推送到 master 分支自动部署，无构建步骤。多个 git remote（origin、gitea、gongfeng）。

本地测试：直接在浏览器中打开 `index.html`，无需本地服务器。

## 外部依赖

所有 JS/CSS 依赖通过外部 CDN 加载，本地不打包：
- **jQuery 4.0.0**：`code.jquery.com`（`js/jquery.min.js.bak` 是旧版 1.11.3 备份）
- **Font Awesome 6.7.2**：`s4.zstatic.net`，使用 v6 类名（`fa-brands fa-facebook` 而非旧版 `fa fa-facebook`）
- **Google Fonts**：Source Sans Pro（300/600 + italic）

## JS 文件职责

- **`js/main.js`**：核心逻辑——模态框状态机、哈希路由、事件绑定（依赖 jQuery）
- **`js/util.js`**：jQuery 插件集——`placeholder` polyfill（被 `main.js` 调用）、`panel`/`navList`/`prioritize`（模板预置，当前未使用）

## 页面加载流程

`#wrapper` 初始 `opacity:0` → jQuery `$(document).ready` 后 CSS transition 淡入 → `is-loading` 类在 `window.load` 后 100ms 移除，启用动画。`js/util.js` 和 `js/main.js` 均使用 `defer` 加载。

## 模态框架构

### 状态机（CSS 类）
`js/main.js` 通过给 `<body>` 添加 CSS 类管理页面状态：
- `is-loading`：页面加载中（禁用动画），100ms 后移除
- `is-article-visible`：文章模态框已打开（背景模糊/缩放）
- `is-switching`：正在切换文章（跳过延迟）

### 哈希路由
URL hash 直接映射到文章 ID：`#about` → `<article id="about">`。`hashchange` 事件驱动显示/隐藏。

### 过渡锁
`locked` 变量防止快速连续触发过渡动画，延迟为 325ms。已锁定时跳过延迟直接切换（`is-switching` 状态）。

### 关闭文章的方式
1. 点击文章区域外部（`body` 的 click 冒泡）
2. 按 ESC 键（keyCode 27）
3. 点击动态注入的 `.close` div（设置 `location.hash = ''`）

### 导航对齐
当导航项为偶数时，`<nav>` 自动添加 `use-middle` 类，中间项添加 `is-middle` 类，用于居中对齐样式。

## 内容修改

- **个人信息**：`index.html` 中 `<article id="about">` 内
- **导航链接**：`index.html` 中 `<nav>` 的 `<ul>` 内；外链加 `target="_blank"`，内部模态框用 `href="#id"`
- **背景图片**：替换 `images/bg.jpg`
- **样式**：`css/main.css`（IE9 兼容样式在 `css/ie9.css`）

## 内容保护

`index.html` 末尾内联 JS 禁用了右键菜单、复制、粘贴、剪切、文本选择（文本输入框内仍允许）。修改这部分时注意保持文本框例外逻辑。
