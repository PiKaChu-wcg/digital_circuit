# 数字电路课程设计

## 设计方案

### 设计思路

#### 设计要求

本方案要求设计一个模拟信号交通灯

1. 输入电源:直流5V,电流不小于500mA
2. 用红绿两种发光二极管组成一对，模拟交通红绿信号灯.
3. 红绿灯转换中间无黄灯和闪烁提示.
4. 采用两位 7 段数码管,实时显示当前路口通行或禁行剩余时间.
5. 按照每秒减 1 进行显示.
6. 红绿灯转换时间由设置电路设置,可以实现只有设置.

#### 译码显示

采用最简便的DCD_HEX数码管来实现

#### 计数单元

计数单元中由于每隔15秒变换一次红绿灯，我采用了两个74LS192级联，采用减法计数，将一端输出作为另一个74LS194的时钟，并采用置数法，在达到0秒的时候立即置数为15。

#### 定时单元

在定时单元通过一个555定时器组成一个多谐振荡器来产生周期为1s的时间脉冲，从而为30秒倒计时提供了脉冲输入。这里取$R1=51k\Omega$，$R2=47 k $，$C=10\mu F$。由于震荡周期$T=\approx (R1+R2)C=0.7\times (51k\Omega+2\times 47k)\times 10 \mu F=1.015s$，符合实验要求的。

#### 指示灯模块

将同步JK触发器,JK端相连,从而构成同步T触发器,在下降沿到来时，将输出翻转,使得红绿二极管变换显示.

### 具体方案

#### 倒计时

![倒计时](https://github.com/PiKaChu-wcg/digital_circuit/blob/main/daojishi.png)

#### 设置时间

![设置模块](https://github.com/PiKaChu-wcg/digital_circuit/blob/main/shezhi.png)

#### 计数脉冲

![震荡器](https://github.com/PiKaChu-wcg/digital_circuit/blob/main/signal.png)

#### 汇总

![汇总](https://github.com/PiKaChu-wcg/digital_circuit/blob/main/all.png)

### 需要的元器件

| 序号  | 类型   | 名称          | 数量 | 作用 |
| ----- | ------ | --------  | ---- | ---- |
| :one: | 计数器 | 74LS192D       | 2 | 信号灯倒计时 |
| :two: | 计数器 | 74LS160D | 2 | 设置倒计时复位值 |
| :three: | 数码显示器 | DCD_HEX | 4 | 显示倒计时和设置时间 |
| :four: | 灯泡 | PROBE_DIG_RED,<br>PROBE_DIG_RED | 各一个 | 信号灯 |
| :five: | 门电路 | 74LS32D | 1 |  |
| :six: | 555定时器 | 555_VIRTUAL | 1 | 提供定时脉冲 |
| :seven: | 同步T触发器 | 74LS112D | 1 | 存储状态 |
| :eight: | 电阻 | 51k,47k | 各一个 |  |
| :nine: | 电容 | $10\mu F$,$0.01\mu F$ | 各一个 |  |

​	

