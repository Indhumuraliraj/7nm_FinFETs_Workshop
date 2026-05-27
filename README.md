
# FinFET Circuit Design and Characterization

This GitHub repository documents the **10-day workshop on FinFET Circuit Design and Characterization using ASAP7 PDK** offered by **VSD Corp. Pvt. Ltd.**


##  Table of Contents

| Module | Topic(s) Covered |
|--------|------------------|
| 📘 Module 1 | **FinFET Devices and Innovations** |
|  | Path To Zetta Scale Computing |
|  | Introduction To FinFETs |
|  | FEOL Innovations |
|  | BEOL Innovations |
| 📘 Module 2 | **7nm FinFET Inverter Performance Analysis** |
|  | NFET DC Characteristics Using 7nm PDKs |
|  | PFET DC Characteristics Using 7nm PDKs |
|  | CMOS Inverter Characteristics Using 7nm FinFETs |
|  | CMOS Inverter_vtc Characteristics|
|  | Module 2 Assignment - 7nm Inverter Characterization |
| 📘 Module 3 | **Design of a BandGap Reference Circuit** |
|  |  Design of a BGR Circuit |
|  | Module 3 Assignment - Bandgap Reference Design and Simulation using Xschem |


##  Workshop Objectives

- Understand FinFET device architecture and scaling challenges
- Explore FEOL and BEOL innovations
- Perform DC and transient simulations using ASAP7 PDK
- Analyze CMOS inverter characteristics
- Design and simulate a Bandgap Reference (BGR) circuit
- Gain hands-on experience with Xschem and Ngspice# 7nm_finFET_workshop

---
# 1. FinFET Devices and Innovations

## 1.1 Path To Zetta Scale Computing

### Overview

The evolution of computing has always been driven by society’s need to solve increasingly complex problems. From code-breaking machines during World War II to today’s AI-powered supercomputers, semiconductor technology has continuously evolved to deliver higher performance, smaller devices, and lower power consumption.

![Image]()
However, modern applications such as:

- Artificial Intelligence (AI)
- Precision Medicine
- Climate Modeling
- Earthquake Prediction
- Autonomous Systems
- Quantum Simulations
- Advanced Scientific Computing

require computational capabilities far beyond what traditional architectures can provide.

To meet these demands, the semiconductor industry is moving toward **zeta-scale computing**, where systems are expected to perform:

```math
10^{21} \text{ FLOPS}
```

## 1.1.1  Historical Evolution of Computing

###  Early Computing Era

The first generation of computers was built to solve specialized military and scientific problems.

### Examples:
- **Bombe Machine** → Used by Alan Turing to break Enigma encryption.
- **ENIAC** → Vacuum-tube based electronic computer.
- **EDVAC** → Introduced binary computing and the von Neumann architecture.

These systems:
- Occupied entire rooms
- Consumed massive power
- Required heavy cooling systems

Today, devices with millions of times more performance fit inside a smartphone.

### Moore’s Law and CMOS Scaling

For decades, Moore’s Law enabled exponential growth in computing power by increasing transistor density.


## 1.1.2 CMOS Evolution Areas
![Image]()

### Patterning Technology

Lithography continuously evolved to shrink transistor dimensions:

| Technology | Wavelength |
|---|---|
| Early Lithography | 248 nm |
| Advanced Lithography | 193 nm |
| EUV Lithography | 13.5 nm |

Smaller wavelengths enabled:
- Higher transistor density
- Faster switching
- Lower area consumption



### Channel Material Evolution

Traditional silicon channels eventually faced mobility limitations.

Evolution:
- Silicon (Si)
- Silicon-Germanium (SiGe)
- 2D Materials (future)

These materials improve:
- Carrier mobility
- Speed
- Power efficiency



###  Interconnect Material Evolution

Interconnect materials also evolved to reduce resistance.

Evolution:
- Aluminum (Al)
- Copper (Cu)
- Ruthenium (Ru) (future)

This reduces:
- RC delay
- Signal loss
- Interconnect power consumption



### Gate Stack Evolution

Gate materials evolved significantly over technology nodes.

Evolution:
- Polysilicon + SiO₂
- High-k Metal Gate (HKMG)

At 45nm technology nodes, HKMG became essential to reduce leakage current.



## 1.1.3 Problems with Traditional Planar MOSFETs

As transistor dimensions scaled below 28nm, traditional planar MOSFETs started facing major limitations.

### Key Challenges

### Short Channel Effects (SCE)

When channel length becomes extremely small:
- Drain influence increases
- Gate loses control over the channel
- Leakage current rises significantly



### Leakage Current

Variations between source and drain create:
- Subthreshold leakage
- Increased static power dissipation
- Reduced OFF-state performance



### Heat and Power Problems

Higher transistor density caused:
- Excessive heat generation
- Cooling limitations
- Frequency saturation

Modern processors reached a practical power limit around:
- 100W to 125W

This prevented further clock-frequency scaling.



## 1.1.4 Impact of Mobile Computing

After 2010, mobile devices became dominant over PCs.

Mobile systems introduced strict constraints:
- Limited battery power
- No active cooling systems
- Need for low power dissipation

As a result:
- Frequency scaling slowed down
- Energy efficiency became the primary focus

---

## 1.2 Introduction to FinFETs
### 1.2.1 What is FinFET?

FinFET (Fin Field Effect Transistor) is a three-dimensional transistor technology in which the conducting channel is formed as a vertical silicon fin, and the gate wraps around the fin from multiple sides. This structure provides better electrostatic control, reduces leakage current, improves switching performance, and enables lower power consumption compared to traditional planar MOSFETs.

| **VCTAT** <br> ![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/vctat_temp.png) | **VPTAT** <br> ![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/vpat_temp.png) |
|:---:|:---:|

### 1.2.2 Why FinFET Technology?

To solve the limitations of planar MOSFETs, the semiconductor industry introduced **FinFETs (Fin Field Effect Transistors)**.

FinFETs use a 3D fin-shaped silicon structure where the gate wraps around multiple sides of the channel.

This provides:
- Better gate control
- Lower leakage current
- Improved switching behavior
- Reduced short channel effects



### 1.2.3 FinFET Working Principle

In planar MOSFETs:
- The gate controls the channel from only one side.

In FinFETs:
- The gate wraps around the fin from multiple sides.

This significantly improves electrostatic control over the channel.



### 1.2.4 Why FinFET is Needed

The major reason for introducing FinFET technology was the inability of planar transistors to continue scaling efficiently.

### Problems in Planar CMOS:
- Short Channel Effect (SCE)
- Drain Induced Barrier Lowering (DIBL)
- High subthreshold leakage current
- Increased static power dissipation
- Poor ON/OFF switching ratio
- Frequency saturation due to power limits

### FinFET Solutions:
- Better ON/OFF switching
- Lower subthreshold current
- Lower operating voltage
- Reduced dynamic power
- Improved electrostatic control
- Better scalability for advanced nodes


## 1.2.5 Advantages of FinFETs

### Better ON/OFF Switching

FinFETs provide improved switching characteristics.

ON-OFF performance is measured using:
- Subthreshold swing
- Leakage current

FinFETs achieve:
- Lower subthreshold leakage
- Faster switching
- Improved threshold control



### Reduced Dynamic Power

Dynamic power relation:

```math
P \propto C V^2 f
```

Where:
- \(C\) = capacitance
- \(V\) = voltage
- \(f\) = frequency

Because FinFETs can operate at lower voltages:
- Dynamic power reduces significantly



### Reduced Leakage Current

FinFETs suppress:
- Drain-induced barrier lowering (DIBL)
- Short channel effects
- Subthreshold conduction



###  Improved Electrostatic Control

Multi-side gate control improves:
- Channel stability
- Threshold voltage control
- Device reliability

---


# 1.3 FEOL Innovations

## Introduction

FEOL (Front-End-Of-Line) innovations mainly focus on improving transistor performance, reducing leakage current, increasing transistor density, and continuing CMOS scaling beyond the limitations of planar MOSFETs. As technology nodes become smaller, traditional scaling methods alone are no longer sufficient, so new transistor structures, materials, and layout optimization techniques are introduced.

---

## 1.3.1 CMOS Technology Inflection Points
| **VCTAT** <br> ![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/vctat_temp.png) | **VPTAT** <br> ![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/vpat_temp.png) |
|:---:|:---:|


Initially, CMOS scaling followed Dennard scaling, where reducing transistor size also reduced power consumption while increasing transistor density and performance. During this period, many important innovations were introduced such as copper interconnects, strained silicon, low-k dielectrics, and High-k Metal Gate (HKMG) technology.

As scaling moved below 22nm, planar MOSFETs started suffering from severe short channel effects and leakage current problems. This led to the introduction of FinFET technology, which provided better electrostatic control and reduced leakage current.

Further scaling introduced:
- Multiple patterning techniques
- EUV lithography
- Gate-All-Around (GAA) transistors
- Future CFET architectures
- 2D semiconductor materials

These innovations help continue Moore’s Law at advanced technology nodes.



## 1.3.2 Standard Cell Area Scaling
| **VCTAT** <br> ![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/vctat_temp.png) | **VPTAT** <br> ![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/vpat_temp.png) |
|:---:|:---:|


As process nodes shrink, improving transistor density becomes more difficult. To achieve better area scaling without making fabrication extremely expensive, several scaling booster techniques are used through DTCO (Design Technology Co-Optimization).

These techniques improve:
- Standard cell density
- Routing efficiency
- Power efficiency
- Area optimization



### 1.3.2.1 Track Reduction (Fin Depopulation)

Track reduction reduces the number of fins or reduces the height of active regions in FinFET standard cells.

This helps:
- Reduce standard cell height
- Increase transistor density
- Lower power consumption

However, reducing the number of fins may also reduce transistor performance.



### 1.3.2.2 Single Diffusion Break (SDB)

Single Diffusion Break removes extra dummy gate spacing at cell boundaries.

This technique:
- Improves layout compactness
- Increases effective transistor density
- Reduces unused area between standard cells


### 1.3.2.3 Contact Over Active Gate (COAG)

COAG allows the contact to land directly over the active gate instead of placing it outside the gate region.

This helps:
- Reduce spacing between devices
- Improve layout density
- Reduce standard cell size



### 1.3.2.4 Buried Power Rail (BPR)

Buried Power Rail moves the power rails below the active device layer instead of using upper metal routing layers.

Advantages include:
- More routing space for signals
- Reduced routing congestion
- Improved logic density
- Lower IR drop
- Better power delivery



## 1.3.3 Parasitic Resistance and Capacitance

As transistor dimensions continue shrinking, parasitic resistance and capacitance become major factors affecting performance and power consumption.

In advanced technologies like FinFETs, GAAFETs, and CFETs, parasitic effects strongly influence:
- Delay
- Drive current
- Energy efficiency



### 1.3.3.1 Parasitic Resistance
![image]()


Parasitic resistance increases significantly in advanced nodes because contact dimensions become smaller while current density increases.

Major resistance components include:
- Contact resistance
- Epitaxial resistance
- FEOL resistance
- BEOL resistance
- Spacer resistance

Among these, contact resistance becomes one of the dominant challenges, especially in NFET devices.

To reduce resistance:
- Better contact engineering is used
- Source/drain doping is improved
- Lower Schottky barrier materials are introduced



### 1.3.3.2 Parasitic Capacitance
![image]()


At smaller nodes, parasitic capacitance becomes more dominant than gate capacitance.

Major capacitance sources include:
- Overlap capacitance
- Fringe capacitance
- Contact-to-channel capacitance

Spacer engineering is widely used to reduce parasitic capacitance by introducing low-k spacer materials and eventually air spacers.

Reducing parasitic capacitance improves:
- Switching speed
- Power efficiency
- Delay performance



## 1.3.4 Device Scaling
![image]()


As gate lengths approach sub-5nm dimensions, conventional silicon transistors face fundamental scaling limitations such as:
- Source-to-drain tunneling
- Leakage current increase
- Poor electrostatic control
- Surface roughness effects

Because of these challenges, researchers are exploring new channel materials such as Transition Metal Dichalcogenides (TMDs) including:
- MoS₂
- WS₂
- WSe₂

These materials provide:
- Better electrostatic control
- Reduced leakage
- Improved energy efficiency
- Better scalability for ultra-small devices



## 1.3.5 3D Structures (CFET)
![image]()


CFET (Complementary FET) is a future transistor architecture where NMOS and PMOS devices are stacked vertically instead of placing them side-by-side.

This structure helps:
- Increase transistor density
- Reduce chip area
- Improve scaling capability

CFET is considered the next evolution after Gate-All-Around FETs for future advanced semiconductor technologies.



## 1.4 BEOL Innovations
![Image]()
### Introduction

BEOL (Back-End-Of-Line) innovations focus on interconnects, signal routing, and power delivery inside integrated circuits.

As transistor scaling continues, interconnect delay and resistance become major bottlenecks because transistor performance improves faster than metal interconnect performance.

Therefore, BEOL innovations are important for:
- Reducing RC delay
- Improving routing efficiency
- Enhancing power delivery
- Lowering congestion
- Improving overall chip performance



### 1.4.1 Extending Copper Interconnects
![Image]()

Copper interconnects have been widely used because of their low resistance. However, at advanced nodes, copper faces scaling challenges due to:
- Electron scattering
- Barrier overhead
- Increased resistivity

To continue using copper:
- Selective barrier deposition
- Via optimization
- Improved metallization techniques

are introduced.



### 1.4.2 Transition to Non-Copper Metals


As copper scaling becomes difficult, alternative metals are explored such as:
- Ruthenium (Ru)
- Cobalt (Co)
- Molybdenum (Mo)

These materials offer:
- Better electromigration reliability
- Lower resistance at smaller dimensions
- Improved interconnect performance



### 1.4.3 Backside Power Delivery Network (BS-PDN)
![Image]()
Traditional front-side power delivery uses the same metal layers for both signals and power routing, causing routing congestion and IR drop issues.

Backside Power Delivery Network (BS-PDN) moves power routing to the backside of the wafer.

This provides:
- Reduced routing congestion
- Better power integrity
- Lower IR drop
- Improved signal routing
- Better standard cell scaling

BS-PDN is considered one of the most important BEOL innovations for future technology nodes.

---

# 2. 7nm FinFET Inverter Performance Analysis

## 2.1 NFET DC Characteristics Using 7nm PDKs

### N-FinFET (N-Type Fin Field Effect Transistor)

N-FinFET is an advanced 3D transistor structure where electrons act as the majority charge carriers. It is the FinFET version of an NMOS transistor and is designed to overcome the limitations of traditional planar MOSFETs at smaller technology nodes.

In an N-FinFET, the conducting channel is formed as a vertical silicon fin, and the gate wraps around the fin from multiple sides, providing better electrostatic control over the channel. When a positive gate voltage greater than the threshold voltage is applied, electrons flow from source to drain, allowing current conduction.

### NFET Schematic in Xschem 
**nfet.sch** <br> ![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/nfet_sch.png)  
### DC Analysis
**id** <br> ![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/nfet_id.png) 





## 2.2 PFET DC Characteristics Using 7nm PDKs

### P-FinFET (P-Type Fin Field Effect Transistor)

P-FinFET is an advanced 3D transistor structure where holes act as the majority charge carriers. It is the FinFET version of a PMOS transistor and is designed to overcome the limitations of traditional planar MOSFETs at smaller technology nodes.

In a P-FinFET, the conducting channel is formed as a vertical silicon fin, and the gate wraps around the fin from multiple sides, providing better electrostatic control over the channel. When a negative gate voltage greater than the threshold voltage is applied, holes flow from source to drain, allowing current conduction.
### PFET Schematic in Xschem 
**pfet.sch** <br> ![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/pfet_sch.png)  
### DC Analysis
**id** <br> ![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/pfet_id.png) 


## 2.3 CMOS Inverter Characteristics Using 7nm FinFETs
### CMOS FinFET Inverter

A CMOS FinFET inverter is an advanced digital logic inverter designed using complementary FinFET transistors: an N-FinFET and a P-FinFET. It performs the same NOT operation as a traditional CMOS inverter but offers better performance, lower leakage current, and improved power efficiency at advanced technology nodes.

In a CMOS FinFET inverter:
- The P-FinFET is connected between the supply voltage (\(V_{DD}\)) and the output.
- The N-FinFET is connected between the output and ground (\(GND\)).
- Both transistor gates are connected together as the input.

FinFET technology uses a 3D fin-shaped channel where the gate wraps around the fin from multiple sides, providing superior electrostatic control compared to planar CMOS transistors.

### CMOS Inverter Schematic in Xschem 
**CMOS_Inverter.sch** <br> ![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/CMOS_inverter_sch.png)

### Working Principle

### Input = LOW (0)
- P-FinFET turns ON
- N-FinFET turns OFF
- Output is connected to \(V_{DD}\)
- Output becomes HIGH (1)

### Input = HIGH (1)
- P-FinFET turns OFF
- N-FinFET turns ON
- Output is connected to ground
- Output becomes LOW (0)

Thus, the CMOS FinFET inverter produces the logical complement of the input signal.

## 2.3.1 DC Characteristics

The DC characteristics describe the relationship between:
- Input Voltage (\(V_{IN}\))
- Output Voltage (\(V_{OUT}\))

### DC Analysis
**Vin_Vout** <br> ![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/CMOS_inverter_vin_vout.png)

This relationship forms the Voltage Transfer Characteristic (VTC) curve.

### Operating Regions

### Region 1
- N-FinFET OFF
- P-FinFET ON
- Output = HIGH

### Region 2
- Both transistors partially ON
- Transition region
- Rapid switching occurs

### Region 3
- N-FinFET ON
- P-FinFET OFF
- Output = LOW


## 2.4 CMOS Inverter_vtc Characteristics

### Overview
This session focuses on CMOS inverter analysis using 7nm FinFET technology. The key objective is to understand how **W/L ratio (nfins)** impacts electrical characteristics such as switching behavior, current, power, delay, and noise performance.

In 7nm FinFET PDK, **only nfins (number of fins)** is varied for NMOS and PMOS while **channel length (L = 7nm)** remains constant.


## 2.4.1 W/L Ratio (Fin Count in FinFET)

### Definition
In FinFET technology, W/L ratio is represented using **number of fins (nfins)** instead of width (W). It directly affects:
- Current drive capability
- Switching speed
- Power consumption

> W/L ∝ nfins​

### SPICE Note
- Vary `nfins` for NMOS and PMOS
- L is fixed = 7nm



## 2.4.2 Switching Threshold Voltage (Vth)

### Definition
Switching threshold voltage is the input voltage at which:

> Vin = Vout

It depends on strength ratio of PMOS and NMOS.



### SPICE Command
```spice
meas dc v_th when nfet_out=nfet_in
```
**Vin_Vout** <br> ![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/vin_vout.png)

## 2.4.3 Drain Current (Id)

### Definition

Drain current (Id) is the current flowing from drain to source controlled by gate voltage.
> Id ∝ Vds

Behavior
Triode region: current increases linearly
Saturation region: current becomes constant

### SPICE Command
```spice
let id = v2#branch
plot id
```

**Drain_Current** <br> ![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/id.png)

## 2.4.4 Power Consumption
### Definition

Power consumption is the average energy used by the circuit over time.

> P = T1​∫Vdd⋅I(t)dt

### SPICE Command
```spice
let trans_current = v2#branch
meas tran id_pwr integ trans_current from=20e-12 to=60e-12
let power = abs((id_pwr * 0.7)/40)
print power
```

## 2.4.5 Propagation Delay (Tp)
### Definition

Propagation delay is the time difference between input and output transitions measured at 50% switching point.
> Tp​ = (Trise​+Tfall)/2​​


### SPICE Command
```spice
meas tran tpr when nfet_in=0.35 RISE=1
meas tran tpf when nfet_out=0.35 FALL=1
let tp = (tpf + tpr)/2
print tp
```

## 2.4.6 Gain (Av)
### Definition

Gain represents how much output voltage changes with respect to input voltage.

> Av​ = dVin​/dVout​​
### SPICE Command
```spice
let gain_av = abs(deriv(nfet_out))
plot gain
```

## 2.4.7 Noise Margin
### Definition

Noise margin defines the immunity of CMOS circuits to noise in logic levels.
> NMH = VOH−VIH

> NML = VIL−VOL

### SPICE Command
```spice
meas dc vil find nfet_in when nfet_out=gain CROSS=1
meas dc voh find nfet_out when nfet_out=gain CROSS=1
meas dc vih find nfet_in when nfet_out=gain CROSS=2
meas dc vol find nfet_out when nfet_out=gain CROSS=2

let nmh = voh - vih
let nml = vil - vol
print nmh
print nml
```

## 2.4.8 Transconductance (Gm)
### Definition

Transconductance is the change in drain current with respect to change in gate voltage.

> gm = dVgs/dId

### SPICE Command
```spice
let gm = real(deriv(id, nfet_in))
meas dc gm_max MAX gm
plot gm
```

**Gain_Margin** <br> ![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/gm.png)

## 2.4.9 Frequency (f)
### Definition

Maximum switching frequency based on propagation delay.

> f = 1/(Trise​+Tfall)​​

### SPICE Command
```spice
tran 0.1n 100p
meas tran tr when nfet_in=0.07 RISE=1
meas tran tf when nfet_out=0.63 FALL=1
let t_delay = tr + tf
let f = 1/t_delay
print f
```
## 2.4.10 Output Resistance (Rout)
### Definition

Output resistance is the ratio of change in output voltage to change in drain current.

> R_out = dId/dVout

### SPICE Command
```spice
let r_out = deriv(nfet_out, id)
plot r_out
```
**Resister_out** <br> ![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/rout.png)

----

# Module 2 Assignment - 7nm Inverter Characterization
## Overview
This assignment focuses on the **characterization of a 7nm FinFET CMOS inverter** using SPICE simulation. The goal is to study how device sizing (W/L ratio represented by nfins) affects key performance parameters such as switching behavior, delay, power, and gain.

You will simulate an inverter circuit, vary transistor parameters, and extract important electrical characteristics to complete a final **characterization table**.


## Objective
To analyze and understand the performance of a 7nm FinFET inverter by extracting key metrics from SPICE simulation results and studying the impact of device sizing on circuit behavior.

## Procedure

## 1. Run Simulation
- Load the provided SPICE deck (`Inverter.sp`)
- Perform DC and transient analysis as required


---

## 2. Parameter Variation
- Modify transistor parameters:
  - PMOS width (W or nfins)
  - NMOS width (W or nfins)
- Observe how performance changes with different sizing ratios


## Characteristics Table

| S.No | wp (µm) | lp (µm) | wp/lp | wn (µm) | ln (µm) | wn/ln | v_th (V) | id_max (mA) | Av | power (mW) | tp (ps) | f (GHz) |
|------|--------|--------|--------|--------|--------|--------|----------|-------------|----|------------|---------|----------|
| 1 | 0.4935 | 0.0070 | 70.5 | 0.4935 | 0.0070 | 70.5 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 2 | 0.4935 | 0.0070 | 70.5 | 0.5640 | 0.0070 | 80.5714 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 3 | 0.4935 | 0.0070 | 70.5 | 0.6345 | 0.0070 | 90.6429 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 4 | 0.4935 | 0.0070 | 70.5 | 0.7050 | 0.0070 | 100.714 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 5 | 0.4935 | 0.0070 | 70.5 | 0.7755 | 0.0070 | 110.786 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 6 | 0.4935 | 0.0070 | 70.5 | 0.8460 | 0.0070 | 120.857 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 7 | 0.4935 | 0.0070 | 70.5 | 0.9165 | 0.0070 | 130.929 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 8 | 0.4935 | 0.0070 | 70.5 | 0.9870 | 0.0070 | 141.000 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 9 | 0.4935 | 0.0070 | 70.5 | 1.0575 | 0.0070 | 151.071 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 10 | 0.4935 | 0.0070 | 70.5 | 1.1280 | 0.0070 | 161.143 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 11 | 0.4935 | 0.0070 | 70.5 | 1.1985 | 0.0070 | 171.214 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 12 | 0.4935 | 0.0070 | 70.5 | 1.2690 | 0.0070 | 181.286 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 13 | 0.4935 | 0.0070 | 70.5 | 1.3395 | 0.0070 | 191.357 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 14 | 0.4935 | 0.0070 | 70.5 | 1.4100 | 0.0070 | 201.429 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 15 | 0.4935 | 0.0070 | 70.5 | 1.4805 | 0.0070 | 211.500 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 16 | 0.5640 | 0.0070 | 80.5714 | 0.4935 | 0.0070 | 70.5 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 17 | 0.5640 | 0.0070 | 80.5714 | 0.5640 | 0.0070 | 80.5714 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 18 | 0.5640 | 0.0070 | 80.5714 | 0.6345 | 0.0070 | 90.6429 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 19 | 0.5640 | 0.0070 | 80.5714 | 0.7050 | 0.0070 | 100.714 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 20 | 0.5640 | 0.0070 | 80.5714 | 0.7755 | 0.0070 | 110.786 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 21 | 0.5640 | 0.0070 | 80.5714 | 0.8460 | 0.0070 | 120.857 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 22 | 0.5640 | 0.0070 | 80.5714 | 0.9165 | 0.0070 | 130.929 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 23 | 0.5640 | 0.0070 | 80.5714 | 0.9870 | 0.0070 | 141.000 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 24 | 0.5640 | 0.0070 | 80.5714 | 1.0575 | 0.0070 | 151.071 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 25 | 0.5640 | 0.0070 | 80.5714 | 1.1280 | 0.0070 | 161.143 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 26 | 0.5640 | 0.0070 | 80.5714 | 1.1985 | 0.0070 | 171.214 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 27 | 0.5640 | 0.0070 | 80.5714 | 1.2690 | 0.0070 | 181.286 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 28 | 0.5640 | 0.0070 | 80.5714 | 1.3395 | 0.0070 | 191.357 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 29 | 0.5640 | 0.0070 | 80.5714 | 1.4100 | 0.0070 | 201.429 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 30 | 0.5640 | 0.0070 | 80.5714 | 1.4805 | 0.0070 | 211.500 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 31 | 0.6345 | 0.0070 | 90.6429 | 0.4935 | 0.0070 | 70.5 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 32 | 0.6345 | 0.0070 | 90.6429 | 0.5640 | 0.0070 | 80.5714 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 33 | 0.6345 | 0.0070 | 90.6429 | 0.6345 | 0.0070 | 90.6429 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 34 | 0.6345 | 0.0070 | 90.6429 | 0.7050 | 0.0070 | 100.714 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 35 | 0.6345 | 0.0070 | 90.6429 | 0.7755 | 0.0070 | 110.786 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 36 | 0.6345 | 0.0070 | 90.6429 | 0.8460 | 0.0070 | 120.857 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 37 | 0.6345 | 0.0070 | 90.6429 | 0.9165 | 0.0070 | 130.929 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 38 | 0.6345 | 0.0070 | 90.6429 | 0.9870 | 0.0070 | 141.000 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 39 | 0.6345 | 0.0070 | 90.6429 | 1.0575 | 0.0070 | 151.071 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 40 | 0.6345 | 0.0070 | 90.6429 | 1.1280 | 0.0070 | 161.143 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 41 | 0.6345 | 0.0070 | 90.6429 | 1.1985 | 0.0070 | 171.214 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 42 | 0.6345 | 0.0070 | 90.6429 | 1.2690 | 0.0070 | 181.286 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 43 | 0.6345 | 0.0070 | 90.6429 | 1.3395 | 0.0070 | 191.357 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 44 | 0.6345 | 0.0070 | 90.6429 | 1.4100 | 0.0070 | 201.429 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 45 | 0.6345 | 0.0070 | 90.6429 | 1.4805 | 0.0070 | 211.500 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 46 | 0.7050 | 0.0070 | 100.714 | 0.4935 | 0.0070 | 70.5 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 47 | 0.7050 | 0.0070 | 100.714 | 0.5640 | 0.0070 | 80.5714 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 48 | 0.7050 | 0.0070 | 100.714 | 0.6345 | 0.0070 | 90.6429 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 49 | 0.7050 | 0.0070 | 100.714 | 0.7050 | 0.0070 | 100.714 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
| 50 | 0.7050 | 0.0070 | 100.714 | 0.7755 | 0.0070 | 110.786 | 0.344786 | 0.226071 | 6.42845 | 0.0223352 | 0.700828 | 713.441 |
---

###  Overall Observation 

The simulation results show that the transistor sizing (**wp and wn**) is systematically increased while keeping the channel length constant (**lp = ln = 7 nm**), resulting in a gradual increase in **W/L ratio from 70.5 to 211.5**.


### Key Engineering Insight

Even though the device geometry is being scaled significantly, the electrical output does not respond to sizing changes. This indicates:

- The circuit is likely not load-dependent or not properly switching  
- The inverter may be operating under ideal or constrained measurement conditions  
- The simulation is dominated by fixed biasing or model limitations rather than transistor scaling effects  


## 3. Add Uniqueness to Simulation
To ensure unique results for each student, add a dummy voltage source:

username = indhu
ASCII sum = 105 + 110 + 100 + 104 + 117 = 536

```spice
Vuniq in 0 DC 0.536
```
### Conclusion

The dataset confirms correct geometric scaling of MOS/FinFET dimensions, but the lack of variation in electrical parameters indicates that the circuit is not reflecting true dynamic behavior. This suggests a setup or measurement limitation in the simulation rather than actual device performance.

---


# 3. Design of a BGR (Bandgap Reference) Circuit


## 3.1 What is Bandgap Reference?

A Bandgap Reference (BGR) is an analog circuit used to generate a stable reference voltage that remains nearly constant despite changes in temperature, supply voltage, and process variations. It is widely used in analog and mixed-signal integrated circuits to provide accurate and reliable reference voltages.

The output reference voltage is usually close to the silicon bandgap voltage:

```math
V_{REF} \approx 1.2V
```


![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/lab/Bandgap_reference.png)

## 3.2 Why was Bandgap Reference Introduced?

Electronic circuits such as:
- Voltage regulators
- ADCs
- DACs
- PLLs
- Power management circuits

require a highly stable reference voltage for accurate operation.

However, normal voltage sources vary due to:
- Temperature changes
- Supply voltage fluctuations
- Process variations

These variations affect circuit performance and accuracy.

To overcome these problems, Bandgap Reference circuits were introduced to provide:
- Temperature-independent voltage
- Stable operation
- Reliable circuit performance




## 3.3 Principle of Bandgap Reference

The working principle of a Bandgap Reference is based on combining two voltages with opposite temperature coefficients.

###  CTAT Voltage
(Complementary To Absolute Temperature)

- Voltage decreases with temperature
- Example: Base-Emitter Voltage (\(V_{BE}\))



### PTAT Voltage
(Proportional To Absolute Temperature)

- Voltage increases with temperature
- Generated using thermal voltage differences



## 3.4 Working of Bandgap Reference

The Bandgap Reference circuit combines:
- A CTAT voltage
- A PTAT voltage

in proper proportions so that the temperature effects cancel each other.

Mathematically:

```math
V_REF = V_BE + k(V_T)
```

Where:
- \(V_BE\) = CTAT component
- \(V_T\) = PTAT component
- \(k\) = scaling factor

As temperature increases:
- \(V_{BE}\) decreases
- \(V_T\) increases

These opposite variations balance each other, producing a nearly constant output voltage.

Bandgap Reference circuits are fundamental building blocks in modern semiconductor and VLSI systems because they provide accurate and temperature-independent voltage references.

---

# Module 3 Assignment: Bandgap Reference Design and Simulation using Xschem


##  Objective
This project focuses on the design and simulation of a **Bandgap Reference Circuit** using Xschem and Ngspice.  
The aim is to analyze key performance parameters such as:
- Reference voltage (Vref)
- Line regulation
- Temperature stability
- Startup behavior

## Design and Simulation
In this project, the Bandgap Reference circuit is designed and simulated using Xschem and Ngspice. The circuit performance is analyzed by varying supply voltage and temperature conditions.

### BGR Schematic in Xschem 
![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/lab/Bandgap_ref_sch.png)

## Simulations Performed

### DC Analysis
| Ngspice Console  <br> ![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/DC_Analysis.png) | **VREF** <br> ![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/vref_temp.png) |
|:---:|:---:|

| **VCTAT** <br> ![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/vctat_temp.png) | **VPTAT** <br> ![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/vpat_temp.png) |
|:---:|:---:|

  
### Transient Analysis
| Ngspice Console  <br> ![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/Transient_Analysis.png) | **VREF** <br> ![image](https://github.com/Indhumuraliraj/7nm_finFET_workshop/blob/main/vref_time.png) |
|:---:|:---:|



## Characterization Table


| S.No | VDD (V) | Temp (°C) | Vref (V) | Line Reg. (mV/V) | Startup Time (ns) |
|------|----------|------------|-----------|-------------------|-------------------|
| 1 | 0.8 | 27 | 4.9336 | 0.056 | 2.691 |
| 2 | 0.9 | 27 | 4.9336 | 0.056 | 2.691 |
| 3 | 1.0 | 27 | 4.9336 | 0.056 | 2.691 |
| 4 | 1.0 | -40 | 4.9369 | 0.056 | 2.679 |
| 5 | 1.0 | 125 | 4.9272 | 0.056 | 2.713 |



##  Observation

- The Bandgap Reference circuit maintains a nearly stable reference voltage across temperature variations.
- The startup time slightly varies with temperature.
- The line regulation value is very small, indicating good supply stability.
- The output reference voltage remains close to 4.93 V under different operating conditions.




## Unique Design Requirement

To ensure each student's results are unique, a resistor must be added based on ASCII sum of username.

Example:
- Username: Indhu  
- ASCII Sum = 105 + 110 + 100 + 104 + 117 = 504Ω


```spice
Runiq bias out 504
```

## conclusion
The simulation results demonstrate that the Bandgap Reference circuit provides a stable output voltage with minimal variation across different operating conditions. The startup behavior and line regulation characteristics confirm proper circuit operation.

---

