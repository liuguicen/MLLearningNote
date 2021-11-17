特征值分解：
对于实对称矩阵，可以做特征值分解，这在大学的线代里面讲过。也就是$ A=Q^T∧Q $
其中$Q,Q^T$为标准正交矩阵,即有$QQ^T$=I

特征值分解要求A实对称，对于其它类型不行，于是有了奇异值分解。

定义：对于一个m*n的实矩阵A，A可写作$A=UMV^T$的形式
其中$V，V^T$均为标准正交矩阵，即$UU^T = I, VV^T=I$
V成为左奇异矩阵，$V^T$称为右奇异矩阵
其中
$$
M = 
\left[
\begin{array}{}
δ_1    & 0      &\cdots    & 0    & \cdots  & 0 \\
0      & δ_2    &\cdots    & 0    & \cdots  & 0 \\
\vdots &        & \ddots   & 0    & \cdots  & 0 \\
0      & \cdots &          & δ_m  & \cdots & 0 \\
\end{array}   
\right]_{m*n}
$$

M可称为长方形对角矩阵
M对角线上元素称为A的奇异值。

step1 构造$A^TA$，它n*n,且实对称，这个显然

然后根据特征值分解理论，对$A^TA$进行特征值分解，$A^TA = VDV^T$， 可以得到一组标准正交基$ v = \{v_1,v_2, \cdots, v_n\}$, 自然的有$(A^TA)v_i = λ_iv_i$
  
$ $
step2 构造 $(Av_i)^T(Av_j) = v_i^TA^TAv_j = v_i^Tλ_jv_j =  λ_jv_i^Tv_j$
因为V= $\{v_1,v_2, \cdots, v_n\}$是标准正交基，如果i≠j，那么$λ_jv_i^Tv_j = 0 $
$如果i = j，那么λ_jv_i^Tv_j = λ_j$ 

step3 
$A^TA 不一定可逆，它的秩r(A^TA) = r, V中存在r个正交向量满足A^TAv_i≠0, 此时显然Av_i≠0 $
$再根据step2结论，故一定存在一组正交基 (Av_1,Av_2,\cdots,Av_r),
对于r个之外的向量A^TAv_i = 0，Av_i不一定不为0，所以不考虑$

$ $
step4
对$Av_i单位化，用δ_iu_i表示，由step2，Av_i的模，|Av_i|^2 =  λ_i, |Av_i|= sqrt(λ_i) = δ_i$
$u_i为Av_i的单位向量，也就是u_i = \frac{Av_i}{|Av_i|} = \frac{Av_i}{\sqrtλ_i}$

最后得到$Av_i = \sqrtλ_i u_i （就是向量的模乘以单位方向)= δ_iu_i$ 其中 $δ_i = \sqrt{λ_i}$

step 5 
利用扩展基定理，将$\{u_1,u_2,\cdots,u_r\}$扩展为n个R^m中的标准正交基，扩展的过程中u_i的维度由n变成了m，这里不明白，直觉上可以这样操作，就是r不大于n或者m，把低维维空间的单位正交向量放到高维空间没问题？注意r≤m
于是有$$AV = A(v_1,\cdots, v_r,\cdots, v_m, 0, \cdots, v_n) \\ 
= (Av_1, \cdots, Av_r,\cdots,Av_m, A0, \cdots,A0)\\
= (δ_1u_1, \cdots, δ_ru_r, 0u_{r+1}, \cdots, 0u_m， \cdots, 0)\\
= \left[
\begin{array}{}
u_1&
u_2&
\cdots&
u_m
\end{array}   
\right]_{m*m} 
\left[
\begin{array}{}
δ_1    &        &       &        \\
       & \ddots &       &        \\
       &        & δ_r   &\cdots  \\ 
\end{array}   
\right]_{m*n} \\
=UM $$
故，$A = AVV^T = UMV^T$

总结：
首先，理解基本的特征值分解概念
step1，构造A^TA
step2，构造$(Av_i)^TAv_J，求值
step3, 证明r个正交向量，$(Av_1,...,Av_r),秩
step4，单位化Avi为ui，并将u扩展到n维
最后，转换AV = UM，得出A = UMV^T


性质： 奇异值可以看做一个矩阵的代表值，当奇异值越大是，它代表的信息越多
应用，
1、图像压缩，取前面若干个大的奇异值，可以基本还原出图像本身，很多情况下，前10%甚至1%的奇异值信息量就占了信息量的99%以上了。
2、PCA
3、隐形语义分析

资料：
https://blog.csdn.net/zhongkejingwang/article/details/43053513
https://zhuanlan.zhihu.com/p/110805571