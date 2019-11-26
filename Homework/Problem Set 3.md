成浩鹏 181250020

---

## Problem 1

Let ${\displaystyle G(V,E)}$ be an undirected graph with positive edge weights ${\displaystyle w:E\to \mathbb {Z} ^{+}}$. Given a partition of ${\displaystyle V}$ into ${\displaystyle k}$ disjoint subsets ${\displaystyle S_{1},S_{2},\ldots ,S_{k}}$, we define

${\displaystyle w(S_{1},S_{2},\ldots ,S_{k})=\sum _{uv\in E \atop \exists i\neq j:u\in S_{i},v\in S_{j}}w(uv)}$
as the cost of the **${\displaystyle k}$-cut** ${\displaystyle \{S_{1},S_{2},\ldots ,S_{k}\}}$. Our goal is to find a ${\displaystyle k}$-cut with maximum cost.

1. Give a poly-time greedy algorithm for finding the weighted max ${\displaystyle k}$-cut. Prove that the approximation ratio is ${\displaystyle (1-1/k)}$.
2. Consider the following local search algorithm for the weighted max cut (max 2-cut).
   Fill in the blank parenthesis. Give an analysis of the running time of the algorithm. And prove that the approximation ratio is 0.5.

> start with an arbitrary bipartition of ${\displaystyle V}$ into disjoint ${\displaystyle S_{0},S_{1}}$;
> while (true) do
>    if ${\displaystyle \exists i\in \{0,1\}}$ and ${\displaystyle v\in S_{i}}$ such that (          )
>       then ${\displaystyle v}$ leaves ${\displaystyle S_{i}}$ and joins ${\displaystyle S_{1-i}}$;
>       continue;
>    end if
>    break;
> end

#### 回答

1. 算法

   > 初始一个点的集合的集合$T=\{\{v_1\},\{v_2\},\ldots,\{v_{\mid V\mid}\}\}$
   >
   > 当$\mid T\mid>k$执行：
   >
   > ​	选择$S_i,S_j\in T$，使得$S_i$中的点与$S_j$中的点之间的边权之和，在所有可能的选择中最小
   >
   > ​	$T=T-S_i-S_j+S_i\cup S_j$，从T中删去$S_i$和$S_j$，再加入$S_i\cup S_j$
   >
   > 返回$w(T)$即为所求

   设$SOL_i$为$\mid T\mid=i$时，$T$中元素之间的距离之和，则$SOL_n=\sum_{uv\in E} w(uv)\ge OPT$。
   
   当$\mid T\mid=i+1$时，图$T$中有$C_{i+1}^2$条边，其中可能包含权为$0$的边，那么边的平均权值为$\overline{w_i}=\frac{1}{C_{i+1}^2}SOL_{i+1}$，则必然存在一条边的权小于等于$\overline{w_i}$，则$SOL_i\ge SOL_{i+1}-\overline{w_i}=(1-\frac{1}{C_{i+1}^2})SOL_{i+1}$，迭代可得$SOL_k\ge \overline{w_i}*\prod_{i=k}^{n-1}{(1-\frac{2}{(i+1)i})}\ge\overline{w_i}*(1-2(\frac{1}{k}-\frac{1}{n}))$。
   
   所以$\alpha\ge\frac{SOL_k}{OPT}\ge\frac{\overline{w_i}*(1-2(\frac{1}{k}-\frac{1}{n}))}{\overline{w_i}}=1-2(\frac{1}{k}-\frac{1}{n})\approx1-\frac{1}{k}$。
   
2. **括号内填入**：$w(S_i,S_{1-i})<w(S_i-\{v\},S_{1-i}\cap\{v\})$

   **运行时间分析**：在while循环内，需要枚举最多$\mid V \mid$个点，每个点需要最多$\mid V\mid$的时间来计算$w(S_i,S_{1-i})$，所以运行时间为$O(\mid V\mid^2)$。然后每一次局部的调整，都说明$w(S_i,S_{1-i})$变大了，并且由于边权为非负整数，那么$w(S_i,S_{1-i})$最少是变化了$1$，所以$w(S_i,S_{1-i})$的变化次数最多能达到$\sum_{uv\in E}w(uv)$。所以总的时间复杂度为$O(\mid V\mid^2\sum_{uv\in E}w(uv))$。
   
   **近似比**：设$w(v)=\sum_{uv\in E,u\in S_{1-i}}w(uv)$，$\forall v\in V$，满足$w(v)\ge\frac{\sum_{uv\in E}w(uv)}{2}$（如果不满足，那么$v$就应该放到另一个集合）。则$w(S_i,S_{1-i})=\frac{\sum_{v\in V}{w(v)}}{2}\ge\frac{\sum_{v\in V}{\frac{\sum_{uv\in E}w(uv)}{2}}}{2}=\frac{2\sum_{uv\in E}{w(uv)}}{4}=\frac{\sum_{uv\in E}{w(uv)}}{2}\ge\frac{OPT}{2}$，所以$\alpha\ge\frac{1}{2}$。

## Problem 2

Given ${\displaystyle m}$ subsets ${\displaystyle S_{1},S_{2},\ldots ,S_{m}\subseteq U}$ of a universe ${\displaystyle U}$ of size ${\displaystyle n}$, we want to find a ${\displaystyle C\subseteq \{1,2,\ldots ,{m}\}}$ of fixed size ${\displaystyle k=|C|}$ with the maximum **coverage** ${\displaystyle \left|\bigcup _{i\in C}S_{i}\right|}$.

- Give a poly-time greedy algorithm for the problem. Prove that the approximation ratio is ${\displaystyle 1-(1-1/k)^{k}>1-1/e}$.

#### 回答

> 初始$C=\{\},A=\{1,2,\ldots,n\}$
>
> 循环$k$次：
>
> ​	选择$t\in A$，使得$\mid\displaystyle S_t\cup \bigcup_{i\in C}S_i\mid$在所有选择中最大
>
> ​	$A=A-\{t\},C=C\cup\{t\}$
>
> 返回$C$

设第$i$次，新覆盖了$a_i$个点，那么总共覆盖了$b_i=\sum_{j=1}^ia_j$个点，设最大的覆盖数为$OPT$，那么还剩下未覆盖数为$OPT-b_i$，那么在接下来的$k-i$次覆盖中最多还能覆盖$OPT-b_i$个点，那么存在第$i+1$次能够新覆盖$a_{i+1}\ge\frac{OPT-b_i}{k-i}>\frac{OPT-b_i}{k}$。由$b_{i+1}=b_i+a_{i+1}$得$OPT-b_{i+1}=OPT-b_i-a_{i+1}< OPT-b_i-\frac{OPT-b_i}{k}=(OPT-b_i)(1-\frac{1}{k})$，所以$OPT-b_k<(1-\frac{1}{k})^k(OPT-b_0)=(1-\frac{1}{k})^kOPT$，得$b_k>(1-(1-\frac{1}{k})^k)OPT$，所以$\alpha>1-(1-\frac{1}{k})^k>1-\frac{1}{e}$。

## Problem 3

In the *maximum directed cut* (MAX-DICUT) problem, we are given as input a directed graph ${\displaystyle G(V,E)}$. The goal is to partition ${\displaystyle V}$ into disjoint ${\displaystyle S}$ and ${\displaystyle T}$ so that the number of edges in ${\displaystyle E(S,T)=\{(u,v)\in E\mid u\in S,v\in T\}}$ is maximized. The following is the integer program for MAX-DICUT:

${\displaystyle {\begin{aligned}{\text{maximize}}&&&\sum _{(u,v)\in E}y_{u,v}\\{\text{subject to}}&&y_{u,v}&\leq x_{u},&\forall (u,v)&\in E,\\&&y_{u,v}&\leq 1-x_{v},&\forall (u,v)&\in E,\\&&x_{v}&\in \{0,1\},&\forall v&\in V,\\&&y_{u,v}&\in \{0,1\},&\forall (u,v)&\in E.\end{aligned}}}$
Let ${\displaystyle x_{v}^{*},y_{u,v}^{*}}$ denote the optimal solution to the **LP-relaxation** of the above integer program.

- Apply the randomized rounding such that for every ${\displaystyle v\in V}$, ${\displaystyle {\hat {x}}_{v}=1}$ independently with probability ${\displaystyle x_{v}^{*}}$. Analyze the approximation ratio (between the expected size of the random cut and OPT).
- Apply another randomized rounding such that for every ${\displaystyle v\in V}$, ${\displaystyle {\hat {x}}_{v}=1}$ independently with probability ${\displaystyle 1/4+x_{v}^{*}/2}$. Analyze the approximation ratio for this algorithm.

#### 回答

- $OPT\le OPT_{LP}=\sum_{(u,v)\in E}y^*_{u,v}$

  $Pr[(u,v)是割]=Pr[\hat x_u=1\ and\ \hat x_v=0]=x^*_u*(1-x^*_v)\ge (y^*_{u,v})^2$

  $\mathbb E[割数]\ge\sum_{(u,v)\in E}{(y^*_{u,v})^2}\ge\frac{(\sum_{(u,v)\in E}y^*_{u,v})^2}{\left|E\right|}\ge\frac{OPT^2}{\left|E\right|}$
  
- $Pr[(u,v)是割]=Pr[\hat x_u=1\ and\ \hat x_v=0]=(1/4+x^*_u/2)*(1-1/4-x^*_v/2)\\=\frac{1}{4}\left[ \frac{1}{4}+\frac{1}{2}(1-x^*_v+x^*_u)+x^*_u(1-x^*_v) \right]\\\ge\frac{1}{4}(y^*_{u,v}+\frac{1}{2})^2$

  $\mathbb E[割数]\ge\frac{1}{4}\sum_{(u,v)\in E}{(y^*_{u,v}+\frac{1}{2})^2}\\\ge\frac{1}{4}\frac{(\sum_{(u,v)\in E}(y^*_{u,v}+\frac{1}{2}))^2}{\left|E\right|}\\=\frac{1}{4}\frac{(\sum_{(u,v)\in E}y^*_{u,v}+\frac{1}{2}\left|E\right|)^2}{\left|E\right|}\\\ge\frac{1}{4}\frac{(OPT+\frac{1}{2}\left|E\right|)^2}{\left|E\right|}$

## Problem 4

Recall the MAX-SAT problem and its integer program:

${\displaystyle {\begin{aligned}{\text{maximize}}&&&\sum _{j=1}^{m}y_{j}\\{\text{subject to}}&&&\sum _{i\in S_{j}^{+}}x_{i}+\sum _{i\in S_{j}^{-}}(1-x_{i})\geq y_{j},&&1\leq j\leq m,\\&&&x_{i}\in \{0,1\},&&1\leq i\leq n,\\&&&y_{j}\in \{0,1\},&&1\leq j\leq m.\end{aligned}}}$
Recall that ${\displaystyle S_{j}^{+},S_{j}^{-}\subseteq \{1,2,\ldots ,n\}}$ are the respective sets of variables appearing positively and negatively in clause ${\displaystyle j}$.

Let ${\displaystyle x_{i}^{*},y_{j}^{*}}$ denote the optimal solution to the **LP-relaxation** of the above integer program. In our class we learnt that if ${\displaystyle {\hat {x}}_{i}}$ is round to 1 independently with probability ${\displaystyle x_{i}^{*}}$, we have approximation ratio ${\displaystyle 1-1/\mathrm {e} }$.

We consider a generalized rounding scheme such that every ${\displaystyle {\hat {x}}_{i}}$ is round to 1 independently with probability ${\displaystyle f(x_{i}^{*})}$ for some function ${\displaystyle f:[0,1]\to [0,1]}$ to be specified.

- Suppose ${\displaystyle f(x)}$ is an arbitrary function satisfying that ${\displaystyle 1-4^{-x}\leq f(x)\leq 4^{x-1}}$ for any ${\displaystyle x\in [0,1]}$. Show that with this rounding scheme, the approximation ratio (between the expected number of satisfied clauses and OPT) is at least ${\displaystyle 3/4}$.
- Derandomize this algorithm through conditional expectation and give a deterministic polynomial time algorithm with approximation ratio ${\displaystyle 3/4}$.
- Is it possible that for some more clever ${\displaystyle f}$ we can do better than this? Try to justify your argument.

#### 回答

- $Pr[满足C_j]=1-\prod_{i\in S_j^+}{(1-f(x^*_i))}\prod_{i\in S_j^-}{f(x_i^*)}\\\ge1-\prod_{i\in S_j^+}{(1-1+4^{-x_i^*})}\prod_{i\in S_j^-}{4^{x_i^*-1}}\\=1-4^{-\sum_{i\in S_j^+}{x_i^*}+\sum_{i\in S_j^-}{(x_i^*-1)}}\\\ge1-4^{-y_j^*}\\\ge\frac{3}{4}y^*_j$

  所以$E[满足的子句数]\ge\frac{3}{4}\sum_{j=1}^m{y_j^*}\ge\frac{3}{4}*OPT$

- >$i=1\to n$，循环n次
  >
  >​	选择$x_i\in\{0,1\}$，使得$E[满足的子句数|x_1,x_2,_\ldots,x_i]最大$

  设$OPT$为最多的满足的数量，$a_i$为确定$x_i$后新增的满足的子句数量，$b_i=E[满足的子句数|x_1,x_2,_\ldots,x_i]=\sum_{j=1}^ia_j$为已满足的子句数量，而$x_{i+1}\in\{0,1\}$至少能在剩下的$OPT-b_i$个子句中满足一半，也就是$a_{i+1}\ge\frac{OPT-b_i}{2}$。$b_{i+1}=b_i+a_{i+1}$则$OPT-b_{i+1}=OPT-b_i-a_{i+1}\le OPT-b_i-\frac{OPT-b_i}{2}=\frac{1}{2}(OPT-b_i)$，迭代得$OPT-b_n\le\frac{1}{2}^n(OPT-b_0)=\frac{1}{2}^nOPT$，所以$E[满足的子句数|x_1,x_2,_\ldots,x_n]=b_n\ge(1-\frac{1}{2}^n)OPT\ge\frac{3}{4}OPT$。

- 选择$1-k^{-x}\leq f(x)\leq k^{x-1}$

  $Pr[满足C_j]=1-\prod_{i\in S_j^+}{(1-f(x^*_i))}\prod_{i\in S_j^-}{f(x_i^*)}\\\ge1-\prod_{i\in S_j^+}{(1-1+k^{-x_i^*})}\prod_{i\in S_j^-}{k^{x_i^*-1}}\\=1-k^{-\sum_{i\in S_j^+}{x_i^*}+\sum_{i\in S_j^-}{(x_i^*-1)}}\\\ge1-k^{-y_j^*}\\\ge\frac{k-1}{k}y^*_j$

  所以$E[满足的子句数]\ge\frac{k-1}{k}\sum_{j=1}^m{y_j^*}\ge\frac{k-1}{k}*OPT$

  选择更大的$k$可以达到更好的近似比。

## Problem 5

The following is the weighted version of set cover problem:

Given ${\displaystyle m}$ subsets ${\displaystyle S_{1},S_{2},\ldots ,S_{m}\subseteq U}$, where ${\displaystyle U}$ is a universe of size ${\displaystyle n=|U|}$, and each subset ${\displaystyle S_{i}}$ is assigned a positive weight ${\displaystyle w_{i}>0}$, the goal is to find a ${\displaystyle C\subseteq \{1,2,\ldots ,m\}}$ such that ${\displaystyle U=\bigcup _{i\in C}S_{i}}$ and the total weight ${\displaystyle \sum _{I\in C}w_{i}}$ is minimized.

- Give an integer program for the problem and its LP relaxation.
- Consider the following idea of randomized rounding: independently round each fractional value to ${\displaystyle \{0,1\}}$ with the probability of the fractional value itself; and repeatedly apply this process to the variables rounded to 0 in previous iterations until ${\displaystyle U}$ is fully covered. Show that this can return a set cover with ${\displaystyle O(\log n)}$ approximation ratio with probability at least ${\displaystyle 0.99}$.

#### 回答

- **ILP**

  ${\displaystyle {\begin{aligned}{\text{minimize}}&&&\sum _{v\in V,x_v=1}w_v\\{\text{subject to}}&&&\sum_{v\in e}x_v\ge1,&&e\in E\\&&&x_v\in \{0,1\},&&v\in V\end{aligned}}}$

  **LP-relaxation**

  ${\displaystyle {\begin{aligned}{\text{minimize}}&&&\sum _{v\in V,x_v\ge\frac{1}{2}}w_v\\{\text{subject to}}&&&\sum_{v\in e}x_v\ge1,&&e\in E\\&&&x_v\in [0,1],&&v\in V\end{aligned}}}$

- 