# MatPPW - Materials Pseudopotential Plane Wave Calculator

MatPPW is a specialized DFT (Density Functional Theory) calculation software, part of the **3D Specialized Integrated Platform for Materials Simulation**. This tool is compiled from MATLAB and designed for high-throughput computational materials science workflows.

## Overview

MatPPW is a standalone executable that performs specialized plane wave DFT calculations. It's optimized for HPC (High Performance Computing) environments and integrates with the CATL-HTC (High-Throughput Computing) platform for materials discovery and characterization.

## Prerequisites

### MATLAB Runtime R2024a

MatPPW requires **MATLAB Runtime R2024a** to run.

**On the HPC cluster**, the runtime is pre-installed at:
```
/public/software/apps/MATLAB/runtime/R2024a
```

**For local installation**, download MATLAB Runtime R2024a from:
- https://www.mathworks.com/products/compiler/mcr/index.html

Alternatively, if you have MATLAB installed, you can locate the MCR installer by running:
```matlab
>> mcrinstaller
```
in the MATLAB prompt.

## Installation

### On HPC Cluster

1. Clone this repository:
```bash
git clone <repository-url>
cd Matppw_calculation
```

2. The executable and run script are located in:
```
matppw/dist_matppw/
```

3. Make the run script executable:
```bash
chmod +x matppw/dist_matppw/run_matppw.sh
```

### Local Installation

If installing locally, ensure you:
1. Install MATLAB Runtime R2024a
2. Set up the required environment variables (see Configuration section)
3. Extract the matppw executable package

## Usage

### Basic Usage

Run matppw using the provided shell script:

```bash
./matppw/dist_matppw/run_matppw.sh /public/software/apps/MATLAB/runtime/R2024a /full/path/to/your/input.toml
```

**Syntax:**
```bash
./run_matppw.sh <MATLAB_RUNTIME_DIR> <INPUT_TOML_FILE>
```

**Parameters:**
- `MATLAB_RUNTIME_DIR`: Path to MATLAB Runtime installation
  - On HPC: `/public/software/apps/MATLAB/runtime/R2024a`
  - Local: Your MATLAB Runtime or MATLAB installation directory
- `INPUT_TOML_FILE`: Full path to your input configuration file (TOML format)

### Example

```bash
cd matppw/dist_matppw
./run_matppw.sh /public/software/apps/MATLAB/runtime/R2024a /home/user/calculations/example_input.toml
```

## Configuration

### Environment Variables (Optional)

If not using the `run_matppw.sh` script, you can manually set environment variables:

```bash
export MATLAB_RUNTIME=/public/software/apps/MATLAB/runtime/R2024a
export XAPPLRESDIR=$MATLAB_RUNTIME/X11/app-defaults
export LD_LIBRARY_PATH=$MATLAB_RUNTIME/runtime/glnxa64:$MATLAB_RUNTIME/bin/glnxa64:$MATLAB_RUNTIME/sys/os/glnxa64:$MATLAB_RUNTIME/sys/opengl/lib/glnxa64:$LD_LIBRARY_PATH
```

To make these persistent, add them to your `~/.bashrc` or `~/.bash_profile`.

## Input File Format

MatPPW accepts input in **TOML** format. The TOML file should contain all calculation parameters including:
- Structure information
- Calculation settings
- Pseudopotential specifications
- Computational parameters

Refer to the manual (see Documentation section) for detailed input file specifications.

## Output Format

MatPPW generates results in **HDF5 format** following the CATL-HTC-specified calculation results structure.

For detailed information about the output structure, refer to:
```
matppw/hdf5_structure.xlsx
```

This file documents the binary structure and data organization of the HDF5 output files.

## Repository Structure

```
Matppw_calculation/
├── README.md                          # This file
├── matppw/
│   ├── dist_matppw/                   # Compiled executable and runtime files
│   │   ├── matppw                     # Main executable
│   │   ├── run_matppw.sh              # Shell script for execution
│   │   ├── readme.txt                 # Original MATLAB compiler readme
│   │   └── MCRInstaller.zip           # MATLAB Runtime installer (optional)
│   ├── MatPPW_manual_Chinese.pdf      # User manual (Chinese)
│   └── hdf5_structure.xlsx            # HDF5 output format specification
```

## Documentation

### User Manual

A comprehensive Chinese manual is available:
```
matppw/MatPPW_manual_Chinese.pdf
```

This manual includes:
- Theoretical background
- Input file preparation
- Calculation workflows
- Result interpretation
- Examples and tutorials

### Output Format Specification

The HDF5 output structure is documented in:
```
matppw/hdf5_structure.xlsx
```

## Troubleshooting

### Common Issues

**1. Permission Denied**
```bash
chmod +x matppw/dist_matppw/run_matppw.sh
chmod +x matppw/dist_matppw/matppw
```

**2. MATLAB Runtime Not Found**
Ensure the runtime path is correct:
```bash
ls /public/software/apps/MATLAB/runtime/R2024a
```

**3. Library Loading Errors**
The `run_matppw.sh` script handles library paths automatically. If you encounter issues, check that `LD_LIBRARY_PATH` is set correctly.

**4. Input File Errors**
Verify your TOML file syntax and ensure all required parameters are specified according to the manual.

## System Requirements

- **OS**: Linux (64-bit)
- **RAM**: Depends on calculation size (typically 4GB minimum)
- **Disk**: Sufficient space for input/output files
- **MATLAB Runtime**: R2024a

## Performance Notes

For HPC usage:
- MatPPW is designed for batch job submission
- Optimal performance on multi-core systems
- Ensure adequate memory allocation based on system size
- HDF5 output enables efficient post-processing

## Contributing

For issues, feature requests, or contributions, please contact the development team.

## License

[Specify license information]

## Citation

If you use MatPPW in your research, please cite:
```
[Add citation information]
```

## Contact

For support and questions:
- [Add contact information]
- [Add issue tracker or support email]

## Acknowledgments

MatPPW is part of the 3D Specialized Integrated Platform for Materials Simulation.

---

**Note**: This software is part of a high-throughput computational materials platform. For integration with other components of the platform, refer to the main platform documentation.
