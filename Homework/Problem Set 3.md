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



## Problem 2

Given ${\displaystyle m}$ subsets ${\displaystyle S_{1},S_{2},\ldots ,S_{m}\subseteq U}$ of a universe ${\displaystyle U}$ of size ${\displaystyle n}$, we want to find a ${\displaystyle C\subseteq \{1,2,\ldots ,{m}\}}$ of fixed size ${\displaystyle k=|C|}$ with the maximum **coverage** ${\displaystyle \left|\bigcup _{i\in C}S_{i}\right|}$.

- Give a poly-time greedy algorithm for the problem. Prove that the approximation ratio is ${\displaystyle 1-(1-1/k)^{k}>1-1/e}$.

#### 回答



## Problem 3

In the *maximum directed cut* (MAX-DICUT) problem, we are given as input a directed graph ${\displaystyle G(V,E)}$. The goal is to partition ${\displaystyle V}$ into disjoint ${\displaystyle S}$ and ${\displaystyle T}$ so that the number of edges in ${\displaystyle E(S,T)=\{(u,v)\in E\mid u\in S,v\in T\}}$ is maximized. The following is the integer program for MAX-DICUT:

${\displaystyle {\begin{aligned}{\text{maximize}}&&&\sum _{(u,v)\in E}y_{u,v}\\{\text{subject to}}&&y_{u,v}&\leq x_{u},&\forall (u,v)&\in E,\\&&y_{u,v}&\leq 1-x_{v},&\forall (u,v)&\in E,\\&&x_{v}&\in \{0,1\},&\forall v&\in V,\\&&y_{u,v}&\in \{0,1\},&\forall (u,v)&\in E.\end{aligned}}}$
Let ${\displaystyle x_{v}^{*},y_{u,v}^{*}}$ denote the optimal solution to the **LP-relaxation** of the above integer program.

- Apply the randomized rounding such that for every ${\displaystyle v\in V}$, ${\displaystyle {\hat {x}}_{v}=1}$ independently with probability ${\displaystyle x_{v}^{*}}$. Analyze the approximation ratio (between the expected size of the random cut and OPT).
- Apply another randomized rounding such that for every ${\displaystyle v\in V}$, ${\displaystyle {\hat {x}}_{v}=1}$ independently with probability ${\displaystyle 1/4+x_{v}^{*}/2}$. Analyze the approximation ratio for this algorithm.

#### 回答



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



## Problem 5

The following is the weighted version of set cover problem:

Given ${\displaystyle m}$ subsets ${\displaystyle S_{1},S_{2},\ldots ,S_{m}\subseteq U}$, where ${\displaystyle U}$ is a universe of size ${\displaystyle n=|U|}$, and each subset ${\displaystyle S_{i}}$ is assigned a positive weight ${\displaystyle w_{i}>0}$, the goal is to find a ${\displaystyle C\subseteq \{1,2,\ldots ,m\}}$ such that ${\displaystyle U=\bigcup _{i\in C}S_{i}}$ and the total weight ${\displaystyle \sum _{I\in C}w_{i}}$ is minimized.

- Give an integer program for the problem and its LP relaxation.
- Consider the following idea of randomized rounding: independently round each fractional value to ${\displaystyle \{0,1\}}$ with the probability of the fractional value itself; and repeatedly apply this process to the variables rounded to 0 in previous iterations until ${\displaystyle U}$ is fully covered. Show that this can return a set cover with ${\displaystyle O(\log n)}$ approximation ratio with probability at least ${\displaystyle 0.99}$.

#### 回答

