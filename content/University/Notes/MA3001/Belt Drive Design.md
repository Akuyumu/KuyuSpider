---
tags:
  - y3s1-MA3001
status: Completed
---
# Basic Layout
![[Pasted image 20250814170550.png]]
- Belt has high tension
- One side is tight the other has slack
- *Friction is key*
# Types of Belt Drives
![[Pasted image 20250814170713.png]]
## Advantages & Disadvantages

| Traits                      | Flat | Round | V   | Timing |
| --------------------------- | ---- | ----- | --- | ------ |
| Suitable for Long Distance  | ✅    | ✅     |     |        |
| Does not Slip and creep     |      |       |     | ✅      |
| Minimal noise               | ✅    |       |     |        |
| Absorbs torsional vibration | ✅    |       |     |        |
| High efficiency (98%)       | ✅    |       |     |        |
| Good for power transmission |      |       | ✅   |        |
| Good for precision          |      |       |     | ✅      |
## Timing Belts
Made of - rubberized fabric and steel wire  
Best for - transmitting power at a constant angular velocity ratio
- Suitable for precision applications
## V-Belts
Synthetic or steel tensile cords encased in an outer jacket
- Cords - tensile strength and flexing
- Lower rubberized area - withstand compression
- Outer fabric jacket - protection from moisture, heat and dust  

V-shape allow tighter wedging - increase friction - higher torque

> [!NOTE]- Multiple belts increase power transmission!
> As many as 12 or more can be used on a single sheave

![[Pasted image 20250814172625.png]]
### V-belt Standards and Size
![[Pasted image 20250814173446.png]]
### V-belt sheaves with prebored holes
![[Pasted image 20250814173929.png]]
### V-belt sheaves with removable hubs
![[Pasted image 20250814174012.png]]
### Sheave groove
Its normally 32 - 38°, smaller than the 40° of the belt
- This forces the belt to wedge in tighter
![[Pasted image 20250814174745.png]]

---
# Speed and direction
## Speed ratio
$$
\text{SR(Speed Ratio)}=\frac{\eta_1}{\eta_2}=\frac{\omega_1}{\omega_2}=\frac{R_2}{R_1}=\frac{D_2}{D_1}
$$
![[Pasted image 20250815011947.png]]
## Belt drive geometry
$$
\alpha = sin^{-1}(\frac{D_2-D_1}{2C})
$$
![[Pasted image 20250814175527.png]]
## Belt Pitch Length
L = 2 arcs + 2 straight tangent over pitch circles
$$
L=2C+1.57(D_2+D_1)+\frac{(D_2-D_1)^2}{4C}
$$
![[Pasted image 20250814175932.png]]
## Center distance & Angle of Contact
Center distance:
$$
C=\frac{B+\sqrt{B^2-32(D_2-D_1)^2}}{16}
$$
$\text{where  }B=4L-6.28(D_2+D_1)$ 
Angle of contact - on small sheave:
$$
\theta_1=180\degree - 2sin^{-1}(\frac{D_2-D_1}{2C})
$$
- θ1 should be > 120° to prevent slippage
![[Pasted image 20250814180803.png]]
## Length of span between sheaves, Ls
- Determines tendency of belt vibration / whipping
![[Pasted image 20250814181117.png]]

---
# Guidelines for Design of Belt Drives
1) Belt speed > 33m/s requires special sheaves
	1) Belt speed < 5m/s consider other drives
2) Max speed ratio = 3.0
3) Angle of contact on Smaller Pulley > 120° to avoid slipping
4) Recommended centre distance: $D_2<C<3(D_2+D_1)$
	1) to prevent belt slip / whip

![[Pasted image 20250815004234.png]]

---
# Selection of Belts & Sheaves
1) Select minimum belt cross section
2) Select standard pulley sizes (pitch diameter)
3) Specify belt pitch length
4) Determine the number of belts required
$$
\text{No of belts}=\frac{\text{Design Power}}{\text{Corrected Rated Power}}
$$
## Design power - to select minimum belt cross section
$$
\text{Design Power}=\text{service factor}*\text{actual drive power (KW)}
$$
Service factor - from ==Table A-2==  
Actual drive power - power requirement of driven machine  

![[Pasted image 20250815010158.png]]
## Corrected Rated Power
The actual configuration of the belt drive can be different from that used by the manufacturer to test the belt for its rated power. The manufacturer used the same diameter for the driving and driven pulleys, and a certain belt length.
$$
\text{Corrected Rated Power}=C_\theta C_L*\text{Rated Power}
$$
- Rated power - standard value from manufacturer power rating table
- Cθ & CL - from ==table A-5 & A-6==

---
# FBD of belt drive
![[Pasted image 20250815012446.png]]

For typical applications, the tight and slack tensions F1 and F2 are assumed to be parallel:

![[Pasted image 20250815012753.png]]

---
# References
![[MA3001 Part 1 - Intro & Belt Drives July 2019.pdf]]

---
Return to [[MA3001 Machine Element Design - Home]]
