成浩鹏 181250020

---

## Problem 1

Let ${\displaystyle X}$ be a real-valued random variable with finite ${\displaystyle \mathbb {E} [X]}$ and finite ${\displaystyle \mathbb {E} \left[\mathrm {e} ^{\lambda X}\right]}$ for all ${\displaystyle \lambda \geq 0}$. We define the **log-moment-generating function** as

${\displaystyle \Psi _{X}(\lambda ):=\ln \mathbb {E} [\mathrm {e} ^{\lambda X}]\quad {\text{ for all }}\lambda \geq 0}$,
and its dual function:

${\displaystyle \Psi _{X}^{*}(t):=\sup _{\lambda \geq 0}(\lambda t-\Psi _{X}(\lambda ))}$.
Assume that ${\displaystyle X}$ is NOT almost surely constant. Then due to the convexity of ${\displaystyle \mathrm {e} ^{\lambda X}}$ with respect to ${\displaystyle \lambda }$, the function ${\displaystyle \Psi _{X}(\lambda )}$ is strictly convex over ${\displaystyle \lambda \geq 0}$.

- Prove the following Chernoff bound:
  ${\displaystyle \Pr[X\geq t]\leq \exp(-\Psi _{X}^{*}(t))}$.
  In particular if ${\displaystyle \Psi _{X}(\lambda )}$ is continuously differentiable, prove that the supreme in ${\displaystyle \Psi _{X}^{*}(t)}$ is achieved at the unique ${\displaystyle \lambda \geq 0}$ satisfying
  ${\displaystyle \Psi _{X}'(\lambda )=t}$
  where ${\displaystyle \Psi _{X}'(\lambda )}$ denotes the derivative of ${\displaystyle \Psi _{X}(\lambda )}$ with respect to ${\displaystyle \lambda }$.

- **Normal random variables.** Let ${\displaystyle X\sim \mathrm {N} (\mu ,\sigma )}$ be a Gaussian random variable with mean ${\displaystyle \mu }$ and standard deviation ${\displaystyle \sigma }$. What are the ${\displaystyle \Psi _{X}(\lambda )}$ and ${\displaystyle \Psi _{X}^{*}(t)}$? And give a tail inequality to upper bound the probability ${\displaystyle \Pr[X\geq t]}$.
- **Poisson random variables.** Let ${\displaystyle X\sim \mathrm {Pois} (\nu )}$ be a Poisson random variable with parameter ${\displaystyle \nu }$, that is, ${\displaystyle \Pr[X=k]=\mathrm {e} ^{-\nu }\nu ^{k}/k!}$ for all ${\displaystyle k=0,1,2,\ldots }$. What are the ${\displaystyle \Psi _{X}(\lambda )}$ and ${\displaystyle \Psi _{X}^{*}(t)}$? And give a tail inequality to upper bound the probability ${\displaystyle \Pr[X\geq t]}$.
- **Bernoulli random variables.** Let ${\displaystyle X\in \{0,1\}}$ be a single Bernoulli trial with probability of success ${\displaystyle p}$, that is, ${\displaystyle \Pr[X=1]=1-\Pr[X=0]=p}$. Show that for any ${\displaystyle t\in (p,1)}$, we have ${\displaystyle \Psi _{X}^{*}(t)=D(Y\|X)}$ where ${\displaystyle Y\in \{0,1\}}$ is a Bernoulli random variable with parameter ${\displaystyle t}$ and ${\displaystyle D(Y\|X)=(1-t)\ln {\frac {1-t}{1-p}}+t\ln {\frac {t}{p}}}$ is the [Kullback-Leibler](https://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence) divergence between ${\displaystyle Y}$ and ${\displaystyle X}$.
- **Sum of independent random variables.** Let ${\displaystyle X=\sum _{i=1}^{n}X_{i}}$ be the sum of ${\displaystyle n}$ independently and identically distributed random variables ${\displaystyle X_{1},X_{2},\ldots ,X_{n}}$. Show that ${\displaystyle \Psi _{X}(\lambda )=\sum _{i=1}^{n}\Psi _{X_{i}}(\lambda )}$ and ${\displaystyle \Psi _{X}^{*}(t)=n\Psi _{X_{i}}^{*}({\frac {t}{n}})}$. Also for binomial random variable ${\displaystyle X\sim \mathrm {Bin} (n,p)}$, give an upper bound to the tail inequality ${\displaystyle \Pr[X\geq t]}$ in terms of KL-divergence.
  Give an upper bound to ${\displaystyle \Pr[X\geq t]}$ when every ${\displaystyle X_{i}}$ follows the geometric distribution with a probability ${\displaystyle p}$ of success.

#### 回答

- $Pr[X\ge t]=Pr[e^{\lambda X}\ge e^{\lambda t}]$，运用Markov Inequality有$Pr[e^{\lambda X}\ge e^{\lambda t}]\le\frac{E[e^{\lambda X}]}{e^{\lambda t}}=e^{\Psi _X(\lambda )-\lambda t}\le e^{-\Psi_X^*(t)}$，于是$Pr[X\ge t]\le \exp(-\Psi_X^*(t))$。

  设$f(\lambda)=\lambda t-\Psi_X(\lambda)$，则令$f'(\lambda)=t-\Psi_X'(\lambda)=0$得$\Psi_X'(\lambda)=t$，则$\Psi_X^*(t)=\lambda t-\int\Psi_X'(\lambda)d\lambda=Ct$，其中$C$为一常数。所以要让$\Psi_X^*(t)$取到上界，就需要满足$\Psi_X'(\lambda)=t$。

- $E[e^{\lambda X}]=e^{\mu\lambda+\frac{\sigma^2\lambda^2}{2}}$，则$\Psi_X(\lambda)=\mu\lambda+\frac{\sigma^2\lambda^2}{2}$，$\displaystyle \Psi_X^*(t)=\sup_{\lambda\ge0}{(\lambda t-\mu\lambda-\frac{\sigma^2\lambda^2}{2})}=\sup_{\lambda\ge0}{(-\frac{\sigma^2\lambda^2}{2}+(t-\mu)\lambda)}=\begin{cases}0,t\le\mu\\\frac{(t-\mu)^2}{2\sigma^2},t>\mu\end{cases}$

  $Pr[X\ge t]\le \exp(-\Psi_X^*(t))=\exp(-\frac{(t-\mu)^2}{2\sigma^2})$

- $\displaystyle E[e^{\lambda X}]=\sum_{k=0}^\infin{e^{\lambda k}e^{-v}v^k/k!}=e^{-v}\sum_{k=0}^\infin{\frac{(e^\lambda v)^k}{k!}}=e^{-v}e^{e^\lambda v}=e^{(e^\lambda-1)v}$，则$\Psi_X(\lambda)=(e^\lambda-1)v$，$\displaystyle \Psi_X^*(t)=\sup_{\lambda\ge0}{(\lambda t-(e^\lambda-1)v)}$

  令${\Psi_{X}'(\lambda)=t}$得$\lambda=\ln\frac{t}{v}$代入得$\sup \Psi_X^*(t)=t\ln\frac{t}{v}-t+v$，则$Pr[X\ge t]\le \exp(-\Psi_X^*(t))\le \exp(t-v-t\ln\frac{t}{v})$

- $E[e^{\lambda X}]=pe^\lambda+(1-p)*1=pe^\lambda+1-p$

  $\Psi_X(\lambda)=\ln(pe^\lambda+1-p),\Psi_X'(\lambda)=\frac{pe^\lambda}{pe^\lambda+1-p}$

  由${\Psi_X'(\lambda)=t}$得$\lambda=\ln\frac{t(p-1)}{p(t-1)}=\ln\frac{t}{p}-\ln\frac{1-t}{1-p},\ln(pe^\lambda+1-p)=\ln\frac{pe^\lambda}{t}=\lambda-\ln\frac{t}{p}$

  $\Psi_X^*(t)=\lambda t-\ln(pe^\lambda+1-p)=\lambda t-\lambda+\ln\frac{t}{p}=(t-1)(\ln\frac{t}{p}-\ln\frac{1-t}{1-p})+\ln\frac{t}{p}=(1-t)\ln\frac{1-t}{1-p}+t\ln\frac{t}{p}$

- $\displaystyle \Psi_X(\lambda)=\ln E[e^{\lambda X}]=\ln E[e^{\lambda\sum_{i=1}^nX_i}]=\ln E[\prod_{i=1}^ne^{\lambda X_i}]=\ln \prod_{i=1}^nE[e^{\lambda X_i}]=\sum_{i=1}^n\ln E[e^{\lambda X_i}]=\sum_{i=1}^n\Psi_{X_i}(\lambda)$

  $\displaystyle \Psi_X^*(t)=\sup_{\lambda\geq0}(\lambda t-\Psi_X(\lambda))=\sup_{\lambda\geq0}(\sum_{i=1}^n(\lambda \frac{t}{n})-\sum_{i=1}^n\Psi_{X_i}(\lambda))=\sum_{i=1}^n\sup_{\lambda\geq0}(\lambda \frac{t}{n}-\Psi_{X_i}(\lambda))=\sum_{i=1}^n\Psi_{X_i}^*(\frac{t}{n})$，因为$X_i$独立同分布，所以$\displaystyle \Psi_X^*(t)=\sum_{i=1}^n\Psi_{X_i}^*(\frac{t}{n})=n\Psi_{X_i}^*(\frac{t}{n})$
  
  $\Psi_{X_i}^*(\frac{t}{n})=(1-\frac{t}{n})\ln\frac{1-\frac{t}{n}}{1-p}+\frac{t}{n}\ln\frac{\frac{t}{n}}{p}=(1-\frac{t}{n})\ln\frac{n-t}{1-p}+\frac{t}{n}\ln\frac{t}{p}-\ln n$
  
  $Pr[X\ge t]\le \exp(-\Psi_X^*(t))=\exp(-n\Psi_{X_i}^*(\frac{t}{n}))=\exp(n\ln n-(n-t)\ln\frac{n-t}{1-p}-t\ln\frac{t}{p})$
  
  $Pr[X\ge t]=1-Pr[X<t]=1-{t-1\choose n}p^n(1-p)^{t-1-n}\\=1-\frac{(t-1)!}{n!(t-1-n)!}*p^n(1-p)^{t-1-n}\\=1-p^n(1-p)^{t-1-n}\prod_{i=1}^n\frac{t-1-n+i}{i}\\\le1-p^n(1-p)^{t-1-n}(1+(t-1-n)\sum_{i=1}^n\frac{1}{i})\\\le1-p^n(1-p)^{t-1-n}(1+(t-1-n)\ln n)$

## Problem 2

An ${\displaystyle n}$-dimensional hypercube ${\displaystyle Q_{n}}$ is a graph with ${\displaystyle 2^{n}}$ vertices, where each vertex is represented by an ${\displaystyle n}$-bit vector, and there is an edge between two vertices if and only if their bit-vectors differ in exactly one bit.

Given an ${\displaystyle n}$-dimensional hypercube with some non-empty subset of vertices ${\displaystyle S}$, which is called marked black. Let ${\displaystyle f(u)}$ denote the shortest distance from vertex ${\displaystyle u}$ to any black vertex. Formally,

${\displaystyle f(u)=\min _{v\in S}\mathrm {dist} _{Q_{n}}(u,v),}$

where ${\displaystyle \mathrm {dist} _{Q_{n}}(u,v)}$ denotes the length of the shortest path between ${\displaystyle u}$ and {\displaystyle v}{\displaystyle v} in graph ${\displaystyle Q_{n}}$ .

Prove that if we choose ${\displaystyle u}$ from all ${\displaystyle 2^{n}}$ vertices uniformly at random, then, with high probability, ${\displaystyle f(u)}$ can not deviate from its expectation too much:

${\displaystyle \mathrm {Pr} [|f(u)-\mathbb {E} [f(u)]|\geq t{\sqrt {n\log n}}]\leq n^{-c}.}$

Give the relation between ${\displaystyle c}$ and ${\displaystyle t}$.

#### 回答

对于任意两个顶点$u,v$的距离，不会超过$n$，因为其向量表示只有$n$位。

设随机变量序列$X_1,\ldots,X_n$表示长为$n$的一条路径，设$Y_i=E[f(u)\mid X_1,\ldots,X_i],0\le i\le n$，特别地，$Y_0=E[f(u)],Y_n=f(u)$。

考虑$Y_i=E[f(u)\mid X_1,\ldots,X_i]$，路径上每增加一个新的顶点，一种情况是远离目标点而去，需要再多走一步返回，另一种情况是向着目标点走，所以有$\mid Y_i-Y_{i-1}\mid\le2$。根据`Azuma's Inequality`有$Pr[\mid Y_n-Y_0\mid\ge t]\le2\exp(-\frac{t^2}{2\sum_{k=1}^n{2^2}})=2\exp(-\frac{t^2}{8n})$，$t$用$t\sqrt{n\log n}$代入有$Pr[\mid Y_n-Y_0\mid\ge t\sqrt{n\log n}]\le2\exp(-\frac{(t\sqrt{n\log n})^2}{8n})=2exp(-\frac{t^2\log n}{8})=2n^{-t^2/8}\le n^{-t^2/8+1}$

所以$Pr[\mid f(u)-E[f(u)]\mid\ge t\sqrt{n\log n}]=Pr[\mid Y_n-Y_0\mid\ge t]\le n^{-t^2/8+1}$，此时$c=t^2/8-1$。

## Problem 3

Let ${\displaystyle Y_{1},Y_{2},Y_{3},\ldots ,Y_{n}}$ be a set of ${\displaystyle n}$ random variables where each ${\displaystyle Y_{i}\in \{0,1\}}. $All variables ${\displaystyle Y_{i}}$ follow some joint distribution over ${\displaystyle \{0,1\}^{n}}$ and they may NOT be mutually independent. Assume the following property holds for ${\displaystyle (Y_{i})_{1\leq i\leq n}}$. For any ${\displaystyle 1\leq i\leq n}$ and it holds that

${\displaystyle \forall c_{1}\in \{0,1\},c_{2}\in \{0,1\},\ldots ,c_{i-1}\in \{0,1\},\quad \Pr[Y_{i}=1\mid \forall 1\leq j<i,Y_{j}=c_{j}]\leq p.}$

Let ${\displaystyle X_{1},X_{2},X_{3},\ldots ,X_{n}}$ be a set of ${\displaystyle n}$ mutually independent random variables where each ${\displaystyle X_{i}\in \{0,1\}}$. Assume

${\displaystyle \forall 1\leq i\leq n:\quad \Pr[X_{i}=1]=p.}$

Prove that for any ${\displaystyle a\geq 0}$, it holds that

${\displaystyle \Pr \left[\sum _{i=1}^{n}Y_{i}\geq a\right]\leq \Pr \left[\sum _{i=1}^{n}X_{i}\geq a\right].}$

Prove that for any ${\displaystyle t\geq 0}$, it holds that

${\displaystyle \Pr \left[\sum _{i=1}^{n}Y_{i}\geq np+t\right]\leq \exp \left(-{\frac {2t^{2}}{n}}\right).}$

**Hint:** Although random variables ${\displaystyle Y_{1},Y_{2},Y_{3},\ldots ,Y_{n}}$ may not be mutually independent, we can still bound the tail probability for ${\displaystyle \sum _{i=1}^{n}Y_{i}}$. This tool is called the stochastic dominance.

To prove the first inequality, you only need to construct a coupling ${\displaystyle {\mathcal {C}}}$ between ${\displaystyle (X_{i})_{1\leq i\leq n}}$ and ${\displaystyle (Y_{i})_{1\leq i\leq n}}$ such that

${\displaystyle \Pr _{\mathcal {C}}[\,\forall 1\leq i\leq n,Y_{i}\leq X_{i}\,]=1.}$

This implies the random sequence ${\displaystyle (Y_{i})_{1\leq i\leq n}}$ is stochastically dominated by the random sequence ${\displaystyle (X_{i})_{1\leq i\leq n}}$.

#### 回答

- 设$Pr[Y_i=1\mid\forall1\le j<i,Y_j=c_j]=p_i<p$，其中$p_i$是与$Y$的前$i-1$项相关的变量

  对于某一确定的$X$和$Y$，构造$Z_1,\ldots,Z_n$，满足

  - 如果$X_i=0$，则$Z_i=0$
  - 如果$X_i=1$，则有概率$\frac{p_i}{p}$使$Z_i=1$

  此时，有$Pr[\forall1\le i\le n,X_i\ge Z_i]=1$，从而$Pr[\sum_{i=1}^nX_i\ge a]\ge Pr[\sum_{i=1}^nZ_i\ge a]$

  而$Pr[Z_i=1]=Pr[X_i=1]*\frac{p_i}{p}=p_i<p$，此时$Z$和$Y$是同分布的，所以也就有$Pr[\sum_{i=1}^nX_i\ge a]\ge Pr[\sum_{i=1}^nY_i\ge a]$

  对于其他的$X$和$Y$，同理也有此结论，所以对于任意$X$和$Y$，都有$Pr[\sum_{i=1}^nY_i\ge a]\le Pr[\sum_{i=1}^nX_i\ge a]$
  
- - 当$t=0$时，$Pr[\sum_{i=1}^nY_i\ge np+t]\le1$成立
  - 当$t>0$时，设$X=\sum_{i=1}^nX_i$，由`Chernoff Bound`$Pr[X\ge E[X]+t]\le\exp(-\frac{2t^2}{n})$得$Pr[\sum_{i=1}^nX_i\ge np+t]\le\exp(-\frac{2t^2}{n})$，又有$Pr[\sum_{i=1}^nX_i\ge a]\ge Pr[\sum_{i=1}^nY_i\ge a]$，所以$Pr[\sum_{i=1}^nY_i\ge np+t]\le\exp(-\frac{2t^2}{n})$

## Problem 4

Let ${\displaystyle U}$ be a universal set. We use ${\displaystyle 2^{U}}$ to denote the collection of all subsets of ${\displaystyle U}$. Let ${\displaystyle {\mathcal {F}}}$ be a family of hash functions, in which each hash function ${\displaystyle h:2^{U}\rightarrow \{0,1\}^{m}}$ maps subsets of ${\displaystyle U}$ to 0-1 vectors of length ${\displaystyle m}$. A locality sensitive hashing scheme is a distribution on a family ${\displaystyle {\mathcal {F}}}$ of hash functions operating on ${\displaystyle 2^{U}}$, such that for two subsets ${\displaystyle A,B\in 2^{U}}$,

${\displaystyle (1)\qquad \Pr _{h\in {\mathcal {F}}}[h(A)=h(B)]=sim(A,B).}$

Here ${\displaystyle sim:2^{U}\times 2^{U}\rightarrow [0,1]}$ is called the similarity function. Given a hash function family ${\displaystyle {\mathcal {F}}}$ that satisfies Equation (1), we will say that ${\displaystyle {\mathcal {F}}}$ is a locality sensitive hash function family corresponding to similarity function ${\displaystyle sim(\cdot ,\cdot )}$.

- For any similarity function ${\displaystyle sim(A,B)}$ that admits a locality sensitive hash function family as defined in Equation (1), prove that the distance function ${\displaystyle d(A,B)\triangleq 1-sim(A,B)}$ satisfies triangle inequality, formally,
  ${\displaystyle \forall A,B,C\in 2^{U}:\quad d(A,B)+d(B,C)\geq d(A,C).}$

- Show that there is no locality sensitive hash function family corresponding to Dice's and the Overlap coefficient. Dice's coefficient is defined as:
  ${\displaystyle sim_{Dice}(A,B)={\frac {2|A\cap B|}{|A|+|B|}}.}$

  Overlap coefficient is defined as:

  ${\displaystyle sim_{Ovl}(A,B)={\frac {|A\cap B|}{\min(|A|,|B|)}}.}$

  <font color="blue">Hint: use the triangle inequality result. </font>

- Construct a collection of hash function ${\displaystyle {\mathcal {B}}}$ where ${\displaystyle f:\{0,1\}^{m}\rightarrow \{0,1\}}$ for each ${\displaystyle f\in {\mathcal {B}}}$, together with a probability distribution on ${\displaystyle {\mathcal {B}}}$ such that
  ${\displaystyle \forall x,y\in \{0,1\}^{m}:\quad \Pr _{f\in {\mathcal {B}}}[f(x)=f(y)]={\begin{cases}1&{\text{ if }}x=y;\\{\frac {1}{2}}&{\text{ if }}x\neq y.\end{cases}}}$

  Then use the hash function family ${\displaystyle {\mathcal {B}}}$ to prove the following result. Given a locality sensitive hash function family ${\displaystyle {\mathcal {F}}}$ (${\displaystyle h:2^{U}\rightarrow \{0,1\}^{m}}$ for each ${\displaystyle h\in {\mathcal {F}}}$) corresponding to a similarity function ${\displaystyle sim(A,B)}$, we can obtain a locality sensitive hash function ${\displaystyle {\mathcal {F}}'}$ (${\displaystyle h':2^{U}\rightarrow \{0,1\}}$ for each ${\displaystyle h'\in {\mathcal {F}}'}$) corresponding to the similarity function ${\displaystyle {\frac {1+sim(A,B)}{2}}}$.

#### 回答

