# 🎯 鸿渚资源分享站

一个基于 **Markdown + GitHub Pages** 的现代化、纯静态、多类型资源分享网站。支持网页推荐、软件下载、文件分享和技术文章四种资源类型，并可集成付费功能。

**在线演示：** `https://watchfleeting.github.io/starsea-shares/`

---

## ✨ 核心特性

-   **📂 纯静态架构**：无需服务器与数据库，完全依赖 GitHub Pages 免费托管。
-   **📝 Markdown 驱动**：所有内容（资源卡片、文章、文件详情）均通过 Markdown 文件管理，易于编写与维护。
-   **🔗 多资源类型**：清晰区分**网页分享**、**软件分享**、**文件分享**和**文章分享**。
-   **🎨 现代化 UI**：响应式设计，支持深色/浅色主题，拥有平滑的交互动画与毛玻璃效果。
-   **💰 付费功能就绪**：可集成 PayPal，支持数字商品售卖与内容解锁（需自行配置）。
-   **⚡ 性能优异**：快速的加载速度与流畅的浏览体验。

---

## 🚀 快速开始

### 1. 获取项目
将项目代码部署到你的 GitHub 仓库。你可以选择：
- **Fork** 本模板仓库。
- 或直接**下载源码**，上传到你自己的新仓库。

### 2. 启用 GitHub Pages
1.  进入仓库的 **Settings**（设置）页面。
2.  在左侧边栏中选择 **Pages**（页面）。
3.  在 **Source**（来源）部分，选择 `Deploy from a branch`（从分支部署）。
4.  在 **Branch**（分支）部分，选择你的主分支（如 `main` 或 `master`），文件夹选择 `/(root)`（根目录）。
5.  点击 **Save**（保存）。稍等片刻，你的网站就会在 `https://<你的用户名>.github.io/<仓库名>` 上线。

### 3. 初始化本地内容
按照下文 **“📁 项目结构”** 和 **“📝 内容管理”** 章节的说明，创建并修改示例 Markdown 文件和 `data-index.json` 索引。

---

## 📁 项目结构

```
你的仓库根目录/
├── index.html                 # 网站唯一的主页面
├── data-index.json            # 核心索引文件，列出所有需加载的.md文件
├── README.md                  # 本说明文件
├── success.html               # （可选）支付成功跳转页面
│
├── data/                      # 所有内容数据
│   ├── cards/                 # 资源卡片定义（一个.md文件对应一张首页卡片）
│   │
│   ├── articles/              # 完整文章内容（由文章卡片调用）
│   │
│   └── files/                 # 文件分享详情（由文件卡片调用）
│
└── assets/                    # 静态资源（图片、文件等）
    └── covers/                # 卡片封面图片
```

---

## 📝 内容管理：一切皆 Markdown

所有内容都通过编写 Markdown 文件来创建。每个 `.md` 文件都包含 **YAML 前置元数据（Front Matter）** 和正文内容。

### 1. 资源卡片 (`data/cards/` 目录下)
每个文件定义首页上的一张卡片。

**文件名示例：** `01_my_resource.md`
````yaml
---
# 基础信息
id: 1
title: "资源名称"
description: "关于这个资源的一段详细描述。"
category: "分类名称"
type: "web" # 类型：web(网页)/software(软件)/file(文件)/article(文章)
icon: "fas fa-globe" # FontAwesome 图标类名

# 展示信息
tags: ["热门", "推荐"]
author: "鸿渚"
date: "2025-01-20"
cover: "/assets/covers/cover.jpg" # 卡片背景图URL

# --- 类型专属字段（根据上述 type 选择填写）---
# 类型为 ‘web‘ 或 ‘software’ 时填写：
url: "https://example.com"

# 类型为 ‘article‘ 时填写：
contentRef: "data/articles/my-article.md"

# 类型为 ‘file‘ 时填写：
fileRef: "data/files/my-file-details.md"

# --- 付费功能字段（可选）---
price: 9.99
currency: "USD"
is_paid: true
paypal_button_id: "YOUR_BUTTON_ID"
---

（这里是卡片的备注区，可为空。主页不会显示这里的内容。）
````

### 2. 完整文章 (`data/articles/` 目录下)
当用户点击类型为 `article` 的卡片时，会展示对应文件的内容。

**文件名示例：** `my-article.md`
````yaml
---
id: "article-1"
title: "文章标题"
author: "作者"
date: "2025-01-20"
readTime: "10分钟阅读"
tags: ["教程", "Markdown"]
---

# 这里是文章的正文

使用标准的 **Markdown 语法** 来书写你的精彩内容。

## 二级标题
- 列表项
- 另一个列表项

> 一段引人深思的引用。

```javascript
// 支持代码高亮
console.log("Hello, World!");
```

![图片描述](/assets/covers/example.jpg)
````

### 3. 文件详情 (`data/files/` 目录下)
当用户点击类型为 `file` 的卡片时，会展示对应文件的下载信息和详情。

**文件名示例：** `my-file-details.md`
````yaml
---
id: "file-1"
title: "文件展示标题"
fileName: "ultimate-resources.zip"
fileSize: "215 MB"
fileType: "zip"
downloadUrl: "https://your-cdn.com/file.zip" # 文件的实际下载直链
password: "" # 解压密码（如有）
description: "这里是文件的详细描述和使用说明。"
---

## 🗂️ 内容清单
- 具体包含哪些资源...
- 使用教程...

## ⚠️ 注意事项
- 使用前请确认...
- 兼容性说明...
````

### 4. 更新索引 (`data-index.json`)
**重要！** 每当你新增了 `.md` 文件，都必须在根目录的 `data-index.json` 文件中注册它的路径。

```json
{
  "cards": [
    "data/cards/01_nhentai.md",
    "data/cards/02_ehviewer.md",
    "data/cards/03_design_resources.md",
    "data/cards/04_ai_painting.md",
    "data/cards/05_your_new_card.md" // 在此处添加新卡片路径
  ],
  "articles": [
    "data/articles/ai-painting-guide.md"
    // 在此处添加新文章路径
  ],
  "files": [
    "data/files/design-resources-details.md"
    // 在此处添加新文件详情路径
  ]
}
```

---

## ⚙️ 付费功能配置（可选）

本项目已预留 PayPal 集成接口，实现付费内容解锁。以下是简明的配置路径：

### 路径概览

| 交付方式       | 复杂度 | 自动化程度 | 推荐场景         |
| -------------- | ------ | ---------- | ---------------- |
| **手动交付**   | ⭐☆☆☆☆ | 手动       | 初期测试，低频   |
| **兑换码系统** | ⭐⭐☆☆☆ | 半自动     | 小型内容，低成本 |
| **自动交付**   | ⭐⭐⭐⭐☆ | 全自动     | 正式运营，重体验 |

### 基础步骤
1.  **获取 PayPal 按钮ID**：在 [PayPal商家平台](https://www.paypal.com/buttons/) 创建“立即购买”按钮，并获取其 `hosted_button_id`。
2.  **标记付费资源**：在对应卡片的 Markdown 元数据中设置 `is_paid: true`、`price` 及 `paypal_button_id`。
3.  **配置成功页面**：在 PayPal 按钮设置中，将“返回URL”指向你部署好的 `success.html`。
4.  **选择交付方式**：
    - **手动交付**：用户支付后，你通过 PayPal 通知邮件获取买家信息，手动发送资源。
    - **进阶自动化**：可通过无服务器函数（如 Vercel）验证支付，并自动发放兑换码或生成云存储临时下载链接。

> **安全提示**：切勿在前端代码中暴露真实下载链接或 API 密钥。

---

## 🎨 自定义与扩展

-   **修改网站信息**：直接编辑 `index.html` 文件中的 `<title>` 和 `<header>` 部分。
-   **调整主题颜色**：在 `index.html` 的 `<style>` 标签内修改 `:root` 下的 CSS 变量，如 `--color-web`、`--color-software` 等。
-   **添加新资源类型**：需要在 `index.html` 的 JavaScript 逻辑和 CSS 样式中同时添加对新类型的支持。

---

## ❓ 常见问题 (FAQ)

**Q: 为什么我新加的卡片没有显示在首页？**
A: 请按顺序检查：1. 确保 `data-index.json` 中已添加了新卡片的路径；2. 检查 Markdown 文件的 YAML 格式是否正确（以 `---` 开始和结束）；3. 尝试清除浏览器缓存后刷新（Ctrl+F5 或 Cmd+Shift+R）。

**Q: 网站流量和存储有限制吗？**
A: GitHub Pages 每月有 100GB 带宽和 1GB 存储空间的限制。如果分享大型文件，强烈建议使用第三方对象存储服务（如阿里云OSS、Backblaze B2），并将 `downloadUrl` 指向该服务提供的链接。

**Q: 如何备份我的内容？**
A: 整个 `data/` 目录包含了你的所有核心内容，定期备份此目录和 `data-index.json` 文件即可。

---

## 📄 许可证

本项目采用 [MIT 许可证](LICENSE)。您可以自由地使用、修改和分发此项目。

---

## 🤝 贡献与支持

欢迎提交 Issue 和 Pull Request 来改进项目！
如果您觉得这个项目有帮助，请给它一个 ⭐ Star，这是对开发者最大的鼓励。

**遇到问题？**
- 请先查阅本文件及代码注释。
- 通过 GitHub Issues 提交问题。

- 如需安全漏洞报告，请通过邮件私下联系。

