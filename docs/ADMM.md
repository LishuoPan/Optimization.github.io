##### 3.1 Algorithm

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
The **iterations of ADMM** (unscaled form) is 
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
where $u=(1/\rho)y$ is the *scaled dual variable.* The **augmented Lagrangian** is
$$
L_\rho=f(x)+g(z)+(\rho/2)\|r+u\|^2_2-(\rho/2)\|u\|^2_2
$$
 It is the same as unscaled form.

$\color{blue}{Proof}$:
$$
\begin{align}
(\rho/2)\|r+u\|^2_2 &=(\rho/2)\|Ax+Bz-c+\frac{1}{\rho}y\|^2_2\\
&=(\rho/2)\left[\|Ax+Bz-c\|^2_2+(\rho/2)y^T(Ax+Bz-c)+\frac{1}{\rho^2}\|y\|^2_2\right]\\
&=(\rho/2)\|Ax+Bz-c\|^2_2+y^T(Ax+Bz-c)+(1/2\rho)\|y\|^2_2\\ \\ 
(\rho/2)\|u\|^2_2 &=(\rho/2)\times(1/\rho^2)\|y\|^2_2\\
&=\frac{1}{2\rho}\|y\|^2_2\
\end{align}
$$
**ADMM(scaled)**  can be expressed as
$$
\begin{align}
x\mbox{-minimization step: }  x^{k+1}&:=arg\min_x (  f(x)+(\rho/2)\|Ax+Bz^k-c+u^k\|^2_2 )\tag{3.5}  \\
z\mbox{-minimization step: }z^{k+1}&:=arg\min_z (  g(z)+(\rho/2)\|Ax^{k+1}+Bz-c+u^k\|^2_2 )\tag{3.6}\\
\mbox{Dual variable update: }u^{k+1}&:=u^k+Ax^{k+1}+B^{k+1}-c.\tag{3.7}
\end{align}
$$
Defining the residual at iteration $k$ as $r^k=Ax^k+Bz^k-c$, we see that 
$$
u^k=u^0+\sum_{j=1}^{k} r^j
$$
the running sum of the residuals. 

We use the unscaled form when we wish to emphasize the role of the dual variable or to give an interpretation thet relies on the (unscaled) dual variable. 

##### Convergence

**Assumpition 1**: The (extended-real-valued) funcitons $f$: $\mathbb{R}^n\rightarrow\mathbb{R}\cup \{+\infty\}$ and $g:\mathbb{R}^m\rightarrow\mathbb{R}\cup\{+\infty\}$ are close, proper, and convex.

The funciton satisfies as.1 if and only if its epigraph 
$$
\textbf{epi} \ f=\{(x,t)\in\mathbb{R}^n\times\mathbb{R}|f(x)\leq t\}
$$
is a closed nonempty convex set.

Assumption 1 allows $f$ and $g$ to be nondifferentiable and to assume the value $+\infty$. We can take $f$ to be **the indicator function** of a closed nonempty convex set $C$, 
$$
\begin{equation}  
f(x) = 
\left\{  
             \begin{array}{lr}  
             1,  \mbox{for } x\in C   \\ 
           +\infty,     \mbox{otherwise}
             \end{array}  
\right.  
\end{equation}
$$
In this case, the $x$-minimization step (3.2) will involve solving a constrained quadratic program over $C$, the effective domain of $f$. 

 **Assumption 2**: The unaugmented Lagrangian $L_0$ has a saddle point.

There exists $(x^*,z^*,y^*)$, not necessarily unique, for which
$$
L_0(x^*,z^*,y)\leq L_0(x^*,z^*,y^*)\leq L_0(x,z,y^*)
$$
holds for all $x,z,y$. 

$L_0(x^*,z^*,y^*)$ is finite for any saddle point $(x^*,z^*,y^*)$. This implies that $(x^*,z^*)$ is a solution to (3.1), so $Ax^*+Bz^*=c$ and $f(x^*)<\infty,g(z^*)<\infty$. It also implies that strong duality holds. 

**3.2.1 Convergence** 

* *Residual convergence.* $r^k \rightarrow0$ as $k \rightarrow\infty$. 

* *Objective convergence.*  $f(x^k )+g(z^k)\rightarrow p^*  \mbox{as}\  k\rightarrow\infty$. 

* *Dual variable convergence.* $y^k\rightarrow y^* \mbox{as}\ k\rightarrow \infty $, where $y^*$ is a dual optimal point. 

  Note that $x^k$ and $z^k$ need not converge to optimal values. 

  ​

**3.2.2 Convergence in Practice**

The general case ADMM will be practically useful mostly in cases when modest accuracy is sufficient. 

##### Optimality Conditions and Stopping Criterion

The necessary and sufficient optimality conditions for the ADMM problem (3.1) are primal feasibility,
$$
Ax^*+Bz^*-c=0 \tag{3.8}
$$
and dual feasibility,
$$
\begin{align}
0\in \partial f(x^*)+A^Ty^* \tag{3.9}\\
0\in \partial g(z^*)+B^Ty^* \tag{3.10}
\end{align}
$$
Here, $\partial$ denotes the *subdifferential operator*.  

Since $z^{k+1}$ minimizes $L_\rho (x^{k+1},z,y^k)$ by definition, we have
$$
\begin{align}
0&\in\partial g(z^{k+1})+B^Ty^k+\rho B^T(Ax^{k+1}+Bz^{k+1}-c)\\
&=\partial g(z^{k+1})+B^Ty^k+\rho B^Tr^{k+1}\\
&=\partial g(z^{k+1})+B^Ty^{k+1}
\end{align}
$$
This means that $z^{k+1}$ and $y^{k+1}$ always satisfy (3.10). Now we have to optimize (3.8) and (3.9). 

Since $x^{k+1}$ minimizes $L_\rho (x,z^{k},y^k)$ by definition, we have
$$
\begin{align}
0&\in\partial f(x^{k+1})+A^Ty^k+\rho A^T(Ax^{k+1}+Bz^{k}-c)\\
&=\partial f(z^{k+1})+A^T(y^k+\rho r^{k+1}+\rho B(z^k-z^{k+1}))\\
&=\partial f(z^{k+1})+A^Ty^{k+1} +\rho A^TB(z^k-z^{k+1})
\end{align}
$$
or equivalently,
$$
\rho A^TB(z^{k+1}-z^{k}) \in \partial f(x^{k+1})+A^Ty^{k+1}
$$
We define $s^{k+1} = \rho A^TB(z^{k+1}-z^{k}) $ as the *dual residual* at iteration $k+1$, and $r^{k+1}=Ax^{k+1}+Bz^{k+1}-c$ as the *primal residual* at iteration $k+1$. These two resuduals converge to zero as ADMM proceeds. The (3.10) always holds for $(x^{k+1},z^{k+1},y{k+1})$. 

**3.3.1 Stopping criteria**

