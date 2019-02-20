[//]: # (#math )
# Multivariable Calculus
## Fundamentals
1. The derivative of f(x), df/dx, describes exactly the slope of a particular point on the curve. The slope determined by the derivative can be used to simplify(fit) a curve when the change of x is very small.[:link:](https://www.youtube.com/watch?v=dfvnCHqzK54&list=PLSQl0a2vh4HC5feHa6Rc5c0wbRTx56nF7&index=16)
$$
\frac{df}{dx}=\lim_{\Delta{x} \to 0}\frac{\Delta{f}}{\Delta{x}}=\lim_{\Delta{x} \to 0}\frac{f(x+\Delta{x})-f(x)}{\Delta{x}}
$$
- $\frac{df}{dx}$ can also be interpreted as the rate of change of *f* with respect to the change of *x*
2. For most cases:[:link:](https://www.youtube.com/watch?v=J08-L2buigM&index=18&list=PLSQl0a2vh4HC5feHa6Rc5c0wbRTx56nF7)
$$
\frac{\partial{f}}{\partial{y}}(\frac{\partial{f}}{\partial{x}}) = \frac{\partial{f}}{\partial{x}}(\frac{\partial{f}}{\partial{y}})
$$
3. Gradient is just an extension of derivatives for **scalar-value-multivariable** functions:[:link:](https://www.youtube.com/watch?v=qZlBjnC3iro&list=PLSQl0a2vh4HC5feHa6Rc5c0wbRTx56nF7&index=32)
$$
\nabla{}f(x,y)=\nabla{f}=\begin{bmatrix}\frac{\partial{f}}{\partial{x}}\\\\\frac{\partial{f}}{\partial{y}}\end{bmatrix}=\begin{bmatrix}\frac{\partial{}}{\partial{x}}\\\\\frac{\partial{}}{\partial{y}}\end{bmatrix}f
$$
4. The directional derivatives of *f*: [:link:](https://www.youtube.com/watch?v=4tdyIGIEtNU&list=PLSQl0a2vh4HC5feHa6Rc5c0wbRTx56nF7&index=23)
$$
\nabla_{\overrightarrow{w}}f(\overrightarrow{v})=\nabla{f}(\overrightarrow{v})\cdotp{\overrightarrow{w}}
$$
- This interprets as: the derivative of *f* at point $\overrightarrow{v}$ along the direction of $\overrightarrow{w}$
- where $\overrightarrow{w}$ is a unit vector in the input space
5. Multivariable chain rule:[:link:](https://www.youtube.com/watch?v=qZlBjnC3iro&list=PLSQl0a2vh4HC5feHa6Rc5c0wbRTx56nF7&index=30)
- What is change rate of *f* with respect to the change of *t* ?
$$
\frac{df(x(t),y(t))}{dt}=\frac{\partial{f}}{\partial{x}}\frac{dx}{dt}+\frac{\partial{f}}{\partial{y}}\frac{dy}{dt}
$$ 
6. The Laplacian is sort of analog to second order derivatives for **scalar value multivariable functions**:[:link:](https://www.youtube.com/watch?v=EW08rD-GFh0&list=PLSQl0a2vh4HC5feHa6Rc5c0wbRTx56nF7&index=65)
- It measures the concavity of a point, that is, whether it is **on average** greater or less than its neighbors. For example, when positive, the Laplacian indicates the point is within a upward concave[:link:](https://www.youtube.com/watch?v=JQSC0lCPG24&list=PLSQl0a2vh4HC5feHa6Rc5c0wbRTx56nF7&index=68)
$$
\triangle{f(x,y)} = div(\nabla{\cdotp}f(x,y))=\nabla{\cdotp}\nabla{}f(x,y)=\begin{bmatrix}\frac{\partial{}}{\partial{x}}\\\\\frac{\partial{}}{\partial{y}}\end{bmatrix}\cdotp{}\begin{bmatrix}\frac{\partial{}}{\partial{x}}\\\\\frac{\partial{}}{\partial{y}}\end{bmatrix}f(x,y)=\frac{\partial{}^2f}{\partial{x^2}}+\frac{\partial{}^2f}{\partial{y^2}}
$$
1. Local linear approximation[:link:](https://www.youtube.com/watch?v=o7_zS7Bx2VA&list=PLSQl0a2vh4HC5feHa6Rc5c0wbRTx56nF7&index=77)
+ For scalar value function, the loacl neighbor of _$f$_ at _$X_0$_ can be approximated by the sum of _$f(X_0)$_ and the gradient at _$X_0$_ times the shift _$h$_
$$
L(X_0+h) = f(X_0)+\nabla{f(X_0)}\cdotp{h}
$$
8. Hessian matrix:[:link:](https://www.youtube.com/watch?v=LbBcuZukCAw&index=82&list=PLSQl0a2vh4HC5feHa6Rc5c0wbRTx56nF7)
- The Hessian matrix $H_f$ is a **matrix value** function that takes **scalar value multivariable** function $f$.
- It is a symmetric matrix and only consists of the second order derivatives of $f$
$$
H_{f(x,y)}=\begin{bmatrix}\frac{\partial{^2f}}{\partial{^2x}}\frac{\partial{^2f}}{\partial{y}\partial{x}}\\\\\frac{\partial{^2f}}{\partial{y}\partial{x}}\frac{\partial{^2f}}{\partial{^2y}}\end{bmatrix}
$$
9. Local quadratic approximation[:link:](https://www.youtube.com/watch?v=ClFrIg0PpnM&list=PLSQl0a2vh4HC5feHa6Rc5c0wbRTx56nF7&index=84)
- The local quadratic approximation of a **scalar value multivariable function** has 3 terms: constant term, linear term and quadratic term
$$
Q(\vec{X_0}+\vec{h})=f(\vec{X_0})+\nabla{f(\vec{X_0})}\vec{h}+\vec{h}^TH_f(\vec{X_0})\vec{h}
$$
- Where $\vec{h}$ is a little shift from $\vec{X_0}$
- $\nabla{f(\vec{X_0})}$ is the gradient of f evaluated at  $\vec{X_0}$
- $H_f(\vec{X_0})$ is the Hessian of f evaluated at $\vec{X_0}$
10. Second partial derivatives test[:link:](https://www.youtube.com/watch?v=sJo7D74PAak&list=PLSQl0a2vh4HC5feHa6Rc5c0wbRTx56nF7&index=88)
- This works for any scalar value multivariable function $f$
  1. Find out all the points with flat slope(**critical points**) => $\nabla{f}=\vec{0}$ 
  2. Distinguish local mamxima/minima from saddle points => $det(H_f)>0$ indicates true minima/maxima, while $<0$ indicates saddle points
  - *COMMENT: If the concavities of arbitray two dimensions don't agree with each other, it must be a saddle point*
  3. For true minima/maxima points, test the concavity (2nd derivative) of arbitray dimension to distinguish minima from maxima
  - *COMMENT: For minina/maxima points, concavities of all dimensions all agree to positive or negative*
   
11. Constraint optimization problem
- Lagrange multiplier[:link:](https://www.youtube.com/watch?v=hQ4UNu1P2kw&list=PLSQl0a2vh4HC5feHa6Rc5c0wbRTx56nF7&index=94)
- Lagrangian, simple transform of Lagrange multiplier but is more friendly to computer[:link:](https://www.youtube.com/watch?v=hQ4UNu1P2kw&list=PLSQl0a2vh4HC5feHa6Rc5c0wbRTx56nF7&index=97)


## Differrent notations of the same term
1. second order derivatives, **first x then y**:[:link:](https://www.youtube.com/watch?v=J08-L2buigM&list=PLSQl0a2vh4HC5feHa6Rc5c0wbRTx56nF7&index=18)
$$
\frac{\partial{f}}{\partial{y}}(\frac{\partial{f}}{\partial{x}}) =  \frac{\partial^2f}{\partial{y}\partial{x}}=f_{xy}
$$
2. directional derivatives:
$$
\nabla_{\overrightarrow{v}}f=\frac{df}{d\overrightarrow{v}}=\partial_{\overrightarrow{v}}f
$$where $\overrightarrow{v}$ is a unit vector in the input space