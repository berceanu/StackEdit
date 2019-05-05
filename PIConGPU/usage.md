## Usage
```bash
# clone the parameter set from an example
$ pic-create $PIC_EXAMPLES/LaserWakefield $HOME/picInputs/lwfa_001
# or from an existing simulation
$ pic-create $SCRATCH/runs/lwfa_001/input $HOME/picInputs/lwfa_001
$ cd $HOME/picInputs/lwfa_001
# edit compile time include/picongpu/param/*.param files: laser profiles, particle distribution, etc
$ pic-edit grid laser density #...
# out-of-source build
$ pic-build
# see ./bin/picongpu --help for plugin options
# edit etc/picongpu/<number>.cfg file for runtime parameters: plugins, box size, etc
# see $PICSRC/docs/TBG_macros.cfg
## also see etc/picongpu/8.cfg listing from page 20 of 03_Input_...pdf
# submit job to cluster queue
$ tbg -s -t -c etc/picongpu/4.cfg $SCRATCH/runs/lwfa_001
# or explicitly tbg --submit qsub --tpl etc/picongpu/hypnos-hzdr/k80.tpl --cfg etc/picongpu/4.cfg $SCRATCH/runs/lwfa_001
```

## Conditions
- `Sim-Box-Size` in one direction must be integer multiple of `SuperCellSize` * `N_gpus` in that direction
- `SuperCellSize = 8x8x4` cells^3, see `memory.param`
### Moving window
- at least 2 GPUs required!
- simulation box is distributed over `N_gpus_y - 1`

## Folder contents
- `$PICSRC/share/picongpu/examples/`: Example configurations
- `./etc/picongpu/<cluster-name>/*.tpl`: Template file for `TBG` defining cluster-specific variables and `PIConGPU` invocation
- `./lib/python/picongpu/`: Files to read output of diagnostic plugins and to configure parameters scans via the GUI
- `./cmakeFlags`: File to configure (non-GUI) parameter scans
### Simulation output
- `./input/`: Containing input set, including `picongpu` binary
- `./tbg/`: Containing file `submit.start` which is submitted to batch system
	- `tail -n 1 tbg/submit.start` shows `tbg` command that was used to run the sim
- `./simOutput/`: simulation data output
