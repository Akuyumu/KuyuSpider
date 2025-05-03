---
tags:
  - y2s2-MA2005
status: Completed
---
# Orthographic Projection
## Drawing Standards
Line types:
- Visual Aid
    
    ![[References/Images/image 17.png|image 17.png]]
    
    ![[References/Images/image 1 2.png|image 1 2.png]]
    
|   |   |   |
|---|---|---|
|A|Thick Continuous|Visible outlines & Edges|
|B|Thin Continuous|Dimension, Projection line, Hatching line|
|C|Thin Short dashes|Hidden outlines & Edges|
|D|Thin Chain|Centre lines, Pitch lines|
|E|Thin Chain, Thick Ended|Cutting plane|
|F|Thin continuous Irregular|Limits of partial view / sections|
|G|Thin chain short double dashes|Outlines of adjacent parts. Alternative and extreme positions of movable parts. Initial outlines prior to forming.|
## Precedence of Line
Visible line > Hidden line > Center line
- Hidden line - Thin short dashes
    
    ![[References/Images/image 2 2.png|image 2 2.png]]
    

> [!important] Intersections of hidden lines should form L, T, V or Y corners
---
- Centre lines - for symmetrical axis, bolt circles and path of motion
    
    ![[References/Images/image 3 2.png|image 3 2.png]]
    
    ![[References/Images/image 4 2.png|image 4 2.png]]
    

> [!important] can be thin continuous line for small hole
---
  
## Orthographic Systems
- First angle Projection
    
    ![[References/Images/image 5 2.png|image 5 2.png]]
    
- Third angle Projection
    
    ![[References/Images/image 6 2.png|image 6 2.png]]
    
- ISO Projection Symbols
    
    ![[References/Images/image 7 2.png|image 7 2.png]]
    

> [!important] First angle is projected past the sight-line while third angle is projected back towards the sight-line
## Isometric Drawing
Isometric — all angles are equal (30$\degree$to horizontal)
**True-length distances** are shown along isometric lines
**Hidden lines** should be omitted unless absolutely necessary to completely describe the object
  
## Visualising Orthographic Views
A straight, visible or hidden line means:
- Edge between two surfaces
- Edge view of a surface
- Limiting element of a curved surface
### Normal surface
Parallel to plane of projection
- **True shape** is projected onto that plane
    
    ![[References/Images/image 8 2.png|image 8 2.png]]
    
### Inclined surface
Perpendicular to one plane of projection but inclined to adjacent planes
- **Edge view - True length** on perpendicular plane
    
    ![[References/Images/image 9 2.png|image 9 2.png]]
    
- Same shape; same no. of sides on adjacent planes
### Oblique surface
Inclined to all principle planes
- does not appear true size in any standard view
    
    ![[References/Images/image 10 2.png|image 10 2.png]]
    
- Parallel edges on the object appear parallel on all views
## Holes & Threads
![[References/Images/image 11 2.png|image 11 2.png]]
  
![[References/Images/image 12 2.png|image 12 2.png]]
  
![[References/Images/image 13 2.png|image 13 2.png]]
- Threaded hole drawing
    
    ![[References/Images/image 14 2.png|image 14 2.png]]
    
- External thread drawing
    
    ![[References/Images/image 15 2.png|image 15 2.png]]
    
## Sectioning

> [!important] To show internal features clearly, minimising hidden lines
### Full Sectioning
Features
- Features shown — behind cutting plan
- **No hidden lines**
- No need to section parts with **no interior details** (e.g. Shaft, screws, bolts)
    - Particularly ribs and lugs — unless transversely cut
Hatching
- Hatched area should be completely bounded by outline
- Same part — hatch in same direction & spacing
- Hatching should not be parallel to outline
- Thin parts can be completely black — gaps between thin parts needed for clarity
Special cases
- Lugs
    
    ![[References/Images/image 16 2.png|image 16 2.png]]
    
- Ribs
    
    ![[References/Images/image 17 2.png|image 17 2.png]]
    
- Spoke
    
    ![[image 18.png]]
    
### Offset Section

> [!important] To show internal details that lie on more than 1 parallel plane
### Half Section
- **Center line** seperates sectioned half from unsectioned half
- **Hidden line** is omitted in unsectioned half
    
    ![[image 19.png]]
    
### Aligned section
![[image 20.png]]
### Revolved section
![[image 21.png]]
## True length
### By Aux view
![[image 22.png]]
  
![[image 23.png]]
### Identifying TL
![[image 24.png]]
### Finding True Shape
1. Identify line with **True Length**
2. Aux view perpendicularly to that line to find **edge view** (where plane is seen as a line)
3. Aux view parallel to edge view to find true shape
![[image 25.png]]
### Others
Dihedral Angle: Angle between two planes
- Angle between edge views
Shortest distance
- Length between point(view) and line
True angle
## Auxiliary Projection
### First vs Third angle
![[image 26.png]]
Views are the same, only relative position is changed
## Dimensioning & Annotations

> [!important] ISO R129 (Dimensioning) & ASME Y14.5 (GD&T)
Basic Information
Size & location of features — Material — Number required
Higher level Information
Tolerances (size and geometric) — Surface roughness — Assembly process description
Dimensioning practices
![[image 27.png]]
- Radius
    
    ![[image 28.png]]
    
- Spheric
    
    ![[image 29.png]]
    
- Chamfer
    
    ![[image 30.png]]
    
- Taper / slope
    
    ![[image 31.png]]
    
- Keyway
    
    ![[image 32.png]]
    
- Diameter
    
    ![[image 33.png]]
    
- Arc / Chord
    
    ![[image 34.png]]
    
- Square / flat
    
    ![[image 35.png]]
    
- Undercut
    
    ![[image 36.png]]
    
- Equally spaced repeated
    
    ![[image 37.png]]
    
### Dimensioning practices (ISO R129)
1. R for arcs (<180) — $\varnothing$ for circles (>180) — SR/$S\varnothing$ for spherical radius / diameter
2. Don’t dimension hidden lines — pick views that show it’s true size and shape
    1. Dimension on views that show the **contour**
3. Ensure all dimensions are accounted for — avoid over/under dimensioning
4. Only **angles have units**
5. Reference dimensions require parenthesis (xx)
6. Locate circular features by dimensioning to centerline
7. Use **centerline for symmetry**
8. Dimension circles on side view > front view for clarity
### Dimensioning appearance (ISO R129)
1. Value should be written **above dimension line — with offset**
2. Put values/arrows outside extension line if not enough space
3. Dimensions should be **outside the view** — unless it **improves clarity**
4. Extension lines should have a **visible gap from view** and **extend beyond** dimension line
5. Extension and Dimension lines **should not cross**
    1. Extension lines can cross
6. **Line up dimension lines** as much as possible
7. Extension lines & notes should be drawn nearest to point of interest