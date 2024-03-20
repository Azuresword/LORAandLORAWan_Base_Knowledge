#  无线电传输和传播
#lora信号基础 
## 基础知识
### 单位和定义 -- dB
#dB

公式 
$power\ ratio(dB) =10.log_{10}(\frac{P_{R}}{P_{T}})$

![[Pasted image 20240320032258.png]]

如果计算后的数值是正数，那么是增益（gain），如果计算结果是负数，是一个衰减(attenuation)

公式也可以改写为
$\frac{P_{R}}{P_{T}}=10^{\frac{Power\ ratio(dB)}{10}}$
常用数值表

![[Pasted image 20240320032729.png]]

### 单位和定义 --dbm
#dBm
dBm（分贝毫瓦）是一种用于表示功率的单位，它是相对于1毫瓦（mW）的对数比值。
计算公式如下
$Power（dBm）=10*\log_{10}(\frac{Power(watt)}{0.001})$

转换后公式为
$Power(Watt) =0.001*10^{\frac{power(dBm)}{10}}$
![[Pasted image 20240320034157.png]]



### RSSI, sensitivity, SNR, link budget（接受到的信号强度，灵敏度，信噪比，链路预算）
#RSSI  #sensitivity #SNR #Link_budget 

接受端同时接受到了Power PR 和Noise PN
![[Pasted image 20240320034620.png]]

几个名词解释
RSSI  The Received Signal Strength Indication    PR

sensitivity  可感知程度  是接收器可感知的最小PR功率（最小RSSI），如果RSSI低于灵敏度，信号不可检测

SNR   信噪比  接受功率（PR）与噪声功率PN的比值

这几个值都用dB来表示 ，当满足以下条件时可以接受到信号：
RSSI > snesitivity
SNR 不低于阈值，

####  小练习
 发送端以2db的天线提供13dbm的信号，空气损耗为60db，接收天线增益2db，连接到灵敏度为-80dbm的接收器
，信号会被接受吗

13dbm+2dbi-60db+2dbi   = -43 dB

-43dB  > -80dB

==备注==:
dBm、dBi 和 dB 都是分贝（decibel，dB）的单位，但它们用来表示不同的量：

- **dBm** 表示的是绝对功率水平，以毫瓦为参考。例如，0 dBm 相当于 1 毫瓦的功率。
- **dBi** 表示的是相对增益，它比较的是一个天线与理论上的全向同相天线（isotropic antenna）的增益差异。全向同相天线是一个假想的天线，它在所有方向上均等地分散功率。
- **dB** 是一个相对单位，用于表示比例或增益/损失的变化。它是一个无维度的单位，可以用来表示任何类型的比率，包括功率比和电压比。
#### 出现问题后的解决方式
1. 读取lorawan device log 
![[Pasted image 20240320090154.png]]
显示当前  rssi  -13 snr是9.5，都是很好的数字，信号质量高
2. 如果接受功率Rp低于sensitivity，处理方法，
	1. 增加PT，但是PT也有极限限制，传输功率收到规格限制，868MHz的最大功率PT为14dBm（25mW）。
	2. 提高sensitivity，
#### Link budget
PT - snesitivity
在刚刚的练习中，信号功率为13dBm，信号敏感度为80dBm，链路预算为 93 dB
❄️In LoRa, we have a link budget of about 157 dB.
🔥In LTE (4G) we have a link budget of about 130 dB. 

![[Pasted image 20240320091914.png]]

### Lora 的传输距离
#fspl  #lora传输距离
FSPL (dB)=20log10​(d)+20log10​(f)+20log10​(c4π​)

信号在空气中的传播遵循FSPL方程

$FSPL(dB)=20\log_{10}(d)+20\log_{10}(f)+20\log_{10}(\frac{4\pi}{c})$

其他写法和常数 #Q2-FSPL的常数
![[Pasted image 20240320100445.png]]
![[Pasted image 20240320100457.png]]

其中 
- d 是发射机和接收机之间的距离（单位：米）
- f 是信号频率（单位：赫兹
- c 是光速，大约 3×10^8 米/秒
- log⁡10log10​ 表示以10为底的对数

第一功效可以在给定距离和频率的情况下计算出接受到的Pr（dBm）
Pr（dBm）=Pt（dBm）-FSPL（dB）
![[Pasted image 20240320101053.png]]

![[Pasted image 20240320101119.png]]

### 阅读一款Lora收发器的参数
![[Pasted image 20240320101725.png]]

其中支持的最大链路预算为170dB 

而在其中提到sensitivity 为148dBm

那么发射功率就是22dBm
那么出现了问题，EU标准最大发射功率为14dBm，那么最大链路预算只能到14+148=162dBm
在LoRa中，扩频系数越大，在噪声环境下的传输性能越好。
表10显示了根据扩频系数，我们将能够进行传输的信噪比。
![[Pasted image 20240320102507.png]]

随着SF的上升，SNR变低，也就是可以接受的信噪比变的更大 例如SF8可以接受噪声比信号高十倍，SF12可以接受噪声比信号高100倍。

但是随着SF的上升需要的chips/symbol也会变得更多.


