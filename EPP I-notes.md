# Computer Engineering Principles and Practice I

# 1. Fundamentals of Electricity

## 1.1 Electrical Quantities
### Electrical quantities

| Quantity | Description |
| ----- | ----- |
| Electric charge | The physical property of matter that causes it to experience a force when placed in an electromagnetic field The charge carried by an electron: $$q_e=-16.02\times10^{-19}\text{ C}$$ In a conductor, electrons move under the influence of an electric field, giving rise to an electric current opposite to the flow of electrons. |
| Voltage | It is a measure of the **energy transferred per unit charge** when the charge is moved from one point to another point Unit of voltage: Volt (V) $$V = \frac{E}{Q}$$ Also called electromotive force (EMF) The ‘+’ terminal is at a higher energy level than the ‘-’ terminal. |
| Electric Current | The time rate of flow of electrical charges through an element Unit: Ampere (A) $$I = \frac{Q}{t}$$ Electric current has a direction, and it is the direction of flow of positive charges. |
| Electric Power | Rate of energy transfer. $$\text{P}=\text{V}\times I = \frac{E}{q}\times\frac{q}{t} = \frac{V^2}{R}=I^2R$$ |
| Resistance and Ohm’s law | When electric current flows through a wire or other circuit elements, it encounters some opposition. $$V= I\times R$$ Ohm’s Law states that the voltage across an ideal resistor is proportional to the current through it. Ohm’s law is an empirical relationship which can be observed, but it is also an approximation It does not hold at very high or low voltage and current values. Resistance also depends on the material and geometry of the element. $$R=\rho \frac{L}{A}$$ |
| Active Element (Source) | If a positive charge enters the negative polarity and exits the positive polarity of an element. The charge gains energy from the element. The element is a source (active element). |
| Passive Element (Load) | If positive charge enters the positive polarity and exits the negative polarity of an element. The charge loses energy in the element The element is a “load” (passive element) |

### Power Loss

* When current flows through resistance, charged particles lose energy to the element, which results in a voltage drop. The energy loss also heats up the element. Hence power loss is given by the formula:  
* $P_L = V\times I = \left(I\times R\right) \times I = I^2 R$	  
* Hence,  
* $P_L\propto I^2$

### Internal Resistance
* In reality, batteries have an internal resistance. There will be a voltage drop across this internal resistance. The higher the load current, the higher the voltage drop and the higher the power loss.
$$V = V_{total} - i_L R_{i}$$
* Wires must have sufficient thickness.
* Recalling the resistivity v/s resistance formula, as the cross sectional area increases, resistance decreases, and power loss decreases for the same current.
    * e.g. Jumper cables for jump-starting cars are very thick because of their high current. If they were done with breadboard wires, the wires would melt.



## 1.2 Kirchoff's Current and Voltage Laws 

### Kirchoff's Current Law
The sum of all currents entering a node is equal to the sum of all currents leaving a node.
* This is based on the *conservation of charges*.
* Current = Flow of charges
    * $I=\frac{Q}{t}$
* Since charges cannot be created nor destroyed, net flow of charges into or out of a node must be 0 (See figure 1.2.1).

<div align="center">
    <figure>
        <img src="assets/EPP1/1.2.1.png" alt="Figure 1.2.1">
    </figure>
</div>

$$\text{Figure 1.2.1:}\quad  i_1 = i_2 + i_3 + i_4$$

KCL can be applied to a supernode, which is any enclosed portion of the circuit. We visualise this as a black box with unknown elements and wirings.

<div align="center">
    <figure>
        <img src="assets/EPP1/1.2.2.png" alt="Figure 1.2.2">
    </figure>
</div>

$$\text{Figure 1.2.2:}\quad  i_1 = i_2 + i_3 + i_4$$

### Kirchoff's Voltage Law
Around any closed loop, the sum of voltage rises is equal to the sum of voltage drops.
* This is derived from the conservation of power.
* Voltage rises when we go from negative to positive polarity.
* Voltage drops when we go from positive to negative polarity.
    * $V_b =V_1+V_2+V_3$  (see Figure 1.2.3)

<div align="center">
    <figure>
        <img src="assets/EPP1/1.2.3.png" alt="Figure 1.2.3">
    </figure>
</div>

$$\text{Figure 1.2.3:}\quad  V_b = V_1 + V_2 + V_3$$

Derivation:
* Total power consumed by resistors:
    * $V_1I + V_2I+V_3I=I(V_1+V_2+V_3)$
* Power supplied by battery:
    * $P = V_bI$
* By conservation of power,
$$V_b = V_1 + V_2 + V_3$$

## 1.3 Resistances in Series and Parallel
## 1.4 Voltage Division Principle
## 1.5 Current Division Principle
# 2. Thevenin Equivalent Circuit
## 2.1 Concept of Thevenin Equivalent Circuit
# 3. Circuit Analysis Techniques
## 3.1 Polarity
## 3.2 Passive and Active elements
## 3.3 Node Voltage Analysis
# 4. Capacitors
## 4.1 Capacitance
## 4.2 Capacitance in Series and Parallel
## 4.3 Capacitor Equations
## 4.4 DC Transients
# 5. Inductors
## 5.1 Faraday's Law
## 5.2 Inductance in Series and Parallel
## 5.3 Energy Storage
## 5.4 Inductor's Transient Current
# 6. AC Circuits
## 6.1 Root-Mean-Square (RMS)
## 6.2 Phase Difference
## 6.3 Complex Domain (j), Phasors
## 6.4 Impedance of Inductors, Capacitors and resistors
## 6.5 AC Circuit Analysis with Phasors and Impedances 
