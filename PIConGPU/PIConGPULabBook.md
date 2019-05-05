### TODOS
- [x] HDF5 Spack debugging @CETAL [#2777](https://github.com/ComputationalRadiationPhysics/picongpu/issues/2777)
- [x] run with less frequent `HDF5` output
- [x] Nitrogen run @CETAL @HOME
- [ ] Dubna install [#2752](https://github.com/ComputationalRadiationPhysics/picongpu/issues/2752)
- [ ] make radiation python module compatible to other modules [#2778](https://github.com/ComputationalRadiationPhysics/picongpu/issues/2778)
- [ ] PWFA references from [Downer et al](https://paperpile.com/shared/OJUNKl)
- [ ] Spack development workflow [#2787](https://github.com/ComputationalRadiationPhysics/picongpu/issues/2787) + [sourcetrail](https://www.sourcetrail.com)

#### next
- [ ] PIConGPU @ Hypnos `hydrogen` `PWFA` `2D` `radiation plugin` `bunch acceleration`
- [ ] [bunch acceleration example](https://github.com/steindev/picongpu/tree/topic-2018_bunch-accel-ulf/share/picongpu/examples/BunchAcceleration)
- [ ] macro-particle form factors for coherent and incoherent radiation [zenodo](http://dx.doi.org/10.5281/zenodo.1161232)


### Resources
- Official [repository](https://github.com/ComputationalRadiationPhysics/picongpu)
- Manual on [readthedocs](https://picongpu.readthedocs.io/en/0.4.1/)
- Doxygen docs for the [API](http://computationalradiationphysics.github.io/picongpu)
- [Homepage](https://www.hzdr.de/db/Cms?pOid=31887&pNid=0)
- Project [wiki](https://github.com/ComputationalRadiationPhysics/picongpu/wiki)

### Bunch acceleration example
> If you adjust this example (density.param, etc..) and eventually also  
include temperature Manipulators (for finite emittance) you can obtain  
an electron bunch with your desired properties after some initial  
acceleration. Then you just create a checkpoint and after a restart with  
a recompiled PIConGPU using a standard pusher you can directly use this  
electron bunch for your subsequent PWFA setting.

#### Parameters from PRL **120** 254802 (2018)
- LWFA stage, w. `CALDER-CIRC`
	* 800 nm, 15 J, 30 fs (FWHM intensity) linearly polarized along $x$ axis, spot size 23 $\mu$m FWHM int., $a_0 = 6$
	* speed of light in vaccum c = 0.2998 $\mu$m/fs
	* laser angular frequency $\omega_0$ = 2.355 ~~rads~~/fs; $c/\omega_0 = 0.1273$ $\mu$m/~~rad~~; $\omega_0^{-1} = 0.4246$ fs/~~rad~~
	* laser focal plane at the begining of the entrance ramp of the pre-ionized plasma
	* 15 mm plasma, $n_e = 1.75 \times 10^{18}$ cm${}^{-3}$, linear entrance ramp of 200 $\mu$m
	* use 3 poloidal modes
	* Esirkepov algorithm with Boris pusher
	* moving window
		+ 3200x200 cells, 16 ppc, so $1.02 \times 10^7$ macro-particles
		+ $\Delta z = 0.25\, c/\omega_0 = 31.83$ nm longitudinal, $\Delta r = 4 \, c/\omega_0 = 509.2$ nm radial
	* time step $\Delta t = 0.249\, \omega_0^{-1} = 0.105$ fs, total propagation length 22 mm
- Transition between stages
	* position and momenta of electrons recorded 
	* low energy part ($E < 350$ MeV) is filtered out
	* electron beam consists of $1.2 \times 10^5$ macro-particles
	* beam self-field is computed in the vacuum and initialized before the simulation starts
- PWFA stage, w. `CALDER`
	* 3.3 mm preionized plasma, $n_e = 1.1 \times 10^{20}$ cm${}^{-3}$, linear entrance ramp of 25 $\mu$m
		* $n_{beam} > 1.8 n_e$ so $n_e \leq 2 \times 10^{20}$ cm${}^{-3}$ in order to generate wakefield
		* the 30 $\mu$m long electron beam generates a current of tens of kA
		* max beam energy 2 GeV
	* Esirkepov algorithm with Boris pusher
	* moving window
		+ 800x200x200 cells (z,x,y)
		+ $\Delta z = \Delta x = \Delta y = 0.5\,c/\omega_0 = 63.65$ nm
	* time step $\Delta t = 0.288\, \omega_0^{-1} = 0.122$ fs
	* 1 ppc, so $3.2 \times 10^7$ particles
	* vacuum propagation of electron beam for 65 $\mu$m before it enters the plasma
- Single stage run, w. `CALDER`
	* 2400x200x200 cells, 2ppc, so $1.92 \times 10^8$ macro-particles
	* $\Delta z = 0.25\,c/\omega_0 = 31.83$ nm, $\Delta x = \Delta y = 4 \, c/\omega_0 = 509.2$ nm
	* $\Delta t = 0.248\, \omega_0^{-1} = 0.105$ fs
	* 200 $\mu$m linear ramp followed by 19 mm plateau at $n_e = 1 \times 10^{19}$ cm${}^{-3}$


### Running the LWFA example @ CETAL with adios

```
pic-create $PIC_EXAMPLES/LaserWakefield $HOME/picInputs/adiosLWFA
pic-build -b "cuda:60"
```
```
diff -Naru etc/picongpu/8.cfg.old etc/picongpu/8.cfg

--- /home/andrei/picInputs/h5LWFA/etc/picongpu/8.cfg.old	2018-10-29 14:20:54.298800616 +0200
+++ etc/picongpu/8.cfg	2018-11-04 00:38:11.296744333 +0200
@@ -36,7 +36,7 @@
 TBG_devices_y=4
 TBG_devices_z=1
 
-TBG_gridSize="192 2048 160"
+TBG_gridSize="512 2048 512"
 TBG_steps="4000"
 
 # leave TBG_movingWindow empty to disable moving window
@@ -68,12 +68,19 @@
           --hdf5.file simData \
           --hdf5.source 'species_all,fields_all'"
 
+# ADIOS raw data output (DISABLED, add to TBG_plugins below to ENABLE!)
+TBG_adios="--adios.period 100   \
+          --adios.file simData \
+          --adios.source 'species_all,fields_all'"
+
+
 # macro particle counter (electrons, debug information for memory)
 TBG_e_macroCount="--e_macroParticlesCount.period 100"
 
 TBG_plugins="!TBG_pngYX                    \
              !TBG_e_histogram              \
              !TBG_e_PSypy                  \
+             !TBG_adios                    \
              !TBG_e_macroCount"
 
 #################################
```
```
tbg -s bash -c etc/picongpu/8.cfg -t etc/picongpu/bash/mpiexec.tpl $SCRATCH/runs/lwfa_adios
```

- simulation completes successfully
-- elapsed time: 1h 2m
-- occupied disk space: 1.8T

#### Running with custom `libSplash`
Follow instructions in [#2777 comment](https://github.com/ComputationalRadiationPhysics/picongpu/issues/2777#issuecomment-435843111):

- Add this to `$SPACK_ROOT/var/spack/repos/builtin/packages/libsplash/package.py`:
```
version('printHDF5ErrorStackOnWrite', branch='topic-printHDF5ErrorStackOnWrite', git='https://github.com/ax3l/libSplash.git')
```
- In your `src/spack-repo/packages/picongpu/package.py`, loosen the constrain on `libSplash`:
```
depends_on('libsplash@1.7.0,printHDF5ErrorStackOnWrite', when='+hdf5')
``` 
and then,
```
spack install picongpu backend=cuda cppflags="-g" ^libsplash@printHDF5ErrorStackOnWrite %gcc@7.3.0
spack load picongpu backend=cuda cppflags="-g" ^libsplash@printHDF5ErrorStackOnWrite %gcc@7.3.0
export SPLASH_VERBOSE=99

pic-create $PIC_EXAMPLES/LaserWakefield $HOME/picInputs/HDF5ErrorStack

cd picInputs/HDF5ErrorStack/
pic-build -b "cuda:60"
cp ../adiosLWFA/etc/picongpu/8.cfg etc/picongpu/8.cfg

nohup tbg -s bash -c etc/picongpu/8.cfg -t etc/picongpu/bash/mpiexec.tpl $SCRATCH/runs/HDF5ErrorStack &
```

### Installing the development version of PIConGPU via `Spack`
As mentioned in this [comment](https://github.com/ComputationalRadiationPhysics/picongpu/pull/2784#issuecomment-435777343/):

> you can always use a preview of `PIConGPU`, without `Changelog` and unannounced breaking changes, by using the `dev` branch via `spack install picongpu@develop`
> `spack uninstall` and `spack install` again for updates

### Nitrogen-based LWFA simulation

- LWFA run output from Hypnos [on GDrive](https://drive.google.com/file/d/1Kj-nqOjhq6pdQMuUAOW2LpNtUbv9mfPw/view?usp=sharing)

**Only in 002/Nitrogen**
`components.param`
`particleFilters.param`
`radiationObserver.param`
`radiation.param`
`speciesAttributes.param`

**Differences**
- [x] `density.param`
- [x] `fieldSolver.param`
- [x] `grid.param`
- [x] `laser.param`
- [x] `particle.param`
- [x] `png.param`
- [x] `precision.param`
- [x] `speciesDefinition.param`
- [x] `speciesInitialization.param`

```
~/picInputs/Nitrogen$ nohup tbg -s bash -c etc/picongpu/64.cfg -t etc/picongpu/bash/mpiexec.tpl $SCRATCH/runs/Nitrogen &
```

- simulation completes successfully
-- elapsed time: 9h 20m
-- occupied disk space: 1.5T


### Useful `Spack` commands
- `$ spack spec -l /<hash>` to check dependencies
- `$ spack load /<hash>` to load a package by hash
- `$ spack find -d /hash` to see dependencies

- [package repositories](https://spack.readthedocs.io/en/latest/repositories.html)
- [specs and dependencies](https://spack.readthedocs.io/en/latest/basic_usage.html#specs-dependencies)
- 


### Torque job scheduler (Hypnos)
List of [commands](https://csdms.colorado.edu/wiki/Help:HPCC_Torque).


### OpenMPI 
- `mpirun --mca btl ^openib ...` in order to "disable" infiniband
  
### Hardware
- with 2 GTX 1080 Ti
	- `FBPIC` 6000x250 with 3 poloidal modes
	- `PIConGPU` 2000x200x200 with ionization and 1 ppc

### PIConGPU params
-   default supercell  `8x8x4`
-   box is 1536x2880x1536; cubic cells $\Delta x = \Delta y = \Delta z$
-   3 ion species and 1 electron species (total of $\sim 10^9$ particles; simulation is field dominated)

### Git commands
- checking out remote branch
```
$ git fetch
$ git checkout <branch>
```

### Bash
- send message to all logged users
```
$ sudo wall -n hi
```
- find different files between two directory trees
```
diff --brief -Nr dir1/ dir2/
```