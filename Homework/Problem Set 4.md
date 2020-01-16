成浩鹏 181250020

---

## Problem 1

Suppose we want to estimate the value of ${\displaystyle Z}$. Let ${\displaystyle {\mathcal {A}}}$ be an algorithm that outputs ${\displaystyle {\widehat {Z}}}$ satisfying ${\displaystyle \Pr[(1-\epsilon )Z\leq {\widehat {Z}}\leq (1+\epsilon )Z]\geq {\frac {3}{4}}.}$

We run ${\displaystyle {\mathcal {A}}}$ independently for ${\displaystyle s}$ times, and obtain the outputs ${\displaystyle {\widehat {Z}}_{1},{\widehat {Z}}_{2},\ldots ,{\widehat {Z}}_{s}}$.

Let ${\displaystyle X}$ be the **median** (中位数) of ${\displaystyle {\widehat {Z}}_{1},{\widehat {Z}}_{2},\ldots ,{\widehat {Z}}_{s}}$. Find the number ${\displaystyle s}$ such that ${\displaystyle \Pr[(1-\epsilon )Z\leq X\leq (1+\epsilon )Z]\geq 1-\delta .}$

Express ${\displaystyle s}$ as a function of ${\displaystyle \delta }$. Make ${\displaystyle s}$ as small as possible.

**Remark**: in this problem, we boost the probability of success from ${\displaystyle {\frac {3}{4}}}$ to ${\displaystyle 1-\delta }$. This method is called the median trick.

**Hint**: Chernoff bound.

#### 回答

令$X_1,X_2,\ldots,X_s$为$0/1$独立随机变量，$X_i=I[(1-\epsilon)Z\le\widehat Z_i\le(1+\epsilon)Z]$，$E[X_i]=\frac{3}{4}$，$\mu=E[\sum_{i=1}^s{X_i}]=\sum_{i=1}^s{E[X_i]}=\frac{3}{4}s$。

要使$(1-\epsilon)Z\le X\le(1+\epsilon)Z$成立，需要使序列$\widehat Z_i$中一半以上的元素满足$(1-\epsilon)Z\le\widehat Z_i\le(1+\epsilon)Z$，即$\sum_{i=1}^s{X_i}>\frac{1}{2}s$。

$Pr[(1-\epsilon)Z\le X\le(1+\epsilon)Z]=Pr[\sum_{i=1}^s{X_i}>\frac{1}{2}s]=Pr[\sum_{i=1}^s{X_i}-\frac{3}{4}s>-\frac{1}{4}s]\\=Pr[|\sum_{i=1}^s{X_i}-\mu|<\frac{1}{4}s]\ge^{Chernoff\ Bound}1-\exp(\frac{-2*(\frac{1}{4}s)^2}{s})=1-\exp(-\frac{1}{8}s)$

$\exp(-\frac{1}{8}s)=\delta\rightarrow s=-8\ln(\delta)$

## Problem 2

Given an undirected graph ${\displaystyle G(V,E)}$ with maximum degree ${\displaystyle \Delta }$, where the vertex set ${\displaystyle V}$ is partitioned into ${\displaystyle r}$ disjoint subsets, i.e., ${\displaystyle V=S_{1}\cup S_{2}\cup \cdots \cup S_{r}}$ with ${\displaystyle S_{i}\cap S_{j}=\varnothing }$ for all ${\displaystyle i\neq j}$. We call a vertex set ${\displaystyle T}$ is a transversal of the partition ${\displaystyle \{S_{1},S_{2},\cdots ,S_{r}\}}$, if ${\displaystyle |T\cap S_{i}|=1}$ for all ${\displaystyle 1\leq i\leq r}$. Assume that ${\displaystyle |S_{i}|\geq 2e\Delta }$ for all ${\displaystyle 1\leq i\leq r}$.

1. Prove that there must be an independent transversal (a transversal which is also an independent set) of ${\displaystyle \{S_{1},S_{2},\cdots ,S_{r}\}}$.

**Hint**: Lovász Local Lemma.

2. Design a randomized algorithm that finds an independent transversal of ${\displaystyle \{S_{1},S_{2},\cdots ,S_{r}\}}$ in expected polynomial time.

#### 回答

1. 设$T\cap S_i=\{v_i\}$，则$T=\{v_1,v_2,\ldots,v_r\}$，必然存在一个 transversal 。

   只需证明存在一个 transversal 是独立集。

   设$A_i(1\le i\le r):从S_i中选出来的点与从其他集合中选出来的点相邻$，目标：$Pr[\bigcap^r_{i=1}\overline A_i]>0$

   每个$A_i$都是独立的，除了与最多$\Delta$个其他事件有关以外

   $Pr[A_i]=\frac{1}{|S_i|}\le\frac{1}{2e\Delta}\le\frac{1}{4\Delta}$，由`Lovász Local Lemma (Erdos-Lovász 1975)`得$Pr[\bigcap^r_{i=1}\overline A_i]>0$

   则存在一个独立集的 transversal 。

2. >**算法**
   >
   >1. 随机独立为每个$S_i$选择一个点$v_i$
   >2. 判断$\{v_1,v_2,\ldots,v_r\}$是否为独立集的 transversal
   >3. 如果不是则跳转到第1步
   >4. 输出$T=\{v_1,v_2,\ldots,v_r\}$

   $Pr[v_2与v_1相邻]=\frac{\Delta}{|S_2|\Delta}=\frac{1}{|S_2|}$

   $Pr[v_3与v_1或v_2相邻]=\frac{2\Delta}{|S_3|\Delta}=\frac{2}{|S_3|}$

   $Pr[v_i与v_1或v_2或\ldots或v_{i-1}相邻]=\frac{(i-1)\Delta}{|S_i|\Delta}=\frac{i-1}{|S_i|}$

   则$Pr[一次随机能够找到解]=(1-Pr[v_2与v_1相邻])\ldots(1-Pr[v_r与v_1或v_2或\ldots或v_{r-1}相邻]])\\=(1-\frac{1}{|S_1|})(1-\frac{2}{|S_2|})\ldots(1-\frac{r-1}{|S_r|})\\\ge(1-\frac{1}{2e\Delta})(1-\frac{2}{2e\Delta})\ldots(1-\frac{r-1}{2e\Delta})\\\ge1-\frac{1+2+\ldots+r-1}{2e\Delta}\\=1-\frac{r(r-1)}{4e\Delta}\\\ge1-\frac{r^2}{4e\Delta}$

   $Pr[一次随机找不到解]\le\frac{r^2}{4e\Delta}$

   重复运行算法的第$1-3$步$x=\frac{\ln n}{\ln\Delta-2\ln r+\ln 4+1}$次，则$Pr[算法返回错误解]\le(\frac{r^2}{4e\Delta})^x=\frac{1}{n}$，则$Pr[返回正确解]\ge1-\frac{1}{n}$。

## Problem 3

Given an undirected graph ${\displaystyle G=(V,E)}$, the feedback vertex set problem is to find the smallest subset of vertices, whose removal makes the graph acyclic.

Let ${\displaystyle {\mathcal {C}}}$ denote the set of all cycles in graph ${\displaystyle G}$.

Consider the following integer program

${\displaystyle {\begin{aligned}{\text{minimize}}&&&\sum _{v\in V}x_{v}\\{\text{subject to}}&&\sum _{v\in C}x_{v}&\geq 1,&\forall C&\in {\mathcal {C}},\\&&x_{v}&\in \{0,1\},&\forall v&\in V.\end{aligned}}}$

- Write the dual program.
- Use the prime-dual schema to design an approximation algorithm. What is the approximate ratio of your algorithm?
- **Bonus problem**: assuming that the following proposition holds, can your obtain a better approximation algorithm?

Proposition: Given a graph with no degree-1 vertex, it must contain a cycle with at most ${\displaystyle 2\lceil \log _{2}n\rceil }$ vertices of degree ${\displaystyle \geq 3}$, where ${\displaystyle n}$ is the total number of vertices on this graph.

#### 回答



## Problem 4

Let ${\displaystyle G=(V,E)}$ be a simple and undirected graph. The Ising model is a distribution ${\displaystyle \mu }$ over ${\displaystyle \{-1,+1\}^{V}}$ such that

${\displaystyle \forall \sigma \in \{-1,+1\}^{V},\quad \mu (\sigma )={\frac {1}{Z}}\exp \left(-\sum _{\{u,v\}\in E}\beta \sigma (u)\sigma (v)\right),}$

where the parameter ${\displaystyle \beta \in \mathbb {R} }$ is called the inverse temperature and the partition function ${\displaystyle Z}$ is defined as

${\displaystyle Z=\sum _{\tau \in \{-1,+1\}^{V}}\exp \left(-\sum _{\{u,v\}\in E}\beta \tau (u)\tau (v)\right).}$

Hence, ${\displaystyle \mu }$ is a joint distribution of ${\displaystyle |V|}$ random variables and each variable ${\displaystyle v\in V}$ takes its value from ${\displaystyle \{-1,+1\}}$.

Let ${\displaystyle \sigma \in \{-1,+1\}^{V}}$ and ${\displaystyle v\in V}$. Let ${\displaystyle \mu _{v}(\cdot \mid \sigma (V\setminus \{v\}))}$ denote the marginal distribution on ${\displaystyle v}$ conditioning on the value of ${\displaystyle u}$ is fixed as ${\displaystyle \sigma (u)}$ for all ${\displaystyle u\neq v}$.

The Glauber dynamics for Ising model is defined as follows:

- initially, start from an arbitrary ${\displaystyle X\in \{-1,+1\}^{V}}$;
- in each step, pick a vertex ${\displaystyle v\in V}$ uniformly at random, and resample ${\displaystyle X(v)}$ according to the distribution ${\displaystyle \mu _{v}(\cdot \mid X(V\setminus \{v\}))}$.

Here are the problems.

- Calculate ${\displaystyle \mu _{v}(+1\mid \sigma (V\setminus \{v\}))}$ and ${\displaystyle \mu _{v}(-1\mid \sigma (V\setminus \{v\}))}$.

Here ${\displaystyle \mu _{v}(+1\mid \sigma (V\setminus \{v\}))}$ is the probability that ${\displaystyle v}$ takes the value +1 conditioning on the value of ${\displaystyle u}$ is fixed as ${\displaystyle \sigma (u)}$ for all ${\displaystyle u\neq v}$.

- Show that the Glauber dynamics for Ising model is irreducible, aperiodic and reversible with respect to ${\displaystyle \mu }$.

#### 回答



