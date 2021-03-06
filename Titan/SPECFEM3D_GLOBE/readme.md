# Scaling Test Setup


#### A. copy these scripts here:
- copy file `bashrc_setup` to root directory:
  ```
  cp bashrc_setup  ~/.bashrc_setup
  ```

  modify `~/.bashrc` for loading corresponding modules by adding:
  ```
  # load machine specifics
  if [ -f .bashrc_setup ]; then
    . .bashrc_setup
  fi
  ```

- copy setup directory `benchmark-scripts/` to a directory `~/benchmark-scripts`
  ```
  cp -rp ./benchmark-scripts ~/benchmark-scripts
  ```

- copy files `configure.titan.sh` and `mk_titan.sh` to code directory `~/SPECFEM3D_GLOBE/`
  ```
  cp configure.titan.sh ~/SPECFEM3D_GLOBE/
  cp mk_titan.sh ~/SPECFEM3D_GLOBE/
  ```

#### B. configure package:

```
cd ~/SPECFEM3D_GLOBE
./configure.titan.sh
```

compiles package with Cray compilers


#### C. compile to test successful compilation:

```
./mk_titan.sh
```

creates binaries in:
* bin.forward/ - holds `xspecfem3D` for forward simulations
* bin.kernel/  - holds `xspecfem3D` for kernel simulations


#### D. go to benchmark-scripts/ folder and run setups for scaling tests:

```
cd ~/benchmarks/
./setup_benchmark_configuration.sh
```


#### E. setup simulation, e.g., NPROC_XI = 4 and GPU turned on:

```
./setup_strongscaling.pl 4 GPU
```


#### F. go to the scratch work directory, e.g., /lustre/atlas/scratch/dpeter/geo111/ and submit job:

```
cd ${SCRATCH}/RUN/CPUstrong96/
qsub go_benchmark.titan.bash
```

