# LoRa®调制(物理层)   

## 基础概念
### chirp

(Chirp: Compressed High Intensity Radar Pulse).
![[Pasted image 20240321123643.png]]

啁啾脉冲的形式如上图所示，
起始频率是信道频率减去带宽除以2。最后的频率是信道频率加上带宽除以2。图9表示频域中的LoRa调制。
小练习
A LoRa transmission uses the 868,1 MHz channel with a bandwidth of 125 kHz. Can you 
give the start and end frequency of the Chirp?

start: 8681000000 -125000/2 =868 037 500 Hz 
end : 868 162 500 Hz = 868 100 000 + 125 000/2
### 对symbol（chirp）的理解

根本性的理解---例如找一个 SF2 来做展示： 
有4种可能的组合：

1. 00
2. 01
3. 10
4. 11

因此，在SF2编码模式下，你会有4种不同的符号（Chirps），每种符号对应于上面的一种组合。这些符号在传输过程中通过变化其频率的起始点来区分。即使所有符号都会覆盖相同的频率范围并且都有相同的长度和形状，每个符号的频率变化开始点都是唯一的，这样接收器就能区分它们代表的是哪两位二进制代码。

在实际的LoRa系统中，符号是通过频率扫描来实现的。例如，如果我们有一个125kHz的带宽和868.1MHz的中心频率（这是一个典型的LoRa频段），SF2模式下的频率扫描可能是这样的：

- 符号0（代表二进制00）可能从868.075MHz开始，增加到868.2MHz。
- 符号1（代表二进制01）可能从868.085MHz开始，同样增加到868.2MHz。
- 符号2（代表二进制10）可能从868.095MHz开始，增加到868.2MHz。
- 符号3（代表二进制11）可能从868.105MHz开始，增加到868.2MHz。

举个具体的例子，如果你要发送一个二进制序列 `110010`，在SF2下，你会将这个序列分成每2位一组，即 `11` `00` `10`。然后，根据每组的不同，你会发送对应的符号。所以对于 `11`，你会发送符号3，对于 `00`，你会发送符号0，对于 `10`，你会发送符号2。这样，接收器只需要识别出每个符号的起始频率，就可以知道每个符号代表的是哪两位二进制数据了。
![[Pasted image 20240321181526.png]]

### 符号传输时间
![[Pasted image 20240321181633.png]]
在中心频率和带宽一致的情况下 传输时间取决于 SF值， 

具体计算公式
$T_{symbol} =\frac{2^{SF}}{BD width}$
在125KHZ情况下，不同SF值传输的时间
![[Pasted image 20240321182520.png]]
### Lora 在空气中的传输时间
Lora具体的一帧数据包括了，payload，preamble，CRC 三部分
![[Pasted image 20240321182730.png]]
$Time\ on\ air = n_{symbol}*T{symbol}$
$n_{symbol}$是lora的一帧数据的总的字节数

## LoRa® and LoRaWAN® bit rate
### Lora bit rate
计算公式：

$Bit\ Rate= SF*\frac{BDwidth}{2^{SF}}$
#### 案例1（SF7, 125 kHz）

- **扩频因子（SF）**：7
- **带宽（BW）**：125 kHz

计算比特率：

$\text{Bit Rate}_{\text{1}} = \frac{7 \times 125,000}{2^7} = \frac{875,000}{128} \approx 6835.94 \, \text{bps}$
#### 案例2（SF12, 125 kHz）

- **扩频因子（SF）**：12
- **带宽（BW）**：125 kHz

计算比特率：

$\text{Bit Rate}_{\text{2}} = \frac{12 \times 125,000}{2^{12}} = \frac{1,500,000}{4096} \approx 366.21 \, \text{bps}$

案例1的比特率大约为6836 bps，案例2的比特率大约为366 bps。这表明在LoRa通信中，较高的扩频因子会减少比特率，但可以增强信号的穿透力和覆盖范围。

## 编码率对比特率的影响

CR coding rate  和 bit rate 之间存在相关关系  

CR 4/8代表 4个有效bit  编码为8个实际bit  overhead倍数为2
几个个实际的计算案例   

Case 1: For SF7, 125 kHz and CR4/5 > $bit rate = 6.836 kbps / 1.25 = 5469\ bps$
Case 2: For SF12, 125 kHz and CR4/5 > $bit rate = 366 bps / 1.25 = 293\ bps$
![[Pasted image 20240321185509.png]]

### Influence of the LoRa overhead on the bitrate

![[Pasted image 20240321190632.png]]

LORA frame 的所有内容，Lora data是存放在PHY payload当中的

现在主要关注time on air
在下面的案例当中
模拟了SF7、BW125和具有1字节PHY负载的CR4/5传输的Time on Air。
![[Pasted image 20240321190826.png]]

### Influence of LoRaWAN overhead on the bitrate
当我们使用lorawan的时候

![[Pasted image 20240321191143.png]]
user data不完全等于PHY payload   而是和LORAWAN header 一起组成PHY payload
![[Pasted image 20240321191740.png]]
LORAWAN header 一般是13个字节，上面的实际表里涉及到13个字节
+1个字节的有效负载
### Influence of the duty-cycle in the EU868 band

EU868 对于占空比有明确要求：占空比不得大于1%，
对于刚刚验证过的两组参数，现在的bps如下所示：
Case 1: For SF7, 125 kHz and CR4/5 > bit rateLoRaWAN payload 1% = 172.7 bps / 100 = 1.73 bps
Case 2: For SF12, 125 kHz and CR4/5 > bit rateLoRaWAN payload 1% = 6.9 bps /100 = 0.07 bps

此处有一个特殊需要知道的情况：
因为1%占空比规定适用于以下每个频段

863.0 – 868.0 MHz: 1%
868.0 – 868.6 MHz: 1%

这意味着如果一个LoRa终端设备在867.1 MHz信道(863.0 868.0 MHz的一部分)上发送一个LoRa帧，该设备仍然允许在868.1 MHz信道(868.0 - 868.6 MHz的一部分)上发送另一个帧。

## Influence of the LoRaWAN server use policy

oRaWAN服务器还可以限制允许发送的消息数量。

# LORA 传输仿真

## Time on Air 计算

$Time\ on\ air = n_{symbol}*T{symbol}$

n是总共在一帧lora数据当中包含的symbol。
$T_{symbol}=\frac{2^{SF}}{BDwidth}$（附带做个解释，2^SF 是扩频码的可能组合数）
是发送一个symbol所花费的时间

nsymbol计算公式：
![[Pasted image 20240322144301.png]]

在公式里面：
payload  -> lora负载
SF  -> 扩频因子
H =0 ，  Header enable or not
DE =1  ,  low data rate  enable or not 
CR coding rate from 1 to 4
## chirp modulation（调制）
![[Pasted image 20240322150101.png]]

matlab仿真流程，假如symobols：n,再加入本地振荡器通道，f.最后输出lota(t)
例如在SF12的情况下，n=0,1024,2048,3072 情况下频谱图

## chirp demodulation（解调）

![[Pasted image 20240322150338.png]]
1. **LoRa信号（lora(t)）**：这是原始接收到的LoRa信号，是通过空中传输的Chirp信号。
    
2. **本地振荡器和混频器**：接收信号首先与本地振荡器（Local oscillator）产生的信号相结合。这一步骤中，本地振荡器的频率与接收信号的载波频率（f_channel）一致。混频器将LoRa信号转移到基带频率，这样更容易处理。
    
3. **混合下行Chirp（down(t)）**：在信号被转移到基带后，它会与一个预定的下行Chirp信号混合。这一步是为了提取出传输的原始符号信息。通过将接收信号与下行Chirp相乘，可以使信号的频率偏移反映出原始的符号索引。
    
4. **滤波和快速傅立叶变换（FFT）**：混合后的信号会通过一个滤波器，以去除任何不需要的频率成分。然后使用FFT来提取信号中的频率成分，因为在LoRa中，不同的频率表示不同的符号索引。
    
5. **提取符号**：FFT的结果会被用来找到demod(t)的频率，这个频率与原始的符号索引（n）相对应。这个索引值被用来恢复传输的数据。
