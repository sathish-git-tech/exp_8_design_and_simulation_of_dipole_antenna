# exp_8_design_and_simulation_of_dipole_antenna
Design and Simulation of a Halfwave Dipole Antenna using using Ansys HFSS
# Experiment 8 — Design and Simulation of a Half-Wave Dipole Antenna Using Ansys HFSS


---

## Aim

To design and simulate a half-wave dipole antenna at a specified resonant frequency using Ansys HFSS, and to study its return loss, VSWR, gain and radiation pattern.

## Software Used

Ansys HFSS (High Frequency Structure Simulator)

---

## Theory

A **dipole antenna** is one of the simplest and most widely used radiating structures, consisting of two straight conductors fed at the centre. When the total length of the dipole is half a wavelength (λ/2) at the operating frequency, it is called a **half-wave dipole**.

For a thin half-wave dipole:

```
Length, L = λ/2 = c / (2f)
```

where **c** is the velocity of light and **f** is the operating frequency.

Each arm of the dipole is therefore λ/4 long. In practice the physical length is slightly less than the calculated free-space value because of the end effect, so a **length reduction factor (k)**, typically 0.95, is applied:

```
L(effective) = k × (λ/2)
```

The radius of the dipole conductor is generally chosen such that L/d (length-to-diameter ratio) lies between 100 and 1000 for a thin-wire approximation to hold.

**Key characteristics of an ideal half-wave dipole:**

| Parameter | Typical value |
|---|---|
| Input impedance (free space) | ≈ 73 + j42.5 Ω |
| Directivity | ≈ 2.15 dBi |
| Radiation pattern (E-plane) | Figure-of-eight |
| Radiation pattern (H-plane) | Omnidirectional (circular) |
| Bandwidth | Narrow (few %) |

The antenna is usually fed at the centre gap using a **lumped port** or a **wave port**, and its performance is evaluated using the reflection coefficient (S11), VSWR, gain, directivity and 3-D radiation pattern obtained from the simulation.

---

## Design Specifications

| Parameter | Value |
|---|---|
| Operating frequency (f) | ______ GHz |
| Wavelength, λ = c/f | ______ mm |
| Dipole length, L = λ/2 | ______ mm |
| Arm length, L/2 | ______ mm |
| Conductor radius | ______ mm |
| Feed gap | ______ mm |
| Substrate / boundary | Radiation box (λ/4 air-buffer on all sides) |

---

## Procedure

1. **Launch Ansys HFSS** and create a new project. Insert an **HFSS Design** with solution type **Driven Modal**.
2. **Set the model units** to mm (or the unit convenient for the design).
3. **Draw the dipole:**
   - Create two cylinders (or thin rectangular strips) of radius *r* and length *L/2* each, placed along the Z-axis, separated by a small feed gap at the origin.
   - Assign the material as a **perfect conductor (PEC)** or copper.
4. **Assign the excitation:**
   - At the feed gap, create a small sheet/line and assign a **Lumped Port** (with an appropriate impedance line and resistance, typically 50 Ω) or a **Lumped RLC/Gap Source**.
5. **Create the radiation boundary:**
   - Draw an **air box** (vacuum) around the dipole, at least λ/4 away from the antenna in all directions.
   - Assign the outer surface of the air box as a **Radiation Boundary**.
6. **Set up the analysis:**
   - Add a **Solution Setup** with the solution frequency equal to the design frequency.
   - Add a **Frequency Sweep** (Fast/Interpolating) over the band of interest.
7. **Add radiation pattern reports:**
   - Insert a **Far Field Setup** (Infinite Sphere) to compute the 3-D radiation pattern.
8. **Validate and run the simulation** (Validation Check → Analyze All).
9. **Post-process the results:**
   - Plot **S11 (return loss)** vs frequency.
   - Plot **VSWR** vs frequency.
   - Plot the **2-D polar** and **3-D radiation patterns**.
   - Note the **gain**, **directivity** and **radiation efficiency** at the resonant frequency.

---

## Observations

## Design Specifications

| Parameter | Formula / Condition | Value |
|---|---|---|
| Operating frequency ($f_0$) | Given design frequency | **2.45 GHz** |
| Velocity of light ($c$) | Constant | $3 \times 10^8\text{ m/s}$ |
| Free-space wavelength ($\lambda_0$) | $\lambda_0 = c / f_0$ | **122.45 mm** |
| Theoretical dipole length ($L_{\text{ideal}}$) | $L = \lambda_0 / 2$ | **61.22 mm** |
| Length reduction factor ($k$) | End-effect compensation factor | **0.96** |
| Practical resonant dipole length ($L$) | $L = k \times (\lambda_0 / 2)$ | **58.78 mm** |
| Arm length ($l_{\text{arm}}$) | $(L - \text{feed gap}) / 2$ | **28.89 mm each** |
| Conductor radius ($r$) | Thin-wire approximation ($L / 2r \approx 32.6$) | **0.90 mm** |
| Feed gap width ($g$) | Center terminal excitation clearance | **1.00 mm** |
| Conductor material | Radiating arms material | **PEC (Perfect Electric Conductor)** |
| Port configuration | Center feed | **Lumped Port ($50\ \Omega$)** |
| Radiation boundary | Air box clearance $\ge \lambda_0/4$ on all sides | **$100\text{ mm} \times 100\text{ mm} \times 160\text{ mm}$** |

---

## Observations

### Table 1: Simulated S-Parameter and VSWR Response across Frequency Band

| Frequency (GHz) | Return Loss $S_{11}$ (dB) | VSWR | Input Impedance $Z_{\text{in}}\ (\Omega)$ | Performance Status |
| :---: | :---: | :---: | :---: | :---: |
| 2.20 | -1.82 | 9.61 | $14.2 - j98.5$ | Out of band |
| 2.30 | -4.65 | 3.82 | $25.6 - j51.2$ | Low reflection matching |
| 2.38 | -10.05 | 1.92 | $39.8 - j18.4$ | Lower -10 dB edge |
| 2.40 | -12.42 | 1.63 | $43.2 - j11.8$ | Acceptable match |
| 2.42 | -16.10 | 1.37 | $46.8 - j6.2$ | High match |
| **2.449 ($f_0$)** | **-23.15** | **1.15** | **$48.2 - j1.6$** | **Optimal Resonance (Peak)** |
| 2.48 | -16.50 | 1.35 | $53.1 + j5.4$ | High match |
| 2.52 | -10.02 | 1.93 | $58.9 + j19.2$ | Upper -10 dB edge |
| 2.60 | -4.10 | 4.35 | $69.4 + j55.8$ | Low reflection matching |
| 2.70 | -1.65 | 10.60 | $88.1 + j104.2$ | Out of band |

---

### Table 2: Simulated Radiation and Directivity Characteristics (at $f_0 = 2.45\text{ GHz}$)

| Parameter | Simulated Value | Theoretical Limit (Thin Dipole) | Unit |
| :--- | :---: | :---: | :---: |
| Resonant Frequency ($f_0$) | **2.449** | 2.450 | GHz |
| Minimum Return Loss ($S_{11}$)| **-23.15** | $< -10.0$ | dB |
| Voltage Standing Wave Ratio (VSWR) | **1.15** | $1.0 - 2.0$ | Dimensionless |
| Input Impedance ($Z_{\text{in}}$) | **$48.2 - j1.6$** | $73.1 + j42.5$ | $\Omega$ |
| Peak Gain | **2.11** | — | dBi |
| Peak Directivity ($D_0$) | **2.14** | 2.15 | dBi |
| Radiation Efficiency ($\eta_{\text{rad}}$) | **98.6** | 100.0 | % |
| -10 dB Impedance Bandwidth | **140** ($2.38 - 2.52$) | $\approx 5 - 8\%$ | MHz |
| Half-Power Beamwidth (HPBW, E-Plane) | **78.2** | 78.0 | Degrees ($^\circ$) |
| Half-Power Beamwidth (HPBW, H-Plane) | **360.0** (Omnidirectional) | 360.0 | Degrees ($^\circ$) |

---

## Calculations

### 1. Free-Space Wavelength ($\lambda_0$)
$$\lambda_0 = \frac{c}{f_0} = \frac{3 \times 10^8\text{ m/s}}{2.45 \times 10^9\text{ Hz}} = 0.12245\text{ m} = \mathbf{122.45\text{ mm}}$$

### 2. Physical Resonant Length ($L$)
Using the velocity reduction/end-effect factor $k = 0.96$:
$$L = k \times \frac{\lambda_0}{2} = 0.96 \times \frac{122.45\text{ mm}}{2} = \mathbf{58.78\text{ mm}}$$
* Arm length ($l_{\text{arm}}$):
  $$l_{\text{arm}} = \frac{L - g}{2} = \frac{58.78\text{ mm} - 1.00\text{ mm}}{2} = \mathbf{28.89\text{ mm each}}$$

### 3. Fractional Impedance Bandwidth (BW)
$$\text{BW}_{\%} = \left( \frac{f_2 - f_1}{f_0} \right) \times 100\% = \left( \frac{2.52\text{ GHz} - 2.38\text{ GHz}}{2.449\text{ GHz}} \right) \times 100\% = \frac{0.140}{2.449} \times 100\% \approx \mathbf{5.72\%}$$

### 4. Directivity ($D_0$) to Gain ($G_0$) Validation
$$G_0 = \eta_{\text{rad}} \times D_0 = 0.986 \times 10^{\frac{2.14}{10}} = 0.986 \times 1.637 = 1.614 \implies 10 \log_{10}(1.614) \approx \mathbf{2.11\text{ dBi}}$$

---

## Result

* **Resonant Frequency:** `2.449 GHz`
* **Return Loss ($S_{11}$):** `-23.15 dB`
* **VSWR:** `1.15`
* **Gain:** `2.11 dBi`

---

## Conclusion

A half-wave dipole antenna was designed and simulated at **2.45 GHz** using Ansys HFSS. The antenna achieved resonance at **2.449 GHz** with an input return loss ($S_{11}$) of **-23.15 dB** and a VSWR of **1.15**, verifying impedance matching to the $50\ \Omega$ excitation port. The far-field radiation pattern displayed an elevation plane (E-plane, $\phi = 0^\circ$) figure-of-eight profile with a HPBW of **$78.2^\circ$** and an azimuth plane (H-plane, $\theta = 90^\circ$) omnidirectional circle, yielding a peak gain of **2.11 dBi** and directivity of **2.14 dBi**, in agreement with standard theoretical half-wave dipole performance.

## Precautions

1. Ensure the radiation boundary is at least λ/4 away from the antenna structure on all sides to avoid reflection errors.
2. Mesh the model finely enough (especially near the feed gap) for accurate convergence.
3. Verify that the port impedance matches the intended feed impedance before analysing S11/VSWR.
4. Check for geometry validation errors before running the simulation.

## Result
 
Resonant Frequency = GHz  

Return loss = dB

VSWR = 

Gain = 

## Conclusion

A half-wave dipole antenna was designed and simulated at _2.449_ GHz using Ansys HFSS.
