# Ultra-Coarse-Graining at Rapid Local Equilibrium (UCG-RLE) LAMMPS Pair Style

## Overview

This repository contains the implementation of the Ultra-Coarse-Graining at Rapid Local Equilibrium (UCG-RLE) theory for molecular simulations using the LAMMPS molecular dynamics engine. The UCG-RLE approach allows for coarse-grained simulations with rapid local equilibrium of internal states, providing an efficient way to model multi-component systems with complex interfacial dynamics.

The provided code includes:
- **pair\_table\_ucgrle.cpp**: The main C++ file implementing the UCG-RLE pair style for LAMMPS.
- **pair\_table\_ucgrle.h**: The header file defining the relevant data structures and functions used in the implementation.
- **state\_setting.txt**: An example input file for defining coarse-grained types and UCG states in LAMMPS.

## Key Features

- Efficient implementation of UCG force calculations using rapid local equilibrium theory.
- Multi-component liquid and liquid-liquid interface modeling capabilities.
- Optimized for performance by avoiding nested loops in force evaluations.
- Handles three-body-like interactions without requiring a Newton pair style.
- Highly transferable force fields, demonstrated for interfacial systems and hydrogen-bonding liquids.

## Files

### 1. `pair_table_ucgrle.cpp`
This file contains the core implementation of the UCG-RLE pair style in LAMMPS. It calculates the UCG potential energy and forces based on the substate probability functions and local density fields. The key routines include:

- **`threshold_prob_and_partial_from_cv`**: Computes substate probability functions and their radial derivatives.
- **`compute_proximity_function`**: Calculates the proximity function used to evaluate the local density of coarse-grained sites.
- **`compute_proximity_function_der`**: Computes the derivatives of the proximity function, necessary for the force calculations.
- **`compute`**: The main routine responsible for calculating the coarse-grained forces and potential energy during the simulation.

### 2. `pair_table_ucgrle.h`
The header file defines the data structures, constants, and function prototypes needed for the UCG-RLE pair style. It includes:

- Definitions of proximity functions and probability functions used in the UCG calculations.
- Declarations for the `compute` function and other helper routines involved in force evaluation.

### 3. `state_setting.txt`
This file serves as an example input for the UCG-RLE simulations. It defines the coarse-grained types, UCG states, and their associated parameters, including density thresholds and interaction potentials. The example provided is for a liquid-liquid interface system with two internal states for each CG site.

## Installation

1. Clone the repository:
   `git clone https://github.com/jaehyeokjin/UCGRLE-Public.git`
   `cd UCGRLE-Public`
2. Copy the `pair_table_ucgrle.cpp` and `pair_table_ucgrle.h` files to your LAMMPS source directory, usually located in src/PAIR/:
   `cp pair_table_ucgrle.cpp path_to_lammps/src/PAIR/`
   `cp pair_table_ucgrle.h path_to_lammps/src/PAIR/`
3. Compile LAMMPS with the new pair style:
4. Verify that the UCG-RLE pair style is included in the list of available pair styles by running: `lmp_mpi -h`
5. You should see the UCG-RLE pair style listed as pair_style `ucgrle`.

## Usage
To use the UCG-RLE pair style in a LAMMPS input script, include the following commands:
  `pair_style ucgrle`
  `pair_coeff * * state_setting.txt`
Make sure the `state_setting.txt` file is in the same directory or provide the full path.

## Example `state_setting.txt` File
  2 4
  2 density no_entropy
  12.5 11.00
  0.0
  2 density no_entropy
  12.5 7.00
  0.0

This defines a system with two coarse-grained types and two internal states for each type. Modify the parameters in the file to fit your specific simulation setup.

