---
tags:
  - y3s1-MA3010
status: Ongoing
---
# Entropy & Clausius Inequality
Entropy is a *property*
- A measure of the degree of microscopic disorder in the system
- Entropy can be transferred by heat but not by work
- Entropy is not conserved
- Entropy can be generated/created but not destroyed
- Total entropy for isolated systems (system + surroundings) increases for all real processes
## Clausius Inequality
Cyclic integral of 𝛿𝑄/𝑇 is always less than or equal to zero for all cycles regardless of reversible, irreversible cycles
$$\oint \frac{\delta Q}{T} \leq 0$$
- Unit for T must be absolute temperature
### For reversible cycles
Example: Carnot Heat Engine
$$\oint \frac{\delta Q}{T}_{rev} = 0$$
### For irreversible cycles
Example: Any other heat engine
$$\oint \frac{\delta Q}{T}_{irrev} \lt 0$$

> [!tip] Generally, cyclic integrals of any property is zero
> Hence Entropy is a property:
> $$dS = \left(\frac{\delta Q}{T}\right)_{\text{int rev}} \quad (\text{kJ/K})$$

---
# Entropy of Pure Substances
Entropy data for pure substances (including real gases) can be obtained from property tables
## Obtaining Entropy change (using property table)
The difference between the entropy of the initial state vs the finals state
$$\Delta S = S_2 - S_1 = m(s_2 - s_1)$$
** Interpolation may be needed

![[Pasted image 20250915024913.png|400]]

---
# Property Diagrams Involving Entropy
2nd Law analysis: T-s & h-s diagrams

## Analysing T-s Diagrams
Differential form of entropy:
$$
dS = \left(\frac{\delta Q}{T}\right)_{\text{int rev}} \quad (\text{kJ/K}) \quad \rightarrow \delta Q_{\text{int rev}} = T dS \quad (\text{kJ})
$$
$$ \text{Or: } \quad \delta q_{\text{int rev}} = T ds \quad (\text{kJ/kg}) $$
Integrating entropy:
$$ Q_{\text{int rev}} = \int_1^2 T dS \quad (\text{kJ}) \qquad q_{\text{int rev}} = \int_1^2 T ds \quad (\text{kJ/kg})$$

> [!tip]
> Area under the process curve in the T-s diagram represents the heat transfer in an internally reversible process!

![[Pasted image 20250915030918.png|200]]
## Special conditions
### Internally reversible isothermal process
$$Q_{\text{int rev}} = T_0 \Delta S \quad (\text{kJ})$$
$$q_{\text{int rev}} = T_0 \Delta s \quad (\text{kJ/kg})$$

![[Pasted image 20250915031340.png|400]]
### Isentropic process
Constant entropy — vertical line segment

![[Pasted image 20250915031415.png|400]]

---
# *Tds* Relations (Entropy change without Property table)
## 1st Tds Equation (Gibbs Equation)
$$ TdS = dU + PdV \quad \text{or} \quad \boxed{Tds = du + Pdv}$$

> [!NOTE]- Expand for Derivation
> ![[Pasted image 20250915220939.png]]

## 2nd Tds Equation 
$$Tds = dh - vdP$$
Alternative forms:
$$\boxed{ds = \frac{du}{T} + \frac{Pdv}{T}} \quad \boxed{ds = \frac{dh}{T} - \frac{vdP}{T}}$$
> [!NOTE]- Expand for Derivation
> ![[Pasted image 20250915221254.png]]


---
# Entropy Change of Liquids & Solids
Liquids and solids can be approximated as incompressible substances, hence: 
- 𝑑𝑣 ≅ 0
- $ds = \frac{du}{T} + \frac{\cancel{Pdv}}{\cancel{T}} \longrightarrow \quad ds = \frac{du}{T} = \frac{cdT}{T}$
- $c_p = c_v = c \quad \longrightarrow du = cdT$
## Thus, the formula:
$$ s_2 - s_1 = \int_1^2 c(T) \frac{dT}{T} \approx c_{\text{avg}} \ln \frac{T_2}{T_1} \quad \text{(kJ/kg} \cdot \text{K)}$$
- Entropy change for liquids and solids are only dependent on temperature and independent of pressure
## For isentropic
$$\Delta s = 0, \quad \Delta T = 0$$

---
# Entropy Change of Ideal Gases
## Ideal gas equations
$Pv = R_{sp}T \quad PV=mR_{sp}T \quad PV=nR_uT \quad du = c_v dT \quad dh = c_p dT$

where:

$R_u = 8.314J/mol \cdot K \quad R_{sp} = \frac{R_u}{\text{Molar Mass}}$

## Thus, the formulas:
$$ \boxed{s_2 - s_1 = c_{v,avg} \ln \frac{T_2}{T_1} + R_{sp} \ln \frac{v_2}{v_1}} \quad \boxed{s_2 - s_1 = c_{p,avg} \ln \frac{T_2}{T_1} - R_{sp} \ln \frac{P_2}{P_1}}$$
Note:                  $c_{avg} \neq ½(c_1+c_2)$     $c_{avg}=c@T_{avg}$

> [!NOTE]- Expand for Derivation
> ![[Pasted image 20250916012426.png]]
> ![[Pasted image 20250916012441.png]]
## For isentropic
$$ \Delta s=0$$
### From 1st Tds equation
$$ \boxed{\left(\frac{T_2}{T_1}\right)_{isen} = \left(\frac{v_1}{v_2}\right)^{k-1}}$$

> [!NOTE]- Expand for Derivation
> ![[Pasted image 20250916013151.png]]
### From 2nd Tds equation
$$\boxed{\left(\frac{T_2}{T_1}\right)_{isen} = \left(\frac{P_2}{P_1}\right)^{\frac{k-1}{k}}}$$

> [!NOTE]- Expand for Derivation
> ![[Pasted image 20250916013522.png]]
### Combined
$$\boxed{\left(\frac{P_2}{P_1}\right)_{isen} = \left(\frac{v_1}{v_2}\right)^k} \quad \text{or} \quad \boxed{Pv^k = \text{const}}$$

---
# Entropy Change for Reversible Processes
## Internally reversible isothermal heat transfer

$$ \Delta S = \int_1^2 \left(\frac{\delta Q}{T}\right)_{\text{int rev}} = \int_1^2 \left(\frac{\delta Q}{T_0}\right)_{\text{int rev}} = \frac{1}{T_0} \int_1^2 (\delta Q)_{\text{int rev}}$$
$$\boxed{\Delta S = \frac{Q}{T_0} \quad \text{(kJ/K)}}$$
- Where T0 is the constant temperature (K), Q is the heat transfer for the internally reversible process
- Commonly used to determine the entropy change of thermal energy reservoirs that supply/absorb heat indefinitely at constant temperature

---
# Entropy Change for Irreversible Processes

---
