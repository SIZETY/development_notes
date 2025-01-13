# view size 改变后 render 显示的 size 没有变化

## 起因

在写 note-board 的时候，有一个需求：resize 界面大小，画布宽高 resize 大小，渲染的内容不做变化，改了 view 的 `width` 和 `height`，有一部分无法渲染

## 分析

像是 render 的时候多增加出来的一部分区域没有渲染，猜测是不是有什么需要重新设置一下宽高

## 解决方案

```ts
pixiApp.view.width = newWidth
pixiApp.view.height = newHeight
pixiApp.renderer.resize(newWidth, newHeight)
pixiApp.render() // 如果不调用 render 可能会出现屏闪的情况
// 如果有设置 hitArea 需要更新 hitArea 
```