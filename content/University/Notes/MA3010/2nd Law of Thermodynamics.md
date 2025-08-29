---
tags:
  - y3s1-MA3010
status: Completed
---
The 2nd Law of thermodynamics is all about the efficiency of heat transfer processes
# Thermal Energy Reservoirs
Hypothetical body with a relatively large ==thermal energy capacity (mass x specific heat)== that can absorb/supply finite amounts of heat without undergoing any change in temperature.

Source - supplies heat energy![[Pasted image 20250813173634.png]]

Sink - absorbs heat energy![[Pasted image 20250813173651.png]]

---
# Heat Engines
Converts heat to work

![[Pasted image 20250813173911.png]]
## Energy Balance
From first law:
$$
Q-W= \Delta U
$$
The energy balance for heat engines is:
$$
W_{net,out}=Q_H-Q_L
$$
## Thermal Efficiency
$$
\text {Thermal Efficiency}=\frac{\text{Net work output}}{\text {Total heat input}}
$$
So for Heat Engines:
$$
\eta_{th} = \frac{W_{net,out}}{Q_H}=1-\frac{Q_L}{Q_H}
$$
## Kelvin-Planck Statement
*It is impossible for any device that operates on a cycle to receive
heat from a single reservoir and produce a net amount of work.
- Even theoretically perfect heat engines do not have an efficiency of 100%

---
# Reverse Heat Engines
Work is added to induce heat transfer from low temperatures to high temperatures

![[Pasted image 20250813175700.png]]
- E.g. Refrigerator / Heat pumps
## Coefficient of performance
$$
\text {Coefficient of Performance}=\frac{\text{Desired output}}{\text{Required input}}
$$
For Refrigerator: Function - to cool refrigerated space
$$
COP_R=\frac{Q_L}{W_{net,in}}=\frac{Q_L}{Q_H-Q_L}=\frac{1}{Q_H/Q_L-1}
$$

For Heat Pump: Function - to warm heated space 
$$
COP_{HP}=\frac{Q_H}{W_{net,in}}=\frac{Q_H}{Q_H-Q_L}=\frac{1}{1-Q_L/Q_H}
$$
## Clausius Statement
*It is impossible to construct a device that operates in a cycle and produces no effect other than the transfer of heat from a lower-temperature body to a higher-temperature body.*

---
# Perpetual Motion Machine
A device that contradicts either the 1st law or 2nd law of thermodynamics

> [!NOTE] Recap
> 1st Law - energy cannot be created or destroyed, only transformed from one form to another
>
> 2nd Law - the entropy, or disorder, of a closed system never decreases

PMM1: Infinite output with no inputs

![[Pasted image 20250823230827.png]]

PMM2: decreasing entropy

![[Pasted image 20250823230930.png]]

---
# Reversible & Irreversible processes
Reversible process - Can be reversed without leaving traces in the surrounding
- E.g frictionless pendulum

Irreversible process - opposite - Most processes in real life

Internally reversible - no irreversibilities occur within system boundaries (red box)

Externally reversible - no irreversibilities occur outside system boundaries (blue box)

Totally reversible - internally + externally reversible (magenta box) 

![[Pasted image 20250813155731.png]]
## Carnot cycle
A theoretical cycle that sets the limits for heat engines, refrigerator and heat pumps

> [!NOTE] Recap
> ![[Pasted image 20250823235649.png]]

(a) Reversible Isothermal Expansion (1-2, T_H = constant)
- Gas expands at constant temp while absorbing heat from energy source

(b) Reversible Adiabatic Expansion (2-3, T_H drops to T_L)
- Gas does work on surrounding and expands while its temp drops

(c) Reversible Isothermal Compression (3-4, T_L constant)
- Gas compression at constant temp while losing heat to energy sink

(d) Reversible Adiabatic Compression (4-1, T_L rises to T_H)
- Work done on gas to compress it and its temp rises


> [!INFO] The reversed carnot cycle
> The carnot cycle is a reversible cycle that nets the "Carnot refrigeration cycle"


![[Pasted image 20250813160632.png]]
## Carnot Principles
1. The efficiency of an irreversible heat engine is always less than the efficiency of a reversible one operating between the same two reservoirs
$$
\eta_{\text{th},1,\text{irrev}} < \eta_{\text{th},2,\text{rev}}
$$
2. The efficiencies of all reversible heat engines operating between the same two reservoirs are the same
$$
\eta_{\text{th},2,\text{rev}} = \eta_{\text{th},3,\text{rev}}
$$
![[Pasted image 20250824162327.png]]

> [!INFO]- Expand for Proof of Carnot Principles
> Part 1
> ![[Pasted image 20250824162532.png]]
> ![[Pasted image 20250824162640.png]]
> Part 2
> ![[Pasted image 20250824162705.png]]
> ![[Pasted image 20250824162802.png]]
 
# Thermodynamic Temperature Scale
A temperature scale that is independent of the properties of substances that are used to measure temperature is called a thermodynamic temperature scale
- Thermal reservoirs are characterized only by their temperatures
$$
T(K) = T(^{\circ}C) + 273.15
$$
$$
\left(\frac{Q_H}{Q_L}\right)_{\text{rev}} = \frac{T_H}{T_L} \quad \text{or} \quad \left(\frac{Q_L}{Q_H}\right)_{\text{rev}} = \frac{T_L}{T_H}
$$
> [!Info]- Derivation of the scale
> ![[Pasted image 20250824164256.png]]
> ![[Pasted image 20250824164311.png]]
> ![[Pasted image 20250824164324.png]]

---
# Carnot devices
AKA ideal / most efficient devices based on carnot principles
## Carnot heat engine
Thermal efficiency of a *Carnot heat engine*
$$
\eta_{th,\text{rev}} = 1 - \frac{T_L}{T_H}
$$
*!! absolute temps only !!*
![[Pasted image 20250824171153.png]]

## Carnot refrigerator & heat pump
Coefficient of performance for a *Carnot refrigerator*:
$$
\text{COP}_{R,\text{rev}} = \frac{1}{T_H/T_L - 1}
$$
Coefficient of performance for a *Carnot heat pump*:
$$
\text{COP}_{HP,\text{rev}} = \frac{1}{1 - T_L/T_H}
$$
![[Pasted image 20250824171725.png]]

---
# References
![[MA3010 Lecture 1.pdf]]
