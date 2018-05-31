#### Dual Ascent 

Problem to solve:
$$
\begin{equation}
\mbox{minimize} \ \ f(x) \\
\mbox{subject  to} \ \ Ax=b  \tag{2.1}
\\x\ \in\ \mathbb{R}^{n} \ where \ A\  \in\  \mathbb{R}^{m\times n}\ and\ f:\mathbb{R}^{n} \rightarrow \mathbb{R}\ is\ convex
\end{equation}
$$


The Lagrangian for (2.1) is:
$$
L(x,y)=f(x)+y^{T}(Ax-b) 
$$
The dual function is:
$$
g(y) =\inf\limits_{x} L(x,y)=-f^{\ast}(-A^{T}y)-b^{T}y
$$
where $y$ is the dual variable or Lagrange multiplier, and the $f^*$ is the conjugate of the $f$. This function says taht $g(y)$ is convex of $y$.

 The definition of $f^{*}(y) $:
$$
f^{*}(y):\sup\limits_{x\in domf}:(y^{T}x-f(x))
$$
$\color{blue}{Proof}$:
$$
\begin{align}
g(y) &= \inf\limits_{x} L(x,y)=\inf\limits_{x}f(x) +y^{T}Ax-y^{T}b\\&=-\sup\limits_{x}-f(x)+y^{T}(-Ax)+y^{T}b\\&=-f^{*}(-A^{T}y)-y^{T}b
\end{align}
$$
Now, the dual problem is 
$$
\mbox{maximize} \ g(y)
$$
with variable $y\in \mathbb{R}^{m}$.

Assuming the strong duality holds. the optimal values of the primal and dual problems are the same.

The primal optimal point $x^{*}$ form a dual optimal point $y^{*}$ as 
$$
x^{*}=arg\min\limits_{x} L(x,y^{*}),
$$
provided that there is only one minimizer of $L(x,y^{*})$. 

The notation $\mbox{argmin}_{x}F(x)$ denotes any minimizer of $F$. 

In the $dual\ ascent\ method$, we use **greadient ascent** to solve dual problem. Assuming $g$ is differentiable. We first find $x^{+}=argmin_{x}L(x,y)$, then the gradient $\nabla g(y)=Ax^{+}-b$, which is the residual for the equality constraint. 
$$
\begin{align}
x^{k+1}&:=arg\min\limits_{x}L(x,y^{k})\tag{2.2}\\
y^{k+1}&:=y^{k}+\alpha^{k}(Ax^{k+1}-b),\tag{2.3}
\end{align}
$$
where $\alpha^{k}>0$ is a step size, the $k$ is the iteration counter. With appropriate choice of $\alpha^{k}$, $g(y^{k+1})>g(y^{k})$. 

The principle is $\max\limits_{y}g(y)=\max\limits_{x}L(x,y) $, optimizing x and y alternatively to reach $L(x^{*},y^{*})$. 

###### When $g$ is not differentiable 

The residual $Ax^{k+1}-b$ is not the gradient of $g$, but the negative of a subgradient of $-g$.  It is often that $g(y^{k+1})\ngtr g(y^{k})$. The algorithm is usually called the $dual\ subgradient\ method$. 

If $\alpha^{k}$ is chosen appropriately and several other assumptions hold, then $x^{k}$ converges to an optimal point and $y^{k}$ converges to an opotimal dual point. 

However, these assumptions *do not hold* in many cases. For example,  if $f$ is a nonzero affine function of any component of x, $L$ is unbounded below in $x$ for most $y$. 

#### Dual Decomposition 

The $\color{blue}{\mbox{major benefit}}$ of the dual ascent is that it can lead to a decentralized algorithm in some cases.

Suppose, $f$ is *separable*, meaning that
$$
f(x)=\sum_{i=1}^{N}f_{i}(x_i),
$$
where $x=(x_1,…,x_N)$ and the variables $x_i\in\mathbb{R}^{n_i}$ are subvectors of $x$. 

Partitioning the matrix $A$ conformably as 
$$
A=[A_1\cdot\cdot\cdot A_N],
$$
so $Ax=\sum_{i=1}^{N}A_ix_i$, the Lagrangian is 
$$
L(x,y )=\sum_{i=1}^{N}L_{i}(x_i,y)=\sum_{i=1}^{N}(f_{i}+y^TA_ix_i-(1/N)y^Tb)\\\mbox{such that } L(x,y)=f(x)+y^{T}(Ax-b)
$$
which is also separable in $x$. $\color{blue}{\mbox{The x-minimization step splits into N separate prolems that can be solved in parallel.}}$

Now, the algorithm is 
$$
\begin{align}
x^{k+1}_i&:=arg\min\limits_{x_i}L_i(x_i,y^k)\tag{2.4}\\
y^{k+1}&:=y^k+\alpha^{k}(Ax^{k+1}-b).\tag{2.5}
\end{align}
$$
In this case, we refer to the dual ascent mehtod as *dual decomposition*. Dual decomposition is used to do dual acent method for separable $f(x)$. Dual decomposition is distributed dual ascent method. 

###### Implementation

Each iteration of the dual decomposition methods inclued *broadcast* and *gather* operation.  First, $A_ix_i^{k+1}$ are collected(gathered). Second, compute the residual $Ax^{k+1}-b$.  Then, compute the (global) dual variable $y^{k+1}$. Finally, distributed (broadcast)  to the processors that carry out the $N$ individual $x_i$ minimization steps (2.4). 

#### Summary

Advantages: 

Disadvantages: