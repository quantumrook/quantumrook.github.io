---
created: 11, Dec, 2024
modified:
  - 02, Jan, 2025
  - 12, Dec, 2024
---

#Drag #Force 

# Quick Reference

- Drag is a Taylor expansion of a function that depends on velocity.
	- Expanded to three terms, the constant term (first term) is set to zero to match physical systems
	- The second term describes the **linear** component of drag
	- The third term describes the **quadratic** component of drag
- The coefficients are typically scalar multiples of the the cross-sectional diameter of the object
- Take the ratio of **quadratic** to **linear** to see which, if any, terms can be neglected
	- The resulting magnitude can also inform if drag is worth considering in the problem
- The parameter $\tau$ is called the **characteristic time**

### Linear Drag

#### Horizontal Equation of motion:

![[Drag#^LinearDragHorizontalEOM]]

where:
- $\tau$ is defined in this context as $1/k=m/b$
- $x$ is measured positively to the right
- $x=0$ and $v_x=v_{x0}$ at $t=0$

> [!info] Notable Behaviour:
> - as $t\rightarrow\infty$, $v_x(t)\rightarrow0$
> - at $t=\tau$, $v_x(\tau)\approx (0.37)v_{x0}$
> - at $t=3\tau$, $v_x(3\tau)\approx (0.05)v_{x0}$ and we can *effectively* treat the horizontal speed as zero

---

Integrated, the position is given as (using [[Bibliography#^Taylor|Taylor]]'s [[2.2 Linear Air Resistance#^964a14|notation]]):

$$x(t)=x_{\infty}\big(1-e^{-t/\tau}\big)$$

where:
- $\tau$ is still $1/k=m/b$
- $x$ is measured positively to the right

> [!info] Notable Behaviour:
> - as $t\rightarrow\infty$, $x$ asymptotically approaches $x_{\infty}$
> - at $t=\tau$, the object is $0.63x_{\infty}$ away from $x_0$
> - at $t=3\tau$, the object is *effectively* at $x_{\infty}$: $x(3\tau)=0.95x_{\infty}$


#### Vertical Equation of motion:

>[!quote] #src/Taylor-ClassicalMechanics, [[2.2 Linear Air Resistance#Vertical Motion with Linear Drag|2.2.2 Vertical Motion with Linear Drag]]
> ![[2.2 Linear Air Resistance#^6918ad]]

where:
- $\tau$ is defined in this context as $1/k=m/b$
- $y$ is measured positively downwards
- $v_y=v_{y0}$ at $t=0$
- $v_y\rightarrow v_{ter}$ as $t\rightarrow\infty$

>[!note]
>When $v_{ter}$ is small, air resistance is **not negligible**, as $v_{ter}$ is inversely proportional to the coefficient of air resistance, $b$.
>
>Or, phrased differently, the bigger the air resistance (and hence $b$), the smaller the final speed of the object ($v_{ter}$).

---

# Overview

The resistive force, or **drag**, is proportional to the velocity of the object in question in the form of $\textbf{f}_{drag}=\exp{\big(v(t)\big)}\big(-\hat{\textbf{v}}\big)$. Usually, this is Taylor expanded to the first three terms:

$$\begin{equation*}\begin{align*}\textbf{f}\big(v(t)\big)&\approx-\left(a+bv(t)+cv^2(t)\right)\hat{\textbf{v}}\\&\approx-bv(t)-cv^2(t)\hat{\textbf{v}}\end{align*}\end{equation*}$$

where $a$ is set to zero, as there is no resistance when $v(t)=0$. This equation is then broken into two separate parts, the **linear** and **quadratic** forms of drag:

$$\textbf{f}_{lin}\big(v(t)\big) \approx -bv(t)\hat{\textbf{v}}$$

$$\textbf{f}_{lin}\big(v(t)\big) \approx -bv(t)\hat{\textbf{v}} \tag{2}$$

$$\textbf{f}_{lin}\big(v(t)\big) \approx -bv(t)\hat{\textbf{v}} \tag{2}$$^DragEq2

$$\textbf{f}_{quad}\big(v(t)\big) \approx - cv^2(t)\hat{\textbf{v}} \tag{3}$$^DragEq3



where $b$ and $c$ are the corresponding coefficients for the type of drag, both depending on the the [[viscosity]] of the [[medium]] in which the object is traveling and the object's [[cross-sectional area]].

>[!example]+ **Example:** The coefficients defined for Air at [[standard temperature and pressure|STP]]:
> ![[2.1 Air Resistance#^15bffb]]
> ![[2.1 Air Resistance#^e15853]]
> ![[2.1 Air Resistance#^46cdee]]
> from [[2.1 Air Resistance]] in #src/Taylor-ClassicalMechanics

Usually only one of the terms, $f_{lin}$ or $f_{quad}$ is relevant to the object in question, the dominating term can be revealed by examining the ratio between the quadratic and linear terms:

$$\frac{f_{quad}}{f_{lin}} = \frac{cv^2}{bv} = \frac{\gamma D}{\beta}v \tag{1.4}$$

An example of this in use can be found [[2.1 Air Resistance#^04f478|here]] using air at STP, or in short:

| Object        | Neglects  | Form                                    |
| ------------- | --------- | --------------------------------------- |
| Baseball-like | linear    | $\textbf{f}=-cv^2\hat{\textbf{v}}$      |
| Raindrop-like | neither   | $\textbf{f}=-(bv+cv^2)\hat{\textbf{v}}$ |
| Oildrop-like  | quadratic | $\textbf{f}=-bv\hat{\textbf{v}}$        |

---

# Linear Drag

For the case where Linear drag is the dominant component (and quadratic is negligible), the resulting [[equation of motion]] is generally fairly straightforward to solve. The functional form resolves to a [[first-order differential equation]], or in the worst case, a differential equation that can be solved by [[separation of variables]]. Using [[Drag#^DragEq2|Equation (2)]] the equation of motion is defined as

$$m\ddot{\textbf{r}}=m\textbf{g}-b\textbf{v},$$

which is first-order in $v$ (since $\ddot{\textbf{r}}=\dot{\textbf{v}}$). Of technical note, this is an [[inhomogeneous first-order differential equation with constant coefficents]] that is can take the form

$$\dot{\textbf{v}}+\frac{b}{m}\textbf{v}=\textbf{g},$$

or in math speak (general form, omitting vector components):

$$\dot{u}+\alpha u = f.$$

The next important feature of linear drag is that it's equation of motion can be separated to solve each component separately, or in other terms, the **equations of motion are uncoupled**.

>[!quote]+ #src/Taylor-ClassicalMechanics, [[2.2 Linear Air Resistance#2.2 Linear Air Resistance|2.2 Linear Air Resistance, Pages 46-53]]
> ![[2.2 Linear Air Resistance#^0a86ea]]
> ![[2.2 Linear Air Resistance#^a96eec]]
> ![[2.2 Linear Air Resistance#^de5cec]]
> ![[2.2 Linear Air Resistance#^049954]]

The general solution is then of the form $Ae^{-kt}$ where $k$ is $b/m$ and $A$ is replaced with the initial velocity in the $x$-direction. The most common notation is to introduce a parameter, $\tau$, that is $1/k$ (or $m/b$) such that the final form looks like

$$v_x(t) = v_{x0}e^{-t/\tau}\tag{4}$$^LinearDragHorizontalEOM

This equation of motion is then simple to integrate to obtain the description of the object's (horizontal) position using a definite integral,

![[2.2 Linear Air Resistance#^3c5f08]]

The resulting form is given by [[B]]

# Quadratic Drag

More info about Quadratic Drag goes here.

