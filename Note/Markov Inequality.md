如果$X$是只取非负值的随机变量，则对于任意$a>0$有$Pr[X \ge a]\le\frac{EX}{a}$

在$X$是具有连续密度$f$的情况下的证明：

$\displaystyle EX=\int_0^\infty xf(x)dx\\=\int_0^a xf(x)dx+\int_a^\infty xf(x)dx \\\ge \int_a^\infty xf(x)dx \\ \ge \int_a^\infty af(x)dx \\=a\int_a^\infty f(x)dx \\=aPr[X\ge a] \\ \Rightarrow Pr[X\ge a]\le \frac{EX}{a}$