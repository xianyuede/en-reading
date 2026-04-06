# Xianyue Reader (沉浸式英文原版阅读器)

## 📌 项目背景 (Project Context)
本项目是一个专为高强度英文原版阅读打造的极简、纯静态 Web 阅读器。
由于传统阅读平台（如 Kindle、微信读书、PDF 阅读器）在跨端体验、排版控制和划词翻译上存在严重摩擦力，本项目旨在彻底消除这些阻力。
阅读器专为 **手机端 + Arc 浏览器沉浸模式 + 欧路词典长按划词** 工作流优化，主打“零干扰、秒开、全权掌控”。

## 🏗 技术栈与架构 (Tech Stack & Architecture)
本项目采用极客风格的 **纯静态架构 (Vanilla Web)**，零构建工具，无后端数据库。
- **前端:** HTML5, Vanilla CSS (CSS Variables), Vanilla JavaScript.
- **数据层:** 依赖本地静态 `.json` 文件作为伪数据库（拉取配置）+ `.html` 文件作为书籍内容。
- **持久化:** 强依赖浏览器的 `localStorage` 保存阅读进度和主题偏好。
- **部署流:** GitHub 托管代码 -> Cloudflare Pages 自动化零配置部署 (绑定自定义域名)。

## 📁 目录结构 (Directory Structure)
整个应用围绕核心的三个 HTML 页面和 `books/` 目录下的 JSON 配置展开。

```text
xianyue-reader/
├── index.html          # [View] 首页：书架展示 (加载 catalog.json)
├── book.html           # [View] 目录页：书籍章节列表 (加载对应书籍的 toc.json)
├── reader.html         # [View] 阅读页：核心沉浸区 (加载具体 html 章节并处理 localStorage)
├── assets/
│   └── style.css       # [Style] 全局排版、响应式设计与多主题控制
└── books/
    ├── catalog.json    # [Data] 全局书架数据库 (记录所有书籍基础信息)
    └── sapiens/        # [Data] 单本书籍文件夹 (以书名/ID命名)
        ├── cover.jpg   # 书籍本地封面
        ├── toc.json    # 该书的目录数据表 (关联章节标题与 HTML 文件名)
        ├── ch01.html   # 纯净的章节正文 (从 EPUB 解压提取)
        └── ch02.html
        
