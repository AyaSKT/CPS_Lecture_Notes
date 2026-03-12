## 数字通信系统 Digital Communication System

![](Assests/Pasted%20image%2020251222134916.png)

### 基本组成

- 信源 Source: 产生源信号数据流
- 线路编码 Line Codes：将信息编码为电信号波形
- 复用器 Multiplexer
- 再生中继器 Regenerative Repeater：用于在线路中对信号去噪和保持信号完整性

### 信源

- 来自计算机的数据集（Data sets from a computer）
- 数字化语音信号，例如  
  - **PCM（Pulse Code Modulation，脉冲编码调制）**  
  - **DM（Delta Modulation，增量调制）**
- HDTV（高清电视）与遥测数据（Telemetry data）

### 线路编码

- 将数字数据转换为脉冲（waveforms）
- 以适合在物理信道中传输
  
#### 常见线路编码类型（Line Code Examples）

##### RZ（Return-to-Zero，归零码）

- **on-off RZ**
  - 1：正脉冲
  - 0：无信号

- **polar RZ（极性归零码）**
  - 1：正脉冲
  - 0：负脉冲

- **bipolar RZ（双极性归零码）**
  - “1” 在正负之间交替
  - “0”为零电平

##### NRZ（Non-Return-to-Zero，不归零码）

- **on-off NRZ**
- **polar NRZ**

其实RZ和NRZ的区别就是正向的脉冲会不会和下一个正向脉冲连起来。
![](Assests/Pasted%20image%2020251222140153.png)
### 复用器
  
#### 复用的目的

- 合并多个数据源
- 提高信道利用率

### 常见复用方式

- **FDM（Frequency Division Multiplexing，频分复用）**
- **TDM（Time Division Multiplexing，时分复用）**
- **CDM（Code Division Multiplexing，码分复用）**

### 再生中继器

#### 再生中继器的功能

- 沿传输路径按间隔放置
- 功能包括：

  1. 检测接收信号
  2. 消除噪声与失真
  3. 重新生成脉冲并继续传输

---
## 符号间干扰 Intersymbol Inteference, ISI

### 符号间干扰 vs 信道噪声 

**Inter-Symbol Interference（ISI）**

- 由信道频率响应不理想引起
- 脉冲在时间上扩展并与相邻脉冲重叠
- 导致判决错误

**Channel Noise**

- 由随机、不可预测的物理现象产生
- 表现为信道输出端的非期望电信号

### Nyquist 第一准则（零 ISI）
#### 基本思想
通过脉冲成形，使得在采样时刻：

- 当前符号脉冲幅度非零
- 其他符号贡献为零

设比特周期为：

$$

T_b = \frac{1}{R_b}

$$

  

脉冲 $p(t)$ 需满足：

$$

p(t)=

\begin{cases}

1, & t = 0 \\

0, & t = \pm nT_b,\quad n = 1,2,3,\dots

\end{cases}

$$

#### 理想 Nyquist 脉冲

![](Assests/Pasted%20image%2020251222142007.png)
  
#### 物理/几何意义 * **频域对称性**：
这意味着滤波器的幅频特性必须关于截止频率（奈奎斯特频率 $f_N = \frac{1}{2T_s}$）呈现**奇对称**（Vestigial Symmetry）。 
* **直观理解**：如果把滤波器的频谱切下来一块，必须能完美地“补”到另一边，使得整体叠加后平坦。 

### 带滚降因子 $r$ 的 Nyquist 脉冲

  ![](Assests/Pasted%20image%2020251222142124.png)

- $r = 0$：理想情况（最窄带宽）
- $r = 0.5$：工程常用
- $r = 1$：带宽最大，时域振铃最小

### 实现方案

| 方案       | 滤波器类型                      | 特点                                 | 优缺点                                   |
| :------- | :------------------------- | :--------------------------------- | :------------------------------------ |
| **理想方案** | **矩形滤波器** (时域为 Sinc)       | 带宽最小 ($W = 1/2T_s$)                | **物理不可实现**；尾部衰减慢，对时钟抖动极敏感。            |
| **实用方案** | **升余弦滤波器** (Raised Cosine) | 带宽稍大 ($W = \frac{1+\alpha}{2T_s}$) | **广泛使用**；尾部衰减快，抗抖动能力强。$\alpha$ 为滚降系数。 |



---
## 二进制调制 Binary Modulation
  
### 基本假设

- 在数字通信中，假设载波在**一个符号（比特）持续时间内具有单位能量**。
- 数字调制信号的频谱以载波频率 $f_c$ 为中心。
- 与模拟调制类似，假设载波频率 $f_c$ **远大于** 作为调制信号的二进制数据流的“带宽”。

### 载波模型与调制信号表达式

#### 载波幅度假设

假设载波幅度为：

$$

A_c = \sqrt{\frac{2}{T_b}}

$$

其中 $T_b$ 为比特持续时间。
这样的假设可以让载波能量在一个bit时间内等于1，简化计算。
#### 载波信号  

$$

c(t) = \sqrt{\frac{2}{T_b}} \cos(2\pi f_c t + \phi_c)

$$

  
#### 调制信号

设输入二进制基带信号为 $b(t)$，则调制后的信号为：

$$

s(t) = b(t)c(t)

$$

  

即：

$$

s(t) = \sqrt{\frac{2}{T_b}}\, b(t)\cos(2\pi f_c t + \phi_c)

$$


  

### 每比特能量 $E_b$ 的推导

#### 定义

假设载波初始相位 $\phi_c = 0$，则**每比特的发送能量**定义为：

$$

E_b = \int_0^{T_b} |s(t)|^2 dt

$$

  
代入 $s(t)$
  

$$

E_b = \frac{2}{T_b}\int_0^{T_b} |b(t)|^2 \cos^2(2\pi f_c t)\,dt

$$

  

#### 使用三角恒等式

  

$$

\cos^2(2\pi f_c t) = \frac{1}{2}\left[1 + \cos(4\pi f_c t)\right]

$$

  

代入得：

$$

E_b = \frac{1}{T_b}\int_0^{T_b} |b(t)|^2 dt

\;+\;

\frac{1}{T_b}\int_0^{T_b} |b(t)|^2 \cos(4\pi f_c t)\,dt

$$

  

#### 近似处理

假设 $|b(t)|^2$ 在一个 $\cos(4\pi f_c t)$ 周期内近似为常数，则：

$$

\int_0^{T_b} |b(t)|^2 \cos(4\pi f_c t)\,dt \approx 0

$$

  

### 最终结果

  

$$

E_b \approx \frac{1}{T_b}\int_0^{T_b} |b(t)|^2 dt

$$

  

📌 **结论**：  

发送信号的每比特能量 $E_b$ 与用于调制载波的二进制基带信号能量成正比。
也可以理解为，发送信号的能量等于基带信号的平均功率。

---
### 数字调制技术

SK(Shift Keying)的意思就是0和1切换。Keying来源于早期发报员通过按键来切换0和1的状态。

- BASK
- BPSK
- BFSK
- QPSK

  
### 三种基本二进制调制方式

#### 二进制幅移键控（BASK）  

**Binary Amplitude Shift Keying**

$$

b(t) =

\begin{cases}

\sqrt{E_b}, & \text{二进制符号 1} \\

0, & \text{二进制符号 0}

\end{cases}

$$

  

调制信号

  

$$

s(t) =

\begin{cases}

\sqrt{\dfrac{2E_b}{T_b}} \cos(2\pi f_c t), & \text{符号 1} \\

0, & \text{符号 0}

\end{cases}

$$

- 载波幅度 $A_c$ 在两种取值之间切换（如 0 和 1）
- 载波频率 $f_c$ 和相位 $\phi_c$ 保持不变
- 本质：**幅度调制（Amplitude Modulation）**

![](Assests/Pasted%20image%2020251222152645.png)

#### 二进制相移键控（BPSK）  

**Binary Phase Shift Keying**

  

$$

s_i(t) =

\begin{cases}

\sqrt{\dfrac{2E_b}{T_b}} \cos(2\pi f_c t), & \text{符号 1} \\

\sqrt{\dfrac{2E_b}{T_b}} \cos(2\pi f_c t + \pi)

= -\sqrt{\dfrac{2E_b}{T_b}} \cos(2\pi f_c t), & \text{符号 0}

\end{cases}

$$

- 通过切换载波相位来表示二进制信息
- 相位在 $0^\circ$ 和 $180^\circ$ 之间切换
- 载波幅度 $A_c$ 与频率 $f_c$ 保持不变
- 本质：**相位调制（Phase Modulation）**

![](Assests/Pasted%20image%2020251222152910.png)

![](Assests/Pasted%20image%2020251222152938.png)

### 二进制频移键控（BFSK）  

**Binary Frequency Shift Keying**

$$

s_i(t) =

\begin{cases}

\sqrt{\dfrac{2E_b}{T_b}} \cos(2\pi f_1 t), & \text{符号 1} \\

\sqrt{\dfrac{2E_b}{T_b}} \cos(2\pi f_2 t), & \text{符号 0}

\end{cases}

$$

  

其中：

- $f_1 \neq f_2$

- 通过切换载波频率表示二进制信息
- 载波频率 $f_c$ 在两个不同频率之间切换
- 载波幅度 $A_c$ 和相位 $\phi_c$ 保持不变
- 本质：**频率调制（Frequency Modulation）**


![](Assests/Pasted%20image%2020251222152827.png)

### Quadriphase-SK, QPSK

#### 正交相移键控（QPSK）  

#### 基本思想

- 传输信息包含在**正弦载波的相位（phase）**中  
- 载波相位取 **4 个等间隔值**：

  $$

  \frac{\pi}{4},\ \frac{3\pi}{4},\ \frac{5\pi}{4},\ \frac{7\pi}{4}

  $$

- 每一个相位对应 **2 个比特（dibit）**
- QPSK ≈ **两个正交 BPSK 的叠加**


#### QPSK 信号的数学表达

##### 单个符号波形

$$

s_i(t)=

\begin{cases}

\sqrt{\dfrac{2E}{T}}\cos\!\left(2\pi f_c t+(2i-1)\dfrac{\pi}{4}\right), & 0\le t\le T \\

0, & \text{elsewhere}

\end{cases}

$$

  

其中：

- $E$：每个 **QPSK 符号** 的能量  

- $T$：符号持续时间  

- $i = 1,2,3,4$：符号索引  

#### QPSK 的正交分解（I/Q 表示）

利用恒等式：

$$

\cos(a+b)=\cos a\cos b-\sin a\sin b

$$

  

可将 QPSK 信号写为：

$$

s_i(t)

= \sqrt{\dfrac{2E}{T}}\cos\!\left((2i-1)\dfrac{\pi}{4}\right)\cos(2\pi f_c t)

- \sqrt{\dfrac{2E}{T}}\sin\!\left((2i-1)\dfrac{\pi}{4}\right)\sin(2\pi f_c t)

$$
  

#### I/Q 两路 BPSK 的等效表示

- **同相分量（In-phase, I）**

  $$

  a_1(t)=\sqrt{E}\cos\!\left((2i-1)\dfrac{\pi}{4}\right)

  $$

- **正交分量（Quadrature, Q）**

  $$

  a_2(t)=-\sqrt{E}\sin\!\left((2i-1)\dfrac{\pi}{4}\right)

  $$

  

对应取值关系：

$$

\sqrt{E}\cos\!\left((2i-1)\dfrac{\pi}{4}\right)=

\begin{cases}

+\sqrt{E/2}, & i=1,4 \\

-\sqrt{E/2}, & i=2,3

\end{cases}

$$

  

$$

-\sqrt{E}\sin\!\left((2i-1)\dfrac{\pi}{4}\right)=

\begin{cases}

-\sqrt{E/2}, & i=1,2 \\

+\sqrt{E/2}, & i=3,4

\end{cases}

$$

  

两路载波 **相位正交（90° 相差）**，分别调制 I / Q 两个 BPSK 信号。

#### QPSK 相位与比特映射（Gray 编码示例）

| 索引 $i$ | 相位（rad）   | $a_1(t)$      | $a_2(t)$      | 输入 dibit |
| ------ | --------- | ------------- | ------------- | -------- |
| 1      | $\pi/4$   | $+\sqrt{E/2}$ | $-\sqrt{E/2}$ | 10       |
| 2      | $3\pi/4$  | $-\sqrt{E/2}$ | $-\sqrt{E/2}$ | 00       |
| 3      | $5\pi/4$  | $-\sqrt{E/2}$ | $+\sqrt{E/2}$ | 01       |
| 4      | $7\pi/4$  | $+\sqrt{E/2}$ | $+\sqrt{E/2}$ | 11       |
  

📌 **Gray 编码（Gray coding）**：  

相邻相位只相差 **1 bit**，可降低误码率（BER）。



---
## M 进制数字调制 M-ary Digital Modulation


- M 进制数字调制在每一个符号周期 $T$ 内，从 $M$ 个可能信号中选择一个：

  $$

  s_1(t), s_2(t), \dots, s_M(t)

  $$

- 符号持续时间：

  $$

  T = m T_b,\quad M = 2^m

  $$

  其中 $T_b$ 为比特持续时间，$m$ 为每个符号携带的比特数。

- **主要目的**：在带通信道中节省带宽（Bandwidth Conservation），适用于带宽受限的通信场景。

### M-ary 调制的特点

- **带宽效率更高**：相比二进制调制，M 进制调制能在相同带宽下传输更多比特。
- **功率与复杂度增加**：M 越大，系统对功率和接收机复杂度的要求越高。
- **应用场景**：当信道带宽受限、无法使用简单二进制调制时，优先采用 M 进制调制。

### M-ary Phase Shift Keying（M-PSK）

- M-PSK 是 BPSK 的推广，通过一个符号承载多个比特来节省带宽。
- 每 $m=\log_2 M$ 个比特映射为一个符号。
- $2\pi$ 的相位范围被均匀划分为 $M$ 个相位。

#### M-PSK 信号表达式

$$

s_i(t) = \sqrt{\frac{E}{T}} \cos\!\left(2\pi f_c t + \frac{2\pi i}{M}\right),

\quad i = 0,1,\dots,M-1,\; 0 \le t \le T

$$

#### M-PSK 的 I/Q 表示（恒包络）

- 同相分量（In-phase）与正交分量（Quadrature）相互关联，使信号包络恒定。

$$

s_i(t)

= \big[\sqrt{E}\cos\!\left(\tfrac{2\pi i}{M}\right)\big]

  \sqrt{\tfrac{2}{T}}\cos(2\pi f_c t)

- \big[\sqrt{E}\sin\!\left(\tfrac{2\pi i}{M}\right)\big]

  \sqrt{\tfrac{2}{T}}\sin(2\pi f_c t)

$$

  

- 信号幅度：

$$

\sqrt{(\sqrt{E}\cos\tfrac{2\pi i}{M})^2

+(\sqrt{E}\sin\tfrac{2\pi i}{M})^2}

= \sqrt{E}

$$

- **结论**：M-PSK 为恒包络调制，适合非线性信道。

#### M-PSK 的信号空间表示（Signal-Space Diagram）

- 采用二维正交基函数：

$$

\phi_1(t) = \sqrt{\frac{2}{T}}\cos(2\pi f_c t), \quad

\phi_2(t) = \sqrt{\frac{2}{T}}\sin(2\pi f_c t)

$$

- 每个符号对应二维空间中的一个点：

  - 同相分量：$\sqrt{E}\cos(2\pi i/M)$
  - 正交分量：$-\sqrt{E}\sin(2\pi i/M)$

- 所有符号点均匀分布在半径为 $\sqrt{E}$ 的圆上（如 8-PSK）。

![](Assests/Pasted%20image%2020251222155423.png)


  

### M-ary Quadrature Amplitude Modulation（M-QAM）


- 在 M-QAM 中，同相分量和正交分量**相互独立**。
- 不再限制信号包络恒定。

#### M-QAM 信号表达式

$$

s_i(t)

= \sqrt{\frac{2E_0}{T}}\, a_i \cos(2\pi f_c t)

- \sqrt{\frac{2E_0}{T}}\, b_i \sin(2\pi f_c t),

$$

$$

i = 0,1,\dots,M-1,\quad 0 \le t \le T

$$

  

- $a_i, b_i$：同相与正交分量的幅度等级  
- $E_0$：最小幅度信号对应的能量  
- **本质**：ASK 与 PSK 的组合（混合调制）

#### M-QAM 的特殊情况

- **M-ASK**：若 $b_i = 0$，则

$$

s_i(t) = \sqrt{\frac{2E_0}{T}}\, a_i \cos(2\pi f_c t)

$$

- **M-PSK**：若 $E_0 = E$ 且

$$

\sqrt{E^2 a_i^2 + E^2 b_i^2} = \sqrt{E}

$$

则 M-QAM 退化为 M-PSK。

#### M-QAM 的信号空间图

- 信号点排列在**矩形网格**上（如 16-QAM）。
- 同相与正交分量彼此独立。
- 与 M-PSK 不同，M-QAM 的信号点**能量不相等**。
- 常配合 **Gray 编码** 以降低误码率。

  
![](Assests/Pasted%20image%2020251222160511.png)
  

### M-ary Frequency Shift Keying（M-FSK）

- 每个符号使用不同的载波频率表示：

$$

s_i(t) = \sqrt{\frac{2E}{T}}

\cos\!\left(\frac{\pi}{T}(n+i)t\right),

\quad i=0,1,\dots,M-1

$$

- 所有信号具有相同持续时间 $T$ 和能量 $E$。

- 频率间隔为 $1/(2T)$，保证信号正交。

### 正交性条件

$$

\int_0^T s_i(t)s_j(t)\,dt =

\begin{cases}

E, & i=j \\

0, & i\neq j

\end{cases}

$$

  

- **优点**：易于区分符号，抗非线性失真能力强。

### M-FSK 与 M-QAM 对比
  
- M-FSK / M-PSK：恒包络，适合非线性信道  
- M-QAM：包络变化，仅适用于线性信道  

### 多载波调制（Multi-carrier Modulation）

  
- 单载波系统在频率选择性信道中易产生严重符号间干扰（ISI）。
- 多载波调制将数据分散到多个子载波上：
  - 单载波发射功率谱
  - 多载波发射功率谱
  - 多载波接收功率谱

![](Assests/Pasted%20image%2020251222160631.png)

  
### 正交频分复用（OFDM）

  
- OFDM 是典型的多载波调制技术。
- 将高速数据流拆分到多个正交子载波上传输。
- 每个子载波经历近似平坦信道。
- 功率分散在多个子载波上，降低对频率选择性衰落的敏感度。
