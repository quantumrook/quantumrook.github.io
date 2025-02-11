---
title: Modeling Wind
created: 30, Jan, 2025
modified:
  - 11, Feb, 2025
  - 07, Feb, 2025
  - 02, Feb, 2025
  - 30, Jan, 2025
---
As a practical exercise, I am attempting to model wind using my current knowledge of physics and math. There probably will be a point where I do research into how its actually done, but I want to see just how far I can get and ultimately how *correct* my model will be.

---

## Wind as almost reverse drag

Having thought a little on this topic on and off for a couple days, I have a general idea of what this model should look like. Two key characteristics are:

- the force of wind should be a vector field that depends on position and time
- the force of wind should be proportional (in some form) to drag

The first part *feels* fairly straightforward as one could draw analogies of wind to other fields like: gravity, electrostatics/electrodynamics, etc.. The ideal situation would be to get to a point where one could describe the force *felt* by an object in the field through: $\textbf{f}_{wind}(x,y,z,t)$.

Immediately, this reminds me of the wave equation and using separation of variables for its solution. The comparison of a *portion* of wind to a traveling wave doesn't raise any obvious concerns and to that effect the system of a driven LRC circuit might serve as a good simplified model (or maybe just a driven LR/RC/LC circuit).

The second part arises from two thoughts:

1. Imagine the case of a person standing outside on a windy day. Shifting to the wind's inertial reference frame (for the case of a constant force of wind): The person now has the negative of $\textbf{v}_{wind}$ and the force they experience would be drag. This follows from: an object moving through a medium will experience a resistive force from that medium.
2. Both wind and drag explicitly depend on the properties of the medium: temperature and pressure of the gas effect the viscosity as altitude changes. This argument is weak in its current form, and I would go about strengthening it by consulting fluid flow and/or other fluid dynamics.

At this risk of circular reasoning, the property of superposition (for forces) naturally extends the following relation:

$$
\textbf{v}_{wind} = \textbf{v}_{rel,wind} + \textbf{v}_{drag}
$$

Or at least, the concept I'm attempting to relay is that, with Newton's Second law, we have:

$$
m\dot{\textbf{v}} = \textbf{f}_{wind} + \textbf{f}_{drag}
$$

> [!note]
> For simplicity, I'm assuming the object in question has a density such that its buoyancy force exactly counters the gravitational force.

For the initial conditions that the object is at rest at $t=0$, $\textbf{f}_{drag}$ is necessarily at its minimum of zero and $\textbf{f}_{wind}$ would be at its maximum. As the object's velocity increases, $\textbf{f}_{drag}$ naturally increases, but crucially, $\textbf{f}_{wind}$ must decrease. As in, the magnitude of $\textbf{f}_{wind}$ doesn't depend on $\textbf{v}_{obj}$ in the way that drag does, but on the difference between the flow of the wind and the object: 

$$\textbf{v}_{rel,wind} = \textbf{v}_{wind} - \textbf{v}_{obj}$$

Such that, given sufficient time, the object's acceleration naturally approaches zero and the two forces become equal in magnitude:

$$
\textbf{f}_{wind} = - \textbf{f}_{drag}
$$

If this did not occur, we would have the physical situation where an object flowing in the direction of wind would continue to accelerate (in the direction of the wind) as its velocity increases without bound. Another way to think about this situation is that an object flowing in the wind would continue to have increasing **unbounded** kinetic energy and that cannot happen.

Similarly, drag cannot increase in magnitude faster than wind decreases or we end up with the situation where any object that attempts to flow in the wind remains stationary (or ping pongs back and forth as drag responds to drag - this particular behaviour would more likely only be present in a computational model of the previous situation).

From these considerations, we can then describe the theoretical maximum velocity of the object:

$$
\begin{align}
\textbf{f}_{wind} &= - \textbf{f}_{drag}\\
(\text{stuff})\textbf{v}_{rel,wind} &= - (\text{stuff})(-\textbf{v}_{obj})\\
\textbf{v}_{rel,wind} &= \textbf{v}_{obj} \\
\textbf{v}_{wind} - \textbf{v}_{obj} &= \textbf{v}_{obj} \\
\frac{\textbf{v}_{wind}}{2} &= \textbf{v}_{obj}
\end{align}
$$

The "$\text{stuff}$" is a placeholder for the terms present in both forces that must be equal in magnitude for the above consideration: namely, the rate of change of both forces must be equal in magnitude for there to be the situation of zero acceleration at long enough time.

This maximum velocity for the object should also be a theoretical limit in the same sense that terminal velocity (for a free falling object) is a theoretical limit.

### Sense Making: A ball in a tube

Consider a ball in a similarly sized tube with no friction. To the left side of the ball is a section pressurized with a fluid and to the right size of the ball is a vacuum. If we assume the ball and/or tube is lubricated in an idealized way such that friction between the two is negligible, then the only force on the ball is from the pressurized fluid.

Using the method where force is equivalent to pressure times surface area, we can crudely describe our "wind" as:

$$
\textbf{f}_{wind} = P_{gas}\ A_{ball}\ \hat{x}
$$

Where I have mapped the positive $x$ direction to the *right side* of the ball (and the negative $x$ direction is to the left). Recalling that the dimensions of pressure are

$$
\begin{align*}
P &= \frac{[\text{mass}]}{[\text{length}][\text{time}^2]} \\
&= \frac{[\text{mass}]}{\text{length}^3}\cdot\frac{[\text{length}^2]}{[\text{time}^2]}
\end{align*}
$$

Which would lead to the ability to describe pressure as the density of the gas (or liquid) multiplied by the square of its velocity:

$$
P = \rho v^2
$$

This leaves two possible vectors for the pressure to tend to zero:

- the density decreases
- the (relative) velocity of the medium decreases

>[!note] Aside:
>
>Now, I could default to a thermodynamic style of reasoning in that:
>
>"We assume the process introducing more fluid to the pipe is such that the density remains constant."
>
>Which... feels like a cop-out. 
>
>It is not unreasonable to imagine there is a method, albeit likely complicated, that introduces fluid into the pipe in a manner such that the density remains a constant (possibly involving valves at various intervals that open/close based on the ball's location to ensure fluid is being added at the correct rate).
>
>The other approach is "less *cheaty*" by looking at the problem through the lens of an incompressible fluid. Then, by definition, the density must be constant. But I would still need to address the issue of defending why the incompressible case applies to the compressible case.

Instead, I think the stronger (and more intuitive) approach is to use Conservation of Momentum. One of the derivations for pressure involves considering the momentum imparted by each particle against the cross-sectional surface area over a period of time:

$$
P = \frac{\sum_i{\big(\textbf{p}_i\cdot\hat{A}\big)}}{A\Delta t}
$$

or, strictly as a momentum equation:

$$
\Delta\textbf{p} = \textbf{p}_{after} - \textbf{p}_{before}
$$

which becomes:

$$
\textbf{p}_{fluid} + \textbf{p}_{ball,i} = \textbf{p}_{ball,f}
$$

> (The subscripts $i$ and $f$ denote *initial* and *final*).

Now, a more accurate model would account for variable pressure as the fluid flow (in aggregate) remains constant and density varies, but given long enough time scales for the fluid to *even out*, we still approach a pressure of zero as the momentum imparted from the fluid in later and later collisions trends to zero: 

>That is, once the ball has reached a velocity equal to the fluid flow, any subsequent fluid that might interact with the ball will be moving in parallel with the ball (their velocities being equal and the fluid can never *catch up* to the ball).

All of this is to finally state:

>The magnitude of $\textbf{f}_{wind}$ must depend on the difference in velocity between the wind and the object, and given long enough time scales, the ball will reach a maximum velocity as $\textbf{f}_{wind}\rightarrow 0$.


### Sense Making: Adding Drag to the tube

> [!todo]
> 
> Argue ball has max velocity less than that of $\textbf{v}_{wind}$ by looking at pressure difference.
