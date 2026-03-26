# Yasen Jia 个人主页 - 项目说明

> 这是一个基于 Hugo + HugoBlox 的学术简历网站项目

---

## 项目简介

本项目是 **Yasen Jia (贾亚森)** 的个人学术主页，用于展示个人简介、研究项目、发表论文、获奖经历等内容。

### 基本信息

| 项目 | 内容 |
|------|------|
| 作者 | Yasen Jia (贾亚森) |
| 身份 | 北京理工大学 智能机器人专业 研究生 |
| 导师 | 黄岩教授 |
| 研究方向 | 机器人学习、强化学习、腿式机器人控制 |
| 站点地址 | https://lupinjia.github.io |

### 功能特性

- **响应式设计**: 适配桌面端和移动端
- **多主题支持**: 支持亮色/暗色/跟随系统模式
- **内置搜索**: Pagefind 全文搜索功能
- **SEO 优化**: 自动生成 sitemap 和 meta 标签
- **自动部署**: 推送代码自动部署到 GitHub Pages
- **多媒体支持**: 支持视频、图片、PDF 嵌入

---

## 目录结构

```
lupinjia.github.io/
├── .github/
│   └── workflows/
│       └── publish.yaml          # GitHub Actions 自动部署
│
├── config/
│   └── _default/
│       ├── hugo.yaml            # Hugo 核心配置
│       ├── params.yaml          # 站点参数
│       ├── menus.yaml           # 导航菜单
│       ├── languages.yaml       # 多语言配置
│       └── module.yaml          # 模块依赖
│
├── content/
│   ├── _index.md                # 首页配置
│   ├── blog.md                  # 博客列表页
│   ├── experience.md            # 经历页面
│   ├── projects.md              # 项目页面
│   ├── authors/
│   │   └── _index.md            # 作者列表页
│   ├── post/
│   │   ├── _index.md            # 新闻列表页
│   │   ├── 20250819/            # TRON Camp 2025
│   │   ├── 20250712/            # ETH 机器人夏校
│   │   ├── 20240703/            # 优秀毕业生
│   │   └── 20231218/            # Bilibili 总结
│   ├── blog/
│   │   ├── _index.md            # 博客列表页
│   │   ├── hello-world/         # 博客介绍
│   │   └── rl-tutorial/         # 强化学习教程
│   ├── project/
│   │   ├── _index.md            # 项目列表页
│   │   ├── LeggedGym-Ex/        # 腿式机器人训练框架
│   │   ├── RoboStack/           # 机器人技术栈
│   │   ├── music_player_page/   # 音乐播放器页面
│   │   ├── Quadruped Robot Parkour/
│   │   ├── Learning Robust Quadrupedal and Bipedal Locomotion/
│   │   └── Design and Learning-based Control of Agile-PF/
│   └── publication/
│       ├── _index.md            # 论文列表页
│       └── icarm2024/           # ICARM 2024 论文
│
├── data/
│   └── authors/
│       └── me.yaml              # 个人详细信息
│
├── static/
│   └── uploads/                 # 静态文件上传目录
│       ├── 贾亚森_简历.pdf
│       ├── yasenjia_cv_europass.pdf
│       └── Effects_of_Prior_Knowledge_...pdf
│
├── docs/                        # 项目文档
│   ├── design.md                # 设计文档
│   ├── README.md                # 本文件
│   └── blog-guide.md            # 博客使用指南
│
├── resources/                   # Hugo 生成资源
├── hugoblox.yaml               # HugoBlox 版本配置
├── go.mod                      # Go 模块配置
└── README.md                   # 项目根说明
```

---

## 本地开发

### 环境要求

- **Hugo**: v0.153.0 或更高 (extended 版本)
- **Node.js**: v20 或更高
- **Git**: 任意版本

### 安装依赖

#### 1. 安装 Hugo

**macOS:**
```bash
brew install hugo
```

**Windows:**
```powershell
# 使用 Chocolatey
choco install hugo-extended

# 或使用 Scoop
scoop install hugo-extended
```

**Linux:**
```bash
# 下载对应版本
wget https://github.com/gohugoio/hugo/releases/download/v0.153.0/hugo_extended_0.153.0_linux-amd64.deb
sudo dpkg -i hugo_extended_0.153.0_linux-amd64.deb
```

#### 2. 安装 Node.js 依赖

```bash
npm install
```

#### 3. 初始化 Hugo 模块

```bash
hugo mod get -u
hugo mod tidy
```

### 启动开发服务器

```bash
hugo server -D
```

参数说明:
- `-D`: 包含草稿内容
- `--bind 0.0.0.0`: 允许外部访问
- `-p 1313`: 指定端口 (默认 1313)

访问 http://localhost:1313 查看站点。

### 构建生产版本

```bash
hugo --minify
```

构建后的文件在 `public/` 目录。

---

## 内容管理

### 添加新博客文章

博客与新闻是分开的：
- **博客**: 技术文章、教程、学习笔记（位于 `content/blog/`）
- **新闻**: 个人动态、获奖、参加活动（位于 `content/post/`）

1. 创建博客目录:
```bash
mkdir content/blog/my-article-title
```

2. 创建 `index.md`:
```markdown
---
title: "文章标题"
summary: "文章摘要"
date: 2026-03-26
authors:
  - me
categories:
  - 技术
tags:
  - 标签1
---

正文内容...
```

详细说明见 [博客使用指南](./blog-guide.md)。

### 添加新新闻动态

1. 创建新目录:
```bash
mkdir content/post/20260101
```

2. 创建 `index.md`:
```markdown
---
title: "新闻标题"
summary: "简短摘要"
date: 2026-01-01
authors:
  - me
tags:
  - 标签1
  - 标签2
---

正文内容...
```

### 添加新项目

1. 创建项目目录:
```bash
mkdir "content/project/My New Project"
```

2. 添加封面图 `featured.png/jpg`

3. 创建 `index.md`:
```markdown
---
title: "项目名称"
date: 2026-01-01
links:
  - type: site
    url: https://github.com/...
tags:
  - 标签
---

项目描述...
```

### 添加新论文

1. 创建目录:
```bash
mkdir content/publication/conference2025
```

2. 添加 `featured.png` 作为论文封面

3. 创建 `index.md`:
```markdown
---
title: "论文标题"
authors:
  - 作者1
  - me
date: "2025-01-01"
doi: "10.xxxx/xxxxx"
publication_types: ['conference']
publication: "会议名称"
abstract: |
  摘要内容...
---
```

### 更新个人信息

编辑 `data/authors/me.yaml`:

```yaml
name:
  display: 显示名称
role: 职位
bio: |
  个人简介（支持 Markdown）

affiliations:
  - name: 机构名称
    url: https://...

links:
  - icon: brands/github
    url: https://github.com/...

skills:
  - name: 技能分类
    items:
      - name: 技能名称
        description: 描述

awards:
  - title: 奖项名称
    date: '2025-01-01'
```

---

## 部署流程

### 自动部署

项目配置了 GitHub Actions，推送代码到 `main` 分支会自动触发部署:

```bash
git add .
git commit -m "更新内容"
git push origin main
```

部署完成后，访问 https://lupinjia.github.io 查看更新。

### 手动部署

如果需要手动部署:

1. 构建站点:
```bash
hugo --minify
```

2. 生成搜索索引:
```bash
npx pagefind --site "public"
```

3. 部署 `public/` 目录到任意静态托管服务。

---

## 常用命令

| 命令 | 说明 |
|------|------|
| `hugo server -D` | 启动开发服务器 |
| `hugo server --bind 0.0.0.0` | 允许局域网访问 |
| `hugo --minify` | 构建生产版本 |
| `hugo new content/post/new-post/index.md` | 创建新内容 |
| `hugo mod get -u` | 更新模块 |
| `hugo mod tidy` | 清理模块 |
| `npx pagefind --site "public"` | 生成搜索索引 |

---

## 配置说明

### 站点配置 (`config/_default/hugo.yaml`)

```yaml
title: Yasen Jia              # 站点标题
baseURL: 'https://example.com/' # 站点地址
defaultContentLanguage: en    # 默认语言
pagination:
  pagerSize: 10               # 每页显示数量
```

### 站点参数 (`config/_default/params.yaml`)

```yaml
appearance:
  mode: system                # 主题模式: light/dark/system
  color: rose                 # 主题颜色

marketing:
  seo:
    site_type: Person         # 站点类型
    description: '站点描述'
  analytics:
    google_analytics: 'G-xxx' # Google Analytics ID

header:
  navbar:
    show_search: true         # 显示搜索
    show_theme_chooser: true  # 显示主题切换
```

### 导航菜单 (`config/_default/menus.yaml`)

```yaml
main:
  - name: Bio                 # 菜单名称
    url: /                    # 链接地址
    weight: 10                # 排序权重
```

---

## 主题定制

### 修改颜色

编辑 `config/_default/params.yaml`:

```yaml
appearance:
  color: blue                 # 可选: blue, red, green, rose, etc.
```

### 修改首页区块

编辑 `content/_index.md`，修改 `sections` 配置:

```yaml
sections:
  - block: resume-biography-3
    content:
      username: me
  - block: collection
    content:
      title: Recent News
```

### 自定义 CSS

创建 `assets/css/custom.css`:

```css
/* 自定义样式 */
.custom-class {
  color: #ff0000;
}
```

---

## 故障排除

### 构建失败

1. **检查 Hugo 版本**:
```bash
hugo version  # 需要 extended 版本
```

2. **更新模块**:
```bash
hugo mod get -u
hugo mod tidy
```

3. **清除缓存**:
```bash
rm -rf resources/
hugo server -D
```

### 搜索功能不工作

确保构建后生成了搜索索引:
```bash
npx pagefind --site "public"
```

### 图片不显示

- 检查图片路径是否正确
- 确保图片放在正确的目录 (`content/.../featured.jpg`)
- 清除浏览器缓存

### 部署后未更新

1. 检查 GitHub Actions 状态
2. 确保推送到 `main` 分支
3. 等待 1-2 分钟让部署完成
4. 清除浏览器缓存或使用无痕模式

---

## 参考资源

### 官方文档

- [Hugo 官方文档](https://gohugo.io/documentation/)
- [HugoBlox 文档](https://docs.hugoblox.com/)
- [HugoBlox 区块参考](https://docs.hugoblox.com/reference/blocks/)

### 主题相关

- [Academic CV 主题](https://github.com/HugoBlox/theme-academic-cv)
- [HugoBlox 模板](https://hugoblox.com/templates/)

### 社区支持

- [Hugo 论坛](https://discourse.gohugo.io/)
- [HugoBlox Discord](https://discord.gg/z8wNYzb)

---

## 更新日志

### 2026-03-26
- 创建项目文档
- 完善设计文档和说明文档

### 2025-08-19
- 添加 TRON Camp 2025 获奖新闻

### 2025-07-12
- 添加 ETH 机器人夏校经验

### 2025-03-16
- 添加多个项目页面
- 更新简历文件

### 2024-10-18
- 发布 ICARM 2024 论文

### 2024-09-24
- 初始站点搭建

---

## 许可证

本项目使用 [Hugo Academic CV Theme](https://github.com/HugoBlox/theme-academic-cv)，遵循 MIT 许可证。

站点内容版权归 Yasen Jia 所有。

---

## 联系方式

如有问题或建议，欢迎通过以下方式联系:

- 📧 邮箱: jiayasen021003@gmail.com
- 🐙 GitHub: [@lupinjia](https://github.com/lupinjia)
- 🎓 Google Scholar: [Yasen Jia](https://scholar.google.com/citations?user=jimch4UAAAAJ)
