---
title: CSS 基础学习笔记
date: 2026-10-24 00:00:00
permalink: css-basics/
categories: [前端]
tags: [CSS, 前端基础]
comments: false
disableNunjucks: true
---

这篇笔记整理 CSS 的基础概念、常用属性与代码示例，便于学习和查阅。

<!-- more -->

> 涵盖：CSS 引入方式、选择器、三大特性、字体与文本、盒子模型、背景技术、CSS 初始化、字体图标与精灵图。

---

## 目录

- [1. CSS 引入方式](#1-css-引入方式)
- [2. CSS 选择器](#2-css-选择器)
- [3. CSS 三大特性](#3-css-三大特性)
- [4. 字体与文本](#4-字体与文本)
- [5. 盒子模型](#5-盒子模型)
- [6. 背景技术](#6-背景技术)
- [7. CSS 初始化](#7-css-初始化)
- [8. 字体图标与精灵图](#8-字体图标与精灵图)
- [附：速查表](#附：速查表)


---

## 1. CSS 引入方式

### 1.1 行内样式（内联样式）

写在标签的 `style` 属性中，优先级高，但结构和样式混杂。适合临时调试，不适合大量项目代码。

```html
<p style="color:red; font-size:20px;">文字</p>
```

### 1.2 内部样式表

写在 `<head>` 中的 `<style>` 标签里。适合单个页面的小练习或演示，多个页面复用困难。

```html
<style>
  p { color: red; }
</style>
```

### 1.3 外部样式表（推荐）

使用 `<link>` 引入独立 CSS 文件。结构和样式分离，适合真实项目；可被多个页面复用，也便于浏览器缓存。

```html
<link rel="stylesheet" href="./css/index.css">
```

| 方式 | 写法位置 | 适用场景 |
|------|----------|----------|
| 行内样式 | 标签 `style` 属性 | 临时调试 |
| 内部样式表 | `<head>` 中 `<style>` | 单页小练习 |
| 外部样式表 | 独立 `.css` 文件 | 真实项目（推荐） |

---

## 2. CSS 选择器

### 2.1 基础选择器

- **类型选择器**：`p`、`div`、`a`，按标签名选中。
- **类选择器**：`.box`，复用性强，是项目中最常用的选择器。
- **id 选择器**：`#app`，页面中 id 应保持唯一。
- **通配符选择器**：`*`，常用于清除默认 margin/padding，但范围大。

```css
p     { color: red; }
.box  { width: 200px; }
#app  { min-height: 100vh; }
*     { box-sizing: border-box; }
```

### 2.2 层级选择器

| 选择器 | 语法 | 含义 |
|--------|------|------|
| 后代选择器 | `.box p` | 选择 box 内**所有后代** p |
| 子代选择器 | `.box > p` | 只选择**直接子元素** p |
| 相邻兄弟选择器 | `h2 + p` | 选择紧跟 h2 后的**第一个** p |
| 通用兄弟选择器 | `h2 ~ p` | 选择 h2 后面同级的**所有** p |

```css
.nav a      { color: #333; }
.list > li  { margin-bottom: 10px; }
h2 + p      { margin-top: 0; }
h2 ~ p      { color: #666; }
```

### 2.3 伪类选择器

伪类以单冒号 `:` 开头，用于选择处于特定**状态、位置或关系**中的元素，不会在 HTML 中创建新元素。

#### 2.3.1 交互与链接伪类

| 选择器 | 作用 | 常见用法 | 示例 |
|--------|------|----------|------|
| `:link` | 选择尚未访问的链接 | 设置链接初始样式 | `a:link { color: blue; }` |
| `:visited` | 选择已经访问过的链接 | 区分已访问链接；受浏览器隐私限制，只适合修改部分颜色属性 | `a:visited { color: purple; }` |
| `:hover` | 选择鼠标指针悬停的元素 | 导航、按钮、卡片的悬停反馈 | `.card:hover { box-shadow: 0 8px 20px #0002; }` |
| `:active` | 选择正在被按下或激活的元素 | 按钮按下反馈 | `button:active { transform: scale(.98); }` |
| `:focus` | 选择当前获得焦点的元素 | 输入框、按钮的键盘或点击焦点 | `input:focus { border-color: skyblue; }` |
| `:focus-visible` | 选择需要显示明显焦点提示的元素 | 主要为键盘用户显示焦点环 | `button:focus-visible { outline: 2px solid blue; }` |
| `:focus-within` | 选择自身或内部后代获得焦点的元素 | 整体高亮表单项或输入区域 | `.field:focus-within { border-color: blue; }` |

> 链接伪类建议按 `:link` → `:visited` → `:hover` → `:active` 的 LVHA 顺序书写，避免后面的规则覆盖前面的交互状态。

#### 2.3.2 表单状态伪类

| 选择器 | 作用 | 常见用法 | 示例 |
|--------|------|----------|------|
| `:enabled` | 选择可用的表单控件 | 统一设置可操作控件样式 | `input:enabled { background: white; }` |
| `:disabled` | 选择被禁用的表单控件 | 显示不可操作状态 | `button:disabled { opacity: .5; }` |
| `:checked` | 选择已选中的单选框、复选框或选项 | 自定义选中状态、联动其他元素 | `input:checked + label { color: green; }` |
| `:required` | 选择设置了 `required` 的控件 | 标记必填项 | `input:required { border-left: 3px solid red; }` |
| `:optional` | 选择非必填控件 | 区分可选项 | `input:optional { border-left-color: #ccc; }` |
| `:valid` | 选择内容通过校验的控件 | 显示输入正确状态 | `input:valid { border-color: green; }` |
| `:invalid` | 选择内容未通过校验的控件 | 显示输入错误状态 | `input:invalid { border-color: red; }` |
| `:placeholder-shown` | 选择仍在显示占位文字的输入框 | 判断输入框是否为空、制作浮动标签 | `input:placeholder-shown { color: #999; }` |
| `:read-only` | 选择只读控件 | 显示不可编辑状态 | `input:read-only { background: #f5f5f5; }` |
| `:read-write` | 选择可编辑控件 | 统一设置可编辑区域 | `input:read-write { background: white; }` |

#### 2.3.3 结构与位置伪类

| 选择器 | 作用 | 常见用法 | 示例 |
|--------|------|----------|------|
| `:first-child` | 选择父元素中的第一个子元素 | 去掉首项上边距、设置首项样式 | `li:first-child { margin-top: 0; }` |
| `:last-child` | 选择父元素中的最后一个子元素 | 去掉末项边框或下边距 | `li:last-child { border-bottom: 0; }` |
| `:only-child` | 选择父元素中唯一的子元素 | 单项列表使用特殊布局 | `.item:only-child { width: 100%; }` |
| `:nth-child(n)` | 按所有同级元素中的位置选择 | 隔行变色、网格定位 | `li:nth-child(2n) { background: #f5f5f5; }` |
| `:nth-last-child(n)` | 从最后一个子元素开始倒序计数 | 选择倒数若干项 | `li:nth-last-child(-n + 2) { color: red; }` |
| `:first-of-type` | 选择同类型元素中的第一个 | 选择第一个同标签元素 | `p:first-of-type { font-weight: bold; }` |
| `:last-of-type` | 选择同类型元素中的最后一个 | 选择最后一个同标签元素 | `p:last-of-type { margin-bottom: 0; }` |
| `:only-of-type` | 选择同类型元素中唯一的一个 | 单独强调唯一的同类元素 | `img:only-of-type { display: block; }` |
| `:nth-of-type(n)` | 按同类型元素中的位置选择 | 忽略其他标签后进行位置匹配 | `p:nth-of-type(2) { color: blue; }` |
| `:empty` | 选择没有子元素和文本内容的元素 | 隐藏空容器；空格和换行也属于文本节点 | `.message:empty { display: none; }` |

> `:nth-child()` 会统计所有同级元素；`:nth-of-type()` 只统计相同标签类型。元素类型混排时要特别注意。

#### 2.3.4 逻辑、关系与文档状态伪类

| 选择器 | 作用 | 常见用法 | 示例 |
|--------|------|----------|------|
| `:not(selector)` | 排除符合条件的元素 | 批量设置样式时跳过特定项 | `.item:not(.active) { opacity: .6; }` |
| `:is(selector-list)` | 合并多个选择器，减少重复代码 | 简化多个父级或后代条件 | `:is(header, main, footer) a { color: blue; }` |
| `:where(selector-list)` | 与 `:is()` 类似，但自身优先级为 0 | 编写容易被覆盖的基础样式 | `:where(ul, ol) { padding: 0; }` |
| `:has(relative-selector)` | 根据内部或相邻元素反向选择当前元素 | 父元素状态、条件布局 | `.card:has(img) { padding-top: 0; }` |
| `:root` | 选择文档根元素，HTML 中通常是 `<html>` | 定义全局 CSS 变量 | `:root { --main-color: #1677ff; }` |
| `:target` | 选择与 URL 中 `#锚点` 匹配的元素 | 目录跳转后高亮目标区域 | `section:target { background: #fffbe6; }` |

#### 2.3.5 `nth-child()` 表达式速查

| 表达式 | 选中位置 | 示例 |
|--------|----------|------|
| `n` | 所有元素 | `li:nth-child(n)` |
| `odd` 或 `2n + 1` | 奇数项：1、3、5…… | `tr:nth-child(odd)` |
| `even` 或 `2n` | 偶数项：2、4、6…… | `tr:nth-child(even)` |
| `3n` | 每 3 项中的第 3 项 | `.item:nth-child(3n)` |
| `-n + 3` | 前 3 项 | `.item:nth-child(-n + 3)` |
| `n + 4` | 从第 4 项到最后 | `.item:nth-child(n + 4)` |

#### 2.3.6 综合用法

```css
/* 表格隔行变色 */
tbody tr:nth-child(even) {
  background: #f5f5f5;
}

/* 键盘操作时显示清晰焦点 */
button:focus-visible {
  outline: 2px solid #1677ff;
  outline-offset: 2px;
}

/* 复选框选中后改变相邻标签 */
input[type="checkbox"]:checked + label {
  color: #1677ff;
  font-weight: 700;
}

/* 含图片的卡片使用不同布局 */
.card:has(> img) {
  display: grid;
  grid-template-columns: 120px 1fr;
}
```

### 2.4 伪元素选择器

- `::before` 在元素内容**前**创建虚拟子元素。
- `::after` 在元素内容**后**创建虚拟子元素。
- 必须设置 `content` 属性，哪怕 `content: ""`。
- 常用于清除浮动、装饰线、图标、遮罩层。

```css
.box::after {
  content: "";
  display: block;
  clear: both;
}
```

### 2.5 属性选择器

| 语法 | 含义 |
|------|------|
| `[type]` | 拥有 type 属性的元素 |
| `[type="text"]` | type 值等于 text |
| `[class^="icon-"]` | class 以 `icon-` 开头 |
| `[href$=".pdf"]` | href 以 `.pdf` 结尾 |

```css
input[type="text"]       { border: 1px solid #ccc; }
a[href$=".pdf"]::after   { content: " PDF"; }
```

---

## 3. CSS 三大特性

### 3.1 层叠性

> 通俗理解：把 CSS 想成多人给同一个盒子提意见——都说颜色时，浏览器按权重和先后顺序决定听谁的；权重一样，就听后写的。

- 同一元素、同一属性被多条规则设置时，根据**权重、来源和书写顺序**决定最终样式。
- 权重相同，后写的覆盖先写的。
- 层叠不是冲突本身，而是 CSS **解决冲突的规则**。

### 3.2 继承性

> 通俗理解：像家里的统一着装要求——父元素设置了字体和颜色，子元素通常会跟着用；但宽高、边框、外边距这类盒子尺寸不会自动传下去。

- **能继承**：文本相关属性，如 `color`、`font`、`line-height`、`text-align`。
- **不继承**：盒模型属性，如 `width`、`height`、`margin`、`padding`、`border`。
- 把全站字体和基础颜色写在 `body` 上，就是利用继承。

### 3.3 优先级与权重

> 通俗理解：id 像点名，class 像按小组叫人，标签像按身份叫人。点名更具体，所以更容易生效。

优先级从高到低：

```
!important > 行内样式 > id 选择器 > 类/伪类/属性选择器 > 标签/伪元素选择器 > 通配符 > 继承样式
```

- `!important` 权重最高，但会破坏可维护性，**慎用**。
- 复合选择器权重按组成**累计**，不是简单看长度。
- 继承来的样式权重最低。

```css
#box .title { color: red; }  /* id + class，权重更高 */
.card h2    { color: blue; } /* class + tag */
```

---

## 4. 字体与文本

### 4.1 字体样式

| 属性 | 说明 | 常用值 |
|------|------|--------|
| `font-size` | 字号 | 浏览器默认常为 16px |
| `font-weight` | 字重 | normal、bold、400、700 |
| `font-style` | 字体样式 | normal、italic |
| `font-family` | 字体族 | 中文字体名建议加引号并提供兜底字体 |

font 简写（顺序：`font: 字号/行高 字体族`）：

```css
body {
  font: 16px/1.6 "Microsoft YaHei", Arial, sans-serif;
}
```

### 4.2 文本布局

- `color` 文字颜色。

- `text-align` 行内内容水平对齐。

- `text-indent` 首行缩进，中文段落常用 `2em`。

- `line-height` 行高，可用数值、px、em、百分比。

- `text-decoration` 控制下划线、删除线等。

- `letter-spacing` 字间距

![CSS 文本属性速查表](/images/css-text-properties.svg)

```css
p {
  text-indent: 2em;
  line-height: 1.8;
  text-align: justify;
}
```

### 4.3 单行 / 多行省略号

- 单行省略号三件套：`white-space: nowrap` + `overflow: hidden` + `text-overflow: ellipsis`。
- 多行省略号用 `-webkit-line-clamp`，需配合弹性盒旧语法。
- 省略号只影响视觉显示，原始文本仍在 DOM 中。

```css
.one-line {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
.multi-line {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
```

---

## 5. 盒子模型

### 5.1 盒子组成

> 通俗理解：盒子模型像快递盒——content 是商品，padding 是防震泡沫，border 是纸箱外壳，margin 是快递盒之间的距离。

| 部分 | 说明 |
|------|------|
| content | 内容区域，由 width/height 控制 |
| padding | 内边距，内容与边框之间的距离 |
| border | 边框，包在 padding 外面 |
| margin | 外边距，盒子与其他盒子的距离 |

标准盒模型下：**实际占用宽度 = width + padding-left/right + border-left/right**

```css
.box {
  width: 200px;
  padding: 20px;
  border: 2px solid #333;
  margin: 30px;
}
```

### 5.2 边框 border

border 简写顺序：**宽度 样式 颜色**。样式常用 `solid`、`dashed`、`dotted`。

```css
.box {
  border: 1px solid #ddd;
  border-top: 3px solid #e1251b;
}
```

### 5.3 圆角 border-radius

值的数量与对应角（顺时针）：

| 写法 | 含义 |
|------|------|
| 1 个值 | 四个角相同 |
| 2 个值 | 左上/右下、右上/左下 |
| 3 个值 | 左上、右上/左下、右下 |
| 4 个值 | 左上、右上、右下、左下 |

- **圆形**：正方形盒子 + `border-radius: 50%`。
- **胶囊按钮**：圆角设为宽高较小值的一半（如 200×40 的盒子写 `20px`）。
- 圆角最多只能到盒子边长的一半，超过后按浏览器规则压缩，视觉上不会更圆。

```css
.circle { width: 100px; height: 100px; border-radius: 50%; }
.pill   { width: 200px; height: 40px;  border-radius: 20px; }
.card   { border-radius: 10px 30px 50px 70px; }
```

### 5.4 内边距 padding

- padding 会撑大标准盒模型的实际尺寸。
- 值的数量：1 个＝四边；2 个＝上下、左右；3 个＝上、左右、下；4 个＝上右下左（顺时针）。

```css
.btn { padding: 8px 16px; }
```

### 5.5 外边距 margin

> 通俗理解：margin 像人与人之间保持的距离；上下相邻的两人都要求留距离时，浏览器常常只取较大的那个，而不是相加。

- 块级盒子水平居中：`width` + `margin: 0 auto`。
- **margin 合并**：相邻块级元素垂直 margin 取较大值。
- **margin 塌陷**：父子元素顶部 margin 可能塌陷，可用 `border`、`padding`、`overflow`、`display: flow-root` 处理。

```css
.container {
  width: 1200px;
  margin: 0 auto;
}
```

### 5.6 盒子尺寸 box-sizing

> 通俗理解：content-box 像只量商品本身，泡沫和纸箱另算；border-box 像直接规定快递盒最终尺寸，泡沫和纸箱都算在内。

- `content-box`（默认）：width/height 只包含内容区域。
- `border-box`：width/height 包含 content + padding + border。
- 项目中常用 `* { box-sizing: border-box; }` 降低尺寸计算成本。

```css
* { box-sizing: border-box; }
.box { width: 200px; padding: 20px; border: 1px solid #ddd; } /* 总宽仍是 200px */
```

### 5.7 盒子阴影 box-shadow

参数顺序：**水平偏移 垂直偏移 模糊半径 扩散半径 颜色**。默认外阴影，`inset` 改为内阴影。

```css
.card:hover {
  box-shadow: 0 8px 24px rgba(0,0,0,.12);
}
```

---

## 6. 背景技术

### 6.1 背景颜色与图片

| 属性 | 说明 |
|------|------|
| `background-color` | 背景色 |
| `background-image: url(...)` | 背景图 |
| `background-repeat` | 是否平铺 |
| `background-position` | 背景位置 |
| `background-size` | 背景尺寸，常用 cover、contain |
| `background-attachment: fixed` | 背景固定，可做视差滚动 |

```css
.hero {
  background: url("./img/bg.jpg") center / cover no-repeat;
}
```

### 6.2 线性渐变 linear-gradient

- 可作为 `background-image` 使用。
- 可指定方向：`to right`、`45deg` 等。
- 渐变可叠加背景图做遮罩效果。

```css
.btn {
  background: linear-gradient(90deg, #ff7a59, #1e88e5);
}
```

### 6.3 径向渐变 radial-gradient

- 从中心向外扩散，可指定形状 `circle` 或 `ellipse`。
- 适合做光斑、按钮高光、舞台光感，真实项目要控制使用量。

```css
.light {
  background: radial-gradient(circle, #fff 0%, #85c7ff 50%, transparent 70%);
}
```

---

## 7. CSS 初始化

- 不同浏览器默认样式不完全一致，初始化可减少差异。
- 常见做法：清除 margin/padding、设置 box-sizing、统一字体、去掉列表圆点。
- `normalize.css` 不是完全清零，而是保留合理默认样式并修复浏览器差异。
- 大型项目会在 `base.css` 或 `reset.css` 中统一基础样式。

```css
* { margin: 0; padding: 0; box-sizing: border-box; }
ul, ol { list-style: none; }
a { text-decoration: none; color: inherit; }
```

---

## 8. 字体图标与精灵图

### 8.1 字体图标 iconfont

- 本质是把图标做进字体文件，通过字符或 class 显示。
- 优点：体积小、可通过 `color` / `font-size` 改颜色和大小。
- 常见引入方式：`@font-face` + iconfont class。
- 适合单色图标，不适合复杂彩色图片。

```css
@font-face {
  font-family: "iconfont";
  src: url("./iconfont.woff2") format("woff2");
}
.iconfont {
  font-family: "iconfont";
  font-size: 24px;
  color: #e1251b;
}
```

### 8.2 CSS 精灵图 sprites

- 把多个小图标合成一张大图，减少 HTTP 请求。
- 通过 `background-position`（负值）显示大图中的某一块。
- 需要给元素固定 `width` / `height`。
- 现代项目中常被 SVG symbol、iconfont、打包工具替代，但仍是重要基础概念。

```css
.icon {
  width: 24px;
  height: 24px;
  background: url("./img/sprite.png") -48px 0 no-repeat;
}
```

---

## 附：速查表

| 需求 | 写法 |
|------|------|
| 水平居中块级盒子 | `margin: 0 auto`（需有 width） |
| 圆形 | 正方形 + `border-radius: 50%` |
| 胶囊按钮 | `border-radius: 高度的一半` |
| 单行省略号 | `nowrap + hidden + ellipsis` |
| 多行省略号 | `-webkit-line-clamp` |
| 清除浮动 | `::after { content:""; display:block; clear:both; }` |
| 全局盒模型 | `* { box-sizing: border-box; }` |
| 卡片阴影 | `box-shadow: 0 8px 24px rgba(0,0,0,.12)` |
