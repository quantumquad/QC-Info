## Basic Physics Definitions

### Planck's Constant

**Planck's constant (h)** has the value:

> **h = 6.62607015 × 10⁻³⁴ joule·seconds (J·s)**

This is a **defined** constant — it's exact because it's used in defining the kilogram in the SI system.

---

### Units of h:
- **Joule·second (J·s)**  
- You can also write this as **kg·m²/s**, since:  
  1 J = 1 kg·m²/s², so J·s = kg·m²/s

---

### Reduced Planck's constant (**ħ**, or “h-bar”):
> **ħ = h / (2π) = 1.054571817 × 10⁻³⁴ J·s**

It **has the same units** as h:  
> **Joule·second (J·s)**

---

Both h and ħ appear in quantum mechanics:
- h: used in Planck's equation, \( E = h f \)
- ħ: used in Schrödinger’s equation, Heisenberg uncertainty, etc.

Cool! Let’s walk through an example and see how the units of **h** or **ħ** make sense physically.

---

### **Example 1: Planck’s Equation**
> \( E = h f \)  
Where:
- \( E \) is energy (in **joules**, J)
- \( f \) is frequency (in **1/s**, or **Hz**)
- \( h \) is Planck’s constant

Let’s check the units:

\[
[h] = \text{J·s}, \quad [f] = \text{1/s}
\]
\[
E = h f \Rightarrow [E] = (\text{J·s}) \cdot (1/\text{s}) = \text{J}
\]

Units check out: energy in joules.

---

### **Example 2: Heisenberg Uncertainty Principle**
> \( \Delta x \cdot \Delta p \geq \frac{\hbar}{2} \)

Where:
- \( \Delta x \) is position uncertainty (in **meters**)
- \( \Delta p \) is momentum uncertainty (in **kg·m/s**)
- \( \hbar \) has units of **J·s**, which is **kg·m²/s**

Let’s check:

\[
[\Delta x \cdot \Delta p] = \text{m} \cdot \text{kg·m/s} = \text{kg·m²/s}
\]
\[
[\hbar] = \text{kg·m²/s}
\]

So both sides have the same units. Again, it checks out.

---

### **1. Schrödinger Equation (Time-Independent)**

\[
-\frac{\hbar^2}{2m} \frac{d^2 \psi}{dx^2} + V(x) \psi = E \psi
\]

Where:
- \( \hbar \): reduced Planck’s constant (**kg·m²/s**)
- \( m \): mass (in **kg**)
- \( \psi \): wavefunction (unitless or normalized)
- \( V(x) \): potential energy (**J**)
- \( E \): total energy (**J**)

#### Let’s analyze the units of the kinetic energy term:

\[
\frac{\hbar^2}{2m} \cdot \frac{d^2 \psi}{dx^2}
\]

Step by step:
- \( \hbar^2 \) has units \( (kg \cdot m^2 / s)^2 = kg^2 \cdot m^4 / s^2 \)
- Dividing by mass \( m \) (in kg):  
  \[
  \frac{\hbar^2}{m} \Rightarrow kg \cdot m^4 / s^2
  \]
- The second derivative \( \frac{d^2}{dx^2} \) has units of \( 1/m^2 \)
- So:
  \[
  \frac{\hbar^2}{2m} \cdot \frac{d^2 \psi}{dx^2} \Rightarrow kg \cdot m^2 / s^2 = \text{J}
  \]

This term has units of **energy**, matching both \( V(x) \psi \) and \( E \psi \). All consistent!

---

### **2. Hydrogen Atom Energy Levels**

Formula for energy levels in hydrogen:

\[
E_n = -\frac{m e^4}{8 \varepsilon_0^2 h^2} \cdot \frac{1}{n^2}
\]

Or in terms of ħ:

\[
E_n = -\frac{m e^4}{2 (4\pi \varepsilon_0)^2 \hbar^2} \cdot \frac{1}{n^2}
\]

Where:
- \( m \): mass of the electron (kg)
- \( e \): charge of the electron (Coulombs)
- \( \varepsilon_0 \): vacuum permittivity
- \( \hbar \): reduced Planck’s constant
- \( n \): energy level (1, 2, 3, …)

Final units:
- All the constants combine to give units of **Joules**
- Energy decreases as \( 1/n^2 \), giving negative energy levels (bound states)

For the ground state:
\[
E_1 \approx -13.6 \, \text{eV}
\]

And **that number** — 13.6 eV — pops up all over physics and chemistry!

---

Let’s dive into the **Bohr radius**, which is another spot where **ħ** shows up in a very elegant way — and it helps show why quantum systems aren’t just tiny classical orbits.

---

### **Bohr Radius Formula**  
\[
a_0 = \frac{4\pi \varepsilon_0 \hbar^2}{m e^2}
\]

Where:
- \( a_0 \): Bohr radius — average distance between the proton and electron in hydrogen
- \( \varepsilon_0 \): vacuum permittivity (units: **C²/(N·m²)** or **C²·s²/(kg·m³)**)
- \( \hbar \): reduced Planck constant (**kg·m²/s**)
- \( m \): electron mass (**kg**)
- \( e \): electron charge (**C**)

---

### **Let’s check the units**

Start with:
\[
[\hbar^2] = \left(kg \cdot m^2/s\right)^2 = kg^2 \cdot m^4 / s^2
\]

And:
- \( [\varepsilon_0] = C^2 / (N \cdot m^2) = C^2 \cdot s^2 / (kg \cdot m^3) \)
- \( [e^2] = C^2 \)
- \( [m] = kg \)

So putting it all together:

\[
[a_0] = \frac{(C^2 \cdot s^2)/(kg \cdot m^3) \cdot kg^2 \cdot m^4 / s^2}{kg \cdot C^2}
\]

Simplify:
- \( C^2 \) cancels
- \( kg \) cancels one from numerator and denominator
- \( s^2 \) cancels
- Left with:

\[
a_0 \rightarrow m
\]

Perfect — the Bohr radius has units of **meters**, as expected!

---

### **Value:**
\[
a_0 \approx 5.291772109 \times 10^{-11} \text{ meters}
\]

This is the typical “size” of a hydrogen atom — a quantum result, not something you'd get from classical physics.

---

### **Why ħ shows up:**

- It relates **wavelength and momentum** via:  
  \[
  \lambda = \frac{h}{p} = \frac{2\pi \hbar}{p}
  \]
- In hydrogen, the electron’s orbit must "fit" an integer number of wavelengths — this quantization leads directly to energy levels and sizes like the Bohr radius.

So **ħ is basically what sets the scale** for how small quantum systems are. Without it, everything would behave classically, and atoms wouldn’t exist as stable structures.

---

### **Definition of the Fine-Structure Constant (α):**

## Fine-Structure Constant and Its Relation to ħ

The **fine-structure constant** (denoted by `α`) is a dimensionless constant that plays a key role in quantum electrodynamics. It links fundamental constants:

```
α = e² / (4π ε₀ ħ c)
```

Where:
- `e` is the elementary charge
- `ε₀` is the vacuum permittivity
- `ħ` is the reduced Planck constant (`h / 2π`)
- `c` is the speed of light

### Units Check

- Numerator: `e²` has units of C²
- Denominator: `ε₀ ħ c` also gives C²

So the units cancel out — α is **dimensionless**.

### Numerical Value

```
α ≈ 1 / 137.035999 ≈ 0.007297
```

### Physical Meaning

- α measures the **strength of the electromagnetic interaction**.
- It determines:
  - How tightly the electron is bound to the nucleus
  - The splitting of atomic energy levels (fine structure)
  - The probability of photons interacting with charged particles
  - How fast the electron moves in atomic orbits

### Electron Speed in Bohr Model

In the ground state of hydrogen:

```
v = α * c
```

This means the electron moves at about 1/137 the speed of light.

### Relation to Bohr Radius

The Bohr radius is defined as:

```
a₀ = (4π ε₀ ħ²) / (m e²)
```

Rewriting in terms of α:

```
a₀ = ħ / (m c α)
```

This shows that increasing α would shrink the hydrogen atom — a stronger electromagnetic force pulls the electron in tighter.

---

### Summary

- `ħ` sets the scale for quantum mechanics
- `e` and `ε₀` set the scale of electric charge
- `c` connects to relativity
- `α` ties all of them together as a pure number

Even small changes in α would change the structure of atoms and the chemistry of life.

---


---

# Quantum Constants and Equations

This document summarizes key quantum mechanical concepts and constants with units and examples.

---

## Planck’s Constant (h) and Reduced Planck’s Constant (ħ)

```
h = 6.62607015 × 10⁻³⁴ J·s  (exact, defined)
ħ = h / (2π) ≈ 1.054571817 × 10⁻³⁴ J·s
```

Units:
- `J·s` = `kg·m²/s`
- Both `h` and `ħ` have the same units

---

## Planck’s Equation

```
E = h * f
```

Where:
- `E` is energy (in joules, J)
- `h` is Planck’s constant
- `f` is frequency (in Hz or 1/s)

### Units Check

```
[h] = J·s
[f] = 1/s

E = h * f => J·s * 1/s = J
```

---

## Schrödinger Equation (Time-Independent)

```
- (ħ² / 2m) * (d²ψ / dx²) + V(x) * ψ = E * ψ
```

Where:
- `ψ(x)` is the wavefunction
- `ħ` is reduced Planck constant
- `m` is the particle mass
- `V(x)` is potential energy
- `E` is total energy

### Units of Kinetic Term

```
[ħ²] = (kg·m²/s)² = kg²·m⁴/s²
[ħ² / m] = kg·m⁴/s²
[d²/dx²] = 1/m²

=> (ħ² / m) * (1/m²) = kg·m²/s² = J
```

Units match energy.

---

## Bohr Radius

```
a₀ = (4π ε₀ ħ²) / (m e²)
```

Where:
- `ε₀` is vacuum permittivity
- `ħ` is reduced Planck constant
- `m` is the mass of the electron
- `e` is the elementary charge

### Units Check

```
[ħ²] = kg²·m⁴/s²
[ε₀] = C²·s² / (kg·m³)
[e²] = C²

Numerator: ε₀ ħ² = (C²·s² / kg·m³) * (kg²·m⁴ / s²) = kg·m
Denominator: m e² = kg·C²

a₀ = kg·m / (kg·C² / C²) = m
```

### Value

```
a₀ ≈ 5.291772109 × 10⁻¹¹ m
```

Also expressed as:

```
a₀ = ħ / (m c α)
```

---

## Fine-Structure Constant (α)

```
α = e² / (4π ε₀ ħ c) ≈ 1 / 137.035999
```

- **Dimensionless**
- Appears in all electromagnetic interactions

### Meaning

- Governs the strength of the electromagnetic force
- Appears in atomic structure, photon interactions, and QED
- The speed of the electron in the Bohr model ground state is:

```
v = α * c
```

---

## Summary

- `h`, `ħ`: set the scale for quantum mechanics
- `e`, `ε₀`: describe electric interactions
- `c`: speed of light, linking to relativity
- `α`: dimensionless measure of EM strength — a bridge between light, charge, and quantum behavior
- Changing `α` would radically change chemistry and the stability of matter

---

