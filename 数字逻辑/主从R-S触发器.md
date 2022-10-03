---
title: 主从R-S触发器
date: 2022-07-27 09:10:54
tags:
- 数字逻辑
categories:
- [数字逻辑, 触发器]
---
# 主从RS触发器
为了解决空翻问题引入

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207270933441.png)

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207270934220.png)

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207270935644.png)

- 输入端$R_D$：直接置0端
	- $R_D$等于0时，会使得Q等于0
- 输入端$S_D$：直接置1端
	- $S_D$等于0时，Q就等于1
- 在正常工作时，它们都不能等于0，因为它一旦等于0，直接置0或者置1了。都等于0，又违背了约束条件，所以正常工作时，一般让它们都为1
- 因为它们都为1，对与非门是不起作用的，于是分析的时候可以不看它们

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207270942684.png)
主触发器的输出是从触发器的输入
![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207270942377.png)
主触发器和从触发器时钟反相
- CP=1
	- 从触发器锁定
	- 主触发器响应
- CP=0
	- 主触发器锁定
	- 从触发器响应

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207270948578.png)
## 分析
- 总结
   - 前沿采样
   - 后沿定局
   - 状态变化是在时钟脉冲的后沿
   - 状态变化锁定在一个时间点，而不是一个时间段，过了这个状态，无论它怎么变化，主触发器的状态是被锁定的，因此不会导致从触发器发生变化（就是图中一点的例子），因此无“空翻”
对于此触发器而言。它的状态变化是发生在CP的下降沿，因此称它为下降沿触发器
![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202210031013494.png)
加了一个小圆圈，加了表示下降沿触发，不加便是上升沿触发
## 功能

- 主触发器输出
- 从触发器输入
- 与钟控触发器功能一致

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202210031015139.png)
![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207271050266.png)

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207271050046.png)
