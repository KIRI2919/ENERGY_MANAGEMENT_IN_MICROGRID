
This project focuses on the development and simulation of an **Energy Management System (EMS) for a Microgrid operating in Grid-Connected Mode**.

The system integrates **Photovoltaic (PV) generation, Battery Energy Storage System (BESS), DC-DC converters, a three-phase grid-connected inverter, PLL synchronization, dq-axis control, and PWM-based inverter control**.

The complete system was developed and analyzed using **MATLAB/Simulink** as part of the **EC9130 – Distribution Automation & Smart Grid** course at the Department of Electrical & Electronic Engineering, Faculty of Engineering, University of Jaffna.

---

## 🎯 Objectives

The main objectives of this project are:

- Develop a PV generation system with a Boost Converter.
- Implement a Battery Energy Storage System (BESS).
- Design a bidirectional DC-DC converter for battery charging and discharging.
- Develop a rule-based Energy Management System (EMS).
- Model a three-phase grid-connected inverter.
- Implement PLL-based grid synchronization.
- Develop dq-axis control using PI controllers.
- Implement PWM-based inverter switching control.
- Analyze the voltage, current, frequency, and PWM responses of the system.

---

## 🏗️ System Architecture

The overall system consists of the following major components:

```text
                    ☀️ PV Array
                        │
                        ▼
                 Boost Converter
                        │
                        ▼
                 ┌─────────────┐
                 │   DC BUS    │
                 │    600 V    │
                 └─────────────┘
                   │         │
                   │         │
                   ▼         ▼
                BESS      DC Load
              400 V
                   │
                   ▼
          Bidirectional DC-DC
              Converter
                   │
                   └──────────────► DC Bus

                 DC Bus
                    │
                    ▼
          Three-Phase Inverter
                    │
                    ▼
              Filter Inductor
                    │
                    ▼
             Three-Phase Grid
                400 V, 50 Hz

        ┌────────────────────────┐
        │ Energy Management      │
        │ System (EMS)            │
        └────────────────────────┘

☀️ PV System

The PV array was modelled considering:

Irradiance: 1000 W/m²
Temperature: 25°C

A Boost Converter was used to increase and regulate the PV voltage.

The Boost Converter operates using an IGBT switching device and stores energy in the inductor during the ON state and releases it during the OFF state.

The ideal voltage gain is:

$$ V_{out} = \frac{V_{in}}{1-D} $$
🔋 Battery Energy Storage System

A 400 V Battery Energy Storage System was integrated into the DC microgrid.

The battery operating SOC range was defined as:

Minimum SOC: 20%
Maximum SOC: 90%

The battery is used to:

Store excess PV energy.
Supply power when PV generation is insufficient.
Support DC bus power balance.
Improve overall system stability.
🔄 Bidirectional DC-DC Converter

Since the battery voltage is 400 V and the DC bus voltage is 600 V, a bidirectional DC-DC converter was used for voltage matching and two-way power transfer.

Discharging Mode – Boost Mode
Battery (400 V)
       │
       ▼
Boost Converter
       │
       ▼
DC Bus (600 V)

Used when PV generation is insufficient.

Charging Mode – Buck Mode
DC Bus (600 V)
       │
       ▼
Buck Converter
       │
       ▼
Battery (400 V)

Used when excess PV power is available.

🧠 Energy Management System

A rule-based EMS was implemented to determine the operating mode of the battery.

The power difference is calculated as:

$$ P_{diff} = P_{PV} - P_{Load} $$
🔋 Charging Mode

Condition:

$$ P_{diff} > 100 $$

If:

$$ SOC < SOC_{max} $$

the battery is charged using Buck Mode.

⚡ Discharging Mode

Condition:

$$ P_{diff} < -100 $$

If:

$$ SOC > SOC_{min} $$

the battery supplies power through Boost Mode.

⏸️ Idle Mode

Condition:

$$ -100 \leq P_{diff} \leq 100 $$

The battery remains inactive.

The duty cycle is limited to:

$$ 0 \leq D \leq 0.95 $$

to maintain stable converter operation.

A three-phase grid-connected inverter system was modelled and simulated.

Grid Parameters
Parameter	Value
Grid Voltage	400 V line-to-line
Phase Voltage	≈ 230 V RMS
Frequency	50 Hz
DC Source	600 V

The theoretical phase voltage is:

$$ V_{phase} = \frac{400}{\sqrt{3}} \approx 230V $$
🔄 Phase-Locked Loop (PLL)

A Phase-Locked Loop (PLL) was implemented to synchronize the inverter with the three-phase grid.

The PLL provides:

Grid frequency
Grid phase angle
Synchronization information for dq transformation

The simulated grid frequency reaches approximately 50 Hz, indicating proper synchronization.

📐 dq-Axis Control

The three-phase current is transformed from the abc reference frame to the dq reference frame.

The control strategy uses:

Id → Active power control
Iq → Reactive power control

PI controllers are used to reduce the error between reference and measured values.

In the implemented system:

$$ I_q \approx 0 $$

indicating that the reactive power component is very small.

⚙️ PWM Inverter Control

A three-phase Universal Bridge inverter using IGBT switching devices was implemented.

PWM signals are generated to control the inverter switching.

The modulation signal is constrained within:

$$ -1 \leq m \leq 1 $$

This prevents over-modulation and improves stable inverter operation.

📊 Simulation Results

The system was analyzed using MATLAB/Simulink scopes.

DC Microgrid Results
PV voltage settles around 450 V.
The simulated DC output voltage reaches approximately 1200 V.
Initial duty-cycle transients settle quickly.
PV current shows an initial transient before reaching a stable condition.
Battery charging/discharging operation was controlled using SOC limits.
Grid-Connected Results
RMS phase voltage: approximately 220–230 V
Grid frequency: 50 Hz
Current waveform: approximately sinusoidal
Small current ripple is observed due to PWM switching.
Three-phase PWM signals are balanced and periodic.
PLL maintains grid synchronization.
\(I_d\) remains relatively stable.
\(I_q\) remains close to zero.
🛠️ Software and Tools
MATLAB
Simulink
Simulink Power Electronics / Electrical components
MATLAB Function blocks
Scope-based waveform analysis

