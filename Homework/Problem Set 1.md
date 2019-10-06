## Problem 1

Modify the Karger's Contraction algorithm so that it works for the *weighted min-cut problem*. Prove that the modified algorithm returns a weighted minimum cut with probability at least ${\displaystyle {\frac {2}{n(n-1)}}}$. The weighted min-cut problem is defined as follows.

- **Input**: an undirected weighted graph ${\displaystyle G(V,E)}$, where every edge ${\displaystyle e\in E}$ is associated with a positive real weight ${\displaystyle w_{e}}$;
- **Output**: a cut ${\displaystyle C}$ in ${\displaystyle G}$ such that ${\displaystyle \sum _{e\in C}w_{e}}$ is minimized.

#### 回答

**更新算法**

> while $|V|>2$ do
>
> ​	choose an edge $uv\in E$ uniformly at random;
>
> ​	$G=Contract(G,uv)$

原先每次是等概率地选取边，需要修改为每次按剩余边的权值所占比重来等概率选边。

假设当前$G=(V,E)$，边权和为$\displaystyle \sum _{e \in E}{w_e}$，则选中某一条边$e_1$的概率为$\displaystyle \frac {w_{e_1}} {\sum _{e \in E}{w_e}}$。

**证明**

设$P_{correct}$为算法得到最小割的概率，$P_C$为算法得到某一个特定最小割$C$的概率，显然$P_{correct} \geq P_C$。

设$e_1,e_2,...,e_{n-2}$为每一次压缩的边，则

$$P_C=Pr[得到C]\\=Pr[e_i \notin C, \forall i \in \{1,2,...,n-2\}]\\=\prod _{i=1}^{n-2} Pr[e_i \notin C \mid \forall j < i, e_j \notin C]$$

令$p_i=Pr[e_i \notin C \mid \forall j < i, e_j \notin C]$，表示在前$i-1$次压缩中没有$C$中的边被压缩的前提下，$e_i \notin C$的概率。

因为$C$是某一个最小割，所以$\sum _{e \in C}{w_e}$是所有割中最小的。

那么对于$E$中的任意一个点$v$来说，以$v$为顶点的所有边$\{vu,u是所有顶点为v的边的另一顶点\}$，记为$U_v$，则$\sum _{e \in C}{w_e} \le \sum _{e \in U_v}{w_e}$，也就是最小割的边权之和小于等于以$v$为顶点的所有边的权值之和。

证明：假设存在一个点$v$满足$\sum _{e \in C}{w_e} > \sum _{e \in U_v}{w_e}$，那么就可以把$v$和其他所有点分开形成两个连通分量，此时的割比$C$小，矛盾。

由上可知，每一个点的边权之和有下界，即$C$的边权之和，从而整张图$G=(V,E)$的边权之和有下界，即$\sum _{e \in E}{w_e} \ge \frac {\mid V \mid \sum _{e \in C}{w_e}}{2}$，这个结论对于压缩过程中每一步产生的中间结果的图都成立。

证明：每个点最少有$\sum _{e \in C}{w_e}$的边权和，共有$\mid V \mid$个点，而每条边被计算两次，所以总权值之和至少为$\frac {\mid V \mid \sum _{e \in C}{w_e}}{2}$。

回到$p_i=Pr[e_i \notin C \mid \forall j < i, e_j \notin C]\\=1-Pr[e_i此时是最小割中的边]\\=1-\frac {\sum _{e \in C}{w_e}} {\sum _{e \in E_i}{w_e}}$

代入$\sum _{e \in E}{w_e} \ge \frac {\mid V \mid \sum _{e \in C}{w_e}}{2}$，则$p_i \geq 1-\frac {2} {\mid V_i \mid}=1-\frac {2}{n-i+1}$。

所以$P_{correct}=Pr[返回最小割]\\\geq Pr[返回特定最小割C]\\=Pr[e_i \notin C \mid \forall j < i, e_j \notin C]\\=\prod _{i=1}^{n-2} Pr[e_i \notin C \mid \forall j < i, e_j \notin C]\\\geq \prod _{i=1}^{n-2}{1-\frac {2}{n-i+1}}\\=\prod_{k=3}^{n}{\frac {k-2}{k}}\\=\frac{2}{n(n-1)}$

所以更新算法能够以最小$\frac{2}{n(n-1)}$的概率返回带权最小割。

## Problem 2

Let ${\displaystyle G=(V,E)}$ be a graph, where ${\displaystyle n=|V|}$ and ${\displaystyle m=|E|}$. In class, we generated a random cut ${\displaystyle \{S,T\}}$ by sampling ${\displaystyle X_{v}\in \{0,1\}}$ uniformly and independently for each ${\displaystyle v\in V}$ and constructing ${\displaystyle S=\{v\in V\mid X_{v}=1\}}$ and ${\displaystyle T=\{v\in V\mid X_{v}=0\}}$. Now, consider an alternative way to generate the random cut ${\displaystyle \{S,T\}}$. Suppose that ${\displaystyle n}$ is an even number. Define a collection of subset as

${\displaystyle {\mathcal {F}}=\{H\subseteq V:|H|=n/2\}}$.
We sample a random subset ${\displaystyle S\in {\mathcal {F}}}$ uniformly at random and construct ${\displaystyle T=V\setminus S}$.

- Give the expected size ${\displaystyle |E(S,T)|}$ of such random cut.

- Let ${\displaystyle {\mathcal {R}}(\cdot )}$ denote such a random source that given any ${\displaystyle 0\leq p\leq 1}$, ${\displaystyle {\mathcal {R}}(p)}$ returns an independent random sample ${\displaystyle X\in \{0,1\}}$ such that ${\displaystyle \Pr[X=1]=p}$. Give an algorithm that uses ${\displaystyle {\mathcal {R}}(\cdot )}$ as a subroutine to generate random subset ${\displaystyle S\in {\mathcal {F}}}$ uniformly at random. Prove the correctness of your algorithm. Analyze the number of times that the random sources is called by the algorithm.

