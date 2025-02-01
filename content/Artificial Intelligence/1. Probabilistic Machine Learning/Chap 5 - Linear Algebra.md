# Linear Algebra
Linear algebra is the study of matrices and vectors.
### Introduction
#### Notation
###### Vectors
A vector $x \in \mathbb{R}^{n}$ is a list of n numbers, usually written as a column vector.

$$
x = \begin{bmatrix}
x_{1} \\
x_{2} \\
\vdots  \\
x_{n}
\end{bmatrix}
$$
unit vector $e_{i}$ is a vector of all 0's, except entry $i$, which has value 1:
$$
e_{i} = (0, \dots,0, 1, 0, \dots, 0) 
$$
This is also called a one-hot vector.

##### Matrices
A matrix $A \in \mathbb{R}^{m\times n}$ with m rows and $n$ columns is a 3d array of number arranged as follows:
$$
A = \begin{bmatrix}
a_{11}  & a_{12} & \dots & a_{1n} \\
a_{21} & a_{22} & \dots  & a_{2n} \\
\vdots  &  \vdots  & \vdots  \\
a_{m_{1}} & a_{m_{2}} & \dots  & a_{mn}
\end{bmatrix}
$$
If $m = n$ , the matrix is said to be square.

##### Tensors
A tensor (in machine learning terminology) is just a generalization of a 2d array to more than 2 dimensions.

The number of dimensions is known as the order or rank of the tensor.
We can reshape a matrix into a vector by stacking its columns on top of each other, as shown in Figure 7.1. This is denoted by $$vec(A) =[A:,1; · · · ; A:,n] ∈ R mn×1$$
#### Vector spaces
##### Vector addition and scaling
We can view a vector $x \in \mathbb{R}^{n}$ as defining a point in n-dimensional Euclidean space. A **vector space** is a collection of such vectors, which can be added together, and scaled by scalars in order to create new points.
##### Linear independence, spans and basis sets
A set of vectors $\{x_{1},x_{2},\dots,x_{n}\}$ is said to be (linearly independent), if no vector can be represented as a linear combination of the remaining vectors.
Conversely, a vector which can be represented as a linear combination of the remaining vectors is said to be (linearly) dependent.

The **span** of a set of vectors $\{x_{1},x_{2},\dots,x_{n}\}$ is the set of all vectors that can be expressed as a linear combination of $\{x_{1}, \dots, x_{n}\}$ That is,
$$
\text{span} (\{x_{1}, \dots, x_{n}\}) \triangleq \big\{v : v = \sum_{i=1}^{n} \alpha _{i}x_{i}, \alpha_{i} \in \mathbb{R} \big\}
$$
##### Linear maps & matrices
A **Linear map** or **linear transformation** is any function $f:\mathcal{V} \to \mathcal{W}$ such that $f(v+w) = f(v) +f(w)$ and $f(a \space v) = a \space f(v)$ for all $v,w \in \mathcal{V}$. 

##### Range & Nullspace of a matrix
The range (sometimes also called the column space) of this matrix is the span of the columns of $A$. In other words.
$$
range(A) \triangleq \{v \in \mathbb{R}^{m} : v = Ax, x \in \mathbb{R}^{n}\}
$$

The nullspace of a matrix $A \in \mathbb{R}^{m\times n}$ is the set of all vectors that get mapped to the null vector when multiplied by A.
$$
\text{nullspace}(A) \triangleq \{x \in \mathbb{R}^{n} : Ax = 0\}
$$
##### Linear projection
The **projection** of a vector $y \in \mathbb{R}^{m}$  onto the span of $\{x_1, \dots, x_n\}$ (here we assume $x_{i} \in \mathbb{R}^{m}$ ) is the vector $v ∈ span$ ($\{x_1, \dots, x_n\}$), such that $v$ is as close as possible to $y$, as measured by the Euclidean norm $∥v − y∥_2$. We denote the projection as $\text{Proj}(y; {x1, . . . , xn})$ and can define it formally as
$$
\text{Proj}(y; \{x_{1}, \dots, x_{n}\}) = argmin_{v \in span({x_{1}, \dots, x_{n}})} ||y- v||_{2}
$$
#### Norms of a vector and matrix
Measuring the size of a vector and matrix.
##### Vector norms
A norm of a vector $||x||$ is, informally, a measure of the length of the vector. More formally , a norm is any function $f: \mathbb{R}^{n}\to \mathbb{R}$ that satisfies 4 properties :
- For all $x \in \mathbb{R}^{n}$ , $f(x)\geq 0$ (non-negativity)
- $f(x)=0$ if and only if $x=0$ (definiteness)
- For all $x \in \mathbb{R}^{n}$ , $t\in \mathbb{R}$, $f(tx) = |t|f(x)$ (absolute value homogeneity)
- For all $x, y \in \mathbb{R}^{n}$ , for $f(x+y)\leq f(x)+ f(y)$ (triangle inequality)
##### Matrix norms
Suppose we think of a matrix $A \in \mathbb{R}^{m\times n}$ as defining a linear function $f(x) = Ax$. We define the induced norm of $A$ as the maximum amount by which $f$ can lengthen any unit-norm input:
$$
||A||_{p} = \underset {x \neq 0} {\max} \frac{||Ax||_{p}}{||x||_{p}} = \underset {||x||= 1}{\max} ||Ax||_{p}
$$

#### Properties of a matrix
##### Trace of a square matrix
The trace of a square matrix $A \in \mathbb{R}^{n\times n}$ denoted by $\text{tr}(A)$ , is the sum of diagonal elements in the matrix :
$$
\text{tr}(A) \triangleq \sum_{i=1}^{n} A_{ii}
$$
it has the following properties, where $c \in \mathbb{R}$ is a scalar, and $A, B \in \mathbb{R}^{n\times n}$ are square matrices :
$$
\begin{align}
\text{tr}(A) &= \text{tr}(A^{T}) \\
\text{tr}(A+B) &= \text{tr}(A) + \text{tr}(B) \\
\text{tr}(cA) &= c\text{tr}(A) \\
\text{tr}(AB) &= \text{tr}(BA) \\
\text{tr}(A) &= \sum_{i=1}^{n} \lambda_{i} &  \text{where } \lambda_{i}\text{ are the eigenvalues of A}
\end{align}
$$
We also have the following important **cyclic permutation property**: For A, B, C such that ABC is square, 
$$
tr(ABC) = tr(BCA) = tr(CAB)
$$
##### Determinant of a square matrix
The determinant of a square matrix, denoted det(A) or |A|, is a measure of how much it changes a unit volume when viewed as a linear transformation.

The determinant operator satisfies these properties, where $A, B \in \mathbb{R}^{n \times n}$
$$
\begin{align}
|A| &= |A^{T}| \\
|cA| &= c^{n}|A| \\
|AB| &= |A||B| \\
|A| &= 0  & \text{iff A is singular} \\
|A^{-1}| &= \frac{1}{|A|} & \text{if  A is not singular}  \\
|A| &= \prod_{i=1}^{n} \lambda & \text{where }\lambda \text{ are the eigen values}
\end{align}
$$

##### Rank of a matrix
The column rank of a matrix A is the dimension of the space spanned by its columns, and the row rank is the dimension of the space spanned by its rows.
It is denoted by $rank(A)$ .
Properties :
- For $A ∈ \mathbb{R}^{m×n}$, $rank(A) ≤ min(m, n)$. If $rank(A) = min(m, n)$, then $A$ is said to be full rank, otherwise it is called rank deficient. 
- For $A ∈ \mathbb{R}^{m×n}$, $rank(A) = rank(A^{T}) = rank(A^{T}A) = rank(AA^{T})$. 
- For $A ∈ \mathbb{R}^{m×n}, B ∈ \mathbb{R}^{n\times p}$ , $rank(AB) ≤ min(rank(A),rank(B))$.
- For $A, B ∈ \mathbb{R}^{m×n}$, $rank(A + B) ≤ rank(A) + rank(B)$
##### Condition numbers
The condition number of a matrix A is a measure of how numerically stable any computations involving A will be. It is defined as follows:
$$
\mathcal{K} (A)  \triangleq ||A|| \cdot ||A^{-1}||
$$
where $||A||$ is the norm of the matrix. 
#### Special types of matrices
##### Diagonal matrix
A diagonal matrix is a matrix where all non-diagonal elements are 0. This is typically denoted by $D = \text{diag}(d_{1},d_{2},\dots,d_{n})$ with
$$
D = \left(\begin{array}{cc}
d_{1} & & & \\
& d_{2} & & \\
& & \dots &  \\
& & & d_{n}
\end{array}\right)
$$
The **identity matrix**, denoted by $I \in \mathbb{R}^{n\times n}$ is a square matrix with ones on the diagonal and zeros everywhere else, $I =\text{diag}(1,1,\dots,1)$. It has the property that for all $A \in \mathbb{R}^{n\times n}$,
$AI = A = IA$

A **block diagonal matrix** is one which contains matrices on its main diagonal, an is 0 everywhere else.

A **band-diagonal matrix** only has non-zero entries along the diagonal, and k side of the diagonal, where $k$ is the bandwidth.
##### Triangular matrices

An upper triangular matrix only has non-zero entries on and above the diagonal. A triangular matrix only has non-zero entries on and below the diagonal.
Triangular matrices have the useful property that the diagonal entries of A are the eigenvalues of A, and hence the determinant is the product of diagonal entries: $\det(A)= \prod_{i}A_{ii}$.
##### Positive definite matrices

##### Orthogonal matrices
Two vectors $x,y \in \mathbb{R}^{n}$ are orthogonal if $x^{T}y=0$, A vector $x \in \mathbb{R}^{n}$ is normalized if $||x||_{2}=1$. 
A set of vectors that is pairwise orthogonal and normalized is called orthonormal.
A square matrix $U \in \mathbb{R}^{n\times n}$ is orthogonal if all its columns are orthonormal.
### Matrix multiplication
The product of two matrices $A \in \mathbb{R}^{m\times n}$ and $B \in \mathbb{R}^{n\times p}$ is the matrix 
$$
C = AB\in \mathbb{R}^{m\times p}
$$
where 
$$
C_{ij} = \sum_{k=1}^{n} A_{ik}B_{kj} 
$$
Note that in order for the matrix product to exist, the number of columns in $A$ must equal the number of rows in $B$. Matrix multiplication generally takes $O(mnp)$ time.
###### Properties
- Associative : $(AB)C = A(BC)$
- Distributive : $A(B+C) = AB+AC$
- Not commutative :  $AB \neq BA$
#### Vector-vector products
Given two vectors $x,y \in \mathbb{R}^{n}$ the quantity $x^{T}y$ called the inner product, dot product or scalar product of the vectors, is real number given by 
$$
\langle x,y \rangle \triangleq x^{T}y = \sum_{i=1}^{n} x_{i}y_{i}
$$
Note that it is always the case that $x^{T}y = y^{T}x$.

Given vector $x \in \mathbb{R}^{m}, y\in \mathbb{R}^{n}$ , $xy^{T}$ is called the outer product of the vectors. It is a matrix whose entries are given by $(xy^{T})_{ij} =x_{i}y_{i}$
$$
xy^{T} \in \mathbb{R}^{m\times n} = \begin{bmatrix}
x_{1}y_{1} & x_{1}y_{2} & \dots & x_{1}y_{n} \\
x_{2}y_{1} & x_{2}y_{2} & \dots & x_{2}y_{n}  \\
\vdots & \vdots & \vdots & \vdots \\
x_{m}y_{1} & x_{m}y_{2} & \dots & x_{m}y_{n}
\end{bmatrix}
$$
#### Matrix-vector products
Given a matrix $A \in \mathbb{R}^{m\times n}$ and a vector $x \in \mathbb{R}^{n}$ m their product is a vector $y= Ax \in \mathbb{R}^{m}$.  If we write $A$ by rows and then we can express $y= Ax$ as follows
$$
y= Ax = \begin{bmatrix}
- & a_{1}^{T} & - \\
- & a_{2}^{T} & - \\
& \vdots & -  \\
- & a_{m}^{T} & - 
\end{bmatrix}

\qquad
x = \begin{bmatrix}
a_{1}^{T}x \\
a_{2}^{T}x  \\
\dots \\
a_{m}^{T}x \\

\end{bmatrix}
$$
In other words, the $i$th entry of $y$ is equal to the inner product of the $i$th row of $A$ and $x$, $y_{i}=a_{i}^{T}x$ 
Alternatively 

$$
y = Ax = \begin{bmatrix}
| & | & \quad & | \\
a_{1} & a_{2} & \dots & a_{n} \\
| & | & \quad & |
\end{bmatrix}
\begin{bmatrix}
x_{1} \\
x_{2} \\
\dots \\
x_{n}
\end{bmatrix}

= \begin{bmatrix}
| \\
a_{1} \\
|
\end{bmatrix} x_{1} + \begin{bmatrix}
| \\
a_{1} \\
|
\end{bmatrix} x_{2}
+ \dots + \begin{bmatrix}
| \\
a_{n} \\
|
\end{bmatrix} x_{n}
$$
In other words, $y$ is the linear combination of the columns of $A$, where the coefficients of the linear combination are given by the entries of $x$. We can view the columns of A as a set of basis vectors defining a linear subspace.
#### Matrix-matrix products
Matrix multiplication is that $i$, $j$ entry of $C$ is equal to the inner product of the $i$th row of $A$ and the $j$th column of $B$. 

$$
C = AB = \begin{bmatrix}
- & a_{1}^{T} & - \\
- & a_{2}^{T} & - \\
& \vdots &  \\
- & a_{m}^{T} - 
\end{bmatrix}

\begin{bmatrix}
| & | & \quad | \\
b_{1} & b_{2} & \dots & b_{p} \\
| & | & \quad | 
\end{bmatrix}
= \begin{bmatrix}
a_{1}^{T}b_{1} & a_{1}^{T}b_{2} & \dots & a_{1}^{T}b_{p} \\
a_{2}^{T}b_{1} & a_{2}^{T}b_{2} & \dots & a_{2}^{T}b_{p} \\
\vdots & \vdots &  \vdots & \vdots  \\
a_{m}^{T}b_{1} & a_{m}^{T}b_{2} & \dots & a_{m}^{T}b_{p}
 \end{bmatrix}
$$


![[matrix multiplication.png]]
### Matrix inversion

The inverse of a square matrix $A\in \mathbb{R}^{n\times n}$ is denoted by $A^{-1}$ and is the unique matrix such that 
$$
A^{-1} A = I = A A^{-1}
$$
$A^{-1}$ exists if and only if $\det(A) \neq {0}$ . If $\det(A) = 0$, it is called a singular matrix.
The following are properties of the inverse; all assume that $A,B \in \mathbb{R}^{n\times n}$ are non-singular:
$$
\begin{align}
& (A^{-1})^{-1} = A \\
& (AB)^{-1} = B^{-1}A^{-1} \\
& (A^{-1})^{T} = (A^{T})^{-1} \triangleq A^{-T}
\end{align}
$$
For a case of a $2\times 2$ matrix, the expression for $A^{-1}$ is simple enough to give explicitly. We have 
$$
A = \left(\begin{matrix}
a & b \\
c & d
\end{matrix}\right), \qquad A^{-1} = \frac{1}{|A|} \left( \begin{matrix}
d & -b \\
-c & a
\end{matrix}\right)
$$
For a block matrix
$$
\left (
\begin{matrix}
A & 0 \\
0 & B
\end{matrix}
\right)
^{-1} = \left(\begin{matrix}
A^{-1} & 0 \\
0 & B^{-1}
\end{matrix}\right)

$$
### Eigenvalue decomposition(EVD)
##### Basics
Given a square matrix $A \in \mathbb{R}^{n\times n}$ , we say that $\lambda \in \mathbb{R}$ is an eigenvalue of $A$ and $u\in \mathbb{R}^{n}$ is the corresponding eigenvector if 
$$
Au= \lambda u, \qquad\qquad u\neq 0
$$
Intuitively, this definition means that multiplying $A$ by the vector $u$ results in a new vector that points in the same direction as $u$ but is scaled by a factor $\lambda$ .
$$
A(cu) = cAu = c\lambda u = \lambda(cu)
$$
here $cu$ is also an eigen vector.
We can rewrite the equation above to state that $(\lambda, x)$ is an eigenvalue-eigenvector pair of $\mathbf{A}$ if 
$$
(\lambda \mathbf{I}- \mathbf{A})u = 0, u \neq 0
$$
###### Properties of eigenvalue and eigenvectors
- The trace of a matrix is equal to the sum of its eigenvalues
$$
	\mathrm{Tr}(\mathbf{A}) = \sum_{i=1}^{n} \lambda_{i}
$$
- The determinant of $\mathbf{A}$ is equal to the product of its eigenvalues
$$
	\det(\mathbf{A}) = \prod_{i=1}^{n} \lambda_{i}
$$

- The rank of $\mathbf{A}$ is equal to the number of non-zero eigenvalues of $\mathbf{A}$.
- If $\mathbf{A}$ is non-singular then $\frac{1}{\lambda_{i}}$ is an eigenvalue of $A^{-1}$ with associated eigenvector $u_{i}$. 
$$
	\mathbf{A}^{-1}u_{i} = \left( \frac{1}{\lambda_{i}} \right)u_{i}
$$
- The eigenvalues of a diagonal or triangular matrix are just the diagonal entries. 

##### Diagonalization
We can write all the eigenvector equations simultaneously as 
$$
\mathbf{AU = UΛ}
$$
where the columns of $\mathbf{U} \in \mathbb{R}^{n\times n}$ are the eigenvectors of $\mathbf{A}$ and $\mathbf{Λ}$ is a diagonal matrix whose entries are eigenvalues of $A,$
$$
\mathbf{U} \in \mathbb{R}^{n\times n} = \begin{bmatrix}
| & | & \qquad |  \\
u_{1} & u_{2} & \dots & u_{n} \\
| & | & \qquad | 
\end{bmatrix}, \mathbf{\Lambda} = \text{diag}(\lambda_{1},\dots, \lambda_{n})
$$
If the eigenvectors of $A$ are linearly independent, then the matrix $U$ will be invertible, so
$$
\mathbf{A = U \Lambda U^{-1}}
$$
A matrix that can be written in this form is called **diagonalizable**.

##### Eigenvalues and eigenvectors of symmetric matrices
When $\mathbf{A}$ is real and symmetric, it can be shown that all the eigen values are real, and the eigenvectors are orthonormal, i.e, $u_{i}^{T}u_{j} = 0$ if $i\neq j$ and $u_{i}^{T}u_{i }=1$ where $u_{i}$ are the eigenvectors. In matrix form this becomes $\mathbf{U^{T}U = UU^{T} = I}$ ; hence we $\mathbf{U}$ is an orthogonal matrix.
$$
\begin{align}
\mathbf{A = U\Lambda U^{T}} &= \left(\begin{matrix}
| & | & \qquad &|  \\
u_{1} & u_{2} & \dots & u_{n} \\
| & | & \qquad &| 
\end{matrix}\right) \left(\begin{matrix}
\lambda_{1} & & &  \\
& \lambda_{2} & & \\
& & \dots &  \\
&&& \lambda_{n}
\end{matrix}\right) \left(\begin{matrix}
- & u_{1}^{T} & - \\
- &u_{2}^{T} & -  \\
 & \vdots & \\
- & u_{n}^{T} & -
\end{matrix}\right) \\
& = \lambda_{1} \left(\begin{matrix}
| \\
u_{1} \\
| 
\end{matrix}\right) \left(\begin{matrix}
- & u_{1}^{T} & - 
\end{matrix}\right)  + \dots + \lambda_{n} \left(\begin{matrix}
|  \\
u_{n} \\
|
\end{matrix}\right) \left(\begin{matrix}
- & u_{n}^{T} & - 
\end{matrix}\right)  = \sum_{i=1}^{n} \lambda_{i}u_{i}u_{i}^{T}
\end{align}
$$
Thus multiplying by any symmetric matrix $\mathbf{A}$ can be interpreted as multiplying by a rotation matrix $\mathbf{U^{T}}$, a scaling matrix $\mathbf{A}$, followed by an inverse rotation $\mathbf{U}$.
This is corresponds to rotating, upscaling and then rotating back.
##### Geometry of quadratic forms
A quadratic form is a function that can be written as 
$$
f(x) = x^{T} \mathbf{A}x
$$
where $x \in \mathbb{R}^{n}$ and $\mathbf{A}$ is a positive definite, symmetric n-by-n matrix. Let $\mathbf{A = U \Lambda U^{T}}$ be a diagonalization of $\mathbf{A}$. Hence we can write
$$
f(x) = x^{T} \mathbf{A}x = x^{T} \mathbf{U\Lambda U}^{T}x = y^{\mathbf{T}} \mathbf{\Lambda }y = \sum_{i=1}^{n} \lambda_{i}y_{i}^{2}
$$
where $y_{i} = x^{\mathbf{T}}u_{i}$ and $\lambda_{i} > 0$ .
##### Power method
Power method is used to compute the eigenvector corresponding to the largest eigenvalue of a real, symmetric matrix. 

Let $\mathbf{A}$ be a matrix with orthonormal eigenvectors $u_{i}$ and eigenvalues $|\lambda_{1}| > |\lambda_{2}| \geq \dots \geq |\lambda_{m}|\geq 0$, so $\mathbf{A = U \Lambda U}^{T}$. Let $v_{(0)}$ be an arbitrary vector in the range of $\mathbf{A}$, so $\mathbf{A} v_{(0)}$ for some $x$. Hence we can write $v_{(0)}$ as
$$
v_{0} = \mathrm{U (\Lambda U^{T}x)} = a_{1}u_{1}+ \dots+ a_{m}u_{m} 
$$
for some constants $a_{i}$. We can now repeatedly multiply $v$ by $\mathrm{A}$ and renormalize :

##### Deflation
We can compute subsequent eigenvectors and values. Since the eigenvectors are orthonormal, and eigenvalues are real, we can project out the $u_{1}$ components from the matrix as follows : 
$$
A^{(2)} = ({I-u_{1}u_{1}^{T}}) \mathbf{A^{(1)}} = A^{(1)} - {u_{1}u_{1}^{T}A^{(1)}} = \mathbf{A^{(1)} } = \lambda_{1} {u_{1}u_{1}^{T}}
$$

This is called matrix **deflation**.
### Singular value decomposition(SVD)
Any (real) $m\times n$ matrix A can be decomposed as 
$$
\mathbf{A = USV}^{T} = \sigma \left( \begin{matrix}
| \\
u_{1} \\
|
\end{matrix}\right) \left(\begin{matrix}
- & v_{1}^{T} & -
\end{matrix} \right)
+ \dots + \sigma_{r} \left(\begin{matrix}
|  \\
u_{r} \\
|
\end{matrix}\right)

\left(\begin{matrix}
- v_{r}^{T} & -
\end{matrix}\right)
$$
where $\mathbf{U}$ is an $m\times n$ whose columns are orthonormal (so $\mathbf{U^{T}U = I_{m}}$), $\mathbf{V}$ is an $n\times n$ matrix whose row and columns are orthogonal (so $\mathbf{V^{T}V = VV^{T} = I_{m}}$) and $\mathbf{S}$ is an $m\times n$ matrix containing the $r= \min(m,n)$ singular values $\sigma_{i} \geq 0$ on the main diagonal, with 0s filling the rest of the matrix. The columns of U are the left singular vectors and the columns of V are the right singular vectors. This is called the **singular value decomposition** or **SVD** of the matrix.
##### Connection between SVD and EVD
##### Pseudo inverse
The **Moore-Penrose pseudo-inverse** of $A$, pseudo inverse denoted by $\mathbf{A}^{\dagger}$ , is defined as the unique matrix that satisfies the following 4 properties.
$$
\begin{align}
&\mathbf{AA^{\dagger}A} = A \\
&\mathbf{A^{\dagger}AA^{\dagger} = A^{\dagger}} \\
&\mathbf{(AA^{\dagger})^{T} = \mathbf{AA^{\dagger}}} \\
&\mathbf{(A^{\dagger}A)^{T} = A^{\dagger}A} 
\end{align}
$$


##### SVD and the range and nullspace of a matrix

$$
\textbf{A}x = \sum_{j:\sigma > 0} \sigma_{j}(v^{T}x)u_{j} = \sum_{j=1}^{r} \sigma_{j} (v^{T}x)u_{j}
$$
where $r$ is the rank of $A$. Thus any $Ax$ can be written as a linear combination of the left singular vectors $u_{1},\dots u_{r}$, so the range of $A$ is given by
$$
\text{range}(\textbf{A}) = \text{span}({u_{j}:\sigma_{j}>0})
$$
with dimension $r$.
To find a basis for the null space, let us now define a second vector $y\in \mathbb{R}^{n}$ that is a linear combination of right singular vectors for the zero singular values.

$$
y= \sum_{j:\sigma=0} c_{j}v_{j} = \sum_{j=r+1}^{n} c_{j}v_{j}  
$$
since the $vj$'s are orthonormal, we have
$$
\textbf{A}y= \textbf{U} \left( \begin{matrix}
\sigma_{1}v_{1}^{T}y \\
\vdots \\
\sigma_{r}v_{r}^{T}y \\
\sigma_{r+1} v_{r+1}^{T}y \\
\vdots \\
\sigma_{n}v_{n}^{T}y
\end{matrix} \right)
= \textbf{U} \left( \begin{matrix}
\sigma_{1}0 \\
\vdots \\
\sigma_{r}0 \\
0v^{T}_{r+1}y \\
\vdots \\
0v^{T}_{n}y
\end{matrix} \right)
 = \textbf{U0}
 = 0
$$
Hence the right singular vectors form an orthonormal basis for the null space:

$\text{nullspace}\textbf{A}=\text{span}(\{ v_{j}:\sigma=0 \})$

with dimension $n-r$. we see that
$$
\text{dim(range(\textbf{A}))} + \text{dim(nullspace(\textbf{A}))} = r+ (n-r) = n
$$
This is often written as
$$
\text{rank} + \text{nullity} = n
$$
This is called the **rank-nullity theorem**.
##### Truncated SVD
Let $\textbf{A=USV}^{T}$ be the SVD of $\textbf{A}$ and let $\hat{\textbf{A}}_{K} =U_{k}S_{k}V_{K}^{T}$, where we use the first $K$ columns of $\textbf{U}$ and $\textbf{V}$. 
If $K=r=\text{rank}(\textbf{A})$ there is not error introduced by this decomposition. But if $K<r$, we incur some error. This is called a **truncated SVD**.
### Other decompositions
##### LU factorization
We can factorize any square matrix $\textbf{A}$ into a product of a lower triangular matrix $\textbf{L}$ and an upper triangular matrix $\textbf{U}$
$$
\begin{bmatrix}
a_{11} & a_{12} & a_{13} \\
a_{21} & a_{22} & a_{23} \\
a_{31} & a_{32} & 1_{33}
\end{bmatrix}
= 
\begin{bmatrix}
l_{11} & 0 & 0 \\
l_{21} & l_{22} & 0 \\
l_{31} & l_{32} & l_{33}
\end{bmatrix}
\begin{bmatrix}
u_{11} & u_{12} & u_{13} \\
0 & u_{22} & u_{23} \\
0 & 0 & u_{33}
\end{bmatrix}
$$
In general we may need to permute the entries in the matrix before creating this decomposition. To see this, suppose $a_{11} = 0$. Since $a11 = l_{11}u_{11}$, this means either $l_{11}$ or $u_{11}$ or both must be zero, but that would imply $L$ or $U$ are singular. To avoid this, the first step of the algorithm can simply reorder the rows so that the first element is nonzero. This is repeated for subsequent steps. We can denote this process by 
$$
\textbf{PA = LU}
$$

where $\textbf{P}$ is a permutation matrix, i.e., a square binary matrix where $P_{ij}=1$ if row j gets permuted to row $i$. This is called **partial pivoting**.
##### QR decomposition
Suppose we have $\textbf{A}\in \mathbb{R}^{m\times n}$ representing a set of linearly independent basis vectors and we want to find a series of orthonormal vectors $q_{1}, q_{2}\dots$ that span the successive subspaces of $\text{span}(a_{1}),\text{span}(a_{1},a_{2}),$ etc. In other words we want to find vectors $q_{j}$ and coefficients $r_{ij}$ such that 
$$
\left(\begin{matrix}
| & | &\quad & | \\
a_{1} & a_{2} & \dots & a_{n} \\
| & | & \quad & |
\end{matrix}\right)
= 
\left(\begin{matrix}
| & | &\quad & | \\
q_{1} & q_{2} & \dots & q_{n} \\
| & | & \quad & |
\end{matrix}\right)

\left(\begin{matrix}
r_{11} & r_{12} & \dots & r_{1n} \\
& r_{22} & \dots & r_{2n} \\
& & \ddots & \\
&&& r_{nn}
\end{matrix}\right)
$$
We can write this 
$$
\begin{align}
a_{1} &= r_{11}q_{1}  \\ \\
a_{2} &= r_{12}q_{1} + r_{22}q_{2} \\
& \vdots \\
a_{n} &= r_{1n} q_{1} + \dots + r_{nn}q_{n}
\end{align}
$$
So we see $q_{1}$ spans the space of $a_{1}$ , and $q_{1}$ and $q_{2}$ span the space of $\{ a_{1},a_{2} \}$ 
In matrix notation we have
$\textbf{A} = \hat{\textbf{Q}} \hat{\textbf{R}}$
where $\hat{\textbf{Q}}$ is a $m\times n$ with orthonormal columns and $\hat{\textbf{R}}$ is $n\times n$ and upper triangular. This is called **reduced QR** or **economy QR factorization** of $\textbf{A}$.
##### Cholesky decomposition
Any symmetric positive definite matrix can be factorized as $\textbf{A= R}^{T}\textbf{R}$, where $\textbf{R}$ is upper triangular with real, positive diagonal elements. (This can also be written as $\textbf{A = LL}^{T}$, where $\textbf{L = R}^T$ is lower triangular.) This is called a **Cholesky factorization** or **matrix square root**. In NumPy, this is implemented by `np.linalg.cholesky`. The computational complexity of this operation is $O(V^3 )$, where $V$ is the number of variables, but can be less for sparse matrices.
### Solving systems of linear equations
An important application of linear algebra is the study of systems of linear equations. 
For example consider the following set of 3 equations :
$$
\begin{align}
3x_{1} + 2x_{2} - x_{3} &= 1 \\
2x_{1} - 2x_{2} + 4x_{3} &= -2 \\
-x_{1} + \frac{1}{2}x_{2} - x_{3} &= 0 \\
\end{align}
$$
We can represent this in matrix-vector form as follows:
$$
\textbf{Ax=b}
$$
where 
$$
A = \left( \begin{matrix}
3 &2  & -1  \\
2 & -2 & 4 \\
-1  & \frac{1}{2}  & -1
\end{matrix} \right), b= \left(\begin{matrix}
1  \\
-2 \\
0
\end{matrix}\right)
$$
The solution is $x= [1,-2,-2]$. 
In general if we have $m$ equations and $n$ unknowns, then $\textbf{A}$ will be a $m\times n$ matrix, and $b$ will be a $m\times {1}$ vector. If $m=n$ there is a single unique solution. If $m<n$ the system is underdetermined, so there is not a unique solution. If $m>n$, the system is overdetermined.
### Matrix calculus
##### Derivates
Consider a scalar-argument function $f:\mathbb{R}\to \mathbb{R}$. We define its derivate at a point $x$ to be the quantity
$$
f'(x) \triangleq \lim_{ h \to 0 } \frac{f(x+h)-f(x)}{h}
$$
assuming the limit exists. This measures how quickly the output changes when we move a small distance in input space away from x. 
The use of symbol $f'$ to denote the derivative is called **Lagrange notation**. The second derivate which measures how quickly the gradient is changing is denoted by $f''$ and The nth derivate function is denoted $f^{(n)}$. 
We can use **Leibniz notation** in which we denote the function by $y=f(x)$ and its derivative by $\frac{dy}{dx}$ or $\frac{d}{dx}f(x)$. To denote the evaluation of the derivate at a point $a$, we write $\frac{df}{dx} \Bigg|_{x=a}$.
##### Gradients
We can extend the notation of derivates to handle vector-argument functions, $f:\mathbb{R}^{n}\to \mathbb{R}$ , by defining the **partial derivative** of $f$with respect to $x_{i}$ to be
$$
\frac{\partial f}{\partial x_{i}} = \lim_{ h \to 0 } \frac{f(x+he_{i}) - f(x)}{h}
$$
where $e_{i}$ is the ith unit vector. 
The gradient of a function at a point x is the vector of its partial derivatives:
$$
g =\frac{\partial f}{\partial x} = \nabla f = \left(\begin{matrix}
\frac{\partial f}{\partial x_{1}}  \\
\vdots \\
\frac{\partial f}{\partial x_{n}}
\end{matrix}\right)
$$
To emphasize the point at which the gradient is evaluated, we can write
$$
g(x^{*}) = \triangleq \frac{\partial f}{\partial x} \Bigg|_{x*}
$$
We see that the operator $\nabla$ maps a function $f:\mathbb{R}^{n}\to \mathbb{R}$ to another function $g:\mathbb{R}^{n}\to \mathbb{R}^{n}$ . Since $g()$ is a vector valued function, it is known as a vector field. By contrast, the derivation function $f'$ is a scalar field.
##### Directional derivative
The **directional derivative** measures how much the function $f:\mathbb{R}^{n}\to \mathbb{R}$ changes along a direction $v$ in space. It is defined as follows
$$
D_{v}f(x) = \lim_{ h \to 0 } \frac{f(x+hv) - f(x)} {h}
$$
##### Total derivative
Suppose that some of the arguments to the function depend on each other. Concretely, suppose the function has the form $f(t, x(t), y(t))$ . We define the total derivative of $f$ with respect to $t$ as follows :
$$
\frac{\partial f}{\partial t} = \frac{\partial f}{\partial t} + \frac{{\partial f}}{\partial x} \frac{dx}{dt} + \frac{\partial f}{\partial y} \frac{dy}{dx}
$$
Total differential 
$$
df= \frac{\partial f}{\partial t} dt + \frac{\partial f}{\partial x} dx + \frac{{\partial f}}{\partial y} dy
$$
##### Jacobian
Consider a function that maps a vector to another vector, $f: \mathbb{R}^{n}\to \mathbb{R}^{m}$ , the **Jacobian matrix** of this function is an $m\times n$ matrix of partial derivatives:
$$
\textbf{J}_{f}(x) = \frac{\partial f}{\partial x^{T}} \triangleq\left(\begin{matrix}
\frac{\partial f_{1}}{\partial x_{1}} & \dots & \frac{\partial f_{1}}{\partial x_{n}} \\
\vdots & \ddots & \vdots \\
\frac{\partial f_{m}}{\partial x_{1}} & \dots &  \frac{{\partial f_{m}}}{\partial x_{n}}
\end{matrix}\right)

= \left(\begin{matrix}
\nabla f_{1}(x)^{T} \\
\vdots \\
\nabla f_{m}(x)^{T}
\end{matrix}\right)
$$

##### Hessian
For a function $f:\mathbb{R}^{n}\to \mathbb{R}$ that is twice differentiable, we define the **Hessian matrix** as the $n\times n$ matrix of second partial derivatives:
$$
\textbf{H}_{f} = \frac{\partial^{2}f}{\partial x^{2}} = \nabla^{2}f = \left(\begin{matrix}
\frac{\partial^{2}f}{\partial x_{1}^{2}} & \dots & \frac{\partial^{2}f}{\partial x_{1}\partial x_{n}} \\
& \vdots & \\
\frac{\partial^{2}f}{\partial x_{n} \partial x_{1}} & \dots & \frac{\partial^{2}f}{\partial x^{2}_{n}}
\end{matrix}\right)
$$

##### Gradients of commonly used functions.
Consider a differentiable function $f:\mathbb{R}\to \mathbb{R}$ ,  Here are some useful identities from scalars calculus.
$$
\begin{align}
\frac{d}{dx}cx^{n} &= cnx^{n-1} \\
\frac{d}{dx}\log(x) &= \frac{1}{x} \\
\frac{d}{dx}\exp(x) &= \exp(x) \\
\frac{d}{dx}[f(x)+ g(x)] &= \frac{df(x)}{dx } + \frac{dg(x)}{dx} \\
\frac{d}{dx}[f(x)g(x)] &= f(x) \frac{dg(x)}{dx} + g(x) \frac{df(x)}{dx}
\end{align}
$$
Chain rule of calculus 
$$
\frac{d}{dx}f(u(x)) = \frac{du}{dx} \frac{df(u)}{du}
$$

###### Function that map vectors to scalars
$$
\begin{align}
&\frac{\partial(a^{T}x)}{\partial x} = a \\
&\frac{\partial(b^{T}Ax)}{dx} = A^{T}b \\
&\frac{\partial(x^{T}Ax)}{\partial x} = (A+ A^{T}) x
\end{align}
$$
###### Function that map matrices to scalars
Consider a function $f:\mathbb{R}^{m\times n}\to \mathbb{R}$ which maps a matrix to a scalar. 

Identities involving quadratic forms 
$$
\begin{align}
& \frac{\partial}{\partial X} (a^{T}Xb) = ab^{T} \\
& \frac{\partial}{\partial x} (a^{T}X^{T}b) = ba ^{T}
\end{align}
$$
Identities involving matrix trace
$$
\begin{align}
& \frac{\partial}{\partial X} \mathrm{Tr}(AXB) = A^{T}B^{T} \\
& \frac{\partial}{\partial X} \mathrm{Tr}(X^{T}A) = A \\
& \frac{\partial}{\partial X} \mathrm{Tr}(X^{-1}A) = - X^{-T}A^{T}X^{-T} \\
& \frac{\partial}{\partial X}\mathrm{Tr}(X^{T}AX) = (A+A^{T}) X
\end{align}
$$
identities involving matrix determinants 
$$
\begin{align}
\frac{\partial}{\partial X}\det(AXB) = \det(AXB)X^{-T} \\
\frac{\partial}{\partial X} \log(\det(X)) = X^{-T}
\end{align}
$$

___
$$
***
$$
