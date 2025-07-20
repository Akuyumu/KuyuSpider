---
tags:
  - y2s2-MA2079
status: Ongoing
---
## Planning the circuitry
Only the model without any circuitry would be a brawn no brains. Here details snippets of our circuit building journey.
### Circuitry schematics
1. A [[V1031 V1039 Li-ion Charger]] with a type-c input is used to charge the [[18650 Li-ion battery]](s)
	1. The [[V1031 V1039 Li-ion Charger]] symbol does not exist so it will be created and named with [[KiCAD Symbol Conventions]]
	2. A [[Misc BMS PCB]] is used interface between the [[18650 Li-ion battery]] and the charging power source + components to power
	3. **The output voltage ranges from 14.4V at low capacity and 16.8V at high capacity**
2. A [[Raspberry Pi 4B]] is used to emulate the [[Raspberry Pico]] as the brain of the system
	1. The [[Raspberry Pico]] cannot exceed 5v/1S voltage
	2. The [[LM2596S-ADJ Buck Converter]] steps down the voltage from 14.4V to 5V ([more details](https://shopee.sg/DC-DC-Buck-Step-Down-Module-LM2596-DC-DC-4.0~40V-to-1.25-37V-Adjustable-Voltage-Regulator-With-LED-Voltmeter-i.161750523.5709524590?xptdk=ff815367-9dbc-419a-8c05-3a13e60d2412))
	3. Power is supplied via VSYS, pin 39
3. The [[L298N Dual H-bridge Motor Driver]] is added for the [[Raspberry Pico]] to interface with the [[RS-550 Brushed DC Motor]]
4. A [[Misc Button]] is added for the user to interface with the product
	1. eg. *click*(turns on at lowest speed). *clicks*(raise speed). *click*(at max speed turns motor off)
![[CircuitSchematic 1.pdf]]
### The circuit - Live & IRL