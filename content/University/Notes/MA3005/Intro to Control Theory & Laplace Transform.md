---
tags:
  - y3s1-MA4832
status: Ongoing
---
# Course Overview
## The aims of this module are to:
- Introduce feedback systems and the concepts of block diagrams and transfer functions and different types of controllers
- Introduce the concept of stability and performance criteria of feedback systems
- Explain the concept of root locus and its application to classical control design
- Introduce frequency response and Bode diagrams-based analysis and design techniques
## Having successfully completed the module, you will be able to:
- determine the step transient response of a system
- determine the frequency response of a system
---
# Types of Control system
## Open loop control
- No feedback, only operator input
## Closed loop control
- Feedback control system automates optimization
![[Pasted image 20250813011632.png]]
---
# Feedback control system
## Regulator system
- Maintain constant output
- Input is seldom changed
![[Pasted image 20250813010008.png]]
## Follow-up system
- set point frequently changed
---
# Application of Control Theory
## Dynamic Analysis
Determination of response of a plant to commands, disturbances and changes in plant parameter
## Control System Design
If dynamic analysis is unsatisfactory and modification of plant is unacceptable, design phase in necessary to select control elements needed to improve dynamic performance to acceptable level
## Method of Analysis
1. Consider system performance in time domain by measuring output response for given input
2. Frequency domain - output response to sinusoidal input is considered in steady state only if transient is allowed to subside before measurement ends
## Requirement of Control Theory
1. Stability
2. Accuracy - in terms of errors
	1. Error - steady state - due to static friction as output ceases to move
	2. Error - can reverse sign, overshoot due to energy
3. Speed of response

> [!NOTE]- Stability and accuracy are incompatible
> A good design is a compromise of both

---
# Systems Classification
## Stationary vs Non-stationary System
Non stationary
- differential / difference eq have one or more coefficients as functions of time

Stationary
- differential / difference eq only have constant coefficient
## Linear vs non linear systems
- principle of superposition holds
## Lumped parameter vs Distributed parameter
Physical characteristics are assumed to concentrate in one or more lumps, independent of spatial distribution

E.g:

| ==bodies==           | rigid          | elastic                |
| -------------------- | -------------- | ---------------------- |
| ==spring==           | massless       | have distributed mass  |
| ==electrical leads== | resistanceless | distributed resistance |

## Continuous vs Discrete variable system

| all system variables are continuous function of time | has one or more variable known only at a particular instant of time |
| ---------------------------------------------------- | ------------------------------------------------------------------- |
| describing equations are differential equations      | equations are difference equations                                  |
|                                                      | e.g. time interval controlled sampled data system                   |


---
# Laplace transforms

# References
![[1-2-Laplace Transform & Block Diagrams-FT- Sem1-2025-26-ver3.pdf]]





