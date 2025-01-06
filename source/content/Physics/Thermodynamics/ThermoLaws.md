---
title: Thermodynamic Laws
created: 5, Nov, 2021
modified:
  - 06, Jan, 2025
---

There are four laws for (Macroscopic) Thermodynamics:

1. The Zeroth Law
2. The First Law (Energy conservation)
3. The Second Law (Entropy Increases)
3. The Third Law (Minimal Entropy)

## The Zeroth

> If two thermodynamic systems are each in thermal equilibrium with a third system, then they are in thermal equilibrium with each other.

## The First

> An equilibrium macrostate of a system can be characterized by a quantity $E$, called internal energy, which has the property that for an isolate system, $E$ is conserved.

If the system is allowed to interact (and transition from one macrostate to another), the resulting change of internal energy can be expressed by: $E = Q + W$

The total differential of $E$ is then expressed as:

$$\newcommand\dbar{đ} dE = \dbar Q + \dbar W$$

- Conservation of Energy
- $E$ is the internal energy of the system
  - $dE$ is a change of the internal energy ([exact](/maths/Differentials.md) & total differential)
  - a function of the state of the system
    - E.g., for a gas in a bottle, the state of the system is described by number of molecules, volume, and temperature.
- $W$ is work
  - $\newcommand\dbar{đ}\dbar W$ is an [inexact](/maths/Differentials.md) differential
  - The work you have to do is not determined by the state of the system; but by the process.
  - Not a state function
- $Q$ is heat transfer
  - $\newcommand\dbar{đ}\dbar Q$ is the heat absorbed by the system.


## The Second

We can quantify the macroscopic state of a system using [Entropy](/physics/Thermodynamics/Entropy.md).

>For an isolated system: $$\Delta S_{system} \geq 0$$

Entropy characterizes the direction of natural processes; E.g., heat cannot (naturally) transfer from a colder body to a hotter body.

If the system is not isolated and undergoes a quasistatic infinitesimal process in which it absorbs heat $\newcommand\dbar{đ}\dbar Q$, then:
$$\newcommand\dbar{đ}dS=\frac{\dbar Q}{T} \Leftrightarrow TdS=\dbar Q$$

## The Third

The limiting property of entropy:

> As the temperature of a system approaches absolute zero, all processes cease and the entropy of the system approaches a minimum value.  $$T\rightarrow 0_+,\qquad S\rightarrow S_0 = 0$$

---

# See Also

## External Resources

- *Fundamentals of Statistical and Thermal Physics* by F. Reif
- *Thermodynamics: A complete undergraduate course* by Andrew F. Steane
- *An Introduction to Thermal Physics* by Daniel V. Schroeder
