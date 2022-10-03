---
title: 基本概念和基本R-S结构
date: 2022-07-24 17:11:44
tags:
- 数字逻辑
categories:
- [数字逻辑, 触发器]
---

# 触发器

## 触发器结构

- 有两个互补的输出端Q和“非Q”
- 有两个稳定状态1和0
   - 1状态：Q=1    非Q=0
   - 0状态：Q=0   非Q=1
- 输入信号不发生变化时， 触发器状态稳定不变
- 在一定输入信号作用下，触发器可以从一个稳定状态转移到另一个稳定状态，输入信号撤销后，保持新的状态不变

## 触发器状态

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207261722903.png)

## 触发器常用描述方法

- 功能表
- 状态表
- 状态图
- 次态方程
- 激励表
- 卡诺图

### 功能表

反映了触发器在不同输入下对应的表格

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207261725285.png)
不定，是说明不允许这种输入
### 状态表

反映了触发器在输入作用下现态和次态之间的转移关系

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207261726923.png)

### 激励表

反映了触发器从现态Q转移到某种次态时，对输入信号的要求

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207261727016.png)

### 状态图

- 反映触发器两种状态之间转移关系的有向图 
- 圆圈表示稳定状态
- 有向线段表示状态转移的方向
   - 起点：现态
   - 终点：次态
   - 触发条件

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207261740349.png)
两个稳定状态：0和1

### 卡诺图

根据触发器的功能表或状态表所得到的反映触发器次态和现态以及输入关系的卡诺图

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207261741176.png)


### 次态方程

反映触发器次态和现态以及输入关系的表达式（常与约束方程一起使用）

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207261742329.png)


## 基本R-S触发器

### 与非门构成的基本R-S触发器
两个与非门和两根反馈线耦合而成

- 直接复位置位触发器
- 构成各种功能触发器的基本部件
- R：置0端或者复位端
- S：置1端或置位端

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207270834974.png)

#### RS=11

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207270835009.png)

#### RS=01

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207270836978.png)


#### RS=10

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207270837587.png)

#### RS=00

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207270837625.png)

#### 基本功能
![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202209280832129.png)


#### 描述
##### 功能表+状态表
![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207270853274.png)
d表示不确定
##### 激励表
![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207270853981.png)
##### 次态方程（重要点）
![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207270853185.png)

#### 特征
- 当与非门构成的基本R-S触发器的同一输入端连续出现多个负脉冲信号，仅第一个使触发器状态发生改变
- 可以用来消除毛刺

### 或非门构成的基本R-S触发器
两个或非门与两根反馈线耦合而成

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207270858725.png)

#### RS=00
![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207270858912.png)

#### RS=01
![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207270859900.png)

#### RS=10

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207270859879.png)
#### RS=11

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207270859918.png)
#### 基本功能
![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202209280857367.png)

#### 描述（重点注意次态方程和约束方程）
![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207270900970.png)

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207270900245.png)

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202207270900132.png)

### 总结
![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202209280903090.png)

- 与非门构成的，输入端加圈，只有R、S等于0时，才可以改变状态，因此称对低电平有效
- 而或非门构成的，输入端没有加圈只有R、S等于1时，才可以改变状态，因此称对高电平有效


- 优点（两种共有的优点）
   - 结构简单
   - 可作为记忆元件独立使用
   - 被作为各种性能完善的触发器的基本组成部分
      - 具有直接复位、置位的功能
- 缺点
   - R、S之间具有约束关系
   - 不能进行定时控制
   - 使用受到一定限制

