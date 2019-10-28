设$X_0,X_1,\ldots$是鞅，且$\forall k\ge1$有$|X_k-X_{k-1}|\le c_k$，那么$\displaystyle Pr[|X_n-X_0|\ge t]\le2exp(-\frac{t^2}{2\sum_{k=1}^n{c^2_k}})$

证明：

先证$\displaystyle Pr[X_n-X_0\ge t]$

令$\forall i\ge1,Y_i=X_i-X_{i-1}$，有$E[Y_i|X_0,\ldots,X_{i-1}]=E[X_i-X_{i-1}|X_0,\ldots,X_{i-1}]=E[X_i|X_0,\ldots,X_{i-1}]-E[X_{i-1}|X_0,\ldots,X_{i-1}]=X_{i-1}-X_{i-1}=0$

令$Z_n=\sum_{i=1}^n{Y_i}=\sum_{i=1}^{n}{X_i-X_{i-1}}=X_n-X_0$，只需确定$Pr[Z_n\ge t]$的上界

由马尔可夫不等式，$Pr[Z_n\ge t]=Pr[e^{\lambda Z_n}\ge e^{\lambda t}]\le \frac{E[e^{\lambda Z_n}]}{e^{\lambda t}}$

$E[e^{\lambda Z_n}]=E[E[e^{\lambda Z_n}|X_0,\ldots,X_{n-1}]]=E[E[e^{\lambda Z_{n-1}+Y_n}|X_0,\ldots,X_{n-1}]]=E[e^{\lambda Z_{n-1}}*E[e^{\lambda Y_n}|X_0,\ldots,X_{n-1}]]$

> 引理
>
> 设$X$是随机变量，且$E[X]=0,|X|\le c$，则对于$\lambda>0$，有$E[e^{\lambda X}]\le e^{\lambda^2c^2/2}$

之前已证$E[Y_n|X_0,\ldots,X_{n-1}]=0$，且$|Y_n|=|X_n-X_{n-1}|\le c_n$，由引理得$E[e^{\lambda Y_n}|X_0,\ldots,X_{n-1}]\le e^{\lambda^2c^2_n/2}$

代回$E[e^{\lambda Z_n}]=E[e^{\lambda Z_{n-1}}*E[e^{\lambda Y_n}|X_0,\ldots,X_{n-1}]]\le E[e^{\lambda Z_{n-1}}*e^{\lambda^2c^2_n/2}]=e^{\lambda^2c^2_n/2}*E[e^{\lambda Z_{n-1}}]$

由递归关系得$E[e^{\lambda Z_n}]\le\Pi_{i=1}^{n}{e^{\lambda^2c^2_i/2}}=exp(\frac{\lambda^2}{2}\sum_{i=1}^{n}{c_i^2})$

代入$Pr[Z_n\ge t]\le \frac{E[e^{\lambda Z_n}]}{e^{\lambda t}}\le exp(\frac{\lambda^2}{2}\sum_{i=1}^{n}{c_i^2}-\lambda t)$

选取$\lambda=\frac{t}{\sum_{i=1}^{n}{c_i^2}}$有$exp(\frac{\lambda^2}{2}\sum_{i=1}^{n}{c_i^2}-\lambda t)=exp(-\frac{t^2}{2\sum_{i=1}^{n}{c_i^2}})$

所以$\displaystyle Pr[X_n-X_0\ge t]=Pr[Z_n\ge t]\le \frac{E[e^{\lambda Z_n}]}{e^{\lambda t}}\le exp(\frac{\lambda^2}{2}\sum_{i=1}^{n}{c_i^2}-\lambda t)=exp(-\frac{t^2}{2\sum_{i=1}^{n}{c_i^2}})$



推论

设$X_0,X_1,\ldots$是鞅，且$\forall k\ge1$有$|X_k-X_{k-1}|\le c$，那么$\displaystyle Pr[|X_n-X_0|\ge t]\le2exp(-\frac{t^2}{2\sum_{k=1}^n{c^2}})=2exp(-\frac{t^2}{2nc^2})$，则$\displaystyle Pr[|X_n-X_0|\ge ct\sqrt{n}]=2exp(-\frac{t^2}{2})=2e^{-t^2/2}$



推广

设$Y_0,Y_1,\ldots$是关于序列$X_0,X_1,\ldots$的鞅，且$\forall k\ge1$有$|Y_k-Y_{k-1}|\le c_k$，那么$\displaystyle Pr[|Y_n-Y_0|\ge t]\le2exp(-\frac{t^2}{2\sum_{k=1}^n{c^2_k}})$