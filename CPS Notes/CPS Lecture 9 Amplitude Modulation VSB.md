#### VSB的需求
-   DSB信号的生成要简单得多，但需要message signal $m(t)$ 两倍的信号带宽。
-   SSB信号具有频谱效率 (spectrum efficient)，因为它所需带宽更少，但精确生成SSB信号相当困难。
    -   通常，消息信号 $m(t)$ 必须在直流附近有一个零点 (null)。
    -   在相移法 (phase shift method) 中所需的移相器 (phase shifter) 只能近似地实现 (realizable only approximately)。
-   SSB依赖于能够滤除一个边带 (filter out one sideband)。
    -   对于音频 (audio) 信号，这是可行的，因为语音频谱 (voice spectrum) 在300 Hz以下会衰减，为过渡带 (transition band) 留出了空间。
    -   这对于其他信号（如视频信号 (video)）是不可能的，因为它们在低频有很强的分量 (strong components at low frequencies)。
-   Vestigial Sideband (VSB) modulation (也称为 asymmetric sideband) 是 DSB (Double-Sideband) 和 SSB (Single-Sideband) 之间的一种折衷。
    -   它继承了 DSB 和 SSB 的优点，但以较小的代价避免了它们的缺点。
    -   VSB 信号相对易于产生 (relatively easy to generate)。
    -   同时，VSB 只传输一个边带 (sideband) 和不需要的边带的一小部分（残留部分，vestige）。因此，VSB 的带宽通常仅比 SSB 信号的带宽大 25%。

-   VSB 特别适用于那些带宽大但没有直流间隙 (dc gap-band) 的消息信号，例如基带数字信号 (baseband digital signals) 和视频信号。

-   VSB modulation 被广泛应用于：
    -   模拟电视系统 NTSC (The analog TV system NTSC)
    -   磁共振成像 (Magnetic Resonance Imaging, MRI)，用于减少需要采集的数据量。

![](Assests/Pasted%20image%2020251121112638.png)
#### VSB Modulation
-   VSB 信号的生成采用标准 AM 或 DSB-SC 调制：
    $$ \phi_{DSB}(t)=m(t) 2\cos\omega_c t $$
    $$ \phi_{DSB}(f)=[M(f+f_c)+M(f-f_c)] $$
    然后使其通过一个 VSB 成形滤波器 $ H_i(f) $：
    $$ \phi_{VSB}(f)=[M(f+f_c)+M(f-f_c)]H_i(f) $$
-   与 SSB 的锐截止滤波器不同，VSB 滤波器是渐变截止滤波器，更易于实现。
![](Assests/Pasted%20image%2020251121113106.png)

#### VSB Demodulation
Baseband signal可以被一个有恰当的VSB filter $H_0(f)$ 同步检波器精确还原。
如果载波足够大，baseband signal甚至可以被包络检波还原。
![](Assests/Pasted%20image%2020251121135846.png)

#### VSB Shaping Filter
需要通过同步解调 (synchronous demodulation) 从接收到的 VSB 信号中恢复出原始消息信号 $ m(t) $。

## 解调过程
1. 与载波相乘  
将接收到的 VSB 信号 $\phi_{VSB}(t)$ 乘以本地载波 $2\cos(\omega_c t)$：

时域表达式：
$$ e(t) = \phi_{VSB}(t) \cdot 2\cos(\omega_c t) $$

频域表达式（通过傅里叶变换）：
$$ E(f) = \phi_{VSB}(f) * [\delta(f+f_c) + \delta(f-f_c)] $$
$$ = \phi_{VSB}(f+f_c) + \phi_{VSB}(f-f_c) $$

2. 频谱特性分析
-   解调后在频域产生两个边带副本 (two copies of sidebands)
-   这两个边带都偏移到了基带 (baseband) 区域
-   关键问题：两个边带在基带区域存在**重叠 (Overlap)**

3. 滤波器补偿
需要设计滤波器 $H_o(f)$ 来补偿重叠造成的影响：
$$ E(f)H_o(f) = [\phi_{VSB}(f+f_c) + \phi_{VSB}(f-f_c)]H_o(f) = M(f) $$

频谱图示说明
1.  $\Phi_{VSB}(f)$：原始 VSB 信号频谱  
2.  $E(f)$：解调后的频谱，显示重叠区域  
3.  $E(f)H_o(f)$：经过滤波器补偿后的频谱，恢复出 $M(f)$
![](Assests/Pasted%20image%2020251121140658.png)

求解接收端滤波器 $H_{o}(f)$：

$$ M(f)=[\phi_{VSB}(f+f_{c})+\phi_{VSB}(f-f_{c})]~{H_o}(f) $$

使用 VSB 已调信号表达式：

$$ \phi_{VSB}(f)=[M(f+f_{c})+M(f-f_{c})]~{H_{i}}(f) $$

可推导得：

$$ \phi_{VSB}(f+f_{c})=[M(f+2f_{c})+M(f)]~{H_{i}}(f+f_{c}) $$

$$ \phi_{VSB}(f-f_{c})=[M(f)+M(f-2f_{c})]~{H_{i}}(f-f_{c}) $$

$$ M(f)=[[Assests/M(f+2f_{c})+M(f)]~{H_{i}}(f+f_{c})+[M(f)+M(f-2f_{c})]~{H_{i}}(f-f_{c})]~{H_o}(f) $$

消除 $\pm 2f_{c}$ 处的频谱分量（将被低通滤波器抑制）：

$$ M(f)=M(f)[H_{i}(f+f_{c})+H_{i}(f-f_{c})]~{H_o}(f) $$

最终得到：

$$ H_{o}(f)=\frac{1}{H_{i}(f+f_{c})+H_{i}(f-f_{c})} \quad |f|\leq B $$
