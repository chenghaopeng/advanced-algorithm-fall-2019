设$X=\sum_{i=1}^nX_i$，$X_1,\ldots,X_n$是独立随机变量且$a_i\le X_i\le b_i,\forall1\le i\le n$。令$\mu=E[X]$，则$Pr[|X-\mu|\ge t]\le 2exp(-\frac{2t^2}{\sum_{i=1}^n{(b_i-a_i)^2}})$



证明：

定义杜布鞅序列$Y_i=E[\sum_{j=1}^nX_j|X_1,\ldots,X_i],Y_0=\mu,Y_n=X$。

$|Y_i-Y_{i-1}|=|E[\sum_{j=1}^nX_j|X_0,\ldots,X_i]-E[\sum_{j=1}^nX_j|X_0,\ldots,X_{i-1}]|\\=|\sum_{j=1}^iX_j+\sum_{j=i+1}^n{E[X_j]}-\sum_{j=1}^{i-1}X_j-\sum_{j=i}^n{E[X_j]}|\\=|X_i-E[X_i]|\\\le b_i-a_i$

应用吾妻不等式，即证得原式。