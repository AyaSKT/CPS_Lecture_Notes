#### 调制的需求
- Analog signals typically have information at lower frequencies.
- It is not practical to transmit a signal using its original frequency range due to Interference and Antenna size

调制即是把原信号的频谱变换到更高的频率上.

#### 调制类型： AM FM PM
对于 $$s(t) = A(t) \cos{(2 \pi f_c(t)t + \phi(t))}$$
- AM:  $A(t)$ 正比于 $m(t)$ 
- FM:  $f_c(t)$ 正比于 $m(t)$
- PM:  $\phi(t)$ 正比于 $m(t)$

#### AM的主要技术
- Double Side Band Suppressed Carrier (DSB-SC) modulation
- Double Side Band With Carrier (DSB-WC) modulation
	-  Also termed as Conventional Amplitude Modulation (AM)
- Single Side Band (SSB) modulation
- Vestigial Side Band (VSB) modulation

#### DSB-SC Modulation
一个baseband的message 乘上 一个有固定频率和相位的余弦波余弦波 $\cos{(2 \pi f_c(t)t + \phi(t))}$ 。 
在DSB-SC中，保持 $A(t) = 1$ 和 $\phi (t) = 0$ ，
则调制后信号为 $$\varphi_{DSB-SC} = m(t) \cos{(2 \pi f_c t)} $$
![](Assests/Pasted%20image%2020251120105023.png)

对于一个带宽为 `B Hz` 的基带信号 `m(t)`，其调制信号的带宽为 `2B Hz`。

以 `±f_c`（或以弧度计为 `±ω_c`）为中心的调制信号频谱包含两个部分：

-   **上边带**：位于 `±f_c` **之外**的部分。
-   **下边带**：位于 `±f_c` **之内**的部分。

除非消息信号 `M(f)` 在零频率处存在一个冲激函数，否则在这种调制方案中，调制信号不会包含载波频率 `f_c` 的离散分量。

#### DSB-SC Demodulation
从调制后信号恢复原信号的过程叫做解调 (Demodulation)

将接收到的信号 $\varphi_{DSB-SC}$ 乘以 $\cos{2\pi f_c t}$ ，经过LPF后可可获得原信号的1/2幅度
![](Assests/Pasted%20image%2020251120110217.png)
This is a **synchronous/coherent detection**, where the transmitter and receiver must be in-phase. 
Synchronising the receiver requires a more complex system.

实际中，传播时延是未知的，transimitter和receiver的相位都可能相对于对方漂移。
假如transimitter在发送时带有一个 $- \frac{ \pi }{2}$ 的相位，则在解调时会导致baseband相互抵消
![](Assests/Pasted%20image%2020251120110632.png)
一种解决方案是使用复指数进行解调 $$e^{j2 \pi f_c t} \Leftrightarrow \delta(f - f_c)$$
![](Assests/Pasted%20image%2020251120111417.png)
此时reciver处理的是复信号。它将乘性的相位误差因子 cos(θ) 变成了一个加性的旋转因子 $e^{j \theta}$ 。在复信号中，相位仅代表方向而非幅度，因此不会对结果的幅度造成影响，消除了相位偏移的问题。
![](Assests/Pasted%20image%2020251120111635.png)

-   **定义**：这是一种正交接收机。
-   **常用领域**：常用于雷达、声纳、超声以及磁共振成像（MRI）系统。
-   **特点**：通常，信号 $m(t)$ 是一个简单脉冲，而有用信息蕴含在相位 $\theta$ 中。例如，气象雷达中的多普勒频移信息。
-   **缺点/成本**：这种接收机的实现成本在于需要处理复信号。
-   **实现方式**：通过跟踪两个实信号来实现：实部（I 通道）和虚部（Q 通道）。

