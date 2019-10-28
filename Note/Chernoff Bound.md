若$X_1, X_2, ...,X_n$是$\{0,1\}$上互相独立的随机变量，令$\mu=\sum_{i=1}^{n}{E[X_i]}$，那么对$\forall \delta>0$有

1. $\displaystyle Pr[\sum_{i=1}^{n}{X_i}\ge(1+\delta)\mu]\le[\frac{e^{\delta}}{(1+\delta)^{1+\delta}}]^\mu<e^{-\mu*\frac{\delta ^2}{2}}$
2. $\displaystyle Pr[\sum_{i=1}^{n}{X_i}\le(1-\delta)\mu]\le[\frac{e^{-\delta}}{(1-\delta)^{1-\delta}}]^\mu<e^{-\mu*\frac{\delta ^2}{2}}$



证明：

令$\displaystyle X=\sum_{i=1}^{n}X_i$，对$\forall t \in R, t > 0$，$\displaystyle Pr[X>(1+\delta)\mu]=Pr[e^{tX}>e^{t(1+\delta)\mu}]<\frac{E[e^{tX}]}{e^{t(1+\delta)\mu}}=\frac{E[e^{t\sum_{i=1}^{n}X_i}]}{e^{t(1+\delta)\mu}}=\frac{E[\Pi_{i=1}^{n}e^{tX_i}]}{e^{t(1+\delta)\mu}}=\frac{\Pi_{i=1}^{n}E[e^{tX_i}]}{e^{t(1+\delta)\mu}}$

因为$X_i=\begin{cases}1\ \ p_i的概率\\0\ \ 1-p_i的概率 \end{cases}$，所以$E[e^{tX_i}]=p_i*e^t+1-p_i=1+p_i(e^t-1)\le e^{p_i(e^t-1)}$

$\displaystyle Pr[X>(1+\delta)\mu]<\frac{\Pi_{i=1}^{n}e^{p_i(e^t-1)}}{e^{t(1+\delta)\mu}}=\frac{e^{(e^t-1)\sum_{i=1}^{n}p_i}}{e^{t(1+\delta)\mu}}=\frac{e^{(e^t-1)\sum_{i=1}^{n}E[X_i]}}{e^{t(1+\delta)\mu}}=\frac{e^{(e^t-1)\mu}}{e^{t(1+\delta)\mu}}=(\frac{e^{(e^t-1)}}{e^{t(1+\delta)}})^\mu=(e^{e^t-1-t(1+\delta)})^\mu$

令$f(t)=e^t-1-t(1+\delta)$，$f'(t)=e^t-(1+\delta)=0 \Rightarrow t=ln(1+\delta)$代入

得$\displaystyle Pr[X>(1+\delta)\mu]<[\frac{e^\delta}{(1+\delta)^{1+\delta}}]^\mu$



同理可得$\displaystyle Pr[X<(1-\delta)\mu]<[\frac{e^{-\delta}}{(1-\delta)^{1-\delta}}]^\mu$

$ln(1-\delta)^{1-\delta}=(1-\delta)ln(1-\delta)=(1-\delta)(-\delta-\frac{\delta^2}{2}+o(\delta^3))=-\delta+\delta^2-\frac{\delta^2}{2}+o(\delta^3)>-\delta+\frac{\delta^2}{2}$

$(1-\delta)^{1-\delta}>e^{-\delta+\frac{\delta^2}{2}}$代入得$\displaystyle Pr[X<(1-\delta)\mu]<[\frac{e^{-\delta}}{(1-\delta)^{1-\delta}}]^\mu<[\frac{e^{-\delta}}{e^{-\delta+\frac{\delta^2}{2}}}]^\mu=e^{-\mu*\frac{\delta^2}{2}}$

$\displaystyle Pr[X<(1-\delta)\mu]<[\frac{e^{-\delta}}{(1-\delta)^{1-\delta}}]^\mu<e^{-\mu*\frac{\delta^2}{2}}$



**好的形式**

- $对于t\ge 2e\mu,Pr[X\ge t]\le2^{-t}$

证明：

令$t=(1+\delta)\mu$，则$1+\delta\ge 2e$，于是

$\displaystyle Pr[X\ge(1+\delta)\mu]\le[\frac{e^\delta}{(1+\delta)^{1+\delta}}]^\mu\\\le[\frac{e}{(1+\delta)}]^{(1+\delta)\mu}\\\le[\frac{e}{2e}]^{(1+\delta)\mu}\\=2^{-t}$



- $t>0,Pr[X\ge E[X]+t]\le exp(-\frac{2t^2}{n}),Pr[X\le E[X]-t]\le exp(-\frac{2t^2}{n})$

