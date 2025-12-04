## Angle Modulation 角度调制

### 角度调制
- 调制波幅度不变
- 通过改变载波的相位和频率来调制
- 曾经多用PM，现在多用FM
- 角度调制远比AM复杂
- 是一个非线性的过程
- 我们注重于FM：
$$
u(t) = A_c \cos{2\pi f_c t + \phi (t)}
$$
### 瞬时频率 Instantaneous Frequency
![](Assests/Pasted%20image%2020251121170338.png)
类比于高中所学的速度定义，在任意一个时间点 $t_0$ ，可以通过对相位求导得到其**瞬时频率**。

一个一般的正弦波
$$
\phi(t) = A \cos \theta(t)
$$
$$
\theta (t) = \omega_c t+ \theta_0
$$ 
 ，其中 $\theta(t)$ 是一个一般的角度，可任意取值。
 
有
$$
\omega_i (t)= \frac{d \theta}{dt} = \theta'(t)
$$
和
$$
\theta(t) = \int_{- \infty}^t \omega_i(t)du = \theta_0 + \int_{0}^t \omega_i(u)du
$$。
我们可以通过改变 $\omega_i(t)$ 或者 $\theta(t)$ 进行调制。
### Phase Modulation 相位调制

 -   **调相 (Phase Modulation, PM) 的基本原理**
    -   顾名思义，我们使瞬时相位 $\theta(t)$ 随消息信号 $m(t)$ 线性变化：
        $$ \theta^{PM}(t) = \omega_{c} t + k_{p} m(t) $$
        这里，$k_p$ 是相位偏差常数（rad/V），决定了相位随调制信号变化的灵敏度。

-   **已调信号表达式**
    -   因此，传输的信号为：
        $$ \phi^{PM}(t) = A_{c} \cos(\omega_{c} t + k_{p} m(t)) $$
        该式表明，载波 $A_c \cos(\omega_c t)$ 的相位中注入了与调制信号 $m(t)$ 成正比的变化量。

-   **瞬时频率**
    -   我们通过求导得到瞬时角频率 $\omega_i^{PM}(t)$：
        $$ \omega_{i}^{PM}(t) = \frac{d\theta}{dt} = \omega_{c} + k_{p} {m}'(t) $$
    -   **关键特性**：PM 信号的瞬时频率 $\omega_i^{PM}(t)$ 与消息信号 $m(t)$ 的**变化率**（即导数 ${m'}(t)$）成正比。
    -   **物理意义**：$m(t)$ 的快速变化会导致其导数 ${m}'(t)$ 的绝对值更大，从而引起瞬时频率更大幅度的偏移。

### Frequency Modulation 频率调制

-   **核心原理**：在频率调制中，使瞬时频率 $\omega_{i}^{FM}(t)$ 随消息信号 $m(t)$ 线性变化。
    $$ \omega_{i}^{FM}(t) = \omega_{c} + k_{f} m(t) $$
    这里，$k_f$ 是频率偏移常数（Hz/V），决定了频率随调制信号变化的灵敏度。

-   **已调信号表达式**：传输的信号是载波相位按特定规律变化的余弦波。
    $$ \phi^{FM}(t) = A_{c} \cos\left( \omega_{c} t + k_{f} \int_{-\infty}^{t} m(u) \, du \right) $$
    该式表明，FM 是通过改变载波的**瞬时相位**（括号内的全部内容）来实现的，而相位的变化量正比于调制信号 $m(t)$ 的积分。

-   **带宽决定因素**：已调信号的带宽由参数 $k_f$ 和消息信号 $m(t)$ 共同决定。
    -   $k_f$ 越大，或 $m(t)$ 的幅度越大、变化越快（频率越高），产生的频率偏移越大，所需带宽也越宽。

-   **瞬时相位**：FM 信号的瞬时相位 $\theta^{FM}(t)$ 是其瞬时频率的积分。
    $$ \theta^{FM}(t) = \int_{-\infty}^{t} \omega_{i}^{FM}(u) \, du = \omega_{c}t + k_{f} \int_{-\infty}^{t} m(u) \, du $$

-   **FM 与 PM 的等效关系**：
    -   一个**频率调制器**的输入 $\omega_{i}^{PM}(t)$ 对于一个**相位调制器**而言，等效于一个**相位调制器**的输入 $\theta^{FM}(t)$。
    -   这揭示了一个深刻联系：**频率调制（FM）可以视为对调制信号 $m(t)$ 先进行积分，再进行相位调制（PM）的结果**。这表明 FM 和 PM 在数学上是紧密相关的，统称为**角度调制**。
