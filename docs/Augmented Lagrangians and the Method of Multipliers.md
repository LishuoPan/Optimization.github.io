#### Augmented Lagrangians and the Method of Multipliers

Purpose: bring robustness to the dual ascent method, and in particular, to yield convergence without assumptions like strict convexity or fiteness of $f$. 

The *Augmented Lagrangians* is:
$$
L_p(x,y)=f(x)+y^T(Ax-b)+(\rho/2)\|Ax=b\|^2_2,
$$
where $\rho>0$ is called the *penalty parameter*. The augmented Lagrangian cna be viewed as the (unaugmented) Lagrangian asscociated with the problem
$$
\mbox{minimize} \ \ \ f(x)+(\rho/2)\|Ax=b\|^2_2\\  \mbox{subject to  } \ Ax=b \ \  \ \ \  \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \
$$
This part is highly related to proximal algorithm. 

​			
​		
​	