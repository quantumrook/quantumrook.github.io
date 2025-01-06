---
title: Ideal Gas
created: 5, Nov, 2021
modified:
  - 06, Jan, 2025
---


## Equation of State

### General

$$pV=nRT$$

### Undergoing Adiabatic Process

$$pV^\gamma = constant \qquad\text{or}\qquad V^{\gamma-1}T = constant$$

## Properties

Summary:

  - The internal energy of an ideal gas only depends on its Temperature
  - Entropy stuff

### Internal Energy

> The internal energy for an ideal gas depends only on the temperature: 
> $$E(T)\rightarrow dE\propto T$$

#### Proof

Let us begin by describing the internal energy of a $n$ [moles](/chem/Moles.md) of gas with using by the two standard [state parameters](/physics/Thermodynamics/Systems#State-Parameters.md) $T$ and $V$. We can plausibly claim that there exists some function $E$ that describes the state of the gas using just $T$ and $V$: $E(T,V)$. Taking the [differential](/maths/Differentials.md) of this function, we obtain the following mathematical description:

$$
\newcommand\wrap[2]{\left(#1\right)_{#2}}
\newcommand\pder[2]{\frac{\partial #1}{\partial #2}}
\begin{aligned}
dE &= dE(T,V) \\
&=\wrap{\pder{E}{T}}{V} dT + \wrap{\pder{E}{V}}{T} dV
\end{aligned}
$$

We consider the change in each parameter under the lens of a [quasi-static](/physics/Thermodynamics/Processes#Quasistatic.md) process such that we can utilize the [thermodynamic identity](/physics/Thermodynamics/Functions#Thermodynamic-Identity.md) to write the heat and work as [exact differentials](/maths/Differentials#Exact.md). Solving this expression for [Entropy](/physics/Thermodynamics/Entropy.md), we not only obtain an expression which seems to describe the total differential of $S$, but that entropy can be described by the two state parameters $E$ and $V$:

$$
\newcommand\dbar{{đ}}
\newcommand\wrap[2]{\left(#1\right)_{#2}}
\newcommand\pder[2]{\frac{\partial #1}{\partial #2}}
\newcommand\pdersq[2]{\frac{\partial^2 #1}{\partial {#2}^2}}
\newcommand\mpder[3]{\frac{\partial^2 #1}{\partial #2 \partial #3}}
\begin{aligned}
\dbar Q = TdS, \qquad &\& \qquad \dbar W = -pdV\\
dE &= TdS - pdV \\
\\
TdS &= dE + pdV \\
\\
dS &= \frac{1}{T}dE + \frac{p}{T}dV\quad\Rightarrow S(E,V)
\end{aligned}
$$

And if we can describe entropy as a function of internal energy and volume, we know what the [parital derivatives](/maths/PartialDerivatives.md) of entropy correspond to the coefficients infront of the differentials:

$$
\newcommand\dbar{{đ}}
\newcommand\wrap[2]{\left(#1\right)_{#2}}
\newcommand\pder[2]{\frac{\partial #1}{\partial #2}}
\begin{aligned}
dS(E,V) = \wrap{\pder{S}{E}}{V} dE &+ \wrap{\pder{S}{V}}{E} dV \\
\\
\wrap{\pder{S}{E}}{V} = \frac{1}{T}, \qquad &\& \qquad \wrap{\pder{S}{V}}{E} = p
\end{aligned}
$$

Finally, recall that with mixed partial derivatives, we note that the order in which the derivatives are operated does not matter from [Clairaut's theorem on equality of mixed partial derivatives](/maths/PartialDerivatives#Clairaut's-Theorem.md). Stated mathematically, we have the following expression which allows us to construct our final series of statements to prove that $E$ does not depend on $V$:

$$
\newcommand\wrap[2]{\left(#1\right)_{#2}}
\newcommand\pder[2]{\frac{\partial #1}{\partial #2}}
\newcommand\pdersq[2]{\frac{\partial^2 #1}{\partial {#2}^2}}
\newcommand\mpder[3]{\frac{\partial^2 #1}{\partial #2 \partial #3}}
\begin{aligned}
\mpder{S}{V}{E} &= \mpder{S}{E}{V}\\
\\
\wrap{\pder{}{V}}{E} \wrap{\pder{S}{E}}{V} = \mpder{S}{V}{E} &= \mpder{S}{E}{V} = \wrap{\pder{}{E}}{V} \wrap{\pder{S}{V}}{E}\\
\\
\wrap{\pder{}{V}}{E} \wrap{\pder{S}{E}}{V} &= \wrap{\pder{}{E}}{V} \wrap{\pder{S}{V}}{E}
\end{aligned}
$$

We can then substitute in our expression for the total differential of $E$ in for the $dE$ in the differential of $S$ to re-express the partial derivatives:

$$
\newcommand\dbar{{đ}}
\newcommand\wrap[2]{\left(#1\right)_{#2}}
\newcommand\pder[2]{\frac{\partial #1}{\partial #2}}
\newcommand\pdersq[2]{\frac{\partial^2 #1}{\partial {#2}^2}}
\newcommand\mpder[3]{\frac{\partial^2 #1}{\partial #2 \partial #3}}
\begin{aligned}
dS = \frac{1}{T}dE + \frac{p}{T}dV &= \frac{1}{T}\left[\wrap{\pder{E}{T}}{V} dT + \wrap{\pder{E}{V}}{T} dV\right] + \frac{p}{T}dV\\
&= \frac{1}{T}\wrap{\pder{E}{T}}{V} dT + \left[\frac{1}{T}\wrap{\pder{E}{V}}{T} + \frac{p}{T}\right] dV\\
\\
\wrap{\pder{S}{T}}{V} = \frac{1}{T}\wrap{\pder{E}{T}}{V}, \qquad &\& \qquad \wrap{\pder{S}{V}}{T} = \frac{1}{T}\wrap{\pder{E}{V}}{T} + \frac{p}{T}\\
\\
\wrap{\pder{}{V}}{T} \wrap{\pder{S}{T}}{V} &= \wrap{\pder{}{T}}{V} \wrap{\pder{S}{V}}{T}\\
\wrap{\pder{}{V} \frac{1}{T}\wrap{\pder{E}{T}}{V}}{T} &= \pder{}{T}\left[\frac{1}{T}\wrap{\pder{E}{V}}{T} + \frac{p}{T}\right]_{V} \\
\end{aligned}
$$

Before carrying out these partial derivatve operations, let us use the equation of state for an ideal gas, $pV=nRT$ to express $p/T$ in a simpler form:

$$
\newcommand\wrap[2]{\left(#1\right)_{#2}}
\newcommand\pder[2]{\frac{\partial #1}{\partial #2}}
\begin{aligned}
\frac{p}{T} &= \frac{nR}{V}\Rightarrow \pder{}{T}\wrap{\frac{nR}{V}}{V}=0
\end{aligned}
$$

Follwing the [chain rule](/maths/PartialDerivatives#Chain-Rule.md) and simplifying the results, we obtain our proof:

$$
\newcommand\dbar{{đ}}
\newcommand\wrap[2]{\left(#1\right)_{#2}}
\newcommand\pder[2]{\frac{\partial #1}{\partial #2}}
\newcommand\pdersq[2]{\frac{\partial^2 #1}{\partial {#2}^2}}
\newcommand\mpder[3]{\frac{\partial^2 #1}{\partial #2 \partial #3}}
\begin{aligned}
\frac{1}{T}\wrap{\mpder{E}{T}{V}}{} &= \left[-\frac{1}{T^2}\wrap{\pder{E}{V}}{T} + \frac{1}{T}\wrap{\mpder{E}{T}{V}}{} + 0 \right]\\
0 &= -\frac{1}{T^2}\wrap{\pder{E}{V}}{T}
\end{aligned}
$$

Noting that $T$ is non-zero, we remove the coefficients and find that the partial derivative of internal energy (for an ideal gas) with respect to volume at **constant** temperature is always $0$:

$$
\newcommand\wrap[2]{\left(#1\right)_{#2}}
\newcommand\pder[2]{\frac{\partial #1}{\partial #2}}
\begin{aligned}
\wrap{\pder{E}{V}}{T} &= 0
\end{aligned}
$$

Therefore, we conclude, for an ideal gas, the state of $E$ is completely specified (and solely dependent) on its absolute temperature $T$.

### Entropy

Ideal gas is sometimes referred to as a "perfect gas" (gas molecules do not interact to have any potential energy; all energy comes from kinetic)

Consider $n_0$ moles of an ideal gas that occupies a volume $V_0$ and at the temperature $T_0$. Let $S_0$ be the molar entropy of the gas at this specific macroscopic state (macro state).

> Molar entropy is the entropy of one mole of this gas.

Calculate the entropy $S(T,V,n)$ of the gas at $T$ and $V$.

- start with first law
- solve for dS
- use $dE$ in terms of molar specific heat capcity
  - we can only do this substitution because we have an ideal gas
  - energy does not depend on internal volume
- use $pV=nRT$ to rewrite $p$ in terms of given variables
- integrate
  - approximate that $C_V(T)$ is constant over small change in $T$


$$
\begin{aligned}
\int_{(T_0, V_0)}^{(T,V)}{dS} &= \int_{T_0}^{T}{nC_V(T)\frac{dT}{T}} + \int \\
Sn-S_0 n_0 &= n\left(\ln{\left(\frac{T}{T_0}\right)}^{C_V} + \ln{\left(\frac{V}{V_0}\right)}^R\right) \\
Sn &= n\left(\ln{\left(\frac{T}{T_0}\right)}^{C_V} + \ln{\left(\frac{V}{V_0}\right)}^R\right) + S_0 n_0 \\
S &= \left(\ln{\left(\frac{T}{T_0}\right)}^{C_V} + \ln{\left(\frac{V}{V_0}\right)}^R\right) + S_0\frac{n_0}{n} \\
S(T,V,n) &= n\left(C_V\ln{(T)}+R\ln{(V)}+S_0(T_0,V_0)\right)
\end{aligned}
$$

---

Start with the First Law:

$$
\begin{aligned}
\bar{d}Q &= dE + \bar{d}W
\end{aligned}
$$

In the case the system undergoes a quasi-static process (at each step, the system can be considered at equilibrium)

$$
\begin{aligned}
TdS &= dE + pdV \\
dS &= \frac{1}{T}dE + \frac{p}{T}dV
\end{aligned}
$$

> recall that if we can write a differential as a total differential, we can conclude: $S=S(E,V)$

$$dS = \left(\frac{\partial S}{\partial E}\right)_V dE + \left(\frac{\partial S}{\partial V}\right)_E dV$$

This tells us that the partial derivatives must be equal to the coefficients of the differentials in the statement above:

$$
\begin{aligned}
\left(\frac{\partial S}{\partial E}\right)_V &= \frac{1}{T}\\
\left(\frac{\partial S}{\partial V}\right)_E &= \frac{p}{T}
\end{aligned}
$$


---

# See Also

## External Resources

- *Fundamentals of Statistical and Thermal Physics* by F. Reif
- *Thermodynamics: A complete undergraduate course* by Andrew F. Steane
- *An Introduction to Thermal Physics* by Daniel V. Schroeder