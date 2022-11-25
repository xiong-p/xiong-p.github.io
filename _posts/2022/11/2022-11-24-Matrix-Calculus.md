---



layout: post



title: "Matrix Calculus"



subtitle: ""



author: "XJX"



header-img: "img/home-bg-art.jpg"



header-mask: 0.2



published: true



tags:



- Linear Algebra



---

# Matrix Calculus

## Definitions

### Gradient

$$f(x) : \mathbb{R}^n \to \mathbb{R}$$


$$
\nabla f(x) = \begin{pmatrix}
 \frac{\partial f(x)}{\partial x_1} \\
 \\
 \dots \\
 \\
 \frac{\partial f(x)}{\partial x_n}
\end{pmatrix}
$$

### Jacobian 

$$f(x): \mathbb{R}^n \to \mathbb{R}^m$$


$$
Df(x) = \begin{pmatrix}
\frac{\partial f_1}{\partial x_1} & \cdots & \frac{\partial f_1}{\partial x_n}\\
\cdot & & \cdot\\
\cdot & & \cdot\\
\frac{\partial f_m}{\partial x_1} & \cdots & \frac{\partial f_m}{\partial x_n}
\end{pmatrix}
$$

### Gradient Matrix

$$
\nabla f(x) = (\nabla f_1(x), \cdots, \nabla f_m(x)) = \left(Df(x)\right)^T
$$

## Differentiability

### $$f: \mathbb{R}^n \to \mathbb{R}$$

$$x \in \mathbb{R}^n, dx \in \mathbb{R}^n, df(x) \in \mathbb{R}$$


$$
d f(x) = \nabla f(x)^T dx
$$

### $$F: \mathbb{R}^n \to \mathbb{R}^m$$

$$x \in \mathbb{R}^n, dx \in \mathbb{R}^n, df(x) \in \mathbb{R}^m $$


$$
d F(x) = D F(x) dx = \nabla F(x) ^T dx
$$

## Rules

###### Composition

   $$f:\mathbb{R}^n \to \mathbb{R}^k, g: \mathbb{R}^k \to \mathbb{R}^m$$

   

$$
d f(g(x)) = \nabla f(g(x))^T dg(x) = \nabla f(g(x))^T \nabla g(x)^T dx \Rightarrow \nabla f(g(x)) = \nabla g(x) \nabla f(g(x))
$$

###### Product

$$
d[fg] = f \cdot d[g] + d[f] \cdot g
$$

###### Transpose

   $$
   d[x^T] = (d[x])^T
   $$

   

## Examples

###### $$f(x) = Ax$$

$$
df(x)=d[Ax] = A dx \\
\nabla f(x) = A^T
$$



###### $$f(x) = \|x\|^2$$

$$
\begin{align*}
	d \|x\|^2 &= d [x^T x] = x^T \cdot d[x] + d[x^T] \cdot x\\
	&= x^T \cdot d[x] + (d[x])^T \cdot x \\
	&= 2x^T \cdot d[x]\\
	\Downarrow
	\\
	\nabla f(x) &= 2x
\end{align*}
$$

###### $$f(x) = x^T A x$$

$$
\begin{align*}
d[x^T A x] &= x^T \cdot d[Ax] + d[x^T] \cdot Ax \\
&=x^T A dx + Ax \cdot (dx)^T \\
&=x^T A dx + (Ax)^T dx\\
&=x^T A dx + x^T A^T dx \\
&= x^T(A + A^T) dx\\
\\
\nabla f(x) &= (A + A^T) x
\end{align*}
$$

######$$f(x) = (x^Tx)x$$

$$
\begin{align*}
d f(x) &= d  (x^Tx)x = (x^T x) dx + d[x^Tx]\cdot x \\
&= (x^T x) dx + (2x^Tdx)x , \text{ since }x^T dx \text{ is a scalar}\\
&= (x^T x) dx + 2 x (x^T dx) \\
&= ((x^T x) \cdot I + 2xx^T) dx, 
\end{align*}
$$

Remark: typical trick in the last step to transform the scalar multiplication to matrix multiplication by introducing the indenttity matrix.



































