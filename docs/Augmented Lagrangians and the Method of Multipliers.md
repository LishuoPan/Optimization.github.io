##### 2.3 Augmented Lagrangians and the Method of Multipliers

Purpose: bring *robustness* to the dual ascent method, and in particular, to yield convergence without assumptions like strict convexity or finiteness of $f$. 

The *augmented Lagrangians* is:
$$
L_{\rho}(x,y)=f(x)+y^T(Ax-b)+(\rho/2)\|Ax-b\|^2_2,\tag{2.6}
$$
where $\rho>0$ is called the *penalty parameter*. We can view this problem as adding a norm2 penalty term to Lagrangian. It can also be viewed as the (unaugmented) Lagrangian asscociated with the problem
$$
\mbox{minimize} \ \ \ f(x)+(\rho/2)\|Ax=b\|^2_2\\  \mbox{subject to  } \ Ax=b \ \  \ \ \  \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \
$$
This part is highly related to proximal algorithm. The associated dual function is $g_p(y)=\inf_{x} L_{\rho}(x,y)$. 

The benefit of including the penalty term ($(\rho/2)\|Ax=b\|^2_2​$) is that $g_\rho​$	can be shown to be differentiable under rather mild conditions on the original problem. 

Applying the dual ascent to the modified problem:
$$
\begin{align}
x^{k+1}&:=arg\min\limits_{x}L_\rho(x,y^{k})\tag{2.7}\\
y^{k+1}&:=y^{k}+\rho(Ax^{k+1}-b),\tag{2.8}
\end{align}
$$
which is known as the *method of multipiers* for solving (2.1). The $x$-minimization step uses the augmented Lagrangian, and the penalty parameter $\rho$ is used as the step size $\alpha^k$, campared to standard dual ascent.  
$$
L(x^*,y^k) \ \& \  L(x^{k+1},y^*) \Longrightarrow \ L(x^*,y^*)
$$
The *method of multipiers* converges under far more general conditions than dual ascent, including cases when $f$ takes on the value $+\infty$ or is not strictly convex. 

For simplicity, we assume $f$ is differentiable, though this is not required for the algorithm to work. The optimality conditions for (2.1) are primal and dual feasibility, 
$$
Ax^*-b=0, \ \ \ \ \ \  \nabla f(x^*)+A^Ty^*=0 
$$
Since 
$$
\begin{align}
\nabla_xL_\rho &= \nabla_x(f(x)+y^T(Ax-b)+\frac{\rho}{2}\|Ax-b\|^2_2) \\&= \nabla_xf(x)+A^Ty+\rho A^TAx-\rho A^Tb\\&=\nabla_xf(x)+A^T(y+\rho(Ax-b))
\end{align}
$$
 By definition, $x^{k+1}$ minimizes $L_\rho(x,y^k)$, so 
$$
\begin{align}
0&=\nabla_xL_\rho(x^{k+1,y^k}) \\ 
&=\nabla_xf(x^{k+1})+A^T(y^k+\rho(Ax^{k+1}-b)) \\
&=\nabla_xf(x^{k+1})+A^Ty^{k+1}	\\
&\Rightarrow \nabla_xf(x^*)+A^Ty^*
\end{align}
$$
By using $\rho$ as the step size in the dual update, the iterate $(x^{k+1},y^{k+1})$ is dual feasible. The primal residual $Ax^{k+1}-b$ converges to zero as the method of multipliers proceeds, yielding optimality. 

When $f$ is separable, the augmented Lagrangian $L_\rho$ is not separable, so the $x$-minimization step (2.7) cannot be carried out separately in parallel for each $x_i$. This means that the basic methos of multipliers cannot be uesd for decomposition. 

#### Summary 

Advantages: Not strict with $f(x)$; good converge property

Disadvantages: distributed  

