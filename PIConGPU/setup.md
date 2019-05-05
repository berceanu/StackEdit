## `picongpu` fork
### Clone 
```bash
$ git clone git@github.com:berceanu/picongpu.git
$ cd picongpu
$ git checkout master
$ git checkout dev
```
### Update (!)
```bash
$ git clone git@github.com:berceanu/picongpu.git
$ cd picongpu # from here (!)
$ git checkout dev
$ git checkout master
$ git remote add upstream https://github.com/ComputationalRadiationPhysics/picongpu.git # only first time
$ git pull --ff-only upstream master
$ git push origin master
$ git checkout dev
$ git pull --ff-only upstream dev
$ git push origin dev
```

## SSH
```bash
$ ssh hemeraviauts # connects to hemera5 login and submit node
$ cp ./src/picongpu/etc/picongpu/hemera-hzdr/k80_picongpu.profile.example ~/k80_picongpu.profile # only first time
$ source ~/k80_picongpu.profile
# https://picongpu.readthedocs.io/en/latest/install/profile.html
```

## Jupyter notebook
```bash
$ ssh hypnosviauts
$ source jupyter.profile
# https://github.com/ComputationalRadiationPhysics/picongpu-workshop/issues/9#issuecomment-463117079
```
- `hzdr.de/jupyter`
	- `Start Jupyter Notebook` with Working Directory set to `/home/bercea20/picongpu-workshop-slides/notebooks` and 2 CPUs
	- wait ~ 1 minute
	- `go to tree`
		- URL will be of the form `http://hypnos5.fz-rossendorf.de:80<xx>/tree?`
- create ssh tunnel on local machine
	```bash
	$ ssh -f bercea20@uts.fz-rossendorf.de -L 90<xx>:hypnos5:80<xx> -N
	```
- go to `localhost:90<xx>` // `richard`
