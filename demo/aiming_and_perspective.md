---
title: 自瞄和透视
lang: zh-CN
---

# 自瞄和透视

## 自瞄

### 规则1

事件
* 持续 - 每名玩家
* 队伍 双方 全部

条件
* 按钮被按下(事件玩家, 主要攻击模式) == 真

动作
* 开始朝向(事件玩家, 向量(位置(事件玩家), 位置(距离准心最近的玩家(事件玩家, 对方队伍(队伍(事件玩家))))), 1000, 至地图, 方向及角速率)

解析
* 通过“条件”，我们找到了正在开枪的玩家（下面成为A玩家）
* “开始朝向”可以移动玩家正面方向，我们要移动的是“事件玩家”，即A玩家
* “方向”为向量，意思是从A玩家，到离准心最近的对方玩家
* 如何找到准心最近的对方玩家？这个玩家应该满足两个条件：一是距离A玩家的准心最近，二是属于对方队伍。
* 因此，我们从A玩家 - 队伍 - 对方队伍，即可找到对方玩家
* 最后，“角速度”用来让“自瞄”更“暴力”一些
* 另外，在这个例子中，我们只设定了“主要攻击模式”。如果需要设定辅助攻击模式，则需要再添加一个规则

### 规则2

事件
* 持续 - 每名玩家
* 队伍 双方 全部

条件
* 按钮被按下(事件玩家, 主要攻击模式) == 假

动作
* 停止朝向(事件玩家)

## 透视

事件
* 持续 - 每名玩家
* 队伍 双方 全部

条件
* 无

动作
* 创建图标(所有玩家(所有队伍), 事件玩家, ARROW: DOWN, 可见和位置, 绿色, 假)

解析
* 我们给事件玩家创建了一个箭头
* 这个箭头可以被所有队伍的所有玩家看见