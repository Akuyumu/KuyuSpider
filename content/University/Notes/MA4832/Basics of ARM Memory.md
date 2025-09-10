---
tags:
  - y3s1-MA4832
status: Ongoing
---
# Binary logic devices
## Binary Logic Notation

| Gate | Notation 1      | Notation 2              | Notation 3     | Notation 4  | Notation 5 |
| ---- | --------------- | ----------------------- | -------------- | ----------- | ---------- |
| NOT  | $A'$            | $\sim A$                | $\overline{A}$ | $\neg A$    |            |
| AND  | $AB$            | $A \cdot B$             | $A * B$        | $A \land B$ | $A \cap B$ |
| OR   | $A+B$           | $A \vee B$              | $A \cup B$     |             |            |
| NAND | $(AB)'$         | $\overline{AB}$         |                |             |            |
| NOR  | $(A+B)'$        | $\overline{A+B}$        |                |             |            |
| XOR  | $A \oplus B$    | $A @ B$                 |                |             |            |
| XNOR | $(A \oplus B)'$ | $\overline{A \oplus B}$ | $(A @ B)'$     | $A @ B$     |            |
## Logic Gates

| Logic Type | Logic Gate Symbol                    | Purpose                                 | Design of Not Gate                   |
| ---------- | ------------------------------------ | --------------------------------------- | ------------------------------------ |
| NOT        | ![[Pasted image 20250825215630.png]] | Reverses the logic                      | ![[Pasted image 20250825215836.png]] |
| AND        | ![[Pasted image 20250825215950.png]] | Only if both input = 1, then output = 1 | ![[Pasted image 20250825220039.png]] |
| OR         | ![[Pasted image 20250825220137.png]] | If any input = 1, output = 1            | ![[Pasted image 20250825220301.png]] |
| XOR        | ![[Pasted image 20250825220319.png]] | If only 1 input = 1, output = 1         | ![[Pasted image 20250825220435.png]] |
| XNOR       | ![[Pasted image 20250825220515.png]] | inverse of XOR                          | ![[Pasted image 20250825220604.png]] |

---
# Registers
## Single bit device
![[Pasted image 20250830225338.png]]
### Clock Signals (enable)
Also know as the *Rising Edge Trigger*
- Only during an enable/rising-edge, will data be copied over from input to output
![[Pasted image 20250830225746.png]]

## 8-bit register
Basically 1-bit register x 8 to form a byte

![[Pasted image 20250830230522.png]]
### Shift register
When an input is received, the output is "shifted" to other registers to create a parallel output

![[Pasted image 20250830230418.png]]

---
# Memory Contruction
## SRAM: Single bit static RAM
Storage is retained when power is cut
- e.g. solid state disk
- Drawback: cost

![[Pasted image 20250902104822.png]]

## DRAM: Single bit dynamic RAM
Data is loss upon power loss

![[Pasted image 20250902105131.png]]

Data bus: each bit has its own data line

![[Pasted image 20250902105228.png]]

## Flash Memory: 1 bit flash cell
SLC(Single Level Cell): Has an extra floating gate
- 2 charge states
- 1 bit per floating gate transistor

![[Pasted image 20250902105418.png]]

Inject electron to write 0 | "Suck out" electron to write 1

![[Pasted image 20250902110018.png]]

## Memory unit
- Memory unit - set of bytes
- Byte - 8 bits
- Bit - one memory cell

![[Pasted image 20250902112418.png]]

### Inputting data to memory unit
Inputting involves
- address of byte (Address Bus)
- data of one or more bytes (Data Bus)

The maximum amount of bytes a memory unit can have is determined by the number of values the address bus can output 
- e.g. 64 bit address bus can have $2^{64}$ values

### Endianness of Memory
Endianness is the ordering or sequencing of bytes of a word of digital data in computer memory storage or during transmission. Words may be represented in big-endian or little-endian manner. Big-endian systems store the most-significant byte of a word at the smallest memory address and the least significant byte at the largest. A little-endian system, in contrast, stores the least-significant byte at the smallest address.
- ARM with linux follows *Little endian*

![[Pasted image 20250902112834.png]]

---
# Memory Space in ARM
> [!NOTE]- Recap
> ![[Pasted image 20250902113006.png]]
## Registers of ARM
![[Pasted image 20250902113248.png]]

- PC: Program Counter
- LP: Link register (saved value of PC)
- SP: Stack pointer
- CPSR: Current Program Status Register
- SPSR: Saved Program Status Register

### Program Status Register: R16

![[Pasted image 20250902114926.png]]

### Cortex M4 Status Register

![[Pasted image 20250902115726.png]]

## Memory inside TM4C123G

![[Pasted image 20250902115801.png]]

![[Pasted image 20250902115815.png]]

## ARM Cortex-M Memory Space
### On-chip Memory Sub-space in ARM
![[Pasted image 20250908181252.png]]

### Off-chip Memory Subspace in ARM
![[Pasted image 20250908181325.png]]

### Private Memory Sub-space in ARM
![[Pasted image 20250908181423.png]]

---
# Memory-Centric Operations
## ARM's instruction format
![[Pasted image 20250908214657.png]]

![[Pasted image 20250908214817.png]]

### Moving data in ARM
![[Pasted image 20250908220316.png]]

### Loading operation in ARM
![[Pasted image 20250908220341.png]]

### Store operation in ARM
![[Pasted image 20250908220817.png]]

### Addition in ARM
![[Pasted image 20250908222520.png]]

### Multiplication in ARM
![[Pasted image 20250908222611.png]]

### Division in ARM
![[Pasted image 20250908222646.png]]

### Forcing Bits to 1 in ARM
![[Pasted image 20250908222928.png]]

### Forcing Bits to 0 in ARM
![[Pasted image 20250908223021.png]]

### Flipping Bits in ARM
![[Pasted image 20250910171305.png]]

---
# Memory-Mapped I/O Devices
Each I/O module has a port, which are all connected by Data Buses

## In reference to ARM Cortex
### Has two internal buses
The ARM Advanced Microcontroller Bus Architecture (AMBA) is an open-standard, on-chip interconnect specification for the connection and management of functional blocks in system-on-a-chip (SoC) designs. It facilitates development of multi-processor designs with large numbers of controllers and peripherals.

### Supports Fast Interrupt Requests
An FIQ is just a higher priority interrupt request, that is prioritized by disabling IRQ and other FIQ handlers during request servicing. Therefore, no other interrupts can occur during the processing of the active FIQ interrupt

### Supports Direct Memory Access
Direct memory access (DMA) is a feature of microprocessor systems that allows
certain hardware subsystems to access main system memory such as RAM (Random
Access Memory) independently of the central processing unit (CPU).

### Includes a Debug Port
JTAG (Joint Test Action Group) specifies the use of a dedicated debug port
implementing a serial communications interface for low-overhead access without
requiring direct external access to the system address and data buses.

## Cortex M4 Pin Diagram
![[Pasted image 20250910172113.png]]

![[Pasted image 20250910172132.png]]

![[Pasted image 20250910172153.png]]

![[Pasted image 20250910172207.png]]

## Blueprints
### GPIO Pad
![[Pasted image 20250910172305.png]]

### Analogue to Digital Conversion Block
![[Pasted image 20250910172349.png]]

### ARM Cortex M4's ADC
![[Pasted image 20250910172430.png]]
![[Pasted image 20250910172516.png]]

### Cortex M4's PWM Module
![[Pasted image 20250910172553.png]]

### Of each PWM Generator
![[Pasted image 20250910172625.png]]

### QEI Module
![[Pasted image 20250910172641.png]]

![[Pasted image 20250910172657.png]]

### Cortex M4's UART
![[Pasted image 20250910172720.png]]

### Cortex M4's SSI
![[Pasted image 20250910175925.png]]



# References
![[MA4832-XM2-ARM Memory.pdf]]****