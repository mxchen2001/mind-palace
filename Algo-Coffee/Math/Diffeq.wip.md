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

An **Ordinary Differential Equation** is an equation with derivative taken with respect to one varible.

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
A homogenous differential equation has the condition that every term in the differential equation has a variable taken to a deriative.

>The following is homogeneous:
>$$y''+2y=0$$
>The following is non-homogeneous due to the $-5$:
>$$y'''+4x^7y''+sin(x)y-5=0$$


### Seperatable ODE
Whenever a **Linear First Order Differential Equation** is **Homogeneous**, the equation can be seperated. An ODE expressed in the form
$$\frac{dy}{dx} = g(x)y $$ 
can be decomposed into
$$\frac{1}{h(y)}=g(x)dx \quad  \text{or} \quad \int \frac{1}{h(y)}=\int g(x)dx$$
which reduces to
$$ ln(y)= H(x) + C \quad \text{or} \quad  y = Ce^{H(x)}$$ 
>**Example:**
>$$(1) \qquad \frac{dy}{dx} = 4y\sin(3x)$$
>$$(2) \qquad \frac{1}{y}dy=4\sin(3x)dx$$
>$$(3) \qquad \int\frac{1}{y}dy = \int 4\sin(3x)dx$$
>$$(4) \qquad \ln(y) = -\frac{4}{3}\cos(3x)+C$$
>$$(5) \qquad y= Ce^{-\frac{4}{3}\cos(3x)}$$



### Non-Homogeneous Linear ODE
To solve a linear ODE in the form of 
$$ y' +P(x)y = Q(x)$$
>Notice the equation can be rewritten to 
>$$ y' +y = \frac{Q(x)}{P(x)}$$
and that $y' + y$ is in the form of a _product rule_ just without the value of the additional products
>
>
>The key is to apply the _chain rule_ in conjunction 
$$\mu'(x)=\mu(x)P(x)$$
>where the only possible $\mu(x)$ would be in the form of
$$\mu(x)=e^{\int P(x)dx}$$
>therefore the final equation, when multiplied by $\mu(x)$ is
$$\mu(x) y' +\mu(x)P(x)y = \mu(x)Q(x)$$
rewriting the left-side of the equation can be expressed in the form of 
$$\mu(x) y' +\mu'(x)y = (\mu(x)y)'$$
then transfering the left side of the equation to the starting gives
$$(\mu(x)y)'= \mu(x)Q(x)$$
integrating both sides
$$\int (\mu(x)y)'= \int \mu(x)Q(x)$$
then isolating the $y$ to the left side gives
$$y = \frac{\int \mu(x)Q(x)}{\mu(x)}$$
>>If you got nothing from this just remember
$$y = \frac{\int \mu Q + C}{\mu}$$
and it will solve all your problems.






### IVP – Initial Value Problem

Given the initial conditions the $C$ term can be computed
> Initial conditions always operate as solution one degree lower than the order of the equation
> 
>Given
>$$y''' + y'' + y ' + y = 0 $$
>An IVP will give
>$$y(a)=b$$
$$y'(c)=d$$
>
>and
>$$y''(e)=f$$


## Second Order ODE
A _Second Order Differential Equation_ is generally expressed as 
$$ L(y) = ay'' + by' + cy$$
where $L$ is an operator that creates the differential equation 
>First find a solution such that taking the derivative subsequently does not annihilate it
>
>>It works out that setting
>$$y = e^{rt}$$
gives
>$$y' = re^{rt}$$
and
>$$y'' = r^2e^{rt}$$
>
>Substituting the values for y into a homogenous equation gives
>$$ ar^2e^{rt} + bre^{rt} + ce^{rt} = 0$$
>pulling out the _e_ gives
$$e^{rt}(ar^2 + br + c)$$
where 
$$(ar^2 + br + c)$$
is the _**Characteristic Equation**_
>
>Solving the Characteristic Equation will give the values of r
>> Ex:
>>$$y'' + 4y' + 2y = 0$$
>>Gives
>>$$e^{rt}[r^2 + 4r + 2]$$
>>Where solving the Characteristic Equation
>>$$\frac{-4\pm \sqrt{4^2-4(1)(2)}}{2(1)}$$
>>Gives
>>$$-2\pm \sqrt{6}$$
>>Therefore the solution would be
>>$$ y(t) = C_1e^{-2 + \sqrt{6}t} + C_2e^{-2 - \sqrt{6}t}$$
>>>
>>>_**Solving an IVP**_
>>>
>>>Given the Inital conditions of
$$ y(0) = 0 \quad y'(0) =1$$ 
$$y(t) = C_1e^{-2 + \sqrt{6}t}+C_e^{-2 - \sqrt{6}t}=0$$
$$ y(0) = C_1+C_2=0$$
or
$$ C_1 = -C_2$$
then
$$y(t) = C_1(-2 + \sqrt{6})e^{-2 + \sqrt{6}t}+C_2(-2 - \sqrt{6})e^{-2 - \sqrt{6}t}$$
$$ y'(0)= (-2 + \sqrt{6})C_1+(-2 - \sqrt{6})C_2=1$$
Where substituting the first gives
$$(-2 + \sqrt{6})C_1-(-2 - \sqrt{6})C_1 = 1$$
$$(-2 + \sqrt{6})C_1=(-2 - \sqrt{6})C_1 + 1$$
$$\sqrt{6}C_1=-\sqrt{6}C_1+1$$
$$2\sqrt{6}C_1=1$$
$$C_1 = \frac{1}{2\sqrt{6}}$$
$$C_2 = -C_1 = \frac{-1}{2\sqrt{6}}$$
Where the particular solution is 
$$y(t) =  \frac{1}{2\sqrt{6}}e^{-2 + \sqrt{6}t} - \frac{1}{2\sqrt{6}}e^{-2 - \sqrt{6}t}$$
>
>*simply trivial



### Complex Roots
For the ODE
$$y'' + y = 0 $$
Gives 
$$ e^{rt}[r^2+1]$$
Where solving the Characteristic Equation gives
$$ r = \pm i $$
>Recall the power expansion
>$$ e^t = 1 + t + \frac{t^2}{2!} + \frac{t^3}{3!} + \frac{t^4}{4!}+...$$
>$$ \cos(t) = 1 - \frac{t^2}{2!} + \frac{t^4}{4!}+...$$
>$$\sin(t) = t - \frac{t^3}{3!} + \frac{t^5}{5!}+...$$
Where substituting $i$ gives
>$$ e^{it} = 1 + it - \frac{t^2}{2!} + i\frac{t^3}{3!} + \frac{t^4}{4!}+...$$
$$ \cos(t) = 1 - \frac{t^2}{2!} + \frac{t^4}{4!}+...$$
$$i\sin(t) = it - i\frac{t^3}{3!} + i\frac{t^5}{5!}+...$$
>>Thus the _**Euler Identity**_
$$e^{it} = \cos(t)+i\sin(t)$$
>
>Using the Euler Identity to solve the original _Complex ODE_
>$$(\cos(t)+i\sin(t)) \quad r=i $$
Gives
$$y_1=C_1\cos(t)+C_2i\sin(t)$$
and
>$$(\cos(t)+i\sin(t)) \quad r=-i $$
Gives
$$y_2=C_3\cos(-t)+C_4i\sin(-t)$$
where the trig identities 
$$\cos(-t)= \cos(t)\qquad \sin(-t)=-\sin(t)$$
when applied to $y=y_1+y_2$ gives
$$y =(C_1+C_3)\cos(t)+(C_2i-C_4i)\sin(t)$$
where reducing the constants gives
$$y_1=C_1\cos(t)+C_2\sin(t)$$
>
>>The general stucture to a Complex ODE's is 
$$ e^{\alpha \pm \beta} \Rightarrow e^{\alpha}[C_1\cos(\beta t) + C_2\sin(\beta t)]$$
>
>>Ex:
>>$$y''−8y'+17y=0 \qquad y(0)=-4 \quad y'(0)=-1$$
>>Create characteristic equation of
>>$$r^2-8r+17$$
>>Where
>>$$\frac{8\pm \sqrt{(-8)^2-4(1)(17)}}{2(1)}=4\pm i$$
>>The general equation
>>$$y(t) = C_1e^{4t}\cos(t)+C_2e^{4t}\sin(t)$$
>>>
>>>
>>>_**Solving an IVP**_
>>>$$y(0)=-4 \quad y'(0)=-1$$
$$y(t)=C_1e^{4t}\cos(t)+C_2e^{4t}\sin(t)$$
$$y(0)=C_1e^{4(0)}\cos(0)+C_2e^{4(0)}\sin(0) $$ 
$$C_1=-4$$
Apply Product Rule
$$y'(t)=4
C_1e^{4t} \cos(t) − C_1e^{4t}\sin(t) + 4 C_2e^{4t}\sin(t) + C_2e^{4t}\cos(t)$$
$$y'(0)=4C_1+C_2=-1$$
$$C_2=15$$
The particular solution is
$$y(t) = -4e^{4t}\cos(t)+15C_2e^{4t}\sin(t)$$
>
>*Again simply trivial

### Linear Dependency
Before we tallk about repeated roots we need to mention the idea of _**Linear Dependency**_. The topic will be dicussed in detail later when we talk about vector but the most important idea is if $f_1$ and $f_2$ are linear combination of each other where multiplying by a constant allows for one to be the other, they are considered linearly dependent

The Wronskian Determinent can be use to check linear dependency. _2X2 Wronskian is shown_

$$W(f_1,f_2)=\begin{bmatrix} f_1 & f_2 \\ f'_1 & f'_2 \end{bmatrix}$$

If
$$det \begin{bmatrix} f_1 & f_2 \\ f'_1 & f'_2 \end{bmatrix}=0$$
Then the two $f_1$ and $f_2$ are **_linearly dependent_**

If
$$det \begin{bmatrix} f_1 & f_2 \\ f'_1 & f'_2 \end{bmatrix}\neq 0$$
Then the two $f_1$ and $f_2$ are **_linearly independent_**

Here is a [_3Blue1Brown_](https://www.youtube.com/watch?v=Ip3X9LOh2dk&list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab&index=7&t=0s) video that visually explains this property.


>Example of both cases
>
>>Linearly Dependent
>>$$3x^2 \;\; and \;\; 56x^2 $$
$$18e^{3t} \;\; and \;\; -7e^{3t}$$
$$4\sin(4t) \;\; and \;\; \sin(4t)$$
>
>>Linearly Independent 
$$4x^3\;\; and \;\; 4x^2$$
$$e^{-t} \;\; and \;\; e^{t}$$
$$4\cos(t) \;\; and \;\; 4\sin(t)$$
>
>*trivial





### Repeated Roots

The Problem with repeated roots is if a characteristic equation generates such that
$$y'' + 4y' +4y = 0$$
will produce 
$$r^2 + 4r + 4$$
and will produce the roots of
$$(r+2)(r+2) \quad r=-2 \;\;\;  m_a=2$$
The $m_a$ denotes algebraic multiplicity 

>When following the method of Real Roots the solution generated is 
$$y(t) = C_1e^{-2t} + C_2e^{-2t}$$
Where 
$$y_1=C_1e^{-2t} \qquad y_2=C_2e^{-2t}$$
Where by inspection
$$y_1, \;\; y_2$$
are linear combinations of one another thus the solution to the second order only produces one solution
$$y(t) = C_1e^{-2t}$$
>
>We call this the **_first solution_** and the **_second solution_** $g$, is under the assumption that  
$$g=Ve^{-2t}$$
Where
$$g' = V'e^{-2t} -2Ve^{-2t}$$
and 
$$g'' = V''e^{-2t} -2V'e^{-2t} -2V'e^{-2t} + 4Ve^{-2t}$$
plugging the $g'$ and $g''$ into the original differential equation gives 
$$e^{-2t}(V''-4V' +4V +4V'-8V+4V) = e^{-2t}(V'') = 0$$
Divide both sides gives
$$V''= 0 $$
Then integrating $V''$ gives
$$V'' = 0 \qquad\;\; V'= C_1 \qquad \;\; V = C_1t + C_2$$
>
>> Therefore to solve this, we need to make the two linearly independent by **_"bumping"_** the order of the solution
>>
>>Using the example from above
>>$$y'' + 4y' +4y = 0 \;\;\;\; \Rightarrow \;\;\;\; r^2 + 4r + 4 \;\;\;\; \Rightarrow \;\;\;\; (r+2)(r+2) \;\; r=-2 \;\;  m_a=2$$
>>The solutions are
>>$$y_1=C_1e^{-2t} \qquad y_2=C_2e^{-2t}$$
>>
>>Where after appying the **_bump_** becomes
>>$$y(t)=C_1e^{-2t} +C_2te^{-2t}$$
>>>The form of a second order repeat root is
>>>$$y(t) = y_1 + ty_2$$
>>>Where this format hold for higher levels of repeated roots
>>>$$y(t) = y_1 + ty_2 + \frac{1}{2!} \ t^2y_3 + \frac{1}{3!} \ t^3y_4t+...\frac{1}{(n-1)!} \ t^{n-1}y_n$$
>>>Note that the constant infront can be eliminated by the $C$
>>>
>>>But this will not show up in the class
>
>*super trivial


## Non-Homogenous
Until now we have only been dealing with homogenous second order differential equations.
The prominent issue with dealing with the particular solutions having _linearly dependent_ solutions.
> If $\psi$ of $t$ is a particular solution to $L(\psi)=g$  and  $y_1$  and  $y_2$are fundemental solutions to $L(y)=0$, then the general solution is 
$$y(t) = \psi +C_1y_1 + C_2y_2$$
Now consider $\Phi - \psi$ where
$$L(\Phi -\psi) = L(\Phi) - L(\psi) = g - g = 0$$
Therefore $\Phi - \psi = 0$ is a solution to
$$\Phi -\psi = 0 = C_1y_1 + C_2y_2$$ 
thus 
$$\Phi = \psi + C_1y_1 + C_2y_2$$

## Constant Coefficient
#### The Method of "Undetermined Coefficients" or "Judicious Guessing"
A _Second Order Constant Coefficient Differential Equation_ will be in the format of 
$$ay'' + by' + cy =f(x)$$
where $a$, $b$, and $c$ are constants
$$\tilde y_h \in ay'' + by' + cy$$
$$\tilde y_p \in f(x)$$
where to solution of $y_h$ and $y_p$ give the general solution of 
$$y = y_h + y_p$$



>Ex: 
$$y''+y'+2y = e^{-t}\cos(t)$$
Create the characteristic equation to find the fundemental solutions
$$r^2+r+2$$
Giving
$$r=-\frac{1}{2} \pm \frac{\sqrt{7}}{2}i$$
Creating the fundemental set of 
$$y_h=e^{-\frac{1}{2}t}C_1\cos(\frac{\sqrt{7}}{2}t) + e^{-\frac{1}{2}t}C_2\sin(\frac{\sqrt{7}}{2}t)$$
>
>>Solving the particular of 
$$f(x) = e^{-t}\cos(t)$$
Create the undetermined $\tilde y_p= \psi$
$$\psi = e^{-t}[A\cos(t)+B\sin(t)]$$
$$=Ae^{-t}\cos(t)+Be^{-t}\sin(t)$$
Taking addition derivatives gives
$$\psi'= -Ae^{-t}\cos(t)-Ae^{-t}\sin(t)-Be^{-t}\sin(t)+Be^{-t}\cos(t)$$
$$\psi''= Ae^{-t}\cos(t)+Ae^{-t}\sin(t)+Ae^{-t}\sin(t)-Ae^{-t}\cos(t) \newline +Be^{-t}\sin(t)-Be^{-t}\cos(t)-Be^{-t}\cos(t)-Be^{-t}\sin(t)$$
Thankfully reduces to
$$\psi''=2Ae^{-t}\sin(t)-2Ae^{-t}\cos(t)$$
Plugging $\psi$, $\psi'$, and $\psi''$ in place of $y$, $y'$, and $y''$
$$\psi''+\psi' +2\psi = e^{-t}\cos(t)$$
Yields
$$2Ae^{-t}\sin(t)-2Ae^{-t}\cos(t) -Ae^{-t}\cos(t) -Ae^{-t}\sin(t)-Be^{-t}\sin(t)+\newline Be^{-t}\cos(t)  + 2Ae^{-t}\cos(t)+2Be^{-t}\sin(t) = e^{-t}\cos(t)$$
Whiches reduces into
$$(A+B)e^{-t}\sin(t) + (A-B)e^{-t}\cos(t) = e^{-t}\cos(t)$$
Therefore the $A$ and $B$ becomes
$$A+B=0 \qquad A-B= 1$$
$$A=\frac{1}{2} \qquad B=-\frac{1}{2}$$
Plugging $A$ and $B$ into $\tilde y_p =e^{-t}[A\cos(t)+B\sin(t)]$ creates
$$e^{-t}[\frac{1}{2}\cos(t)-\frac{1}{2}\sin(t)]$$
Finally $y = y_h + y_p$ produces
$$y(t)=e^{-\frac{1}{2}t}C_1\cos(\frac{\sqrt{7}}{2}t) + e^{-\frac{1}{2}t}C_2\sin(\frac{\sqrt{7}}{2}t)+e^{-t} \frac{1}{2} \cos(t)-e^{-t} \frac{1}{2} \sin(t)$$
Note that from this point the problem can continue as an _IVP_ but honestly that would just be cruel.










### This is a table to practice identifying $\tilde{y}_p$

|$f(x)$|$\tilde{y}_p$|
|:--- |:------------|
|$2$|$A$|
|$3x-4$|$Ax+B$|
|$17x$|$Ax+B$|
|$x^2+x$|$Ax^2+Bx+C$|
|$17e^{3x}$|$Ae^{3x}$|
|$xe^{5x}$|$(Ax+B)e^{5x}$|
|$(2x^2-7)e^{-2x}$|$(Ax^2+Bx+C)e^{-2x}$|
|$3\sin(2x)$|$A\cos(2x)+B\sin(2x)$|
|$\frac{1}{2}\cos(3x)+\sqrt{3}\sin(3x)$|$A\cos(3x)+B\sin(3x)$|
|$\cos(4x)-\sin(6x)$|$A\cos(4x)+B\sin(4x)+C\cos(6x)+D\sin(6x)$|
|$e^{2x}[3\sin(2x)]$|$e^{2x}[A\cos(2x)+B\sin(2x)]$|
|$x\sin(x)$|$(Ax+B)\cos(2x)+(Cx+D)\sin(2x)$|
|$xe^{5x}\sin(2x)$|$e^{5x}[(Ax+B)\cos(2x)+(Cx+D)\sin(2x)]$|
