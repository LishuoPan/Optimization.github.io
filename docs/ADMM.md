###### 3.1 Algorithm

It is an algorithm intended to blend the decomposability of dual ascent with the superior convergence properties of the method of multipliers. 
$$
\begin{align}
\mbox{minimize} \ &f(x)+g(z) \tag{3.1} \\
\mbox{subject to} \ &Ax+Bz=c
\end{align}
$$
with variables $x\in\mathbb{R}^m $ and $z\in \mathbb{R}^m$, where $A\in \mathbb{R}^{p\times n},\ B\in{R}^{p\times m}$, and $c\in\mathbb{R}^p$. We assume $f$ and $g$ are convex. The difference from general linear equality-constrained problem (2.1) is $x$ has been split into two parts, called $x$ and $z$ here, with the objective functions **separable** across splitting. 

The optimal value of (3.1) denoted by
$$
p^*=\inf \{f(x)+g(z)|Ax+Bz=c\}.
$$
We form the **augmented Lagrangian** 
$$
L_0(x,z,y)=f(x)+g(z)+y^T(Ax+Bz-c)\\
L\rho(x,z,y)=f(x)+g(z)+y^T(Ax+Bz-c)+(\rho/2)\|Ax+Bz-c\|^2_2.
$$
The **iterations of ADMM** is 
$$
\begin{align}
x\mbox{-minimization step: }  x^{k+1}&:=arg\min_x L_\rho (x,z^k,y^k)  \tag{3.2}  \\
z\mbox{-minimization step: }z^{k+1}&:=arg\min_xL_\rho(x^{k+1},z,y^k) \tag{3.3}\\
\mbox{Dual variable update: }y^{k+1}&:=y^k+\rho(Ax^{k+1}+Bz^{k+1}-c)\tag{3.4}
\end{align}
$$
where $\rho>0$, $Ax+Bz-c$ is gradient. $\rho$ is the step size. Our target is to find $L(x^*,z^*,y^*)$. 

Different from (3.2), (3.3), (3,4), the following form is minimized **jointly** with respect to the two primal variables. The method of multipliers for (3.1) has the form
$$
\begin{align}
(x^{k+1},z^{k+1})&:=arg\min_{x,z}L_\rho(x,z,y^{k})\\
y^{k+1}&:=y^k+\rho(Ax^{k+1}+Bz{k+1}-c)
\end{align}
$$
**3.1.1 Scale Form**

ADMM can be written in a slightly different form, which is often more convevient. Defining the residual $r=Ax+Bz-c$, we have
$$
\begin{align}
y^Tr+(\rho/2)\|r\|^2_2 &=(\rho/2)\|r+(1/\rho)y\|^2_2-(1/2\rho)\|y\|^2_2\\
&=(\rho/2)\|r+u\|^2_2-(\rho/2)\|u\|^2_2,
\end{align}
$$
where $u=(1/\rho)y$ is the *scaled dual variable.* 

ADMM can be expressed as
$$
\begin{align}
x\mbox{-minimization step: }  x^{k+1}&:=arg\min_x (  f(x)+(\rho/2)\|Ax+Bz^k-c+u^k\|^2_2 )\tag{3.5}  \\
z\mbox{-minimization step: }z^{k+1}&:=arg\min_z (  g(z)+(\rho/2)\|Ax^{k+1}+Bz-c+u^k\|^2_2 )\tag{3.6}\\
\mbox{Dual variable update: }u^{k+1}&:=u^k+Ax^{k+1}+B^{k+1}-c.\tag{3.7}
\end{align}
$$


