# Welcome to Optimization

It is a tutorial for optimization methods. 

## Dual Ascent

**Dual Ascent:** 
$$
L(x,y)=f(x)+y^{T}(Ax-b)
$$


**Dual Decomposition:** 
$$
L(x,y )=\sum_{i=1}^{N}L_{i}(x_i,y)=\sum_{i=1}^{N}(f_{i}+y^TA_ix_i-(1/N)y^Tb)\\\mbox{such that } L(x,y)=f(x)+y^{T}(Ax-b)
$$

## Augmented Lagrangians and the Method of Multipliers

$$
L_{\rho}(x,y)=f(x)+y^T(Ax-b)+(\rho/2)\|Ax-b\|^2_2
$$



## ADMM

$$
L\rho(x,z,y)=f(x)+g(z)+y^T(Ax+Bz-c)+(\rho/2)\|Ax+Bz-c\|^2_2.
$$

