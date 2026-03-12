## BER & SNR

### Bit Error Rate (BER)
**Bit Error Rate (BER)** 用于衡量数字通信系统中比特出错的平均概率。

- 定义为错误比特数与总传输比特数之比：

  $$

  \text{BER} = \lim_{N \to \infty} \frac{n}{N}

  $$

  其中：

  - $n$：错误比特数  
  - $N$：总比特数

- BER 是衡量**信号质量 Signal Quality**的直接指标。

- 在分组通信系统中，常使用 **分组误码率 PER (Packet Error Rate)**，在误码相互独立时可由 BER 推导。


**不同应用的典型 BER 要求：**

- 语音编码（Vocoder Speech）：$10^{-2} \sim 10^{-3}$
- 无线数据（Wireless Data）：$10^{-5} \sim 10^{-6}$
- 视频传输（Video Transmission）：$10^{-7} \sim 10^{-12}$
- 金融数据（Financial Data）：$\le 10^{-11}$

### Signal-to-Noise Ratio (SNR)

- 在数字通信中，SNR 定义为**每比特能量与噪声功率谱密度之比**：

  $$

  \text{SNR}_{\text{digital}} = \frac{E_b}{N_0}

  $$

- 其中：
  - $E_b$：每比特能量（Energy per bit）
  - $N_0$：单边噪声功率谱密度（Noise spectral density）

- SNR 为不同数字调制方案提供了**统一比较标准**。
- 常用于比较不同调制方式在 AWGN 信道下的 BER 性能。


---
## 噪声中的单脉冲检测

### 接收信号模型

![](Assests/Pasted%20image%2020251222161726.png)

对于单脉冲传输系统，接收信号为：

$$

r(t) = s(t) + w(t)

$$

  

等价表示为：

$$

r(t) =

\begin{cases}

s(t) + w(t), & \text{脉冲存在} \\

w(t), & \text{脉冲不存在}

\end{cases}

$$

  

其中：

- $s(t)$：发送信号  
- $w(t)$：加性白高斯噪声（AWGN）

  

### 判决随机变量

用于判断脉冲是否存在的随机变量定义为：

$$

Y = \int_0^T g(T - t)\, r(t)\, dt

$$

  

展开后：

$$

Y = \int_0^T g(T - t)s(t)\,dt

  + \int_0^T g(T - t)w(t)\,dt

$$



- 目标：选择滤波器 $g(t)$，**使输出 $Y$ 的 SNR 最大化**。  

### 噪声项分析

定义噪声贡献：

$$

N = \int_0^T g(T - t)w(t)\,dt

$$

  

### 噪声均值

$$

\mathbb{E}[N]

= \int_0^T g(T - t)\mathbb{E}[w(t)]\,dt

= 0

$$

（AWGN 为零均值噪声）

### 噪声方差

  

$$

\text{Var}(N) = \mathbb{E}[N^2]

$$

  

展开为：

$$

\text{Var}(N)

= \int_0^T \int_0^T

g(T-t)g(T-\tau)\,

\mathbb{E}[w(t)w(\tau)]\,dt\,d\tau

$$

  

对白噪声：

$$

\mathbb{E}[w(t)w(\tau)] = \frac{N_0}{2}\delta(t-\tau)

$$

  

因此：

$$

\text{Var}(N)

= \frac{N_0}{2} \int_0^T |g(T-\tau)|^2 d\tau

$$

  

若滤波器归一化：

$$

\int_0^T |g(t)|^2 dt = T

$$

  

则：

$$

\text{Var}(N) = \frac{N_0 T}{2}

$$


### 线性接收机输出噪声特性

- 均值：$0$
- 方差：$\dfrac{N_0 T}{2}$
- 分布：**高斯分布**  

  （高斯噪声经线性滤波后仍为高斯）


### 信号项分析与匹配滤波器

信号分量：

$$

S = \int_0^T g(T - t)s(t)\,dt

$$

  

为了最大化 SNR，需要最大化 $S$。

### Schwarz 不等式

  

$$

\left|\int g(T - t)s(t)\,dt\right|^2

\le

\int |g(T - t)|^2 dt

\int |s(t)|^2 dt

$$

  

当且仅当：

$$

g(T - t) = c\, s(t)

$$

时取等号。


## Matched Filter（匹配滤波器）

- **匹配滤波器**：与发送信号形状相匹配的滤波器
- 能在 AWGN 信道下**最大化输出 SNR**
- 滤波器冲激响应：

  $$

  g(t) = c\, s(T - t)

  $$
  
### 匹配滤波器输出

  

$$

Y = \int_0^T g(T - t)r(t)\,dt

= c \int_0^T s(t)r(t)\,dt

$$

  

- 输出等价于两个信号的**互相关（Cross-correlation）**
- 因此匹配滤波接收机也称为 **相关接收机（Correlation Receiver）**

  

若接收脉冲定时未知，可计算：

$$

Y(\tau) = c \int_{-\infty}^{+\infty} s(t)r(t-\tau)\,dt

$$


## Optimum Detection of BPSK
### BPSK 发送信号

  

$$

s(t) =

\begin{cases}

A_c \cos(2\pi f_c t), & 0 \le t \le T,\; \text{发送 1} \\

A_c \cos(2\pi f_c t + \pi), & 0 \le t \le T,\; \text{发送 0}

\end{cases}

$$

  

等价表示为：

$$

s(t) = A_c m(t)\cos(2\pi f_c t)

$$

  

其中：

$$

m(t)=

\begin{cases}

+1, & \text{比特 1} \\

-1, & \text{比特 0}

\end{cases}

$$

  
### 多比特一般形式

  

$$

m(t) = \sum_{k=0}^{N} b_k h(t-kT)

$$

  

- $b_k \in \{+1,-1\}$

- $h(t)$：矩形脉冲成形函数


$$Price ( \lim_{\Delta 五花肉 \rightarrow 0} 干锅) = 40 元$$