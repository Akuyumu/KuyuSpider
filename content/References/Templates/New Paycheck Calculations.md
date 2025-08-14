---
tags:
  - Finances
  - Work
status: Completed
hoursworked: 
grabclaims: 
---
# Calculations
## Money earned
Hours worked: `INPUT[number:hoursworked]`
Total for the month: `VIEW[{hoursworked} * 13][math]`

## After CPF
Total for the month: `VIEW[{hoursworked} * 13 * 80%][math]`

## Claims and reinbursements
Grab: `INPUT[number:grabclaims]`

# Expected cash in to bank
Cash in bank: `VIEW[({hoursworked} * 13 * 80%)+{grabclaims}][math]`
