# Extend functionalities

Though pip, you can add more package to your python/Jupyter. The folloing are examples that apply to python3

## Install PYCUDA

If your home directory is in GPFS, open a Terminal in JupyterLab and run the following command:
```
python3 -m pip install pycuda
````

If your home directory is in AFS, ssh to ocio-gpu01 and run the following command:
```
singularity shell --nv -B /cvmfs,/gpfs,/scratch,/nfs,/afs /cvmfs/atlas.sdcc.bnl.gov/jupyter/t3s/slac/singularity/atlas-slac-w-slurm-cli-20200714.sif
```
Once you see the `Singularity>` prompt, type the following command:
```
unset PYTHONPATH
export PATH=$PATH:/usr/local/cuda/bin
python3 -m pip install pycuda
```
To test whether your pycuda works, try [this python script](pycuda.test.py.txt) in JupyterLab. The script contains two URLs that explain the concept of CUDA thread blocks and thread indexing.

## Use DASK with SLURM

[DASK](https://docs.dask.org/en/latest/) allows you to break down a large calculation into smaller parallel pieces. Here we are mostly interested in using DASK to spread the calculation via multiple SLURM jobs.

To enable DASK distributed scheduling/running with SLURM, first make sure when you start a JupyterLab instance, you choose an image that supports SLURM job submission, such as `atlas-jupyter-w-slurm-cli/20200714`. You will also need to use pip3 to install `dask-jobqueue` and `distributed`:

If you home directory is in GPFS, open a Terminal in JupyterLab and run the following command:
```
python3 -m pip install dask-jobqueue distributed
````

If your home directory is in AFS, ssh to ocio-gpu01 and run the following command:
```
singularity exec -B /cvmfs,/gpfs,/scratch,/nfs,/afs /cvmfs/atlas.sdcc.bnl.gov/jupyter/t3s/slac/singularity/atlas-slac-w-slurm-cli-20200714.sif python3 -m pip install dask-jobqueue distributed
```
To test whether your pycuda works, try [this python script](dask.slurm.test.py.txt) in JupyterLab. Please pay to the line `python="/usr/bin/python3"` in the script - do not forget about it. 

