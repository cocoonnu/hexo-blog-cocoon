---
h1: "" # 指定标题
title: DOM/BOM 开发笔记 # 文章标题
description: 这篇文章主要记录 DOM/BOM 相关的开发笔记，包括 DOM 操作、BOM 对象使用等内容 # 文章摘要
tags: [Web]
categories: [技术文档]
topic: technical-documentation
references:
  - "[DOM 常用操作](https://vue3js.cn/interview/JavaScript/Dom.html)"
  - "[DOM 详细解析](https://juejin.cn/post/6875674323042959368)"
  - "[BOM 常用操作](https://vue3js.cn/interview/JavaScript/BOM.html)"
---

<!-- 使用引用标签作为标题 -->

{% quot DOM/BOM 开发笔记 el:h1 %}

<!-- 指定摘要 -->

这篇文章主要记录 DOM/BOM 相关的开发笔记，包括 DOM 操作、BOM 对象使用等内容
{% hashtag DOM https://developer.mozilla.org/zh-CN/docs/Web/API/Document_Object_Model %}
{% hashtag BOM https://vue3js.cn/interview/JavaScript/BOM.html %}

## Event 对象属性

MouseEvent MDN：https://developer.mozilla.org/zh-CN/docs/Web/API/MouseEvent

Event MDN：https://developer.mozilla.org/zh-CN/docs/Web/API/Event

`e` 就是鼠标对象 `MouseEvent`，它继承了 `Event` 事件对象，下面是它的常见属性

- `e.target`：触发绑定事件的对象，可以为本体，也可以为子盒子

- `e.clientX`：鼠标在**页面上可视区域的位置**，从浏览器可视区域左上角开始，即是以浏览器滑动条此刻的滑动到的位置为参考点，随滑动条移而变化

- `e.pageX`：鼠标在**页面上的位置**，从页面左上角开始，即是以页面为参考点，不随滑动条移动而变化

- `e.offsetX`：鼠标在 `e.target` **盒子里的位置**，如果该盒子有边框，则可能出现负值

- `e.stopPropagation`：阻止事件冒泡

- `e.preventDefault`：组件事件默认行为

## DOM 高宽度属性

主要考察盒子模型，一个 DOM 对象包含如下的高宽度属性：

- offsetHeight、offsetWidth：包括盒子的 border + padding + content
- offsetTop、offsetLeft：该元素的上（左）外边框到其父元素的上（左）内边框之间的距离
- clientHeight、clientWidth：包括盒子的 padding + content
- scrollHeight、scrollWidth：包括盒子的 padding + 实际内容的尺寸
- scrollTop、scrollLeft：该盒子相对于其父盒子滚动的距离

> 实际内容是指该盒子可能含有子盒子，子盒子内容尺寸大于该盒子内容尺寸

<br />

**判断可视区**
如何判断一个元素是否在浏览器窗口（也可换成其他父元素）的可视区域中：[判断可视区方案](https://vue3js.cn/interview/JavaScript/visible.html)

```js
function isInViewPortOfOne(el) {
  const viewPortHeight =
    window.innerHeight ||
    document.documentElement.clientHeight ||
    document.body.clientHeight;
  const offsetTop = el.offsetTop;
  const scrollTop = document.documentElement.scrollTop;
  const top = offsetTop - scrollTop;
  return top <= viewPortHeight;
}
```

<br />

**getBoundingClientRect**
这个 API 可以获取当前盒子相对于视口（浏览器页面边缘）的位置属性

- 还可用于判断当前元素是否在可视区：https://vue3js.cn/interview/JavaScript/visible.html#getboundingclientrect
- MDN 官方文档：https://developer.mozilla.org/zh-CN/docs/Web/API/Element/getBoundingClientRect

## DOM API 使用记录

**document**

推荐文章：https://juejin.cn/post/7029691847060488228

| 方法                                | 功能                       | 兼容性                       |
| ----------------------------------- | -------------------------- | ---------------------------- |
| `document.getElementById()`         | 通过 id 得到**元素**       | IE 6                         |
| `document.getElementsByTagName()`   | 通过标签名得到**元素数组** | IE 6                         |
| `document.getElementsByClassName()` | 通过类名得到**元素数组**   | IE 9                         |
| `document.querySelector()`          | 通过选择器得到**元素**     | IE 8 部分兼容、IE 9 完全兼容 |
| `document.querySelectorAll()`       | 通过选择器得到**元素数组** | IE 8 部分兼容、IE 9 完全兼容 |

<br />

**滚动属性与样式**

1. 先确定一个父盒子的宽和高，然后将其样式设置为 `over-flow: auto`，即可开启滚动属性
2. 要控制父盒子的滚动位置直接使用：`ele.scrollTo({ top: 0, behavior: 'smooth' })`
3. 要指定滚动到某个子盒子的位置直接使用：`children.scrollIntoView()`
4. 详细属性可自行查看 MDN：https://developer.mozilla.org/zh-CN/docs/Web/API/Element/scrollIntoView

```tsx
const ele = document.getElementById("ele");
const children = document.getElementById("children");

// block：垂直方向对齐方式    inline：水平方向对齐方式
if (children)
  children.scrollIntoView({
    behavior: "smooth",
    block: "end",
    inline: "nearest",
  });
ele.scrollTo({ top: 0, behavior: "smooth" });
```
