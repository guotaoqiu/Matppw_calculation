# MatPPW - Materials Pseudopotential Plane Wave Calculator

MatPPW is a DFT (Density Functional Theory) calculation software compiled from MATLAB.

## Prerequisites

### MATLAB Runtime R2024a

MatPPW requires **MATLAB Runtime R2024a** to run.

**Download MATLAB Runtime:**
- https://ww2.mathworks.cn/products/compiler/matlab-runtime.html?s_tid=srchtitle_site_search_1_runtime

**On the HPC cluster**, the runtime is pre-installed at:
```
/public/software/apps/MATLAB/runtime/R2024a
```

## Getting the Executable

The executable file (`matppw.zip`) is too large to upload to GitHub.

You can find it on **VDrive2.0** at:
```
Enterprise/CATL/21C LAB/01 各二级机构文件夹/16 HTC+钟意/HTC/个人文件夹/01 HTC-个人文件夹/Qiu Guotao/matppw.zip
```

## Usage on HPC

1. Download `matppw.zip` from VDrive2.0
2. Upload to the HPC cluster
3. Unzip the file:
   ```bash
   unzip matppw.zip
   ```

4. Create a PBS submission script (example below):

```bash
#!/usr/bin/env bash
#PBS -N matppw
#PBS -q test
#PBS -l select=2:ncpus=192:mpiprocs=192
#PBS -o pbs.out
#PBS -j oe

echo "PBS_O_WORKDIR: ${PBS_O_WORKDIR}"
cd ${PBS_O_WORKDIR}

module purge
module load compilers/gcc/10.2.0

export GRIMME_DATA_DIR="/public/home/catl-bpit-hpc21/matppw/data/grimme_d"
MCRROOT="/public/software/apps/MATLAB/runtime/R2024a"

# Set ALL required MATLAB Runtime environment variables
export XAPPLRESDIR="${MCRROOT}/X11/app-defaults"
export LD_LIBRARY_PATH="${MCRROOT}/runtime/glnxa64:${MCRROOT}/bin/glnxa64:${MCRROOT}/sys/os/glnxa64:${MCRROOT}/sys/opengl/lib/glnxa64:${LD_LIBRARY_PATH}"
export MCR_USE_DISPLAY=0

MATPPW_EXEC="/public/home/catl-bpit-hpc21/matppw/dist_matppw/matppw"
INPUT_FILE="/public/home/catl-bpit-hpc21/matppw/catl-test/matppw/t302_opt_bulk/lic6_cg.toml"

echo "Starting matppw..."
"$MATPPW_EXEC" "$INPUT_FILE"

exit_status=$?
echo "matppw exit status: $exit_status"
exit $exit_status
```

5. Submit the job:
   ```bash
   qsub your_submission_script.sh
   ```

## Input and Output

- **Input format**: TOML configuration file
- **Output format**: HDF5

## System Requirements

- **OS**: Linux (64-bit)
- **MATLAB Runtime**: R2024a
- **Required environment**: HPC cluster with PBS job scheduler
