# container.localTransform 是什么

## 起因

学习 [pixijs-board](https://github.com/HYCS09/pixijs-noteboard.git) 遇到的 `rootContainer.localTransform`，不知道是什么

## 分析

chatgpt 查询

## 解决方案

`rootContainer.localTransform` 是在图形编程（例如使用矩阵变换来控制图形对象的位置、旋转和缩放）中常见的一个术语。这个矩阵通常用来描述一个对象在其父容器中的变换状态。

在具体的上下文下，比如使用某种图形库或框架（比如 PIXI.js、CreateJS 等），localTransform 矩阵主要包含以下几个变换信息：

1. **平移（Translation）**：对象在坐标系中的位置。
2. **缩放（Scaling）**：对象在 x 和 y 方向上的缩放比例。
3. **旋转（Rotation）**：对象的旋转角度。

这个矩阵通常是 3x3 矩阵（在二维图形中）或 4x4 矩阵（在三维图形中），并可以通过矩阵乘法来组合多个变换。

### 3x3 矩阵的结构（二维情况）

在二维图形中，localTransform 的结构如下：

```scss
| sx * cos(θ)   sy * -sin(θ)   tx |
| sx * sin(θ)   sy * cos(θ)    ty |
| 0             0              1  |
```

- `sx`, `sy`: 分别表示 x 和 y 方向的缩放因子。
- `θ`: 旋转角度。
- `tx`, `ty`: 分别表示平移的 x 和 y 坐标。

### 用途

通过修改这个矩阵，可以轻松实现对象的移动、旋转和缩放等操作。在渲染时，图形系统会根据这个矩阵来确定对象在屏幕上的最终展示状态。

### 总结

`rootContainer.localTransform` 是一个用于描述对象在其父容器内变换关系的矩阵，通常包含平移、旋转和缩放的信息。在实际开发中，可以根据需要对其进行修改，以实现复杂的图形变换效果。
