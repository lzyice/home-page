# CLAUDE.md

此文件为 Claude Code (claude.ai/code) 在此代码库中工作时提供指导。

## 项目概述

这是一个基于 HTML5 UP "Dimension" 模板构建的静态个人主页网站。该网站作为个人落地页，具有基于模态框的导航和响应式设计。

## 架构设计

### 核心组件
- **单页应用程序**: 使用基于哈希的路由来显示/隐藏内容部分作为模态框覆盖层
- **模态框系统**: 文章以覆盖层形式显示，背景元素具有模糊/缩放过渡效果
- **响应式框架**: 基于 skel.min.js 构建，用于断点管理和响应式行为
- **jQuery 插件**: `js/util.js` 中的自定义实用函数提供面板管理、占位符 polyfill 和触摸交互

### 文件结构
```
/
├── index.html          # 包含导航和文章内容的主页面
├── css/main.css        # 包含响应式断点的主样式表
├── js/main.js          # 模态框过渡和导航的核心应用逻辑
├── js/util.js          # jQuery 实用插件 (panel, placeholder, prioritize)
├── images/             # 包括背景和作者图片的静态资源
├── CNAME              # GitHub Pages 域名配置 (www.uuid.win)
└── ads.txt            # Google AdSense 验证
```

### 关键 JavaScript 架构
- **主导航逻辑** (`js/main.js`): 处理文章显示/隐藏过渡、键盘导航 (ESC) 和滚动管理
- **实用插件** (`js/util.js`): 提供 `$.fn.panel()` 用于模态框行为，`$.fn.placeholder()` 用于表单 polyfill，以及 `$.prioritize()` 用于响应式元素重排序
- **响应式断点**: 在 main.js 中使用 skel 框架定义
  - xlarge: 1680px
  - large: 1280px  
  - medium: 980px
  - small: 736px
  - xsmall: 480px
  - xxsmall: 360px

### 内容保护功能
index.html 中嵌入的 JavaScript 阻止:
- 右键上下文菜单 (文本输入框除外)
- 复制/粘贴操作 (文本输入框除外)
- 文本选择 (文本输入框除外)
- 剪切操作 (文本输入框除外)

## 开发工作流

### 部署
这是一个通过 GitHub Pages 部署到 www.uuid.win 的静态网站。推送到 master 分支时会自动部署更改。

### 测试更改
由于这是一个没有构建过程的静态 HTML/CSS/JS 网站:
1. 直接在浏览器中打开 `index.html` 进行本地测试
2. 使用浏览器开发工具测试响应式行为
3. 验证模态框过渡和键盘导航是否正常工作

### 内容更新
- **个人信息**: 编辑 `index.html` 中 `<article>` 标签内的内容部分
- **导航链接**: 修改 `index.html` 中的 `<nav>` 部分
- **样式**: 更新 `css/main.css` 进行视觉更改
- **背景**: 替换 `images/bg.jpg` 更改背景图片

### Google AdSense
- 账户 ID: ca-pub-5333475055223576 (在 index.html meta 标签和 ads.txt 中配置)
- Ads.txt 文件已正确配置用于 Google AdSense 验证

## 重要说明

### 浏览器兼容性
- 使用 CSS3 功能 (flexbox, transforms, filters)
- 包含 IE9 专用样式表 (`css/ie9.css`)
- util.js 中的占位符 polyfill 用于旧浏览器支持
- 处理移动触摸事件用于滑动交互

### 内容安全
该网站实现了客户端内容保护以防止轻易复制，但这不能替代服务器端安全措施。