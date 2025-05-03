---
tags:
  - y2s2-MA2005
status: Completed
---
## Limits and Fits
### Limits terminology
1. **Basic size** = Theoretical size — e.g. 48.00
    1. **MMC for shaft/hole — Nicest value / least d.p**
2. **Tolerance notation** — 48.00 ± 0.02
3. **Tolerance** = difference between limits of size — e.g. 0.04
4. **Limits of size** = Largest and Smallest size permitted — 48.02 (largest) 47.98 (smallest)
5. **Actual size** = measured size
6. **Maximum material condition (MMC)** — limit of size resulting in maximum material involved
7. **Minimum material consition (LMC)** — limit of size resulting in minimum material involved
### Fits terminology
1. Clearance fit — worst case scenario will still have clearance — size range do not overlap
2. Interference fit — all cases have interference — size range always overlap
3. Transition fit — cases can either have clearance or interference — partial overlap of size range
4. Upper deviation = $\text{max limit of size} - \text{basic size}$
5. Lower deviation = $\text{lower limit of size} - \text{basic size}$
6. Fundamental deviation — deviation closest to basic size
7. Allowance = $\text{min hole}-\text{max shaft}$
## GD&T Fundamental
![[References/Images/image 103.png|image 103.png]]
![[References/Images/image 1 6.png|image 1 6.png]]
![[References/Images/image 2 6.png|image 2 6.png]]
![[References/Images/image 3 6.png|image 3 6.png]]
![[References/Images/image 4 6.png|image 4 6.png]]
![[References/Images/image 5 6.png|image 5 6.png]]
![[References/Images/image 6 6.png|image 6 6.png]]
## Surface texture
![[References/Images/image 7 6.png|image 7 6.png]]
### Notations
- Specifying max roughness
    
    ![[References/Images/image 8 6.png|image 8 6.png]]
    
- Removal of material instructions
    
    ![[References/Images/image 9 6.png|image 9 6.png]]
    
- Lay symbol =
    
    ![[References/Images/image 10 6.png|image 10 6.png]]
    
- Lay symbol X (honing)
    
    ![[References/Images/image 11 6.png|image 11 6.png]]
    
- Lay symbol C (turning)
    
    ![[References/Images/image 12 6.png|image 12 6.png]]
    
  
- Specifying max & min roughness
    
    ![[References/Images/image 13 5.png|image 13 5.png]]
    
- Machining allowance
    
    ![[References/Images/image 14 5.png|image 14 5.png]]
    
- Lay symbol $\perp$ (grinding / shaping)
    
    ![[References/Images/image 15 5.png|image 15 5.png]]
    
- Lay symbol M (lapping)
    
    ![[References/Images/image 16 5.png|image 16 5.png]]
    
- Lay symbol R
    
    ![[References/Images/image 17 5.png|image 17 5.png]]
    
  
## Tolerances
### Form tolerances
Straightness

> For parallel **line element** on surface, its allowed to **vary in depth** within straightness tolerance
- **Flatness:** Same as straightness but for surface
Virtual condition (VC)
VC = MMC (Shaft) + Geometric tolerance
- The modifier $\text{\textcircled {M}}$ allows the feature surface(s) to exceed the maximum material boundary by the amount of form tolerance, meaning that VC = MMC + tolerance.
Angularity

> Deviation of the angle of a feature — e.g. center line of hole
- Parallelism and Perpendicularity is similar
### Location tolerance
Position
$$\text{Positional tolerance} = \sqrt{\text{horizontal tolerance band}^2-\text{vertical tolerance band}^2}$$