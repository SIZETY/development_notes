# 包围盒 AABB 是什么

## 起因

学习 [pixijs-board](https://github.com/HYCS09/pixijs-noteboard.git) 遇到的 获取包围盒AABB 方法，不知道是什么

## 分析

搜索引擎搜索，结果如下：

> [碰撞检测之 AABB 包围盒](https://blog.csdn.net/weixin_43022263/article/details/108550538)

## 解决方案

### 包围盒描述

包围盒算法是一种求离散点集最优包围空间的方法。

基本思想是用体积稍大且特性简单的几何体（称为包围盒）来近似的代替复杂的几何对象。

最常见的包围盒算法有 AABB 包围盒（Axis-aligned bounding box），包围球 （Sphere），方向包围盒 OBB （Oriented bounding box）以及固定方向凸包 FDH （Fixed directions hulls 或 k-DOP）


### AABB 包围盒

AABB 包围盒就是采用一个长方体将物体包裹起来，进行两个物体的相交性检测时，仅检测物体对应的包围盒（包裹物体的长方体）的相交性。

另外，AABB 包围盒有一个重要的特性，那就是包围盒对应的长方体每一个面都是与某个坐标平面平行的，因此，AABB 包围盒又称为 **轴对齐包围盒**。

有了上述约定后，确定 AABB 包围盒就简单多了，仅需要记录 6 个值即可，这 6 个值分别代表包围盒在每个坐标上的最小值与最大值，即：xmin、xmax、ymin、ymax、zmin、zmax。

也就是说实际物体上所有的点都必须满足以下条件:

$$ Xmin <= X <= Xmax $$
$$ Ymin <= Y <= Ymax $$
$$ Zmin <= Z <= Zmax $$


另外，可以将表示 AABB 包围盒的 6 个参数分为以下两组：

$$ Pmin = [Xmin, Ymin, Zmin] $$
$$ Pmax = [Xmax, Ymax, Zmax] $$

其中，Pmin 是 3 个轴坐标中最小值的集合，Pmax 是 3 个轴坐标中最大值的集合。

知道了表示 AABB 包围盒的 6 个参数后就可以非常方便的求到 AABB 包围盒的几何中心，公式如下：

$$ c = (Pmin + Pmax) / 2 $$


### 延伸

1. AABB 包围盒计算
2. 碰撞检测 [光线与包围盒（AABB）的相交算法检测](https://blog.csdn.net/u012325397/article/details/50807880)
