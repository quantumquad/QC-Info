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
