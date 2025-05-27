---
h1: "" # 指定标题
title: GASP 动画库学习指南 # 文章标题
description: GASP 官方文档：https://gsap.com/，这篇文章会大致介绍一些动画工具的使用 # 文章摘要
tags: [GASP]
categories: [技术文档]
topic: technical-documentation
references:
  - "[GASP 官方文档](https://gsap.com/)"
  - "[Getting Started with GSAP](https://gsap.framer.wiki/stated)"
---

<!-- 使用引用标签作为标题 -->

{% quot GASP 动画库学习指南 el:h1 %}

<!-- 指定摘要 -->

GASP 官方文档：[https://gsap.com/](https://gsap.com/)，这篇文章会大致介绍一些动画工具的使用

## GASP 基础使用

首先 GASP 导出了四种动画方式，或者说是数值变化方式，常用的是 `gasp.to(target, {...})` 就是让元素从初始状态变化到目标状态

其中 `target` 可以选择 `DOM` 元素，通常使用`opacity` 和 `transform` 这两个配置项来改变元素的状态和位移，属性参考：[CorePlugins](https://gsap.com/docs/v3/GSAP/CorePlugins/CSS)，还有一些特殊的配置项如：[special-properties](<https://gsap.com/docs/v3/GSAP/gsap.to()#special-properties>)，主要用于控制一些动画的配置比如：`ease、yoyo、repeat、delay、duration`

这里再主要介绍 `stagger` 这个属性：如果 `target` 是一个数组或者选中了多个元素，那么可以让这些元素依次延时 `stagger` 执行相同的动画

```js
gsap.to(".box", {
  duration: 1,
  rotation: 360,
  opacity: 1,
  delay: 0.5,
  stagger: 1,
  ease: "sine.out",
  force3D: true,
});
```

targer 还可以是一个对象或者一个数值，GASP 依然可以精确实现数值的动态变化

```js
let obj = { myNum: 10, myColor: "red" };
gsap.to(obj, {
  myNum: 200,
  myColor: "blue",
  duration: 4,
  onUpdate: () => console.log(obj.myNum, obj.myColor),
});
```

## 时间线的使用

通过 `let tl = gsap.timeline({...})` 创建时间线后，可以决定时间线上动画的执行

时间线本质也是个动画，只不过是拆成了一个个子动画，并且可以控制这些子动画的执行顺序，因此后面的配置项可以控制这个时间线动画的属性：[special-properties-and-callbacks](<https://gsap.com/docs/v3/GSAP/gsap.timeline()#special-properties-and-callbacks>)

```js
let tl = gsap.timeline({ repeat: -1, repeatDelay: 1, yoyo: true }); // 设置时间线动画无限执行
tl.to(".green", { rotation: 360 });
tl.to(".purple", { rotation: 360 });
tl.to(".orange", { rotation: 360 });
```

通过设置 `defaults: { duration: 1, ease: "elastic" }`，配置子动画的默认属性，得到配置的效率提升

```js
var tl = gsap.timeline({ defaults: { duration: 1 } });
//这样每个动画都是1秒的时长，不用重复写了
tl.to(".green", { x: 200 })
  .to(".purple", { x: 200, scale: 0.2 })
  .to(".orange", { x: 200, scale: 2, y: 20 });
```

## tween 实例

通过 tween 实例可以实时控制动画，达到精确交互的效果，官方文档：[Tween](https://gsap.com/docs/v3/GSAP/Tween)

```js
let tween = gsap.to("#logo", { duration: 1, x: 100 }); // 通过一个变量保存对Tween或者Timeline实例的引用
tween.pause(); // 暂停
tween.resume(); // 恢复（继续）
tween.reverse(); // 反向变化
tween.reversed(!tween.reversed()); // 如果在正向则实现正向到反向，否则反之
tween.seek(0.5); // 直接切换到整个动画变化时长的0.5秒的时间点的状态
tween.progress(0.25); // 直接切换到整个变化过程的1/4的节点的状态
tween.timeScale(0.5); // 让运动减速到0.5倍
tween.kill(); // 直接销毁tween实例，让垃圾回收机制可以处理该实例所占用的内存
```

## 动画回调函数

动画属性除了可以传入 `CSS` 位移状态属性，特殊配置项属性，还可以传入动画回调函数 `onStart、onComplete、onUpdate` 等

通常使用的是 `onUpdate`，并且搭配 [requestAnimationFrame](https://blog.csdn.net/cwyp18809/article/details/105096048) 原生函数进行图形绘制，具体文档参考：[special-properties](<https://gsap.com/docs/v3/GSAP/gsap.to()#special-properties>)

```js
onUpdate: (self) => {
  // self.progress 表示滚动的百分比 0-1
  const frameIndex = Math.min(
    FRAME_COUNT,
    Math.ceil(self.progress * FRAME_COUNT + 1)
  );
  requestAnimationFrame(() => {
    img.src = getCurrentFrame(frameIndex);
    context?.drawImage(img, 0, 0);
  });
};
```

## 其他拓展学习

**关键帧动画**
该配置是对一个元素进行分段式动画配置，使用方法参考文档：[keyframes](https://gsap.framer.wiki/keyframes)

```js
// 数组分段形式
gsap.to(".elem", {
 keyframes: [ // 注意这里是数组
  {x: 100, duration: 1, ease: 'sine.out'}, // 定义这个分段动画自己的ease曲线
  {y: 200, duration: 1, delay: 0.5}, // 产生和前个分段动画0.5秒的间隔
  {rotation: 360, duration: 2, delay: -0.25} // 和前一个分段动画产生0.25秒的重叠
 ],
 ease: 'expo.inOut' // 设置整个关键帧动画的曲线
});

// 百分比分段形式
gsap.to(".elem", {
 keyframes: {  // 注意这里是对象
  "0%":   { x: 100, y: 100},
  "75%":  { x: 0, y: 0, ease: 'sine.out'}, // 指定这个分段的动画曲线
  "100%": { x: 50, y: 50 },
   easeEach: 'expo.inOut' // 每个分段的动画曲线
 },
 ease: 'none' // 整个关键帧动画的动画曲线
 duration: 2,
})
```

**滚动插件**

加上滚动插件可以让一个元素的动画和某个元素的滚动捆绑再一起，即滚动开始动画开始滚动停止动画停止，参考文档：[scrollTrigger](https://gsap.com/docs/v3/Plugins/ScrollTrigger/)

```js
gsap.to(".green", {
  rotation: 900,
  duration: 1,
  scrollTrigger: {
    trigger: ".box",
    scrub: 2,
    scrub: true, // 动画重复执行几次
  },
});
```

**在 React 中使用**
基本规范就是使用 `useLayoutEffect、gsap.context、context.revert`，关于在使用动画方面的组件通信可以参考：[withreact](https://gsap.framer.wiki/withreact2)

```jsx
const boxRef = useRef();

useLayoutEffect(() => {
  // 通过Ref的方式来获取到dom元素
  console.log(boxRef); // { current: div.box }
  // 然后我们就可以用gsap的方式来进行动画了
  gsap.to(boxRef.current, {
    rotation: "+=360",
  });
});

return (
  <div className="App">
    <div className="box" ref={boxRef}>
      Hello
    </div>
  </div>
);
```
