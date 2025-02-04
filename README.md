# Sudoku-Inspired Neural Network Simulation

## Overview
This repository contains a simulation of a **Sudoku-inspired threshold-coupled neural network** using **Brian2**, a neural simulation library. The model consists of 81 neurons arranged according to a valid Sudoku solution, with excitatory and inhibitory synaptic connections determined by the Sudoku structure.

## Simulation Details

### Neuron Model
The neurons are modeled with the following differential equation:

```
dv/dt = (I_d + I - v)/tau : 1
I = A*cos(2*pi*f*t) + 0.5 : 1
I_d : 1
```

where:
- `v` is the membrane potential
- `I` is an oscillatory input current with baseline offset
- `I_d` is a random drive current
- `tau` is the membrane time constant

### Network Structure
- **81 neurons** corresponding to Sudoku grid cells
- **Inhibitory connections** for neurons within the **same row**, **column**, or **3 X 3 subgrid**
- **Excitatory connections** within rest of the neurons

### Synaptic Connections
- **Excitatory synapses:** Positive coupling amongst neurons connected via excitation - Leads to synchronization
- **Inhibitory synapses:** Negative coupling amongst neurons connected via inhibition - Leads to desynchronization

## Installation & Dependencies
Ensure you have the required Python packages installed:
```sh
pip install brian2 brian2tools numpy matplotlib tqdm
```

## Running the Simulation
To execute the simulation:
```python
python main.py
```

The script will:
1. Initialize the neuron group based on a Sudoku solution.
2. Construct the connectivity matrix based on the Sudoku structure.
3. Run a **30-second simulation** (real-time equivalent).
4. Save **spike train data**.

## Output Files
- **Spike Train Data**: Saved in `indi/spike_train_seedirandom_with_drive_in{seedi}_exc{exc}_inh{inh}.txt`
- **Plots**:
  - Neuron membrane potentials
  - Population firing rate over time

## Parameters
| Parameter | Description | Value |
|-----------|-------------|-------|
| `A` | Amplitude of input current | `-0.2` |
| `f` | Input oscillation frequency | `10 Hz` |
| `tau` | Membrane time constant | `40 ms` |
| `exc` | Excitatory synaptic weight | `0.002` |
| `inh` | Inhibitory synaptic weight | `0.006` |
| `seedi` | Random seed for reproducibility | `[3]` |
| `I_d` | DC input to each of 9 groups | `0.59 to 0.67 ` |

## Visualization
The script produces:
- **Membrane potential distributions** for all neurons
- **Population rate plots** using `brian_plot(rate_mon)`

## Future Work
- **Adjust synaptic plasticity mechanisms** for dynamic learning
- **Explore different Sudoku solutions** to analyze structural effects
- **Compare with real neuronal recordings** to investigate cognitive representations

