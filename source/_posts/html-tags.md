---
title: HTML 标签学习笔记
date: 2026-10-24 00:00:00
permalink: html-tags/
categories: [前端]
tags: [HTML, 前端基础]
comments: false
disableNunjucks: true
---

本文整理 HTML 常用标签、语义化页面结构、媒体、链接、列表、表格与表单等基础知识，并附代码示例和速查表。

<!-- more -->

> 涵盖：文档骨架、标签关系、标题段落、语义化结构、文本强调、元素分类、图片与路径、音视频、链接锚点、列表、表格、表单、特殊字符。

---

## 目录

- [1. 标题和段落](#1-标题和段落)
- [2. 语义化页面结构](#2-语义化页面结构)
- [3. 文本强调标签](#3-文本强调标签)
- [4. 元素分类](#4-元素分类)
- [5. 图片与路径](#5-图片与路径)
- [6. 音视频标签](#6-音视频标签)
- [7. 链接与锚点](#7-链接与锚点)
- [8. 列表标签](#8-列表标签)
- [9. 表格标签](#9-表格标签)
- [10. 表单标签](#10-表单标签)
- [11. 特殊字符](#11-特殊字符)
- [附：速查表](#附：速查表)

---

## 1. 标题和段落

### 1.1 标题 h1-h6

```html
<h1>课程标题</h1>
<h2>第一章 HTML</h2>
<h3>1.1 文档骨架</h3>
```

### 1.2 段落 p 与换行 br

`p` 表示完整段落，`br` 只表示强制换行，不能把 `br` 当作段落间距工具。

```html
<p>这是一个完整段落。</p>
<p>地址：北京市<br>海淀区</p>
```

---

## 2. 语义化页面结构

语义化标签让结构更清楚，也让维护、SEO、无障碍访问更友好。

### 2.1 header / nav / main / section / article / aside / footer

| 标签 | 含义 |
|------|------|
| `<header>` | 页面头部或某个模块的头部 |
| `<nav>` | 导航链接区域 |
| `<main>` | 页面主体内容，一个页面通常只出现一个 |
| `<section>` | 有主题的小节，通常配合标题使用 |
| `<article>` | 独立完整内容，例如文章、帖子、商品评论 |
| `<aside>` | 侧边栏、推荐、广告、补充信息 |
| `<footer>` | 页面底部或模块底部 |

```html
<header>网站头部</header>
<nav>导航</nav>
<main>
  <section>
    <h2>新鲜好物</h2>
  </section>
</main>
<footer>版权信息</footer>
```

### 2.2 div 与 span

> 通俗理解：div 像一个大收纳箱，适合装一整块内容；span 像给一句话里的几个字贴标签，适合做局部样式。

- `<div>` 是块级通用容器，本身没有语义，常用于布局分组。
- `<span>` 是行内容器，适合包裹一小段文字做局部样式。
- 当存在更准确的语义标签时，**优先使用语义标签**，再考虑 div/span。

---

## 3. 文本强调标签

强调标签既影响默认样式，也表达内容语义。

| 标签 | 语义 | 默认样式 |
|------|------|----------|
| `<strong>` | 重要内容，语义强于 `<b>` | 加粗 |
| `<em>` | 语气强调，语义强于 `<i>` | 倾斜 |
| `<ins>` | 插入内容 | 下划线 |
| `<del>` | 删除内容 | 删除线 |

```html
<p><strong>重要：</strong>表单提交前请检查信息。</p>
<p>这句话需要<em>特别强调</em>。</p>
```

---

## 4. 元素分类

### 4.1 块级元素

> 通俗理解：块级元素像一排货架，默认自己占一整行，后面的内容通常要到下一行开始。

- 常见块级元素：`div`、`p`、`h1`-`h6`、`ul`、`ol`、`li`、`table`、`form`、`header`、`section`。
- 默认独占一行，可以设置 `width`、`height`、`margin`、`padding`。
- 块级元素宽度默认尽量占满父容器。

### 4.2 行内元素

> 通俗理解：行内元素像一句话里的词，默认跟其他文字挤在同一行，大小主要由内容撑开。

- 常见行内元素：`span`、`a`、`strong`、`em`、`label`。
- 默认一行显示多个，宽高一般由内容撑开。
- 水平方向 margin/padding 生效明显，垂直方向对布局影响有限。

### 4.3 行内块元素

- 常见行内块元素：`img`、`input`、`button`。
- 既可以一行排列，又可以设置 `width` 和 `height`。
- 常用于图文按钮、表单控件、图片排列。

| 分类 | 独占一行 | 可设宽高 | 常见标签 |
|------|----------|----------|----------|
| 块级元素 | 是 | 是 | div、p、h1-h6、ul、li |
| 行内元素 | 否 | 否 | span、a、strong、em |
| 行内块元素 | 否 | 是 | img、input、button |

---

## 5. 图片与路径

### 5.1 img 标签

- `src` 表示图片地址，是**必需属性**。
- `alt` 表示替代文本，图片无法加载或屏幕阅读器读取时使用。
- `width`/`height` 可以设置显示尺寸，但通常建议交给 CSS 控制。
- 图片是行内块元素，底部可能出现默认空隙，常用 `display: block` 或 `vertical-align` 调整。

```html
<img src="./img/pic.webp" alt="商品图片">
```

| 属性 | 作用 |
|------|------|
| `src` | 指向要插入页面的图像地址 |
| `alt` | 备选文本，图片无法显示时提示的文字 |
| `width` | 设置图片宽度（建议使用 CSS 修改） |
| `height` | 设置图片高度（建议使用 CSS 修改） |
| `title` | 图像标题，鼠标悬停时显示的文本 |

### 5.2 相对路径

> 通俗理解：相对路径像从当前教室找房间——`./` 是本教室，`../` 是上一层楼，`img/logo.png` 是当前楼层里的 img 房间。

| 写法 | 含义 |
|------|------|
| `./` | 当前目录，可省略但写出来更清楚 |
| `../` | 上一级目录 |
| `img/logo.png` | 当前目录下的子目录 |

- 课堂项目里 HTML、CSS、images、uploads 分目录管理，就是路径练习的核心场景。

---

## 6. 音视频标签

- `<audio>` 用来嵌入音频，常配合 `controls` 显示播放控件。
- `<video>` 用来嵌入视频，可设置 `controls`、`autoplay`、`muted`、`loop`、`poster`。
- 现代浏览器通常要求 `autoplay` 与 `muted` 一起使用才允许自动播放。
- `poster` 是视频未播放前的封面图。

```html
<video src="./media/demo.mp4" controls muted poster="./img/poster.jpg"></video>
<audio src="./media/demo.mp3" controls></audio>
```

### 6.1 视频多格式兼容写法

```html
<video controls>
  <source src="video.mp4" type="video/mp4">
  <source src="video.ogg" type="video/ogg">
  <source src="video.webm" type="video/webm">
  <p>您的浏览器不支持 HTML5 Video 标签，请升级浏览器。</p>
</video>
```

1. 将 `src` 属性分别写在多个 `<source>` 元素中，每个元素指向一种媒体资源。
2. 浏览器会依次检查 `<source>` 元素，并播放第一个自身支持的媒体格式。
3. 每个 `<source>` 元素都应设置 `type` 属性，使浏览器能快速跳过不支持的格式；如果省略 `type`，浏览器可能逐个加载文件，浪费时间和资源。

### 6.2 视频标签常用属性

| 属性 | 作用 |
|------|------|
| `autoplay` | 自动播放 |
| `loop` | 循环播放 |
| `muted` | 静音 |
| `poster` | 设置视频播放前显示的预览图像 |

---

## 7. 链接与锚点

### 7.1 a 标签

- `href` 是跳转地址，可以是网页、文件、邮箱、电话或锚点。
- `target="_blank"` 表示新标签页打开。
- 空链接可写 `href="#"`，真实项目中要避免无意义跳转影响体验。
- 链接文字应该描述目的地，不建议大量使用"点击这里"。

```html
<a href="https://example.com" target="_blank">打开网站</a>
```

### 7.2 锚点链接

- 给目标元素设置 id，例如 `id="chapter1"`。
- 链接写 `href="#chapter1"` 即可跳到对应位置。
- 锚点适合长文章目录、页面内导航、返回顶部。

```html
<a href="#form">跳到表单</a>
<section id="form">...</section>
```

---

## 8. 列表标签

| 标签 | 类型 | 适用场景 |
|------|------|----------|
| `<ul>` + `<li>` | 无序列表 | 导航、商品分类、新闻列表 |
| `<ol>` + `<li>` | 有序列表 | 步骤、排名 |
| `<dl>` + `<dt>`/`<dd>` | 自定义列表 | 名词解释（dt 术语、dd 描述） |

- `<ul>`/`<ol>` 内部必须以 `<li>` 作为直接子元素。
- 导航等场景常用 ul/li 再配合 CSS 去掉默认圆点。

```html
<ul>
  <li>首页</li>
  <li>课程</li>
</ul>
```

---

## 9. 表格标签

### 9.1 table / tr / th / td

| 标签 | 含义 |
|------|------|
| `<table>` | 表格整体 |
| `<tr>` | 一行 |
| `<th>` | 表头单元格，默认加粗居中 |
| `<td>` | 普通单元格 |

- `thead`、`tbody`、`tfoot` 可以进一步划分表头、主体、表尾。

### 9.2 合并单元格

- `rowspan` 表示**跨行**合并。
- `colspan` 表示**跨列**合并。
- 合并后要删除被占用的多余单元格，否则表格结构会错位。
- 先确定从哪个单元格开始合并，再数跨几行或几列。

```html
<td rowspan="2">跨两行</td>
<td colspan="3">跨三列</td>
```

---

## 10. 表单标签

### 10.1 form 容器

- `<form>` 用来包裹一组表单控件。
- `action` 表示提交目标地址。
- `method` 常见值为 `get` 和 `post`。
- 表单项的 `name` 是提交数据的字段名，**没有 name 通常不会随表单提交**。

```html
<form action="/login" method="post">
  <input name="username">
</form>
```

### 10.2 input 常用 type

> 通俗理解：type 决定输入框扮演什么角色——text 像普通填空题，password 像遮住答案的填空题，radio 像单选题，checkbox 像多选题。

| type | 说明 |
|------|------|
| `text` | 单行文本框 |
| `password` | 密码框，输入内容会被遮挡 |
| `radio` | 单选框，同一组必须设置相同 name |
| `checkbox` | 复选框，适合多选 |
| `file` | 文件上传，可配合 multiple 和 accept |
| `submit` / `reset` / `button` | 提交、重置、普通按钮 |

### 10.3 label 提升可用性

- 方式一：label 的 `for` 与控件 `id` 对应，点击文字可聚焦或选中控件。
- 方式二：label 直接**包裹**控件和文字。
- 单选框、复选框尤其适合配 label，点击区域更大。

```html
<input id="male" type="radio" name="gender">
<label for="male">男</label>
<label><input type="checkbox" name="hobby"> 足球</label>
```

### 10.4 select / textarea / button

- `<select>` 配合 `<option>` 实现下拉选择，`selected` 表示默认选中。
- `<textarea>` 表示多行文本，内容区域不要写成 input。
- `<button>` 默认在表单里可能触发表单提交，必要时写 `type="button"`。
- `disabled` 禁用控件，`placeholder` 提示输入内容。

---

## 11. 特殊字符

当你想在页面上展示 HTML 标签本身，而不是让浏览器解析它，就要使用实体字符。

| 实体字符 | 显示为 |
|----------|--------|
| `&nbsp;` | 不换行空格 |
| `&lt;` | 小于号 < |
| `&gt;` | 大于号 > |
| `&amp;` | & 符号 |

```html
&lt;div&gt;这会显示标签文本&lt;/div&gt;
```

---

## 附：速查表

| 需求 | 写法 |
|------|------|
| HTML5 文档声明 | `<!doctype html>` |
| 移动端适配基础 | `<meta name="viewport" content="width=device-width, initial-scale=1.0">` |
| 新标签页打开链接 | `<a href="..." target="_blank">` |
| 页面内跳转 | `id="xx"` + `href="#xx"` |
| 视频自动播放 | `autoplay` + `muted` 同时使用 |
| 单选分组 | 同一组 radio 设置相同 `name` |
| 点击文字选中控件 | `<label for="id">` 或 label 包裹控件 |
| 跨行 / 跨列合并 | `rowspan` / `colspan` |
| 展示标签本身 | `&lt;` `&gt;` 实体字符 |
