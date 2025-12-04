## 使用音调的 FM (FM with a Tone)
### 消息信号的积分:
需要对消息信号进行积分，因为频率调制取决于消息信号的累积值，而不仅仅是其瞬时值。
$$
a(t) = \int_{-\infty}^{t} m(u) du = \frac{1}{2\pi f_m} \sin(2\pi f_m t)
$
这个积分代表 FM 中使用的**相位项**。

### FM 信号表示
FM 信号可以写作：
$$
\hat{\varphi}^{FM}(t) = Ae^{j[\omega_c t + k_f a(t)]}
$
**简化形式:** 将积分 $a(t)$ 代入 FM 信号方程： 
$$
\hat{\varphi}^{FM}(t) = Ae^{j[\omega_c t + \frac{k_f}{2\pi f_m} \sin(2\pi f_m t)]}
$
#### **与贝塞尔函数的联系 (Connection to Bessel Functions):** 
**FM 作为周期函数:**
项 $e^{j\beta \sin(2\pi f_m t)}$，其中 $\beta = \frac{k_f}{2\pi f_m}$，是一个周期函数。我们可以使用傅里叶级数展开此函数：
$
e^{j\beta \sin(2\pi f_m t)} = \sum_{n=-\infty}^{+\infty} c_n(\beta) e^{j 2\pi n f_m t}
$$
其中 $c_n(\beta)$ 是傅里叶系数，它决定了每个谐波的幅度。
周期函数 $f(t)$ 的通用傅里叶系数公式为：
$
c_n = \frac{1}{T} \int_{-\frac{T}{2}}^{\frac{T}{2}} f(t) e^{-j 2\pi n f_m t} dt
$$
系数 $c_n(\beta)$ 是通过对函数进行一个周期的积分得到的：
$
c_n(\beta) = \frac{1}{T} \int_{-\frac{1}{2f_m}}^{\frac{1}{2f_m}} e^{j\beta \sin(2\pi f_m t)} e^{-j 2\pi n f_m t} dt
$$
该积分引出贝塞尔函数：
$
c_n(\beta) = J_n(\beta)
$$
项 $J_n(\beta)$ 是第一类 n 阶贝塞尔函数。
$J_n(\beta)$ 表示围绕载波频率的第 n 个边带的幅度和相位（通过符号）。 
调制指数
$
\beta = \frac{k_f}{2\pi f_m} = \frac{\Delta f}{f_m}
$$
控制信号能量如何在不同谐波之间分布。

$
e^{j\beta \sin(2\pi f_m t)} = \sum_{n=-\infty}^{+\infty} c_n(\beta) e^{j 2\pi n f_m t}
$$
$
c_n(\beta) = \frac{1}{2\pi} \int_{-\pi}^{\pi} e^{j\beta \sin(x)} e^{-jnx} dx = J_n(\beta)
$$
其中 $x = 2\pi f_m t$。
![](Assests/Pasted%20image%2020251201142608.png)

- **单音 FM 信号:** FM 引入了周期性的频率偏移，这可以使用贝塞尔函数来表示。 
- **贝塞尔函数与谐波:** FM 信号包含谐波分量，其幅度由贝塞尔函数确定。 
- **调制指数 $\beta$ 的控制作用:** 调制指数 $\beta$ 控制频率内容如何在谐波之间扩展，越大的 $\beta$ 会导致更宽的扩展。
---
## FM 解调
瞬时频率 $\omega_{i}(t)$ 是 FM 信号相位的**导数**：
$
\omega_{i}(t)=\frac{d}{dt}(\omega_{c}t+k_{f}\int_{-\infty}^{t}m(\alpha)d\alpha)=\omega_{c}+k_{f}m(t)
$$
![](Assests/Pasted%20image%2020251201143821.png)
因此，当我们对 FM 信号的相位进行微分时，我们可以恢复出 $\omega_{c}+k_{f}m(t)$ 项，从而解调出消息信号 $m(t)$。

---
### 基于微分的解调
实现这一目标的最简单方法是使用理想的**微分器** (differentiator)。 对 FM 信号 $\varphi^{FM}(t)$ 应用微分：
$
\varphi^{F\dot{M}}(t)=\frac{d}{dt}(A\cos(\omega_{c}t+k_{f}\int_{-\infty}^{t}m(\alpha)d\alpha))
$$
结果是：
$
\varphi^{F\dot{M}}(t)=A[\omega_{c}+k_{f}m(t)]\sin\left(\omega_{c}t+k_{f}\int_{-\infty}^{t}m(\alpha)d\alpha-\pi\right)
$$
### 包络检测 (Envelope Detection)
- **微分前:** 消息信号 $m(t)$ 调制 FM 信号的频率，但不调制其幅度。
- **微分后:** 消息信号 $m(t)$ 同时影响信号的频率和幅度。 
- 微分后信号的包络为 $A[\omega_{c}+k_{f}m(t)]$。 
- 我们可以通过检测微分后信号的幅度变化（包络）来恢复消息信号。 
![](Assests/Pasted%20image%2020251201144023.png)
- **失真问题:** 如果原始幅度 $A(t)$ 发生变化（例如由于信道噪声），包络会变为 $A(t)[\omega_{c}+k_{f}m(t)]$。这将导致包络检波器的输出与 $m(t)$ 和 $A(t)$ 都成正比，从而导致恢复信号的失真。 
- **PM 信号:** 相同的原理也适用于 PM（相位调制）信号。FM 解调器同样可以用于 PM 解调。

---
### 实际的 FM 解调器：斜率检测 (Slope Detection) 
任何具有正斜率频率响应的线性系统都可以近似微分器的作用。这种方法被称为**斜率检测** (Slope Detection)。 

#### **使用 RC 高通滤波器:** 一个简单的 RC 高通滤波器可用于斜率检测。 
![](Assests/Pasted%20image%2020251201145058.png)
- 频率响应为: $H(f)=\frac{j2\pi fRC}{1+j2\pi fRC}$。 
- 当 $2\pi fRC\ll1$ 时， $H(f) \approx j2\pi fRC$，此时滤波器近似一个微分器（$Y(jf) = X(jf)H(jf)= 2 \pi RC \cdot jfX(jf)$）。 
![](Assests/Pasted%20image%2020251201144543.png)
- 滤波器频率响应中的**线性部分** (Linear segment) 是其能近似微分器行为的关键。 

#### **使用 RLC 电路:** 
- RLC 调谐电路后跟一个包络检波器也可以用作频率检测器。 
- 在谐振频率 $\omega_{0}=\frac{1}{\sqrt{LC}}$ 以下，RLC 电路的频率响应 $|H(f)|$ 近似为线性斜率。 
- **接收器设计要求：** 载波频率必须满足 $\omega_{c}<\omega_{0}$。 


**斜率检测的局限性:** 
- 斜率仅在很小的频带内是线性的。 
- 这会导致在较宽的频率变化范围内输出失真。 
- **改进方法:** 使用由两个斜率检测器组成的**平衡鉴别器** (balanced discriminator)，或使用**比例检测器** (ratio detector) 来更好地防止幅度变化。

---
### 过零检测器 (Zero-Crossing Detectors) 
由于数字集成电路的进步，过零检测器得以应用。 
它们通过计算过零点的数量来测量信号的瞬时频率。 

过零率是输入信号瞬时频率的**两倍**。 
因此，过零检测器可以轻松解调 FM 或 PM 信号。 

---
### 超外差接收机 (Superheterodyne Receivers) 
频率混合器（或转换器）在超外差接收机中至关重要。
它将已调信号 $m(t)cos(\omega_{c}t)$ 的载波角频率从 $\omega_{c}$ 更改为新的**中频 (IF)** $\omega_{IF}$。 
这是通过将已调信号乘以 $2~cos(\omega_{mix}t)$ 来实现的，其中 $\omega_{mix}=\omega_{c}-\omega_{IF}$ 或 $\omega_{mix}=\omega_{c}+\omega_{IF}$。 
混合后的结果为：$x(t)=m(t)[cos(\omega_{c}-\omega_{mix})t+cos(\omega_{c}+\omega_{mix})t]$。 

我们只保留低频分量——差频。 
**超外差接收机的优势:** 
- **1. 下变频至中频 (IF):** 允许使用高灵敏度的放大器，这对于提高整体信号质量和增强弱信号至关重要。 
- **2. 简化滤波器设计:** 在射频 (RF) 上设计带通滤波器非常困难。降至中频 (IF) 简化了滤波器的设计和实现，因为频率更低且更易于管理。

---
### 锁相环 (Phased-Locked Loop - PLL) 
PLL 是一个负反馈系统，主要用于 FM 解调。 
- 它将 FM 信号的相位与本地生成的参考信号的相位进行比较。

#### **PLL 的基本组成部分:** 
- **1. 压控振荡器 (VCO):** 根据输入电压调整其输出频率。 
- **2. 乘法器 (Multiplier):** 作为鉴相器，比较输入信号和 VCO 输出的相位，以检测相位差。 
- **3. 环路滤波器 (Loop Filter $H(s)$):** 对来自乘法器的输出进行滤波，以平滑信号。 
![](Assests/Pasted%20image%2020251201145651.png)
 
#### **PLL 工作原理:** 
- PLL 比较的是信号的**相位**，而不是幅度。VCO 调整其频率以匹配输入信号的相位。这个反馈环路使 VCO 输出能够跟踪输入信号的相位和频率，保持系统锁定和同步。 
 
**产生误差信号:** 
1. 乘法器（鉴相器）的输出包含相位差信息。 
2. 假设输入信号为 $x_{1}(t)=A_{1}cos(\omega_{in}t+\phi_{in})$，VCO 输出为 $x_{2}(t)=A_{2}cos(\omega_{vco}t+\phi_{vco})$。 
3. 乘法器输出为: $\nu_{pd}(t)=A_{1}A_{2}cos(\omega_{in}t+\phi_{in})cos(\omega_{vco}t+\phi_{vco})$。 
4. 使用三角函数积化和差公式，输出重写为： $$ \nu_{pd}(t)=\frac{A_{1}A_{2}}{2}[cos((\omega_{in}-\omega_{vco})t+(\phi_{in}-\phi_{vco}))+cos((\omega_{in}+\omega_{vco})t+(\phi_{in}+\phi_{vco}))] $$ 
5. 此输出包含一个低频（差频）分量 $(\omega_{in}-\omega_{vco})$ 和一个高频（和频）分量 $(\omega_{in}+\omega_{vco})$。 


**低通滤波:** 
环路滤波器（低通滤波器） 移除高频分量 $(\omega_{in}+\omega_{vco})$。 仅保留低频分量，这被称为**误差信号** (error signal)。 
![](Assests/Pasted%20image%2020251201150816.png)
该误差信号与相位差成正比，用作控制信号来调节 VCO 的频率，从而使 PLL 保持锁定。 
![](Assests/Pasted%20image%2020251201150920.png)

**锁定条件 (Lock Condition):** 
当 PLL 锁定时，VCO 的频率与输入信号的频率相匹配，并且两个信号之间的相位差变为恒定。