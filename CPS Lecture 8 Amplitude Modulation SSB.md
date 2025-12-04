#### SSB的需求
-   双边带频谱 (DSB spectrum)（包括抑制载波 (suppressed carrier) DSB-SC 和常规调幅 (AM)）包含两个边带 (sidebands)：
    -   上边带 (Upper Sideband, USB)
    -   下边带 (Lower Sideband, LSB)
    -   这两个边带都包含了基带信号 (baseband signal)  $m(t)$  的完整信息。
-   对于一个带宽为  $B$  Hz 的基带信号  $m(t)$ ，DSB 调制需要两倍于此，即  $2B$  Hz 的射频带宽 (radio-frequency bandwidth) 进行传输。
-   由于每一个边带都承载了消息信号 (message signal) 的完整信息，因此其中任意一个都足以在接收端恢复出原始消息信号。
-   单边带调制 (Single-Sideband modulation, SSB) 通过移除 (removes) 下边带 (LSB) 或上边带 (USB)，使得传输一个消息信号  $m(t)$  仅需要  $B$  Hz 的带宽，从而提高了调幅 (amplitude modulation) 的频谱效率 (spectral efficiency)。
![](Assests/Pasted%20image%2020251121083206.png)
**SSB的transimitter和receiver必须提前约定好使用LSB还是USB**
![](Assests/Pasted%20image%2020251121083308.png)

#### 希尔伯特变换 Hilbert Transform
希尔伯特变换或称正交滤波 (quadrature filtering) 是一种全通滤波操作 (all-pass filtering operation)。该变换保持输入信号幅度谱 (magnitude spectrum) 不变，但会对其频谱产生特定相移 (phase shift)：
- 对信号的正频率部分 (positive frequency spectrum) 产生 -90° 的相移
- 对信号的负频率部分 (negative frequency spectrum) 产生 +90° 的相移

对于信号  $x(t)$ ，其希尔伯特变换  $x_h(t)$  定义为：
$$x_h(t)=\mathcal{H}\{x(t)\}=\frac{1}{\pi} \int_{-\infty}^{\infty} \frac{x(\alpha)}{t-\alpha}  d\alpha$$
这等价于信号与核函数的卷积运算：
$$x_h(t) = x(t) * \frac{1}{\pi t}$$

希尔伯特变换在频域中定义为信号频谱与传递函数的乘积：
$$X_h(f) = -jX(f)\mathrm{sgn}(f)$$

希尔伯特变换器的传递函数为：
$$H(f) = -j\mathrm{sgn}(f) = 
\begin{cases} 
-j = 1\cdot e^{-j\pi/2}, & f > 0 \\
j = 1\cdot e^{j\pi/2}, & f < 0 
\end{cases}$$

从图示可以看出希尔伯特变换的频域特性：
![](Assests/Pasted%20image%2020251121084105.png)

- $|H(f)| = 1$（对所有  $f \neq 0$ ）
- 幅度谱为常数1，表明是**全通滤波器** (all-pass filter)
- $\theta_h(f) = -\pi/2$（当  $f > 0$ ）
- $\theta_h(f) = \pi/2$（当  $f < 0$ ）
- 相位谱呈现奇对称特性

希尔伯特变换器是一个**理想相移器** (ideal phase shifter)：
- 保持所有频率分量的幅度不变
- 对正频率分量产生  $-\pi/2$  的相移
- 对负频率分量产生  $+\pi/2$  的相移
- 通过改变  $m(t)$  每个频率分量的相位来产生其希尔伯特变换  $m_h(t)$
![](Assests/Pasted%20image%2020251121084326.png)

#### SSB AM
对于消息信号  $m(t)$  的频谱  $M(f)$ ，可以将其分解为右半部分 (right half) 和左半部分 (left half) 来进行分析。

右半信号定义为消息谱在正频率部分的分量：

$$ \begin{aligned} M_{+}(f) &= M(f)\cdot u(f) = M(f)\frac{1}{2}[1+\mathrm{sgn}(f)]\\ &=\frac{1}{2}[M(f)+jM_{h}(f)]\end{aligned} $$

其中：
- $u(f)$ 是单位阶跃函数 (unit step function)
- $\mathrm{sgn}(f)$ 是符号函数 (signum function)
- $M_h(f)$ 是  $M(f)$  的希尔伯特变换 (Hilbert transform)

左半信号定义为消息谱在负频率部分的分量：

$$ \begin{aligned} M_{-}(f) &= M(f)u(-f) = M(f)\frac{1}{2}[1-\mathrm{sgn}(f)]\\ &=\frac{1}{2}[M(f)-jM_{h}(f)]\end{aligned} $$
![](Assests/Pasted%20image%2020251121084824.png)

-   上边带频谱可以用消息信号  $m(t)$  及其希尔伯特变换  $m_h(t)$  表示为：
    $$
    \begin{aligned}
    \Phi_{\mathrm{USB}}(f) &= M_{+}(f-f_{c}) + M_{-}(f+f_{c}) \\
    &=\frac{1}{2}[M(f-f_{c}) + M(f+f_{c})] - \frac{1}{2j}[M_{h}(f-f_{c}) - M_{h}(f+f_{c})]
    \end{aligned}
    $$
![](Assests/Pasted%20image%2020251121091129.png)

-   利用傅里叶变换的频移特性，进行傅里叶反变换得到时域表达式：
    -   上边带信号： $\varphi_{\mathrm{USB}}(t) = m(t)\cos\omega_{c}t - m_{h}(t)\sin\omega_{c}t$ 
    -   下边带信号： $\varphi_{\mathrm{LSB}}(t) = m(t)\cos\omega_{c}t + m_{h}(t)\sin\omega_{c}t$ 

-   单边带信号的通用时域表达式可以统一写为：
    $$
    \varphi_{\mathrm{SSB}}(t) = m(t)\cos\omega_{c}t \mp m_{h}(t)\sin\omega_{c}t
    $$

#### SSB Signal Generation
![](Assests/Pasted%20image%2020251121091453.png)

##### 选择性滤波法 (Selective Filtering)
###### 单步调制 One-step
-   **基本原理**：通过一步调制过程 (One-step Modulation Process) 产生双边带 (DSB) 信号，再使用带通滤波器 (BPF) 滤除不需要的边带，保留所需边带 (如上边带 USB)。
-   **关键参数：间隙带宽 (Gap-band)**
    -   在基带信号中，直流间隙带宽定义为  $\omega_{g}=2\pi f_{g}$ 。
    -   经调制后，在载波频率  $f_c$  处，DSB 信号的边带间隙带宽变为  $2\omega_{g}=4\pi f_{g}$ 。
-   **间隙带宽的作用**：该带宽允许使用渐变截止滤波器 (gradual cut-off filters)，降低了实现理想陡峭滤波器的难度。
-   **滤波器性能要求**：为最小化邻道干扰 (adjacent channel interference)，对不期望边带的衰减应至少达到 40 dB。
![](Assests/Pasted%20image%2020251121093146.png)

###### 两步调制 Two-step / Weaver's Method
-   当载波频率过高，间隙带 (Gap-band) 小于  $2f_g$  时，采用中间载波频率  $\omega_{c1}$  先生成一个具有有效更宽间隙带的中间单边带信号 (Intermediate SSB signal)。
![](Assests/Pasted%20image%2020251121093853.png)

-   为防止下边带 (Lower Sideband) 在频率原点附近产生干扰，需满足设计条件：
    $$2(\omega_{c1}+\omega_{g})\geq 0.01\omega_{c2}$$

-   为在目标频率  $\omega_{c2}$  处获得足够的间隙带，需满足设计条件：
    $$\omega_{c1}\geq B+\omega_{g}$$

其中参数定义：
-   $\omega_g$：基带信号的间隙带宽 (Gap-bandwidth)
-   $B$：基带信号的带宽 (Bandwidth)  
-   $\omega_{c1}$：中间载波频率 (Intermediate carrier frequency)
-   $\omega_{c2}$：最终载波频率 (Final carrier frequency)

#### SSB Demodulation
其Demodulator与DSB-SC的synchronous demodulator完全一致
![](Assests/Pasted%20image%2020251121110222.png)
-   单边带抑制载波 (SSB-SC) 信号表达式为：
    $$
    \varphi_{\mathrm{SSB}}(t)=m(t) \cos \omega_{c} t \mp m_{h}(t) \sin \omega_{c} t
    $$

-   解调过程将该信号与载波相乘：
    $$
    \varphi_{\mathrm{SSB}}(t) \cos \omega_{c} t=[m(t) \cos \omega_{c} t \mp m_{h}(t) \sin \omega_{c} t] \cdot 2 \cos \omega_{c} t
    $$

-   展开后得到：
    $$
    =m(t)[1+\cos 2 \omega_{c} t] \mp m_{h}(t) \sin 2 \omega_{c} t
    $$

-   可进一步表示为：
    $$
    =m(t)+\underbrace{[m(t) \cos 2 \omega_{c} t \mp m_{h}(t) \sin 2 \omega_{c} t]}_{\text{载波频率为 } 2\omega_{c} \text{ 的 SSB-SC 信号}}
    $$

-   解调结果分析：
    -   产生基带信号 (baseband signal)  $m(t)$
    -   同时产生载波频率为  $2\omega_{c}$  的另一 SSB 信号
    -   通过低通滤波器 (low-pass filter) 可抑制不需要的 SSB 分量，得到所需的基带信号  $m(t)$

#### Summary
-   **advantages**
    -   允许更好的频谱管理 (better management of the frequency spectrum)。在给定的频率范围内，相比 dsb 信号，可以容纳更多的传输 (more transmission can fit)。
    -   所有发射功率都用于传输信息 (all of the transmitted power is message power)，没有功率浪费在载波上 (none is dissipated as carrier power)。
    -   信号的噪声含量是带宽的指数函数 (the noise content of a signal is an exponential function of the bandwidth)：带宽减半，噪声降低 3db (the noise will decrease by 3db when the bandwidth is reduced by half)。因此，ssb 信号比 dsb 信号受到的噪声污染更小 (ssb signals have less noise contamination)。

-   **limitations**
    -   ssb 接收机的成本高于 dsb 接收机 (the cost of a ssb receiver is higher)。
    -   普通无线电用户通常只希望进行开关机和选台操作 (to flip a power switch and dial a station)。ssb 接收机需要多次精确的频率控制设置以最小化失真 ，并且在使用过程中可能需要持续调整 (may require continual readjustment)。
