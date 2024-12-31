# Hamiltonian Evolution

---

## Relationship Between Spins and Qubits

The terms **spins** and **qubits** are closely related in the context of quantum computing and condensed matter simulations, but their meanings and roles depend on the specific system being modeled and the mapping used. Let’s clarify the difference and why the relationship between spins and qubits varies across different models:

### **1. What Are Spins in Condensed Matter Physics?**
- **Spins** refer to quantum degrees of freedom that represent a two-level system. These are typically:
  - **Physical spins**: The intrinsic angular momentum of particles (e.g., electrons, nuclei).
  - **Effective spins**: Representations of other binary quantum variables, such as particle occupancy, pseudospins, or any system with two distinct states.

- **Spin Models**: Hamiltonians in condensed matter physics, such as the Ising or Heisenberg models, describe interactions between these spins in systems like magnetic materials.

### **2. What Are Qubits in Quantum Computing?**
- **Qubits** are the fundamental units of quantum information, corresponding to two-level quantum systems. They are the "spins" of the quantum computer.

- In simulations, qubits are used to encode the **state** of a quantum system being simulated, whether that system is described in terms of physical spins, particles, or other quantum degrees of freedom.

### **3. Why the Difference Between Spins and Qubits?**
The relationship between spins and qubits depends on how the Hamiltonian of the system is mapped to the quantum computer:

#### **(a) Direct Mapping (Spins = Qubits)**
For models like the **Transverse Field Ising Model**, the Hamiltonian already describes interactions between spins, which correspond directly to qubits:
\[
H = -\sum_{i} J Z_i Z_{i+1} - \sum_i h X_i
\]
- Each **spin** in the model maps to a single qubit.
- This is because the spins in the Ising model are already two-level systems, like qubits.

#### **(b) Indirect Mapping (Spins ≠ Qubits)**
For systems like the **Fermi-Hubbard model**, spins are not directly mapped to qubits because:
1. **Additional Degrees of Freedom**:
   - Each "site" in the Fermi-Hubbard model can hold up to two particles: one spin-up and one spin-down electron.
   - Each spin requires a separate qubit for encoding:
     - **1 site → 2 qubits**: One for spin-up, one for spin-down.

2. **Fermionic Nature**:
   - Fermionic systems require handling of the **anti-commutation relations** between particles.
   - Transformations like **Jordan-Wigner** or **Bravyi-Kitaev** map these fermionic degrees of freedom onto qubits, which increases the qubit count.

For example:
- A 1D Fermi-Hubbard chain with \( L \) sites would require \( 2L \) qubits, representing \( L \) spin-up and \( L \) spin-down electrons.

### **4. Why the Difference in Qubit Requirements?**

#### **Key Factors**:
1. **System Complexity**:
   - **Spin Systems** (e.g., Ising): Each spin is a simple two-level system → 1 qubit per spin.
   - **Fermionic Systems** (e.g., Hubbard): Each site has multiple possible states (e.g., spin-up and spin-down occupancy) → More qubits per site.

2. **Encoding Method**:
   - Models like the Ising model directly describe spins → Qubits = Spins.
   - Models like Fermi-Hubbard describe particles with more complex interactions and states → More qubits needed.

3. **Anti-Commutation Relations**:
   - Fermionic systems require transformations (e.g., Jordan-Wigner) that map fermionic operators to qubits. This mapping adds complexity and increases the qubit count.

### **5. Summary Comparison**

| **Model**                     | **Spins per Site** | **Qubits per Site** | **Reason**                                                                                                                                     |
|-------------------------------|--------------------|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| **Transverse Field Ising**    | 1                 | 1                   | Spins correspond directly to qubits (two-level systems with no additional degrees of freedom).                                                |
| **Fermi-Hubbard (1D)**        | 2 (spin-up/down)  | 2                   | Each site can hold one spin-up and one spin-down electron → Requires 1 qubit per spin.                                                        |
| **Heisenberg Model**          | 1                 | 1                   | Similar to Ising, as each spin directly maps to a qubit.                                                                                      |
| **Bose-Hubbard (Discrete)**   | 1                 | Varies              | Encoding depends on the local Hilbert space (e.g., 4 states per site → \(\lceil \log_2(4) \rceil = 2\) qubits per site).                       |
| **General Fermionic Systems** | Many              | Varies              | Requires mapping fermionic modes to qubits, often increasing qubit count depending on the number of orbitals and particles.                   |

### **6. Why This Matters**
The difference between spins and qubits is crucial for:
- **Hardware Requirements**: Determines how many qubits are needed to simulate the system.
- **Algorithm Design**: Different mappings (e.g., Jordan-Wigner vs. Bravyi-Kitaev) influence the qubit efficiency and complexity.
- **Interpretation**: Understanding whether spins map directly to qubits or require additional encoding helps avoid confusion when analyzing Hamiltonians.

Let me know if you'd like specific examples of mappings for other models or further clarification!

