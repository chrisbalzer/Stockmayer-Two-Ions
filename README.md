# Example Scripts for Two Ions in a Dipolar Solvent
Created by Chris Balzer (balzer@caltech.edu). Distributed under the MIT Licence.

## Overview
This repository contains the necessary input files to calculate one window of a potential of mean force (PMF) for two ions in a Stockmayer fluid. Inputs are provided for symmetric ions (as explored in the paper) and for asymmetric ions (i.e. NaCl).

## Contents
- ``input/``: Input files
- ``output-asymmetric/``: Output files for asymmetric ions
- ``output-symmetric/``: Output files for asymmetric ions

### Asymmetric System Description
1000 water molecules (0.03344 #/A^3) at 300K with dipole moment 1.85 Debyes. Anion and cation are modeled after chlorine and sodium, respectively. The diameters (LJ sigma) for each are 3.0 Angstroms, 3.62 Angstroms, 1.96 Angstroms for water, CL-, and Na+, respectively. The LJ unit of mass is 18.01528 g/mol. The LJ unit of length is 3.0 Angstroms. Water and NaCl parameters from [Shock et al](https://pubs.acs.org/doi/full/10.1021/acs.jpcb.0c00769).

### Symmetric System Description
1000 water molecules (0.03344 #/A^3) at 300K with dipole moment 1.85 Debyes. Anion and cation are monovalent and symmetric in size. The diameters (LJ sigma) for all components are 3.0 Angstroms. The LJ unit of mass is 18.01528 g/mol. The LJ unit of length is 3.0 Angstroms.

*Note that this system size may be too small to accurately get long range electrostatics. Only for demonstration/testing.*

## Input Description
For each example, the distance betweem the two ions is constrained between 2.25 and 6.0 Angstroms (0.75-2.0 sigma). The LAMMPS files provided go through energy minimization, initialization, equilibration, and production. Dump and thermo outputs are less frequent for space saving in the example.
- ``lammps.*.in`` - LAMMPS input file
- ``system.data`` - Initial system configuration
- ``input.equil.colvars`` and ``input.prod.colvars`` - Adaptive Biasing Force (ABF) input files to use the ``COLVARS`` package

## Running the Example
To run the example, LAMMPS must be compiled. Instructions to build LAMMPS can be found [here](https://docs.lammps.org/Build.html). The packages required for this project are the ``DIPOLE``, ``COLVARS``, ``KSPACE``, and ``MISC``. For speed reasons, it may be advantageous to enable the ``GPU`` package. If using the GPU package, one can run the example using

```
lmp_gpu -sf gpu -pk gpu 1 -in lammps.*.in
```

## Output Description
The output files are ...
- ``log.lammps`` - LAMMPS log file
- ``dump.dipoleInit``,``dump.dipoleEquil``,``dump.dipoleProd`` - Coordinates and dipole moment during initialization, equilibration, and production
- ``equil.pmf``, ``prod.pmf`` - The PMF calcualted from ABF
- ``equil.colvars.traj``, ``prod.colvars.traj`` - Instantaneous value of the collective variable (distance between ions)


![](box.gif)
