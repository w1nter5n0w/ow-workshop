---
title: 矢量和向量
lang: zh-CN
---

## 矢量

矢量是一个由三个数字组成的、有方向的量。在OW中，矢量更类似于一个三维坐标点。又分为本地矢量和地图矢量。

本地矢量即原点位于玩家位置，玩家面对方向为Z轴正方向的坐标系。如图所示：

![1.png](https://i.loli.net/2019/05/02/5ccae0fceed41.png)

在这张图中，Z轴正方向为玩家面对的方向。X轴正方向为玩家左侧。Y轴正方向为玩家上方。例如，坐标(1,1,1)即位于玩家的左上方，向前倾。图中的H点坐标为(1,2,1)。

本地矢量和地图矢量可以通过函数“地图矢量”和“本地矢量”互相转换。

## 向量

矢量和向量其实是一个东西。在OW中，向量可以用来方便的表示一个矢量到另一个矢量的方向。

即：`向量(A, B)=矢量(Xb - Xa, Yb - Ya, Zb - Za)`

## 示例

举个例子，我们希望实现一个效果：伤害敌人造成击退。假设A击中B时，我们希望让B在A-B向量上移动10单位。

### 施加推力+向量

这是最简单的实现方式，不做详细解释：

事件
* 玩家受到伤害
* 队伍 双方 全部

动作
* 施加推力(事件玩家, 向量(位置(攻击方), 位置(事件玩家)), 10, 至地图, 取消相反运动)

### 施加推力+矢量

我们也可以手动计算矢量：

事件
* 玩家受到伤害
* 队伍 双方 全部

动作
* 施加推力(事件玩家, 矢量(减(X方向分量(位置(攻击方)), X方向分量(位置(事件玩家))), 减(Y方向分量(位置(攻击方)), Y方向分量(位置(事件玩家))), 减(Z方向分量(位置(攻击方)), Z方向分量(位置(事件玩家)))), 10, 至地图, 取消相反运动)

### 三角函数计算

我们演示一下三角函数的使用。因为比较复杂，特别是OW中编写就更复杂了，所以实际上不会这样写，仅作为参考：

* 通过“向量”我们可以得到一个方向，假设是向量A(X,Y,Z)。
* 余弦：计算向量A与向量(0,Y,Z)的夹角（即向量A与Y-Z平面的夹角），则可以得出Z方向位移=总距离*cos(夹角)
* 正弦：计算向量A与向量(X,Y,0)的夹角（即向量A与X-Y平面的夹角），则可以得出Z方向位移=总距离*sin(夹角)

正弦和余弦可以这样计算：

* `sin = a × b / |a||b|`，可以使用矢量积函数帮助计算
* `cos = a · b / |a||b|`，可以使用标量积函数帮助计算