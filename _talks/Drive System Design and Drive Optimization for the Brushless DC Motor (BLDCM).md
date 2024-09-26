---
title: "Drive System Design and Drive Optimization for the Brushless DC Motor (BLDCM)"
collection: research projects
type: "A research on the design of drive system for BLDCM and drive optimization"
permalink: /research/research-3
venue: "Micro and Special Motor Research Institute, Zhejiang University"
date: 2023-08-12
location: "Hangzhou, China"
---

*<font size=4>Advisor:</font> [<font size=4>Jianqi Qiu</font>](https://person.zju.edu.cn/en/qiujianqi)<font size=4>, Associate Professor, College of Electrical Engineering, Zhejiang University</font>*  

*August, 2023 - October, 2023*
- - -

Research Approach
===

- Designed the half-bridge power transistor driver and pulse-wide-modulation (PWM) signal generation circuit and configured three-phase Hall sensors.
- Designed and implemented a digital control system for the power electronic circuits on a CPLD development board (ispLSI1016), incorporating VHDL for programming logic.
- Prototyped the entire system on a PCB, tested it experimentally, and verified the realization of the expected functions.
- Designed and compared various starting, driving, and speed control strategies for the Brushless DC Motor (BLDCM).

- - -  

How it works
===  

Introduction  
---  

<p style = "text-align:justify; text-justify:inter-ideograph;"> The brushless DC motor is a type of synchronous motor, which includes three main components in its drive system: the power supply, control unit, and the motor itself. In a brushless DC motor, the armature winding is located on the stator, while the magnets are mounted on the rotor for rotation. The commutator is fixed on the stator, and both the magnets and brushes rotate, maintaining a constant relative position, controlled by the armature current.</p>
  
  
<p style = "text-align:justify; text-justify:inter-ideograph;"> Typically, the input is either direct current (commonly 24V) or alternating current (110V/220V). If the input is AC, it must first be converted to DC using a converter. Regardless of whether the input is DC or AC, before the current enters the motor coils, the DC voltage must be converted into three-phase voltage by an inverter to drive the motor. The inverter generally consists of six power transistors (q1 to q6) arranged in an upper arm (q1, q3, q5) and a lower arm (q2, q4, q6) configuration to act as switches controlling the current flow through the motor coils. The control unit provides Pulse Width Modulation (PWM) to determine the switching frequency of the power transistors and the timing of the phase shifting by the inverter.</p>  



Three-Phase Six-State Commutation Process  
---  
<p style = "text-align:justify; text-justify:inter-ideograph;"> The three-phase six-state commutation process, as illustrated in Figure 1, operates with two phases conducting at any given moment. The magnetic potentials generated by the conducting phases superimpose at a 60-degree angle, resulting in a composite magnetic potential that is $\sqrt{3}$ ​times the magnitude of the original potentials and positioned at a 30-degree angle to each of them. At any moment, the composite magnetic potential leads the rotor's magnetic potential by 120 degrees. This leading of the stator's composite magnetic potential over the rotor's magnetic potential by 120 degrees drives the rotation of the brushless motor.</p>  

![Figure1](/images/Figure1.png)  


Three-Phase Six-State Conduction Schematic  
---  
<p style = "text-align:justify; text-justify:inter-ideograph;"> The schematic of the three-phase six-state conduction, shown in Figure 2, depicts ABC three phases each producing a three-step wave. The conduction timing sequence for forward conduction, reverse conduction, and non-conduction is 1:1:1. The conduction follows a cyclic sequence of A+B- → A+C- → B+C- → B+A- → C+A- → C+B- → A+B-, across one electrical cycle (360 electrical degrees), encompassing six magnetic states. Each magnetic state lasts for 60 electrical degrees, and the winding current is bidirectional.</p>  

![Figure2](/images/Figure2.png)  

  
<p style = "text-align:justify; text-justify:inter-ideograph;"> This description outlines the fundamental operating principle of the commutation process in brushless DC motors, highlighting how the precise timing and sequence of phase conduction are critical for the efficient and controlled rotation of the motor.</p>  


Three-Phase Six-State BLDC Motor Control System Principle Diagram  
---  
![Figure_3](/images/Figure_3.png)  



<p style = "text-align:justify; text-justify:inter-ideograph;"> The control system's principle diagram, as shown in Figure 3, depicts the process where three-phase Hall signals are fed into a GAL (Generic Array Logic) chip, along with an external clock input. The GAL chip processes the position information and, based on digital logic expressions, outputs power transistor gating signals based on the position signal processing circuit. These gating signals are then superimposed with an externally input PWM (Pulse Width Modulation) signal to form the final power transistor gating signals. These signals, provided by the GAL chip, are sent to a driving isolation circuit and finally to a three-phase bridge power main circuit.</p>  

- - -  

  
System and Module Circuit Diagrams  
===  
- System circuit diagram

![System](/images/System.png)  

  
- PWM Generation Module
  
<p align="center">
  <img src="/images/PWM.png" width="350">
</p>
  
Outputting PWM (Pulse Width Modulation) waveforms with different duty cycles.  

![PWM_ZKB](/images/PWM_ZKB.png)  

  
Outputting the FFT (Fast Fourier Transform) image of a PWM signal.  

![PWM_FFT](/images/PWM_FFT.png)  

- GAL Chip and Its Circuit

The internal combinational logic of a GAL (Generic Array Logic) chip.  


<p align="center">
  <img src="/images/GAL.png" width="350">
</p>


- IR2136 and Its Circuit

![IR2136](/images/IR2136.png)  

- Three-Phase Power Main Circuit

![TPPMC(/images/TPPMC.png)  

  
- - -  

  
Prototype
===  

![Prototype_](/images/Prototype_.png)  

- - -  


Control strategies implemented by CPLD
===  
- Forward and reverse control
- Speed adjustment
- Soft start
- Brake control

Example: Chopped-Soft-Starter
---  

<b>Basic Approcah</b>  

```VHDL
library ieee;
use ieee.std_logic_1164.all;
use ieee.std_logic_arith.all;
use ieee.std_logic_unsigned.all;


entity demo is
    port(clk: in std_logic;
         HA, HB, HC: in std_logic;
         T1, T2, T3, T4, T5, T6: out std_logic);
end;

architecture demo_architecture of demo is
    signal pwm_sig: std_logic := '1';
begin
    process(clk, HA, HB, HC)
    variable count: std_logic_vector(10 downto 0) := "00000000000";
    variable k: std_logic_vector(10 downto 0) := "00000000000";
    variable clock: std_logic_vector(4 downto 0) := "00000";
    begin
        if (clk'event) and (clk = '1') then
            count := count + 1;
            if(count <= k) then
                pwm_sig <= '1';
            elsif count < 2000 then
                pwm_sig <= '0';
            else
                clock := clock + 1;
                count := "00000000000";
            end if;
            if(clock > 30) then
                k := k + 1;
                clock := "00000";
            end if;
        end if;
        T1 <= not (pwm_sig and (HA and (not HB)));
        T2 <= not (pwm_sig and (HA and (not HC)));
        T3 <= not (pwm_sig and (HB and (not HC)));
        T4 <= not (pwm_sig and (HB and (not HA)));
        T5 <= not (pwm_sig and (HC and (not HA)));
        T6 <= not (pwm_sig and (HC and (not HB)));
    end process;
end demo_architecture;
```

- - -
  