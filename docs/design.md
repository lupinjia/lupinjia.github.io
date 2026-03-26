# Yasen Jia 个人主页设计文档

> 文档版本: 1.0  
> 创建日期: 2026-03-26  
> 项目: lupinjia.github.io

---

## 1. 系统架构

### 1.1 技术栈

```
┌─────────────────────────────────────────────────────────────┐
│                        前端呈现层                            │
│  Hugo Static Site + HugoBlox Theme + TailwindCSS           │
└─────────────────────────────────────────────────────────────┘
                            │
┌─────────────────────────────────────────────────────────────┐
│                        内容管理层                            │
│  Markdown + YAML Front Matter + Hugo Templates             │
└─────────────────────────────────────────────────────────────┘
                            │
┌─────────────────────────────────────────────────────────────┐
│                        部署层                                │
│  GitHub Actions → GitHub Pages                             │
└─────────────────────────────────────────────────────────────┘
```

| 组件 | 技术 | 版本/说明 |
|------|------|-----------|
| 静态站点生成器 | Hugo | 0.153.0 (extended) |
| 主题框架 | HugoBlox | Academic CV Theme |
| CSS 框架 | TailwindCSS | 3.x |
| 搜索索引 | Pagefind | 自动构建 |
| 包管理 | Go Modules | hugo modules |
| 部署 | GitHub Pages | 自动 CI/CD |

### 1.2 架构特点

- **静态生成**: 使用 Hugo 生成纯静态 HTML，无需后端服务器
- **模块化主题**: 基于 HugoBlox 的模块化区块系统，灵活配置页面
- **响应式设计**: TailwindCSS 提供移动端友好的响应式布局
- **自动部署**: GitHub Actions 实现推送即部署

---

## 2. 页面结构

### 2.1 站点地图

```
/
├── /                          # 首页 (Landing Page)
│   ├── Biography Section      # 个人简介 + 头像
│   ├── Recent News            # 最新动态
│   └── Recent Publications    # 最近论文
│
├── /experience/               # 经历页面
│   ├── Resume Experience      # 工作经历
│   ├── Skills & Hobbies       # 技能与爱好
│   └── Awards                 # 获奖记录
│
├── /projects/                 # 项目页面
│   └── Selected Projects      # 项目列表 (网格布局)
│
├── /post/                     # 新闻/博客
│   ├── TRON Camp 2025
│   ├── 优秀毕业生
│   └── ...
│
└── /publication/              # 论文发表
    └── ICARM 2024
```

### 2.2 首页区块设计

| 区块 | Block Type | 功能描述 |
|------|-----------|----------|
| Biography | `resume-biography-3` | 展示头像、简介、下载简历按钮 |
| News | `collection` | 显示最新的 post 内容 |
| Publications | `collection` | 展示论文列表，使用引用格式 |

### 2.3 页面布局模式

```yaml
# 首页布局 (Landing Page)
type: landing
sections:
  - block: resume-biography-3    # 个人简介区块
  - block: collection            # 新闻区块
  - block: collection            # 论文区块

# 经历页面布局
type: landing
sections:
  - block: resume-experience     # 工作经历
  - block: resume-skills         # 技能
  - block: resume-awards         # 奖项

# 项目页面布局
type: landing
sections:
  - block: collection            # 项目网格
    design:
      view: article-grid
      columns: 2
```

---

## 3. 内容管理

### 3.1 内容类型

| 类型 | 目录 | 用途 | 示例 |
|------|------|------|------|
| Author | `data/authors/` | 作者/个人信息 | `me.yaml` |
| Post | `content/post/` | 新闻动态 | `20250819/` |
| Publication | `content/publication/` | 学术论文 | `icarm2024/` |
| Project | `content/project/` | 项目展示 | `LeggedGym-Ex/` |
| Page | `content/*.md` | 独立页面 | `experience.md` |

### 3.2 内容结构示例

#### Author 数据 (`data/authors/me.yaml`)
```yaml
schema: hugoblox/author/v1
name:
  display: YasenJia
  given: Yasen
  family: Jia
role: Robotics Enthusiast
bio: |
  # 支持 Markdown
affiliations:
  - name: Beijing Institute of Technology
links:
  - icon: brands/github
    url: https://github.com/lupinjia
skills:
  - name: Coding
    items:
      - name: Python
awards:
  - title: Outstanding Graduate
```

#### Post/项目内容 (`content/post/xxx/index.md`)
```yaml
---
title: Post Title
date: 2025-08-19
authors:
  - me
tags:
  - Experience
---

正文内容 (支持 Markdown + 视频嵌入)

{{< video src="videos/demo.mp4" controls="yes" >}}
```

#### Publication (`content/publication/icarm2024/index.md`)
```yaml
---
title: 'Paper Title'
authors:
  - Mengya Su
  - me
  - Yan Huang
date: '2024-10-18'
doi: '10.1109/...'
publication_types: ['conference']
publication: In *ICARM 2024*
abstract: |
  摘要内容
---
```

---

## 4. 数据流

### 4.1 构建流程

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│   内容编辑    │────▶│  Git Push    │────▶│ GitHub       │
│  (Markdown)   │     │   to main    │     │ Actions      │
└──────────────┘     └──────────────┘     └──────┬───────┘
                                                  │
                              ┌───────────────────┼──────────┐
                              ▼                   ▼          ▼
                        ┌─────────┐        ┌─────────┐  ┌──────────┐
                        │  Hugo   │        │Tailwind │  │ Pagefind │
                        │  Build  │        │   CSS   │  │  Search  │
                        └────┬────┘        └────┬────┘  └────┬─────┘
                             │                  │           │
                             └──────────────────┴───────────┘
                                                │
                                         ┌──────▼──────┐
                                         │   public/   │
                                         │ (静态站点)   │
                                         └──────┬──────┘
                                                │
                                         ┌──────▼──────┐
                                         │ GitHub      │
                                         │ Pages       │
                                         └─────────────┘
```

### 4.2 构建步骤

1. **检出代码**: `actions/checkout@v4`
2. **安装 Hugo**: `peaceiris/actions-hugo@v3` (v0.153.0 extended)
3. **安装依赖**: Node.js 20 + TailwindCSS CLI
4. **构建站点**: `hugo --minify`
5. **生成搜索索引**: `npx pagefind --site "public"`
6. **部署**: `actions/deploy-pages@v4`

---

## 5. 配置管理

### 5.1 配置文件结构

```
config/
└── _default/
    ├── hugo.yaml      # Hugo 核心配置
    ├── params.yaml    # 站点参数
    ├── menus.yaml     # 导航菜单
    ├── languages.yaml # 多语言配置
    └── module.yaml    # 模块依赖
```

### 5.2 关键配置项

| 配置项 | 文件 | 说明 |
|--------|------|------|
| Site Title | `hugo.yaml` | Yasen Jia |
| Theme Color | `params.yaml` | rose |
| Dark Mode | `params.yaml` | system (跟随系统) |
| Analytics | `params.yaml` | Google Analytics G-P1GPL6RY3W |
| Navbar | `params.yaml` | 固定顶部 + 搜索 + 主题切换 |
| Menu Items | `menus.yaml` | Bio, News, Papers, Experience, Projects |

---

## 6. 组件设计

### 6.1 HugoBlox Blocks 使用

| Block | 用途 | 所在页面 |
|-------|------|----------|
| `resume-biography-3` | 个人简介卡片 | 首页 |
| `resume-experience` | 工作经历/教育 | experience |
| `resume-skills` | 技能展示 | experience |
| `resume-awards` | 奖项列表 | experience |
| `collection` | 内容集合展示 | 首页、projects |

### 6.2 自定义元素

- **自定义图标**: 通过 `assets/media/icons/` 添加
- **视频嵌入**: 使用 Hugo shortcode `{{< video >}}`
- **PDF 链接**: 简历下载链接到 `static/uploads/`

---

## 7. 扩展性设计

### 7.1 可扩展点

| 扩展项 | 方法 | 位置 |
|--------|------|------|
| 新增页面 | 创建 `.md` 文件 | `content/` |
| 新增项目 | 创建项目目录 | `content/project/` |
| 新增论文 | 创建 publication | `content/publication/` |
| 新增技能 | 编辑 author 数据 | `data/authors/me.yaml` |
| 修改导航 | 编辑菜单配置 | `config/_default/menus.yaml` |

### 7.2 主题定制

- **颜色**: 修改 `params.yaml` appearance.color
- **间距**: 通过 `design.spacing` 配置每个区块
- **背景**: 支持纯色或图片背景

---

## 8. SEO 与性能

### 8.1 SEO 配置

- **站点类型**: Person (个人信息站点)
- **Google 验证**: 已配置
- **Robots.txt**: 自动生成
- **Sitemap**: 自动生成

### 8.2 性能优化

- **图片优化**: Hugo 自动生成 WebP 格式
- **资源压缩**: `--minify` 压缩 HTML/CSS/JS
- **懒加载**: 图片懒加载支持
- **搜索**: Pagefind 静态搜索索引

---

## 9. 部署架构

### 9.1 CI/CD 流程

```yaml
触发条件:
  - push to main 分支
  - 手动触发 workflow_dispatch

构建环境:
  - Ubuntu Latest
  - Hugo 0.153.0 extended
  - Node.js 20

部署目标:
  - GitHub Pages
  - 站点地址: https://lupinjia.github.io
```

### 9.2 环境变量

- `WC_HUGO_VERSION`: 0.153.0
- `HUGO_ENVIRONMENT`: production

---

## 10. 安全与维护

### 10.1 安全考虑

- 静态站点，无服务端漏洞风险
- 无需数据库，避免注入攻击
- GitHub Pages HTTPS 自动启用

### 10.2 维护建议

- 定期更新 Hugo 版本
- 保持主题模块更新
- 备份 `content/` 和 `data/` 目录
- 监控 GitHub Actions 构建状态

---

## 附录

### A. 技术参考

- [Hugo 文档](https://gohugo.io/documentation/)
- [HugoBlox 文档](https://docs.hugoblox.com/)
- [TailwindCSS 文档](https://tailwindcss.com/docs)

### B. 文件命名规范

- 项目目录: 使用英文，空格用 `-` 或 `_`
- 图片: `featured.jpg/png` 作为封面
- 日期格式: YYYYMMDD

### C. 内容模板

见项目内各 `index.md` 文件中的 front matter 示例。
