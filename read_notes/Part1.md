#lora信号基础 
# 物联网基础
## 四个维度
🗻 power consumption  能耗
🗻 price   价格
🗻 Size   大小
🗻 computing power  算力
![[4side.png]]
选择具体协议需要考虑的点包括：带宽，传输距离，能耗
## 常用协议
🌀BLE,Zigbee,WIFI,2G,3G,4G,5G,NFC,

![[Pasted image 20240320022810.png]]
虽然NFC的范围和带宽都不行，但是它不需要任何能量就能够正常工作。
新名词定义  ：低功率广域网 ：LPWANS #LPWANs
## 频段
有部分频段是不需要授权并且免费使用的
![[Pasted image 20240320023048.png]]

主要给LORA使用的是868MHZ，433MHz，2.4GHz附近的频段

==注意==：只有868MHz 可以给LoraWan使用

Q[[Part1Q&A]]

## media sharing

### FDM
frequency  division multiplexing
把频段分成好几个频率通道，如图
![[Pasted image 20240320024318.png]]
### TDM
TDM（Time  division multiplexing)
通过时间片的划分为不同的设备提供相同的信道，设备没有同步可能会产生碰撞
### spread spectrum（扩频技术)
#### 基本概念

Lora使用这种技术
在相同时间相同信道发送信息
但是带有特定的信号结构（包含特殊代码或符号）
接收器可以在噪声中检索到该信号。
![[Pasted image 20240320024734.png]].LoRa uses symbols instead (called Chirp), hence its name: Chirp Spread Spectrum (CSS) modulation.  啁啾拓频调制 #啁啾拓频调制 #CSS_Modulation 
#### Spreading spectrum with codes  演示
![[Pasted image 20240320025305.png]]

备注： Hadamard矩阵是以法国数学家雅克·阿达马（Jacques Hadamard）命名的一个方阵，其维度是2的幂次方（例如2x2、4x4、8x8等）。它具有特定的结构，其中每个元素要么是1，要么是-1，并且任意两行或两列之间是正交的。

Hadamard矩阵的构造遵循一种递归模式，称为Hadamard构造规则。从一个1x1的矩阵[1]开始，2阶Hadamard矩阵通过将这个1x1的矩阵复制四次并排列成一个2x2的网格来形成：

[1 1] [1 -1]

要构造4阶Hadamard矩阵，将2阶Hadamard矩阵复制四次并排列成一个4x4的网格：

[1 1 1 1] [1 -1 1 -1] [1 1 -1 -1] [1 -1 -1 1]

这个模式可以递归地延续，构造更高阶的Hadamard矩阵。

码序列（1 1 1 1; 1 -1 1 -1; 1 1 -1 -1; 1 -1 -1 1）具有"正交"的属性。正交表示这些代码序列之间彼此垂直或无关。在扩频通信中，正交码具有重要的作用。

当使用正交码进行扩频时，不同的扩频码序列之间的内积为零，即它们在时间或频域上互相垂直。这意味着在接收端，使用一个扩频码序列解扩后，其他扩频码序列的信号不会干扰解扩后的信号。这种正交性使得多个扩频信号能够在同一时间和频率上共存而不相互干扰。

传输过程 Q2[[Part1Q&A]]
##### 单用户传输
![[Pasted image 20240320030224.png]]

##### 多用户传输
信号叠加

![[Pasted image 20240320030418.png]]
解算的时候分别给不同的扩频码使用即可
![[Pasted image 20240320030434.png]]

#### Lora 使用的扩频方法
能够在同一时间，同一频道上传输。SX1261 LoRa收发器可以使用8个“扩展码”，称为“扩展因子”[SF5, SF6, SF7, SF8, SF9, SF10, SF11和SF12]。因此，我们可以在同一频道上同时进行8次传输。真正的SF(扩散因子)参数将在第3章中详细解释。在LoRaWAN标准中，我们只使用六个SF [SF7到SF12]。

