# 博客功能使用指南

> 本文档介绍如何使用 HugoBlox 博客功能

---

## 功能概览

博客功能已集成到你的个人主页中，与"新闻"分开管理。

- **博客**: 技术文章、教程、学习笔记
- **新闻**: 个人动态、获奖、参加活动等简短消息

---

## 添加新博客文章

### 方法 1: 手动创建

1. 创建博客目录:
```bash
mkdir content/blog/my-article-title
```

2. 创建 `index.md` 文件:
```markdown
---
title: "文章标题"
summary: "文章摘要，会显示在列表页"
date: 2026-03-26
authors:
  - me
categories:
  - 技术      # 可选: 技术、研究、项目、随笔
tags:
  - 标签1
  - 标签2
---

文章内容...支持 Markdown 格式
```

3. (可选) 添加封面图片 `featured.jpg` 或 `featured.png`

### 方法 2: 使用 Hugo CLI

```bash
hugo new content/blog/my-article-title/index.md
```

---

## 分类系统

### 推荐分类

| 分类 | 用途 |
|------|------|
| 技术 | 编程、算法、框架教程 |
| 研究 | 论文阅读、研究方法 |
| 项目 | 项目经验、技术选型 |
| 随笔 | 个人感想、生活记录 |

### 添加分类

在 front matter 中添加:
```yaml
categories:
  - 技术
```

---

## 与新闻的区别

| 特性 | 新闻 (Post) | 博客 (Blog) |
|------|-------------|-------------|
| 内容长度 | 简短动态 | 详细文章 |
| 更新频率 | 不定期 | 定期更新 |
| 分类 | 无 | 有 |
| 目的 | 展示成就 | 分享知识 |

### 使用建议

**适合作为新闻:**
- 获得奖项
- 参加活动
- 项目发布
- 简历更新

**适合作为博客:**
- 技术教程
- 学习笔记
- 项目复盘
- 深度思考

---

## 搜索功能

Pagefind 会自动索引所有博客内容，部署后可通过站点搜索框搜索博客文章。

搜索支持:
- 标题匹配
- 正文内容
- 标签和分类

---

## 本地预览

```bash
# 启动开发服务器
hugo server -D

# 访问 http://localhost:1313/blog/
```

---

## 部署

推送到 main 分支即可自动部署:

```bash
git add .
git commit -m "添加博客文章: xxx"
git push origin main
```

---

## 示例文章

项目中已包含两个示例:

1. `content/blog/hello-world/` - 博客介绍
2. `content/blog/rl-tutorial/` - 技术教程示例

可以参考这些文件的格式创建新文章。
