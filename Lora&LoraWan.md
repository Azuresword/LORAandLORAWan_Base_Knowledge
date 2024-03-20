#lora #lorawan
##  一些前置专用名词
ABP Activation By Personalization - 个人化激活
ADR Adaptive Data Rate - 自适应数据速率
AS Application Server - 应用服务器
AppEUI Application Extended Unique Identifier - 应用扩展唯一标识符
AppKey Application Key - 应用密钥
AppSKey Application Session Key - 应用会话密钥
BW Bandwidth - 带宽
CDMA Code Division Multiple Access - 码分多址
CHIRP Compressed High Intensity Radar Pulse - 压缩高强度雷达脉冲
CID Command IDentifier (MAC Command) - 命令标识符（MAC命令）
CR Coding Rate - 编码率
CRC Check Redundancy Cycle - 冗余校验循环
DevAddr Device Address - 设备地址
DevEUI Device Extended Unique Identifier - 设备扩展唯一标识符
FDM Frequency Division Multiplexing - 频分多路复用
FFT Fast Fourier Transform - 快速傅里叶变换
HTTP HyperText Transfer Protocol - 超文本传输协议
HSM Hardware Security Module - 硬件安全模块
IoT Internet of Things - 物联网
JSON JavaScript Object Notation - JavaScript对象表示法
JoinEUI Join Extended Unique Identifier - 加入扩展唯一标识符
JS Join Server - 加入服务器
LoRa Long Range Device to Cloud platform from Semtech - Semtech的远程设备到云平台
LoRaWAN Long Range Wide Area Network - 远程广域网
LPWAN Low Power Wide Area Network - 低功耗广域网
LTE-M Long Term Evolution Cat M1 - 长期演进类别M1
MIC Message Integrity Control - 消息完整性控制
MQTT Message Queuing Telemetry Transport - 消息队列遥测传输
NB-IoT NarrowBand Internet of Things - 窄带物联网
NS Network Server - 网络服务器
NwkSKey Network Session Key - 网络会话密钥
OTAA Over The Air Activation - 空中激活
QoS Quality of Service - 服务质量
RSSI Received Signal Strength Indication - 接收信号强度指示
SDR Software Digital Radio - 软件数字无线电
SE Secure Element - 安全元件
==SF Spreading Factor - 扩频因子==
SNR Signal over Noise Ratio - 信噪比
TDM Time Division Multiplexing - 时分多路复用
TOA Time One Air - 空中时间
TTI The Things Industries - 物联网行业
TTN The Things Network - 物联网网络
TTS The Things Stack - 物联网堆栈

## 目录结构和学习计划分析

以下是给定文本的目录结构：

1. 嵌入式系统和物联网
   1.1 物联网 (IoT)
   1.2 媒体共享模式
   1.3 采用编码的扩频技术
2. 无线电传输和传播
   2.1 单位和定义
   2.2 LoRa中的传输距离
   2.3 收发器文档
3. LoRa®调制 (物理层)
   3.1 LoRa®调制
   3.2 LoRa®和LoRaWAN®比特率
   3.3 LoRa传输的模拟
   3.4 LoRa传输的实际测试
   3.5 能量消耗
4. LoRaWAN®协议
   4.1 LoRa® - LoRaWAN® - LoRa Alliance®
   4.2 LoRaWAN网络结构
   4.3 LoRaWAN终端设备类别
   4.4 LoRaWAN终端设备的激活：ABP和OTAA
   4.5 ABP和OTAA的优缺点
   4.6 LoRaWAN帧类型
   4.7 MAC命令
   4.8 数据速率、信道和功率
5. LoRaWAN网络和LoRaWAN服务器
   5.1 不同类型的网络
   5.2 LoRaWAN网络配置
6. LoRa / LoRaWAN帧
   6.1 LoRaWAN协议层
   6.2 网关和网络服务器通信
   6.3 IP帧分析
7. 从LoRaWAN服务器导出数据
   7.1 物联网平台提供的服务
   7.2 使用HTTP GET协议导出数据
   7.3 使用HTTP POST协议导出数据
   7.4 MQTT协议介绍
   7.5 使用MQTT协议导出数据
   7.6 使用物联网平台
8. 设计自己的LoRaWAN终端设备
   8.1 可用的LoRaWAN堆栈
   8.2 微控制器 + 收发器架构
   8.3 独立LoRaWAN模块架构
   8.4 微控制器 + LoRaWAN模块架构
   8.5 无线LoRaWAN微控制器架构
   8.6 架构总结
9. 设置自己的LoRaWAN服务器
   9.1 初始信息
   9.2 ChirpStack LoRaWAN服务器
   9.3 配置ChirpStack
10. 设置自己的用户应用 - 物联网平台
   10.1 选择概述
   10.2 从头开始构建物联网平台


主要的规划是 分成三大块   
1. lora信号基础   #lora信号基础  
2. Lora和LoraWan数据协议 #Lora和LoraWan数据协议
3. Lora物联网平台的搭建 #Lora物联网平台的搭建

