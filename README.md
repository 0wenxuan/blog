# Owen 的个人博客

一个不需要 Node.js、npm 或前端框架的 Jekyll 静态博客，构建和发布都交给 GitHub Actions。

- **站点地址**：https://0wenxuan.github.io/blog/
- **仓库**：https://github.com/0wenxuan/blog
- **本地需要的东西**：只有一个 Git。写文章不需要安装 Ruby、Jekyll、Node.js 或 npm。

## 文件都在哪

```text
_config.yml                        站点标题、作者、网址、baseurl
index.html                         首页（个人介绍 + 文章列表 + 项目卡片）
about.md                           关于我
_layouts/default.html              全站框架：导航、页脚
_layouts/post.html                 文章页框架
_posts/*.md                        所有文章
assets/style.css                   全站样式与配色
.github/workflows/pages.yml        自动构建并发布到 GitHub Pages
```

## 写一篇新文章

在 `_posts/` 中复制示例文章，文件名使用：

```text
YYYY-MM-DD-title.md
```

文章开头保留 Front Matter：

```yaml
---
layout: post
title: 文章标题
date: 2026-10-08
excerpt: 一句话摘要
tags:
  - 学习
---
```

第二个 `---` 之后直接写 Markdown 正文：标题、段落、列表、链接、代码块都可以使用。

## 发布流程

1. 修改或新增 `_posts/*.md`。
2. 修改首页内容时编辑 `index.html`。
3. 修改关于页时编辑 `about.md`。
4. 修改配色和排版时编辑 `assets/style.css`。
5. 在浏览器中检查文件内容和链接。
6. `git diff` 检查变更。
7. `git add`、`git commit`、`git push`。
8. GitHub Actions 自动运行 Jekyll，将 Markdown 编译成 HTML 并发布到 GitHub Pages。

## 启用 Pages

`actions/configure-pages` 默认会尝试自动开启 Pages，多数情况下第一次推送就能生效。如果 workflow 报 Pages 相关的错误，手动在仓库里设置一次：

```text
Settings → Pages → Source → GitHub Actions
```

之后每次推送到 `main`，workflow 都会重新生成网站。

## 它是怎么工作的

```text
Markdown 文章
      ↓
Jekyll / GitHub Actions
      ↓
HTML 页面
      ↓
GitHub Pages URL
```

不需要在本地安装 Ruby、Jekyll、Node.js 或 npm。构建发生在 GitHub Actions 上。

注意：仓库里的 `index.html` 是 Jekyll 模板源码，双击本地文件看不到最终页面；最终 HTML 由 GitHub Actions 生成。

## Agent 提示词

```text
/goal 这是一个 Jekyll 静态博客项目，仓库是 0wenxuan/blog，发布地址 https://0wenxuan.github.io/blog/。
请先读取 README、_config.yml、index.html、_layouts 和 _posts。
以后新增文章时，只在 _posts/ 中创建 YYYY-MM-DD-title.md，并使用现有 Front Matter 和 layout: post。
不要引入 React、Vue、Node.js、npm、外部 CDN 或新的构建工具。
修改前先列出文件和计划；修改后检查 Markdown Front Matter、文章链接、相对资源路径和 Git diff。
我确认目标仓库后，才执行 git commit 和 git push。
```
