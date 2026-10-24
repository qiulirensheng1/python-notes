# 编程学习笔记

学习前端和 Python 时整理的基础知识与代码示例。

## 在线阅读

- [博客首页](https://qiulirensheng1.github.io/python-notes/)
- [HTML 标签学习笔记](https://qiulirensheng1.github.io/python-notes/html-tags/)
- [CSS 基础学习笔记](https://qiulirensheng1.github.io/python-notes/css-basics/)
- [Python 基础核心技术文档](https://qiulirensheng1.github.io/python-notes/python-basics/)

博客使用 Hexo 生成，由 GitHub Actions 自动部署到 GitHub Pages。

## 笔记目录

- [HTML 标签学习笔记](source/_posts/html-tags.md)
- [CSS 基础学习笔记](source/_posts/css-basics.md)
- [Python 基础核心技术文档](1.Python基础.md)

## 主要内容

- HTML 标签与页面结构
- CSS 基础样式与布局
- 基础输出、字面量、变量与数据类型
- 字符串、输入输出与运算符
- 条件判断与循环
- 列表、元组、集合、字典等数据容器
- 函数、参数、作用域、匿名函数与递归
- 类型注解与模块

## 更新博客

修改 `source/_posts/` 下对应的 Markdown 文章后提交到 `main` 分支，GitHub Actions 会自动重新构建并发布。

本地预览需要 Node.js 20.19 或更高版本：

```sh
npm ci
npm run server
```

本地生成静态网页：

```sh
npm run build
```
