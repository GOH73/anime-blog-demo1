# CLAUDE.md

此文件为 Claude Code (claude.ai/code) 在本仓库中工作时提供指导。

## 项目概述

这是一个基于 **Hexo** (v7.3.0) 静态网站生成器构建的动漫主题博客。使用 **hexo-theme-redefine** 主题（本地命名为 "defaultone"），具有动漫特色功能，包括 Live2D 角色动画和 particles.js 背景粒子效果。

## 开发命令

### 核心命令
- `npm run server` 或 `hexo server` - 启动本地开发服务器（默认：http://localhost:4000）
- `npm run build` 或 `hexo generate` - 生成静态文件到 `public/` 目录
- `npm run clean` 或 `hexo clean` - 清理生成的文件和缓存
- `npm run deploy` 或 `hexo deploy` - 部署到配置的平台

### 内容管理
- `hexo new post "标题"` - 在 `source/_posts/` 创建新文章
- `hexo new draft "标题"` - 在 `source/_drafts/` 创建新草稿
- `hexo new page "标题"` - 创建新页面

## 架构

### 双层配置系统

本项目使用 Hexo 标准的双层配置结构：

1. **根配置** (`_config.yml`)：站点级别设置
   - 站点元数据（标题、作者、URL）
   - 目录结构（source、public、theme）
   - Hexo 行为（永久链接、分页、生成器）
   - Live2D 小部件配置（模型、位置、显示设置）
   - 激活的主题：`theme: defaultone`

2. **主题配置** (`themes/defaultone/_config.yml`)：主题专属设置
   - 视觉样式（颜色、字体、布局）
   - 首页横幅配置（背景图片、标题、副标题）
   - 导航栏链接和搜索设置
   - 文章渲染（目录、代码块、版权声明、懒加载）
   - 评论系统（Waline、Gitalk、Twikoo、Giscus）
   - 插件（RSS、APlayer、Mermaid）
   - 特效设置（`effects.particles: true`、`effects.cursoreffects: true`）

### 内容结构

- `source/_posts/` - 已发布的博客文章（Markdown 格式）
- `source/_drafts/` - 草稿文章（未发布）
- `source/_data/` - 数据文件（links.yml、masonry.yml）
- `source/about/`、`source/links/`、`source/tags/`、`source/masonry/` - 特殊页面
- `scaffolds/` - 新内容模板（post.md、draft.md、page.md）

### 主题架构 (themes/defaultone)

主题使用 **Hexo 脚本插件系统**：

- `scripts/filters/` - 内容处理过滤器（懒加载、图片处理、加密、链接/表格处理）
- `scripts/events/` - 事件处理器（欢迎信息、404 页面）
- `scripts/modules/` - 自定义 Markdown 标签（note、btn、tabs、folding）
- `scripts/helpers/` - 模板助手（theme、page、meta、recommendation、Waline）
- `scripts/config-export.js` - 导出主题配置到前端
- `scripts/data-handle.js` - 处理数据文件

布局系统：
- `layout/` - EJS 模板（layout.ejs、post.ejs、index.ejs、archive.ejs 等）
- `layout/components/` - 可复用组件（header、footer、sidebar、comments、plugins）
- `layout/pages/` - 页面专属模板（home、tags、friends）
- `layout/utils/` - 实用工具模板（paginator、search、image-viewer）

### 关键依赖

- **hexo-helper-live2d** - Live2D 角色小部件
- **live2d-widget-model-*** - 角色模型（chitose、gf、wanko）
- **particles.js** - 背景粒子效果
- **cursor-effects** - 交互式光标动画
- **hexo-renderer-marked** - Markdown 渲染
- **hexo-renderer-ejs** - 模板渲染
- **hexo-renderer-stylus** - CSS 预处理

## 重要配置说明

### Live2D 配置
Live2D 设置位于根目录 `_config.yml` 的 `live2d:` 键下。模型选择：`model.use: live2d-widget-model-wanko`（可切换为 chitose 或 gf）。

### 主题特效
粒子和光标效果在主题配置中控制：
```yaml
effects:
  particles: true
  cursoreffects: true
```

### 单页体验
主题使用 Swup.js 实现 SPA 式导航（`global.single_page: true`），类似于 pjax。

### 评论系统
支持多个评论系统但默认禁用。在主题配置的 `comment:` 部分启用。可选：waline、gitalk、twikoo 或 giscus。

## 构建流程

主题有自己的构建流程（在 `themes/defaultone/package.json` 中）：
- `npm run build:css` - 构建 Tailwind CSS
- `npm run build:js` - 使用 Terser 压缩 JavaScript
- 这些是主题开发命令，常规博客使用不需要

## 测试文章

使用 `source/_posts/` 中的示例文章进行测试：
- `hello-world.md` - Hexo 默认欢迎文章
- `m3u8.md` - 自定义内容
- `study.md` - 自定义内容

## 部署

配置为 EdgeOne Pages 部署。构建输出目录为 `./public`，构建命令为 `npm run build`。
