# LORAwan网络
#Lora和LoraWan数据协议
LoRa是在两个LoRa终端设备之间或终端设备与网关之间使用的调制类型。当我们谈论整个通信链(从终端设备到LoRaWAN服务器)时，我们谈论的是LoRaWAN标准。LoRaWAN是LoRa协议的扩展，它提供了将设备安全地连接到服务器的功能，以便向最终用户提供数据。

## LORAwan 的结构
### LORA 和LORAWan 区别

LoRa物理层:调制类型(啁啾扩频)和用于在发射器和接收器之间发送数据的物理帧格式。

LoRaWAN标准:网络架构(终端设备、网关、服务器)和更具体的帧格式，允许LoRaWAN终端设备安全地将数据传输到LoRaWAN服务器。

![[Pasted image 20240325145127.png]]

在图中标识的enddevice  gateway network server 以及application server 是硬性要求，设备端和物联网平台并不包含在系统当中

### LORAWan 终端设备
#lorawan终端设备
终端设备广播信号，所有的网关都能够接收到信号并对信号进行处理
### LoraWan网关
#lorawan网关
每个LoRaWAN网关都有一个唯一的标识符(64位EUI)。此ID用于在网络服务器上注册和激活网关。 #lorawan的ID
LORAwan网关同时监听所有的信道以及扩频因子
![[Pasted image 20240325151234.png]]
在收取到lora enddevice的数据之后发送到网络服务器和应用服务器当中，这部分是通过internet ip协议发送的。
### 网络服务器
#网络服务器 #身份验证
lorawan的 network server 会对 重复性的数据进行处理并通过NwkSKey (Network Session Key).进行身份验证。
