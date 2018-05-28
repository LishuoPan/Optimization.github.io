#### Dual Ascent 

Problem to solve:
$$
\mbox{minimize}  \ \ f(x) \\ \mbox{subject  to} \ \ Ax=b  \\x\ \in\ \mathbb{R}^{n} \ where \ A\  \in\  \mathbb{R}^{m\times n}\ and\ f:\mathbb{R}^{n} \rightarrow \mathbb{R}\ is\ convex
$$


The Lagrangian is:
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
$Proof$:
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

In the $dual\ ascent\ method$, we use **greadient ascent** to solve dual problem. Assuming $g$ is differentiable. We first find $x^{+}=argmin_{x}L(x,y)$, then $\nabla g(y)=Ax^{+}-b$, which is the residual for the equality constraint. 
$$
x^{k+1}:=arg\min\limits_{x}L(x,y^{k})\\
y^{k+1}:=y^{k}+\alpha^{k}(Ax^{k+1}-b),
$$
where $\alpha^{k}>0$ is a step size, the $k$ is the iteration counter. With appropriate choice of $\alpha^{k}$, $g(y^{k+1})>g(y^{k})$. 

