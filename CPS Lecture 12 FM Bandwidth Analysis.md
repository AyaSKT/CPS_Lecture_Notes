定义 $a(t)$： $$a(t) = \int_{-\infty}^t m(u) du$$ 。代表了FM的瞬时频率由调制信号的整个过去所决定。

---
### FM 信号表示 (The FM signal Representation) 
FM 信号可以写作： $$ \hat{\varphi}_{FM}(t) = Ae^{j(\omega_c t + k_f a(t))} = Ae^{j(k_f a(t))} e^{j(\omega_c t)} $$
- 这个等式将信号分为**载波部分** $e^{j(\omega_c t)}$ 和**调制部分** $e^{j(k_f a(t))}$。
- 其中 $k_f$ 是**频率灵敏度**（表示载波频率随调制信号变化的程度）。 

### FM 带宽分析
#### 展开 FM 信号 (Expanding the FM signal)
使用**麦克劳林级数展开**（一种在 t=0 处对函数进行的泰勒级数展开），调制信号 $e^{j k_f a(t)}$ 可以被展开为一个幂级数： $$ e^{j k_f a(t)} = \underbrace{1}_{\text{未调制的载波}} + \underbrace{j k_f a(t)}_{\text{线性}} - \underbrace{\frac{k_f^2}{2!} a^2(t) + \dots + \frac{(j k_f)^n}{n!} a^n(t)}_{\text{非线性效应}} $$

FM 信号是真实世界信号，所以我们只关心复指数的实部。展开的 FM 信号的实部是： $$ \varphi^{FM}(t) = \Re[\hat{\varphi}^{FM}(t)] $$ 将此应用于展开的级数，我们得到以下实信号表达式： $$ \varphi^{FM}(t) = A[\cos(\omega_c t) - k_f a(t) \sin(\omega_c t) - \frac{k_f^2}{2!} a^2(t) \cos(\omega_c t) + \dots] $$如果 $a(t)$ 的带宽是 B，当 $a(t)$ 与自身相乘时，频域中的卷积会导致频谱的扩展。
如果原始信号 $a(t)$ 的频率分量范围从 $-B$ 到 $B$，那么在自乘之后，新的频率分量将从 $-2B$ 到 $2B$。 

**FM 波的带宽在理论上是无限的**

#### FM 带宽
- 正弦和余弦项在载波频率 $\omega_c$ 周围贡献了边带。这导致 FM 信号具有多个频率分量，从而增加了其带宽。
- 功率级数展开帮助我们理解 FM 信号具有无限的边带，但这些边带的幅度随高阶项而减小，使得大部分信号能量集中在有限的带宽内。

#### FM 的理论带宽 vs. 实际带宽 
**理论带宽 (Theoretical Bandwidth):** 
- 理论上，FM 信号的带宽是**无限的**，因为 FM 调制会产生无限数量的边带。 
**实际带宽 (Practical Bandwidth):** 
- 对于幅度 $a(t)$ 有界的**实际信号**，重要边带的数量变为有限的。
- 表达式 $\frac{k_f^n a^n(t)}{n!}$ 表明，随着 $n$ 的增加，高阶项变得可以忽略不计，这意味着高阶边带对总信号的贡献非常小。 * 这是因为阶乘 $n!$ 的增长速度远快于 $k_f a(t)$ 的幂。
![](Assests/Pasted%20image%2020251201104451.png)

---
### NBFM (Narrowband FM) 带宽计算
#### FM 信号表示 (FM signal Representation)
$$ \varphi^{FM}(t) \approx A (\cos(2\pi f_c t) - k_f a(t) \sin(2\pi f_c t)) $$
- 这是一个**窄带 FM (narrowband FM)** 信号表示。
- 当调制指数 $\beta = |k_f a(t)| \ll 1$ 时，这个近似是良好的。
- 通常，我们认为 2B 带宽是窄带。
- 相位调制 (Phase Modulation, PM) 具有相似的表达式。

AM vs. 窄带 FM (NBFM)

| 特征          | AM                                                             | NBFM                                                                       |
| :---------- | :------------------------------------------------------------- | :------------------------------------------------------------------------- |
| **信号表示**    | $\varphi_{AM}(t) = A \cos(\omega_c t) + m(t) \cos(\omega_c t)$ | $\varphi_{FM}(t) \approx A [\cos(\omega_c t) - k_f m(t) \sin(\omega_c t)]$ |
| **带宽 **     | 2B                                                             | 2B (窄带近似)                                                                  |
| **相位偏移**    | 没有相位偏移                                                         | 由调制信号引入 $\frac{\pi}{2}$ 的相位偏移                                              |
| **频率随时间变化** | 恒定在 $\omega_c$                                                 | 随 $m(t)$ 变化                                                                |
| **幅度随时间变化** | 随 $m(t)$ 变化                                                    | 幅度保持恒定                                                                     |

#### 困境
- 为了充分利用 FM（或 PM），我们需要使频率偏移足够大
- 需要选择足够大的 $k_f$ 来打破 $|k_f a(t)| \ll 1$ 的条件
- 这就是**宽带 FM (wideband FM)** 的情况
- 我们不能再忽略功率级数中的高阶项
- 我们需要依靠经验公式来估计带宽

---
### WBFM (Wideband FM) 带宽计算
#### WBFM 带宽分析
##### Step 1: 估计消息信号 $m(t)$
从一个低通信号 $m(t)$ 开始，它的带宽为 B Hz。
不直接处理连续信号 $m(t)$，而是使用**阶梯近似**（staircase approximation）来简化它。这意味着我们用小的恒定脉冲来表示 $m(t)$。每个脉冲被称为一个“单元”（cell）。
![](Assests/Pasted%20image%2020251201110908.png)
##### Step 2: 分析估计信号 $m(t)$
使用阶梯近似 $\hat{m}(t)$ 来分析 FM 信号更容易，因为现在每个单元在短时间间隔内具有恒定值。
每个单元都是一个宽度为 $\frac{1}{2B}$ 秒的短脉冲。
每个单元中的（调制后）信号是一个正弦波，其频率由 $\omega_c + k_f m(t_k)$ 决定。
为确保此近似保留原始信号中的所有信息，每个单元的宽度不应大于 $\frac{1}{2B}$ 秒。这个条件来自**采样定理**，它告诉我们需要多频繁地采样信号以保持所有信息完整。

##### Step 3: 正弦波的频谱
$$ rect(2Bt)\cos[\omega_c t + k_f m(t_k)t] $$ $$ F\{rect(2Bt)\} = \frac{1}{2B} \text{sinc} \left(\frac{\omega}{4B}\right) $$ $$ F\{\cos(\omega_0) \cdot f(t)\} = \frac{1}{2} [F\{f(t)\}(\omega - \omega_0) + F\{f(t)\}(\omega + \omega_0)] $$ $$ F\{rect(2Bt)\cos[\omega_c t + k_f m(t_k)]\} $$ $$ = \frac{1}{2} \text{sinc} \left[\frac{\omega + \omega_c + k_f m(t_k)}{4B}\right] + \frac{1}{2} \text{sinc} \left[\frac{\omega - \omega_c - k_f m(t_k)}{4B}\right] $$
##### Step 4: 脉冲中心频率
信号中的每个正弦脉冲对应一个以 $\omega_c + k_f m(t_k)$ 为中心的频率。 $m(t_k)$ 的最小值和最大值（分别表示为 $-m_p$ 和 $m_p$）决定了这些频率的范围。 
- 最小中心频率是 $\omega_c - k_f m_p$。
- 最大中心频率是 $\omega_c + k_f m_p$。
![](Assests/Pasted%20image%2020251201112219.png)

##### Step 5: 脉冲中心频率计算
- 总频谱不仅仅局限于 $\omega_c \mp k_f m_p$。由于 sinc 函数，每个正弦脉冲的频谱都会有一定程度的扩展。sinc 函数的主瓣会在中心频率的任一侧将频率内容扩展 $4\pi B$。 
- 因此，FM 信号的**总带宽**来自中心频率和 sinc 函数引起的扩展。频谱中的最小和最大显着频率为： 
- $\omega_c - k_f m_p - 4\pi B$ 
- $\omega_c + k_f m_p + 4\pi B$

##### Step 6: FM带宽计算
- 最后，FM 带宽约等于使用此表达式计算： $$ B_{FM} = \frac{1}{2\pi}(2k_f m_p + 8\pi B) $$ 简化后，我们得到： $$ B_{FM} \approx 2(\frac{k_f m_p}{2\pi} + 2B) $$ 其中 B 是**双边消息带宽** (two-sided message bandwidth)。
$$ m_p = \frac{m_{max} - m_{min}}{2} $$ $$ \Delta f = k_f \frac{m_p}{2\pi} = k_f \frac{m_{max} - m_{min}}{4\pi} $$ $$ B_{FM} \approx 2(\Delta f + f_m) $$ Where $f_m$ is the maximum frequency of the modulating signal.

### 卡森法则 (Carson's Rule) 
卡森法则 (Carson's Rule) 为 FM 信号的**带宽**提供了一个实用的近似值。 $$ B_{FM} \approx 2(\Delta f + B) $$ 其中: 
- $B_{FM}$: 总 FM 带宽 (单位: Hz) 
- $\Delta f$: 峰值频率偏移 (载波频率与其未调制值之间的最大偏移量) 
- $B$: 消息信号带宽 (调制信号中存在的频率范围)

