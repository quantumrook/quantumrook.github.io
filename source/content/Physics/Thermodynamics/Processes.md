---
title: Thermodynamic Processes
created: 5, Nov, 2021
modified:
  - 06, Jan, 2025
---

## Quasistatic

> [!summary] Definition: 
> A process that describes a sequence of equilibrium states. Changes to the constraints of the system are performed *slow enough* such that the system can be considered to be in equilibrium throughout the process. *Slow enough* is defined to be when the times involved are greater than the thermal relaxation of the system.

> [!example]
> A system undergoing *sufficiently* slow compression or expansion.

Quasistatic processes allow us to define functions of Work $W$ and Heat $Q$ such that $\newcommand\dbar{đ}\dbar W$ and $\newcommand\dbar{đ}\dbar Q$ become exact differentials in the [First Law](/physics/Thermodynamics/ThermoLaws#The-First.md), namely:

$$\newcommand\dbar{đ}\dbar Q\equiv TdS\qquad\&\qquad\dbar W\equiv -pdV$$

## Reversible and Irreversible

### Reversible

 >[!summary] Definition 
 >A reversible process is one such that the system can be restored to its initial state without any net change in the rest of the universe. E.g., a process that leaves the total entropy of the universe unchanged would be reversible.

>[!note] All reversible processes are quasistatic.
**Caution:** This is not an *if and only if*: Reversible implies quasistatic; quasistatic **does not** imply reversible.

### Irreversible

> [!summary] Definition: 
> The contra of a reversible process: A process that changes the total entropy of the universe by creating new entropy.

E.g. A free-expansion of gas is a Quasistatic Irreversible process.

## Iso and Adia

### Isothermal

> [!summary] Definition: 
> A process that occurs at constant Temperature. $$T = constant$$

### Adiathermal

> [!summary] Definition: 
> A process occurring to a system that is thermally isolated. These processes ***usually*** change the Temperature of the system.

E.g., A gas is compressed quasistatically by a piston inside an Thermally Insulated container. No heat is exchanged between the gas, container, or piston; but the compressed volume for the gas corresponds to an increase in temperature:

$$\newcommand\dbar{đ} dE = 0\Rightarrow 0 = \dbar Q + \dbar W\Rightarrow TdS = pdV$$

### Isentropic and Adiabatic

>[!summary] Definition: 
>A process in which the entropy does not change. $$S=constant$$

E.g., a Reversible Adiathermal process.

>[!note] 
>The definition of Adiabatic is not well agreed upon. The working definition given for PH424 is that an Adiabatic process is one in which heat is not transferred.

### Isobaric

>[!summary] Definition:
>A process in which the Pressure does not change. $$p=constant$$

### Isochoric

>[!summary] Definition:
>A process in which the Volume does not change. $$V=constant$$

---

# See Also

## External Resources

- *Fundamentals of Statistical and Thermal Physics* by F. Reif
- *Thermodynamics: A complete undergraduate course* by Andrew F. Steane
- *An Introduction to Thermal Physics* by Daniel V. Schroeder

