Q1：频段的概念，例如868MHz频段具体有多宽，文章讲FDM提到的频段范围是867-868，欧盟标准看到863-868,865-868，863-870，很多种说法，这个具体的值要去哪里看。

A1：

Q2：在网上看到扩频码的另外一种计算方式
扩频后的信号 = 原始信号 * 扩频码序列
例如，假设原始信号为[0, 1, 0, 1]，扩频码序列为[1, -1, 1, -1]。将它们逐个相乘得到扩频后的信号为[0, -1, 0, -1]
书里给出的方法是每个bits分别乘以扩频码，也就是说 两种方法分别算出来会有4位需要传输的和16位需要传输的，这个点有点迷惑。
![[Pasted image 20240320025820.png]]

A2：
