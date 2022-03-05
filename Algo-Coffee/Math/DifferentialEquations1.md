# Differential Equations
Derivative of functions with respect to independent variables 
<center> 

$a_nxy^{(n)} + a_{n-1}xy^{(n-1)} + \dots + \;a_2xy'' + a_1xy' + a_0xy=f(x)$

</center>

**Order** – the degree of the highest derivative
**Ordinary** – a function with only one variable
**Partial** – a function under multiple variables
**ODE** – "Ordinary Differential Equation"
**Linear** – _*described later_
**Homogeneous** _*described later_

## First Order ODE

An **Ordinary Differential Equation** is an equation with derivative taken with respect to one variable.

The [_Picard-Lindelof Theorem_](http://web.mit.edu/jorloff/www/18.03-esg/notes/existAndUniq.pdf)

### Linear ODE

A first order linear ODE generally follows the structure 
<center> 

$ y' +P(x)y = Q(x)$
</center>

Where the degree of every derivative is to the first degree
>An algebraic linear equation:
><center>
>
>$ay_1+y_2=c$
>
></center>
>A differential linear equation:
><center>
>
>$a(x)y'+b(x)y=c(x)$
>
></center>
>
>Therefore $ y'+ x^2y=5 $ is linear while $ y' + y^2 = 0 $ is not linear.

### Homogeneity
A homogenous differential equation has the condition that every term in the differential equation has a variable taken to a derivative.

>The following is homogeneous:
><center>
>
>$y''+2y=0$
>
></center>
>
>The following is non-homogeneous due to the $-5$:
>
><center>
>
>$y'''+4x^7y''+sin(x)y-5=0$
>
></center>


### Separable ODE
Whenever a **Linear First Order Differential Equation** is **Homogeneous**, the equation can be separated. An ODE expressed in the form
<center>

$\frac{dy}{dx} = g(x)y $

</center>

can be decomposed into

<center>

$\frac{1}{h(y)}=g(x)dx \quad  \text{or} \quad \int \frac{1}{h(y)}=\int g(x)dx$

</center>

which reduces to

<center>

$ ln(y)= H(x) + C \quad \text{or} \quad  y = Ce^{H(x)}$

</center>

>**Example:**
><center>
>
>$\frac{dy}{dx} = 4y\sin(3x) \qquad (1)$
>
>$\frac{1}{y}dy=4\sin(3x)dx \qquad (2)$
>
>$\int\frac{1}{y}dy = \int 4\sin(3x)dx \qquad (3)$
>
>$\ln(y) = -\frac{4}{3}\cos(3x)+C \qquad (4)$
>
>$y= Ce^{-\frac{4}{3}\cos(3x)} \qquad (5)$
>
></center>

