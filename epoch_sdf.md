## Installing SDF Python library

1. Download the latest version of `EPOCH`  from [cfsa-pmw.warwick.ac.uk
](https://cfsa-pmw.warwick.ac.uk/EPOCH/epoch) to your local machine. As of 7/11/2018, this is `4.14.8`.
2. We now have to install the `SDF reader` Python module that comes with EPOCH.

```
cd epoch/SDF/C
make
cd epoch/SDF/utilities
source activate <ENV NAME>
which python # should return path to conda's env. Python 3.X
./build
```
where `<ENV NAME>` is the name of the Anaconda environment that you created. If you have not created any, use the default, called `base`, ie. `source activate base`.

This installs in `~/.local/lib/python3.X/site-packages/`. This should be in the Python import path, as can be checked by:
```
$ python
>>> import sys
>>> print('\n'.join(sys.path))
>>> import sdf
```

3. For usage, see SDF page on the [EPOCH wiki](https://cfsa-pmw.warwick.ac.uk/mediawiki/index.php/SDF:Python). You can now also play with the `sdf_helper_2d.ipynb` file that I sent you.

## Installing `postpic`
1. Install `postpic`, following the instructions on their [github page](https://github.com/skuschel/postpic)
```
source activate <ENV NAME>
pip install --user git+https://github.com/skuschel/postpic.git
```
 
2. After installing, check out the [EPOCH SDF example](http://nbviewer.jupyter.org/github/skuschel/postpic-examples/blob/master/epochSDF.ipynb) of `postpic`, ie the file `epochSDF.ipynb`. 

3. For full documentation, see the `postpic` [manual](https://postpic.readthedocs.io/en/latest/).

## Jupyter lab workflow
1. Install the Python 3 [Anaconda distribution](https://www.anaconda.com/download).
2. Go to your notebook folder, ie. where you store your `.ipynb` files.
3. Activate the default Anaconda environment, ie.: `source activate base`
4. Launch the web interface with: `jupyter lab`.
