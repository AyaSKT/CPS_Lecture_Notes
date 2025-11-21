#### DSB-WC/Conventional AM的需求
-   DSB-SC已调信号可能已经传输了数百英里，甚至可能遭受未知的多普勒频移 (Doppler frequency shift)。
-   对DSB-SC信号进行相干解调 (coherent demodulation) 要求receiver拥有一个与输入载波  $\cos(2\pi f_c t)$  同步的载波信号。这一要求在实践中不易实现。
    -   这样的receiver将更难实现，且可能相当昂贵。
    -   这种成本限制了其在广播系统 (broadcasting systems)（每个transmitter对应众多receivers）中的应用。
-   相干解调器 (coherent demodulator) 的一种替代方案是，由transmitter在发送已调信号  $m(t) \cos(2\pi f_c t)$  的同时，附带发送一个载波  $A \cos(2\pi f_c t)$ ，使得receiver无需生成本地相干载波 (coherent local carrier)。
    -   这导致了在广播系统中使用一个昂贵的大功率transmitter，以及多个更简单、更廉价的receivers。
-   这种将载波与已调信号一同传输的方式，被称为常规调幅 (conventional AM)（或AM，也可称为DSB-WC）。

#### DSB-WC Modulation
 $$\varphi_{AM}(t) = [A + m(t)] \cos{(2 \pi f_c t)}$$ 
![](Assests/Pasted%20image%2020251120143359.png)
其频谱与DSB-SC基本一致，但在  $\pm f_c$  处有两个额外的冲激响应。
 $$[A+m(t)] \cos (2 \pi f_c t) \Leftrightarrow \frac{1}{2}[M(f+f_c)+M(f-f_c)]+\frac{A}{2}[\delta(f+f_c)+\delta(f-f_c)]$$ 
![](Assests/Pasted%20image%2020251120143706.png))

#### DSB-WC的缺点

-   作为双边带系统 (double-sideband system), AM在带宽使用上是浪费的，因为传输消息信号中的信息实际上只需要一个边带 (sideband) 就足够了。
-   在传输功率 (transmitted power) 方面，AM的效率也很低 (inefficient), 因为它在传输边带 (sidebands) 的同时还传输了一个大幅度的载波 (large carrier amplitude), 而这个载波本身并不传递任何信息。
-   已调信号 (modulated signal) 的带宽是原始消息信号 (message signal) 带宽的两倍 (double)。如果消息信号带宽为  $B$ Hz, 则AM信号带宽为  $2B$ Hz。

#### AM 信号包络（Envelope）

载波振幅与消息信号振幅之和称为信号包络，其数学表达式为：
 $$E(t) = A + m(t)$$ 
其中  $A$  是载波振幅， $m(t)$  是消息信号。

- 当载波振幅等于或大于消息信号振幅时，调幅信号的包络是消息信号的**真实复现**（true replica）。
- 这是调幅系统中期望的正常工作状态。

- 当载波振幅小于消息信号振幅时，信号包络将出现**正值和负值**。
- 此时包络被整流，成为消息信号的**失真版本**(distorted version)。
- 这种情况称为**载波过调制**(over-modulated)，会导致信号严重失真。
![](Assests/Pasted%20image%2020251120145341.png)

#### AM 调制指数（Modulation Index）
The modulation index μ is the ratio of the peak value of the message signal(  $m_p$  ) to the amplitude of the carrier.
 $$\mu = \frac{m_p}{A_c}$$ 
![](Assests/Pasted%20image%2020251120145953.png)
**更大的调制指数可以减少功耗，但更难以解调。当  $\mu > 1$  时出现过调制**

#### AM 功率效率

AM信号功率包含两个组成部分：
 $$\phi_{\mathrm{AM}}(t) = (A + m(t)) \cos(2\pi f_c t) = A \cos(2\pi f_c t) + m(t) \cos(2\pi f_c t)$$ 
- 载波分量 (carrier component):  $A \cos(2\pi f_c t)$ 
- 边带分量 (sidebands component):  $m(t) \cos(2\pi f_c t)$ 

##### 载波功率(Carrier Power)
 $$P_c = \frac{1}{2} A^2$$ 
载波功率是固定值，不携带信息。

##### 边带功率 (Sideband Power)
 $$P_s = \frac{1}{2} P_m$$ 
其中  $P_m$  是消息信号功率，边带功率携带全部有用信息。

##### 功率效率
- 功率效率 (power efficiency) η 衡量调制技术在功耗方面的效率
- 定义为信息承载部分功率与调制信号总功率的比值
 $$\eta = \frac{\text{useful power}}{\text{total power}} = \frac{\text{sideband power}}{\text{total power}}$$ 

- 边带功率 (sideband power):  $P_s = \frac{1}{2} P_m$ 
- 总功率:  $P_c + P_s$ 
- 功率效率表达式:
 $$\eta = \frac{P_s}{P_c + P_s} = \frac{\frac{1}{2} P_m}{P_c + \frac{1}{2} P_m} = \frac{P_m}{A_c^2 + P_m}$$ 

#### AM Demodulation
检测 (detection) 指从接收数据中提取信号的过程，在某些情况下等同于解调 (demodulation)。
包络检测 (envelope detection) 要正常工作需满足两个条件：
载波频率必须远大于调制信号带宽：
 $$f_c \gg \text{bandwidth of } m(t)$$ 
否则频谱的正负分量会产生重叠 (spectral components overlap)。

载波与调制信号幅度之和必须非负：
 $$A + m(t) \geq 0$$ 
否则当  $A + m(t) < 0$  时会出现相位反转 (phase reversals)。

包络检波器 (envelope detector) 用于从AM调制信号中提取原始基带信号，是常规调幅广播接收机中的核心解调电路.
![](Assests/Pasted%20image%2020251120152711.png)

- 当输入信号  $v_i(t)$  处于正半周时，二极管正向偏置导通
- 电容  $C$  通过二极管快速充电，充电时间常数  $\tau_{charge} = R_d C$  很小
- 电容电压  $v_c(t)$  紧跟输入信号的峰值变化

- 当输入信号电压低于电容电压时，二极管反偏截止
- 电容通过电阻  $R$  缓慢放电，放电时间常数  $\tau_{discharge} = RC$  较大
- 通过合理选择  $RC$  参数，使放电曲线在下一个正半周峰值处重新开始充电

- 放电时间常数应满足：  $\frac{1}{f_c} \ll RC \ll \frac{1}{W}$ 
- 其中  $f_c$  为载波频率， $W$  为调制信号最高频率
- 此条件确保电容电压能有效跟踪包络变化而纹波很小

电容两端的电压  $v_c(t)$  近似再现了原始调制信号的包络  $A + m(t)$ ，从而完成解调过程。

整流检波器将半波整流波形应用于低通滤波器 (low-pass filter)，不同于传统AM包络检波器中的平滑电容器。
![](Assests/Pasted%20image%2020251120153109.png)
整流后的信号可表示为：
 $$V_{\text{rect}}(t) = [(A_C + m(t)) \cos(\omega_C t)] \cdot p(t)$$ 

其中  $p(t)$  为开关函数，用傅里叶级数展开：
 $$p(t) = \frac{1}{2} + \frac{2}{\pi}[\cos(\omega_C t) - \frac{1}{3}\cos(3\omega_C t) + \frac{1}{5}\cos(5\omega_C t) - \cdots]$$ 
相乘后得到：
 $$V_{\text{rect}}(t) = \frac{1}{\pi}(A_C + m(t)) + \text{其他高频项}$$ 
- **直流分量** (dc term):  $\frac{1}{\pi}A_C$ 
- **基带分量** (baseband term):  $\frac{1}{\pi}m(t)$ 

-  $p(t)$  包含载波及其谐波成分
- 通过与  $p(t)$  相乘，整流检波实现了类似于同步检测的效果
- 关键优势：不需要在接收端生成载波信号

这种检测方法本质上是一种准同步检测，通过开关函数的乘法操作有效提取基带信号，同时避免了传统同步检测中对本地载波生成的要求。
