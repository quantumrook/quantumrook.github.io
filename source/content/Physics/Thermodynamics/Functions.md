---
title: Thermodynamic Functions
created: 5, Nov, 2021
modified:
  - 06, Jan, 2025
---

The following are potential energies that can be added to the Thermodynamic Identity to alter the parameterization of internal energy to better reflect the state variables of a [process](/physics/Thermodynamics/Processes.md) or system.

## Thermodynamic Identity

$$E(S,V)$$

Internal energy $E$ is defined in terms of state variables $S$ and $V$, which leads to the standard parameterization of:

$$\newcommand\wrap[2]{\left(#1\right)_{#2}}
\newcommand\pder[2]{\frac{\partial #1}{\partial #2}}\begin{aligned}
dE(S,V) &= \wrap{\pder{E}{S}}{V} dS + \wrap{\pder{E}{V}}{S} dV\\
\\
dE &= T dS - p dV
\end{aligned}$$

## Enthalpy

$$H(S,p)\equiv E+pV$$

$$\newcommand\wrap[2]{\left(#1\right)_{#2}}
\newcommand\pder[2]{\frac{\partial #1}{\partial #2}}
\begin{aligned}
TdS &= dE + pdV \\
dE &= TdS - pdV - Vdp + Vdp \\
dE &= TdS - d(pV) + Vdp \\
dE + d(pV) &= TdS + Vdp \\
d(E+pV) &= TdS + Vdp\\
dH &= TdS + Vdp\\
\\
dH &= \wrap{\pder{H}{S}}{p} dS + \wrap{\pder{H}{p}}{S} dp \\
\\
\wrap{\pder{H}{S}}{p} &= T \\
\wrap{\pder{H}{p}}{S} &= V
\end{aligned}$$

This gives us the following [Maxwell Relation](/physics/Thermodynamics/Maxwell.md):

$$\newcommand\wrap[2]{\left(#1\right)_{#2}}
\newcommand\pder[2]{\frac{\partial #1}{\partial #2}}
\wrap{\pder{T}{p}}{S} = \wrap{\pder{V}{S}}{p}$$

## Helmholtz

$$F(T,V)\equiv E - TS$$

$$\newcommand\wrap[2]{\left(#1\right)_{#2}}
\newcommand\pder[2]{\frac{\partial #1}{\partial #2}}
\begin{aligned}
TdS &= dE + pdV \\
dE &= TdS - pdV - SdT + SdT\\
dE &= d(TS) - pdV - SdT\\
d(E-TS) &= - SdT- pdV\\
dF &= - SdT - pdV\\
\\
dF &= \wrap{\pder{F}{T}}{V} dT + \wrap{\pder{F}{V}}{T} dV \\
\\
\wrap{\pder{F}{T}}{V} &= -S \\
\wrap{\pder{F}{V}}{T} &= -p
\end{aligned}$$

This gives us the following [Maxwell Relation](/physics/Thermodynamics/Maxwell.md):

$$\newcommand\wrap[2]{\left(#1\right)_{#2}}
\newcommand\pder[2]{\frac{\partial #1}{\partial #2}}
\wrap{\pder{S}{V}}{T} = \wrap{\pder{p}{T}}{V}$$

## Gibbs

$$G(T,p)\equiv E - TS + pV$$

Alternatively, we could also define $G$ by either $G\equiv F +pV$ or $G\equiv H-TS$.

$$\newcommand\wrap[2]{\left(#1\right)_{#2}}
\newcommand\pder[2]{\frac{\partial #1}{\partial #2}}
\begin{aligned}
TdS &= dE + pdV \\
dE &= TdS - pdV - SdT + SdT - Vdp + Vdp\\
dE &= d(TS) - d(pV) + Vdp - SdT\\
d(E-TS+pV) &= - SdT + Vdp\\
dG &= - SdT + Vdp\\
\\
dG &= \wrap{\pder{G}{T}}{p} dT + \wrap{\pder{G}{p}}{T} dp \\
\\
\wrap{\pder{G}{T}}{p} &= -S \\
\wrap{\pder{G}{p}}{T} &= V
\end{aligned}$$

This gives us the following [Maxwell Relation](/physics/Thermodynamics/Maxwell.md):

$$\newcommand\wrap[2]{\left(#1\right)_{#2}}
\newcommand\pder[2]{\frac{\partial #1}{\partial #2}}
-\wrap{\pder{S}{p}}{T} = \wrap{\pder{V}{T}}{p}$$

---

# See Also

## External Resources

- *Fundamentals of Statistical and Thermal Physics* by F. Reif
- *Thermodynamics: A complete undergraduate course* by Andrew F. Steane
- *An Introduction to Thermal Physics* by Daniel V. Schroeder
