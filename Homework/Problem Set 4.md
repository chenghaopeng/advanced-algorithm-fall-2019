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



## Problem 2

Given an undirected graph ${\displaystyle G(V,E)}$ with maximum degree ${\displaystyle \Delta }$, where the vertex set ${\displaystyle V}$ is partitioned into ${\displaystyle r}$ disjoint subsets, i.e., ${\displaystyle V=S_{1}\cup S_{2}\cup \cdots \cup S_{r}}$ with ${\displaystyle S_{i}\cap S_{j}=\varnothing }$ for all ${\displaystyle i\neq j}$. We call a vertex set ${\displaystyle T}$ is a transversal of the partition ${\displaystyle \{S_{1},S_{2},\cdots ,S_{r}\}}$, if ${\displaystyle |T\cap S_{i}|=1}$ for all ${\displaystyle 1\leq i\leq r}$. Assume that ${\displaystyle |S_{i}|\geq 2e\Delta }$ for all ${\displaystyle 1\leq i\leq r}$.

1. Prove that there must be an independent transversal (a transversal which is also an independent set) of ${\displaystyle \{S_{1},S_{2},\cdots ,S_{r}\}}$.

**Hint**: Lovász Local Lemma.

2. Design a randomized algorithm that finds an independent transversal of ${\displaystyle \{S_{1},S_{2},\cdots ,S_{r}\}}$ in expected polynomial time.

#### 回答



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



