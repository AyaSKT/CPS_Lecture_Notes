将模拟信号转换为数字信号的步骤
- Sampling 采样
- Quantization 量化
- Encoding 编码
## Sampling
对具有有限能量的信号 $g(t)$ 进行瞬时均匀采样，每隔 $T_s$ 秒一次。 
获得无限的样本序列，记为 $g(nT_s)$。 
- $T_s$ 为采样间隔或采样周期。 
- $f_s = \frac{1}{T_s}$ 为采样频率。 
![](Assests/Pasted%20image%2020251203162855.png)

 **理想采样**： 
 - 理想的采样形式称为瞬时采样。

$$
g_{\delta}(t)=\sum_{n=-\infty}^{\infty}g(nT_{s})\delta(t-nT_{s})
$$

。 
 - $g_{\delta}(t)$ : 是瞬时（理想）采样信号。 
 - $\delta(t - nT_s)$ : 表示位于时间 $t = nT_s$ 的 $\delta$ 函数。

### 采样定理 (The Sampling Theorem) 
- 采样定理是信号分析中最重要的结果之一；它在通信和信号处理中具有广泛的应用。
- 许多现代信号处理技术和整个数字通信方法族都建立在该定理的有效性及其提供的见解之上。

假设信号 $x(t)$ 是严格带限的（band-limited），带宽为 $W$，即对于 $|f| \ge W$，有 $X(f) = 0$。 
令 $x(t)$ 在某些基本采样间隔 $T_s$ 的倍数处被采样，其中 $T_s \le \frac{1}{2W}$。 
那么，可以通过以下重建公式从采样值重建原始信号 $x(t)$：

$$
x(t) = \sum_{n=-\infty}^{\infty} x(nT_s) \,\mathrm{sinc}\left(\frac{t}{T_s} - n\right)
$$

$$
= \sum_{n=-\infty}^{\infty} x\left(\frac{n}{2W}\right) \mathrm{sinc}(2Wt - n)
$$

现在，如果我们对前述关系式的两边求傅里叶变换，并对右边应用卷积定理的对偶形式 (dual of the convolution theorem)，我们得到：

$$
X_{\delta}(f) = X(f) * \mathcal{F}\left[ \sum_{n=-\infty}^{\infty} \delta(t - nT_s) \right]
$$

利用 $\sum_{n=-\infty}^{\infty} \delta(t - nT_s)$ 的傅里叶变换，我们得到：

$$
\mathcal{F}\left[ \sum_{n=-\infty}^{\infty} \delta(t - nT_s) \right] = \frac{1}{T_s} \sum_{n=-\infty}^{\infty} \delta\left(f - \frac{n}{T_s}\right)
$$

代入前一个方程，我们得到：

$$

X_{\delta}(f) = X(f) * \frac{1}{T_s} \sum_{n=-\infty}^{\infty} \delta\left(f - \frac{n}{T_s}\right)
$$

$$

= \frac{1}{T_s} \sum_{n=-\infty}^{\infty} X\left(f - \frac{n}{T_s}\right)
$$

其中

$$
X(f) * \delta\left(f - \frac{n}{T_s}\right) = X\left(f - \frac{n}{T_s}\right)
$$