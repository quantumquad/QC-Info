# Simulating an Electron and Position Orbiting System

## Representing Momentum (Kinetic Energy)
To represent momentum, we need to include both position and momentum in our state representation. In quantum mechanics, position 
𝑥
^
 and momentum 
𝑝
^
 are represented by operators that act on the wavefunction.

Quantum Harmonic Oscillator Basis
A common approach is to use the quantum harmonic oscillator basis, where we can represent the states in terms of position and momentum eigenstates. For simplicity, let's focus on how to initialize a quantum state that includes both position and momentum.

## Initializing Qubits with Position and Momentum
Here's an example of initializing the qubits to represent both position and momentum:
  
    from qiskit import QuantumCircuit, Aer, execute
    from qiskit.quantum_info import Statevector
    import numpy as np
    
    # Define the initial positions and momenta
    x1, y1 = 1.0, 0.0  # Position of Particle 1
    px1, py1 = 0.0, 1.0  # Momentum of Particle 1
    x2, y2 = -1.0, 0.0  # Position of Particle 2
    px2, py2 = 0.0, -1.0  # Momentum of Particle 2
    
    # Function to map positions and momenta to qubit states (simplified example)
    def state_to_qubit_state(x, y, px, py):
        # Example mapping: Use amplitude encoding (simplified for illustration)
        theta = np.arctan2(y, x)
        phi = np.arctan2(py, px)
        return [np.cos(theta/2), np.sin(theta/2) * np.exp(1j * phi)]
    
    # Initialize the quantum circuit with 4 qubits
    qc = QuantumCircuit(4)
    
    # Map positions and momenta to qubit states
    state1 = state_to_qubit_state(x1, y1, px1, py1)
    state2 = state_to_qubit_state(x2, y2, px2, py2)
    
    # Initialize the qubits with the mapped states
    qc.initialize(state1, [0, 1])  # Particle 1
    qc.initialize(state2, [2, 3])  # Particle 2
    
    # Show the circuit
    print(qc)
    
## Measuring Position and Momentum
In quantum computing, measuring position and momentum typically involves transforming the state and performing multiple measurements to extract the desired information.

Position Measurement
To measure the position, you can directly measure the qubit states. However, for a more accurate representation, you may need to use a series of quantum gates to extract the amplitude and phase information:

    from qiskit import transpile
    from qiskit.visualization import plot_histogram

    # Add measurement operations
    qc.measure_all()
    
    # Execute the circuit and get the results
    backend = Aer.get_backend('qasm_simulator')
    job = execute(qc, backend, shots=1024)
    result = job.result()
    counts = result.get_counts(qc)
    
    # Visualize the results
    plot_histogram(counts)
    
### Momentum Measurement
Momentum measurement involves transforming the state into the momentum basis, which can be done using the quantum Fourier transform (QFT):
    
    from qiskit.circuit.library import QFT
    
    # Create a QFT circuit for momentum measurement
    qft_circuit = QFT(4, do_swaps=False).inverse()
    
    # Combine the QFT circuit with the initial state circuit
    qc.append(qft_circuit, [0, 1, 2, 3])
    
    # Add measurement operations
    qc.measure_all()
    
    # Execute the circuit and get the results
    job = execute(qc, backend, shots=1024)
    result = job.result()
    counts = result.get_counts(qc)
    
    # Visualize the results
    plot_histogram(counts)

### Putting It All Together
Initialize the Qubits: Represent both position and momentum using amplitude encoding.

Measure Position: Directly measure the qubit states.

Measure Momentum: Use the quantum Fourier transform to switch to the momentum basis and measure the states.

## Summary
This approach allows you to initialize the qubits with both position and momentum,
and then measure these quantities using appropriate transformations and measurements.

## Setting Initial Position and Momentum

If your initial position and momentum set the particles on a path where they are going to separate, evolving the state with the Hamiltonian should indeed reflect this behavior.

How It Works:
Initial State: You initialize the qubits with the positions and momenta of the particles.

Hamiltonian Evolution: You evolve this state using the Hamiltonian which encodes the kinetic and potential energy terms.

Measurement: By periodically measuring the state, you should observe changes in the qubit states that correspond to the particles moving apart.

What to Expect:
Increasing Distance: The distance between the particles (reflected in the qubit states) should increase over time, indicating that they are moving away from each other.

Changes in Energy: The kinetic and potential energy contributions will change as the particles move, which will be reflected in the Hamiltonian's influence on the state.

### Practical Steps:
To see this in action, you would:

Initialize the Initial State: As described in the earlier examples, encode the positions and momenta into the qubits.

Evolve the State: Use the Hamiltonian to evolve the state over multiple time steps.

Measure the State: After each time step, measure the qubits to extract the positions and momenta.

### Example Code Snippet:
Here's a conceptual example of how you might set up and run this simulation:
 
    from qiskit import QuantumCircuit, Aer, execute
    from qiskit.quantum_info import Statevector
    from qiskit.opflow import X, Z, I, PauliTrotterEvolution, CircuitStateFn
    
    # Define the initial positions and momenta
    x1, y1 = 1.0, 0.0  # Position of Particle 1
    px1, py1 = 0.0, 1.0  # Momentum of Particle 1
    x2, y2 = -1.0, 0.0  # Position of Particle 2
    px2, py2 = 0.0, -1.0  # Momentum of Particle 2
    
    # Function to map positions and momenta to qubit states
    def state_to_qubit_state(x, y, px, py):
        theta = np.arctan2(y, x)
        phi = np.arctan2(py, px)
        return [np.cos(theta/2), np.sin(theta/2) * np.exp(1j * phi)]
    
    # Initialize the quantum circuit with 4 qubits
    qc = QuantumCircuit(4)
    
    # Map positions and momenta to qubit states
    state1 = state_to_qubit_state(x1, y1, px1, py1)
    state2 = state_to_qubit_state(x2, y2, px2, py2)
    
    # Initialize the qubits with the mapped states
    qc.initialize(state1, [0, 1])  # Particle 1
    qc.initialize(state2, [2, 3])  # Particle 2
    
    # Define the Hamiltonian evolution step
    def evolve_state(initial_state, H, num_steps):
        evolved_state = initial_state
        for _ in range(num_steps):
            evolution_operator = PauliTrotterEvolution().convert(H)
            evolved_state = evolution_operator @ evolved_state
        return evolved_state
    
    # Calculate weights based on initial positions
    ke_weight = kinetic_energy_weight(x1, y1, x2, y2)
    pe_weight = potential_energy_weight(x1, y1, x2, y2)
    
    # Define the Hamiltonian with calculated weights
    H = (ke_weight * (X^I^I^I)) + (pe_weight * (Z^I^Z^I))
    
    # Initial state as a StateFn
    initial_state = CircuitStateFn(qc)
    
    # Evolve the state over time
    num_steps = 10  # Number of time steps to simulate
    evolved_state = evolve_state(initial_state, H, num_steps)
    
    # Measurement step
    qc.measure_all()
    backend = Aer.get_backend('qasm_simulator')
    job = execute(qc, backend, shots=1024)
    result = job.result()
    counts = result.get_counts(qc)
    
    # Visualize the results
    plot_histogram(counts)

By following these steps, you can simulate and observe how the particles' positions and momenta evolve over time, reflecting their movement apart due to the initial conditions.

## More Complex Hamiltonian

Let's delve into why we used a simpler Hamiltonian in the example and discuss the implications of using a more complex Hamiltonian with additional terms.

Why Use a Simple Hamiltonian?
Clarity: For illustrative purposes, starting with a simpler Hamiltonian helps to understand the basic principles and steps without being overwhelmed by complexity.

Focus on Core Concepts: The example aimed to demonstrate the process of initializing the state, defining a Hamiltonian, and evolving the state. A simpler Hamiltonian allows us to focus on these core concepts.

Why Use a More Complex Hamiltonian?
Accuracy: A more complex Hamiltonian with additional terms can capture more nuances of the system, providing a more accurate representation of interactions and dynamics.

Detailed Dynamics: Including more terms can account for higher-order interactions, ensuring that all relevant physical processes are modeled.

### Example of a Complex Hamiltonian
Here's a more complex Hamiltonian with additional terms:

    python
    from qiskit.opflow import X, Y, Z, I
    
    # Define the Hamiltonian with more terms
    H = (
        (0.3, 'XIII') + (0.3, 'IXII') + (0.3, 'IIXI') + (0.3, 'IIIX') + 
        (0.3, 'YIII') + (0.3, 'IYII') + (0.3, 'IIYI') + (0.3, 'IIIY') + 
        (0.2, 'ZIZI') + (0.2, 'IZIZ') +
        (0.1, 'XIXI') + (0.1, 'YIYI') + (0.1, 'ZZZZ') +
        (0.1, 'XYXY') + (0.1, 'YXYX')
    )
    
    # Display the Hamiltonian
    print("Complex Hamiltonian:")
    print(H)
    
Implications of Using Different Hamiltonians
Results: A more complex Hamiltonian can provide different and often more accurate results, capturing more details of the system's behavior.

Computation: However, a more complex Hamiltonian can also require more computational resources and time to simulate, especially as the number of terms and qubits increases.

### Choosing the Right Hamiltonian
System Complexity: For simple systems or initial explorations, a simpler Hamiltonian might suffice.

Accuracy Needs: For detailed and precise simulations, especially for research or practical applications, a more complex Hamiltonian with additional terms is preferable.

### Summary
Simple Hamiltonian: Good for initial understanding and less complex systems.

Complex Hamiltonian: Necessary for accurate and detailed simulations of more intricate systems.

Using a more complex Hamiltonian for your simulation can yield richer insights and more precise results. If

## Equilibrium Distance

there is a well-known distance at which equilibrium occurs for an electron-positron pair. This equilibrium distance is determined by the balance between the Coulomb attraction and the kinetic energy of the particles.

Equilibrium Distance: Bohr Radius
For hydrogen-like systems (e.g., electron-proton), the equilibrium distance is known as the Bohr radius 
𝑎
0
. For an electron-positron pair (positronium), the Bohr radius is similarly used as a reference. The Bohr radius is given by:

𝑎
0
=
4
𝜋
𝜖
0
ℏ
2
𝑚
𝑒
𝑒
2
where:

𝜖
0
 is the vacuum permittivity,

ℏ
 is the reduced Planck's constant,

𝑚
𝑒
 is the electron mass,

𝑒
 is the elementary charge.

For positronium, the Bohr radius 
𝑎
0
 is approximately:

𝑎
0
≈
5.29
×
1
0
−
11
 meters
Checking the Hamiltonian
To ensure your Hamiltonian is correctly written, you can:

Analytical Check: Verify that the terms included in the Hamiltonian correctly represent the kinetic and potential energy components based on known physics.

Numerical Simulation: Run a numerical simulation to compare the results with known analytical results for simple cases (e.g., equilibrium distance, energy levels).

Analytical Verification
Kinetic Energy Terms:

Ensure that the kinetic energy terms are correctly scaled and represented by Pauli operators.

Potential Energy Terms:

Verify that the potential energy terms accurately capture the Coulomb attraction between the electron and positron.

### Numerical Simulation Example
Here’s a concrete example to verify the Hamiltonian numerically:

    import numpy as np
    from qiskit import QuantumCircuit, Aer, execute
    from qiskit.opflow import X, Z, I, PauliTrotterEvolution, CircuitStateFn
    
    # Define the equilibrium positions (Bohr radius)
    a0 = 5.29e-11  # Bohr radius in meters
    x1, y1 = a0, 0.0  # Particle 1 at (a0, 0)
    x2, y2 = -a0, 0.0  # Particle 2 at (-a0, 0)
    
    # Define the initial momenta (assuming circular orbit)
    px1, py1 = 0.0, np.sqrt(1 / a0)
    px2, py2 = 0.0, -np.sqrt(1 / a0)
    
    # Define the position and momentum to qubit state function
    def state_to_qubit_state(x, y, px, py):
        theta = np.arctan2(y, x)
        phi = np.arctan2(py, px)
        return [np.cos(theta/2), np.sin(theta/2) * np.exp(1j * phi)]
    
    # Initialize the quantum circuit with 4 qubits
    qc = QuantumCircuit(4)
    
    # Map positions and momenta to qubit states
    state1 = state_to_qubit_state(x1, y1, px1, py1)
    state2 = state_to_qubit_state(x2, y2, px2, py2)
    
    # Initialize the qubits with the mapped states
    qc.initialize(state1, [0, 1])  # Particle 1
    qc.initialize(state2, [2, 3])  # Particle 2
    
    # Calculate weights based on initial positions
    def kinetic_energy_weight(x1, y1, x2, y2):
        distance = np.sqrt((x1 - x2)**2 + (y1 - y2)**2)
        return 1 / (distance + 1e-5)
    
    def potential_energy_weight(x1, y1, x2, y2):
        distance = np.sqrt((x1 - x2)**2 + (y1 - y2)**2)
        return 1 / (distance**2 + 1e-5)
    
    ke_weight = kinetic_energy_weight(x1, y1, x2, y2)
    pe_weight = potential_energy_weight(x1, y1, x2, y2)
    
    # Define the Hamiltonian with calculated weights
    H = (ke_weight * (X^I^I^I)) + (pe_weight * (Z^I^Z^I))
    
    # Initial state as a StateFn
    initial_state = CircuitStateFn(qc)
    
    # Define the time evolution operator
    evolution_operator = PauliTrotterEvolution().convert(H)
    
    # Evolve the state over time
    num_steps = 10
    evolved_state = initial_state
    for _ in range(num_steps):
        evolved_state = evolution_operator @ evolved_state
    
    # Measurement step
    qc.measure_all()
    backend = Aer.get_backend('qasm_simulator')
    job = execute(qc, backend, shots=1024)
    result = job.result()
    counts = result.get_counts(qc)
    
    # Visualize the results
    from qiskit.visualization import plot_histogram
    plot_histogram(counts)

### Key Points
Initialization: Initialize the qubits with the Bohr radius to reflect the equilibrium position.

Hamiltonian Evolution: Use the Hamiltonian to evolve the state and observe the system's behavior.

Verification: Compare the simulation results with known equilibrium distance and energy levels for positronium.

### Conclusion
By setting up the initial positions and momenta correctly and evolving the state using a well-defined Hamiltonian, you can verify whether the Hamiltonian correctly represents the system. For the electron-positron system, the Bohr radius provides a reference point for equilibrium distance.


## Measuring Position and Momentum as Continuous Variables

The position and momentum are continuous variables, and the values can indeed be anywhere between 0 and 1 (or other ranges, depending on the encoding). Let's address how to measure and extract continuous values for position and momentum.

### Measuring Continuous Position and Momentum
Position Measurement
Amplitude Encoding: In quantum computing, the position can be encoded in the amplitude of the qubit states.

#### Extracting Amplitude: 

To extract the position, we can use the probability distribution obtained from measurements and decode the amplitude.

Here's the revised code for extracting continuous position values:

    import numpy as np
    from qiskit import QuantumCircuit, Aer, execute
    from qiskit.visualization import plot_histogram
    from qiskit.quantum_info import Statevector, density_matrix
    
    # Define the initial positions and momenta
    x1, y1 = 0.5, 0.5  # Position of Particle 1
    px1, py1 = 0.3, 0.7  # Momentum of Particle 1
    
    # Function to map positions and momenta to qubit states
    def state_to_qubit_state(x, y, px, py):
        theta = np.arctan2(y, x)
        phi = np.arctan2(py, px)
        return [np.cos(theta/2), np.sin(theta/2) * np.exp(1j * phi)]
    
    # Initialize the quantum circuit with 2 qubits for simplicity
    qc = QuantumCircuit(2)
    
    # Map positions and momenta to qubit states
    state1 = state_to_qubit_state(x1, y1, px1, py1)
    qc.initialize(state1, [0, 1])  # Particle 1
    
    # Simulate the quantum circuit
    backend = Aer.get_backend('statevector_simulator')
    job = execute(qc, backend)
    result = job.result()
    statevector = result.get_statevector(qc)
    
    # Extract position from the statevector (amplitude encoding)
    probabilities = np.abs(statevector)**2
    positions = np.linspace(0, 1, len(probabilities))
    x_position = np.sum(positions * probabilities)
    
    print("Extracted Position:", x_position)

#### Momentum Measurement
For momentum measurement, use the Quantum Fourier Transform (QFT) to transform the state into the momentum basis and then extract the continuous values:

    from qiskit.circuit.library import QFT
    
    # Create a QFT circuit for momentum measurement
    qft_circuit = QFT(2, do_swaps=False).inverse()
    
    # Combine the QFT circuit with the initial state circuit
    qc = QuantumCircuit(2)
    qc.initialize(state1, [0, 1])  # Particle 1
    qc.append(qft_circuit, [0, 1])
    
    # Simulate the quantum circuit
    job = execute(qc, backend)
    result = job.result()
    statevector = result.get_statevector(qc)
    
    # Extract momentum from the statevector (amplitude encoding)
    probabilities = np.abs(statevector)**2
    momenta = np.linspace(0, 1, len(probabilities))
    px_momentum = np.sum(momenta * probabilities)
    
    print("Extracted Momentum:", px_momentum)

### Summary
Position Measurement: Use amplitude encoding to extract continuous position values from the statevector.

Momentum Measurement: Apply QFT to transform the state into the momentum basis and extract continuous momentum values.

This approach ensures that you can extract and interpret continuous values for both position and momentum from the quantum measurements.


