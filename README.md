# JupyterHub for Icesat-2 Hackweek

During the [Icesat-2 hackweek](https://icesat-2hackweek.github.io/) we are going to use a common computational environment running on Amazon Web Services: [https://icesat2.pangeo.io](https://icesat2.pangeo.io). This is a JupyterHub with a common and reproducible Python environment. This repo has some information about the Hub, and a copy of the Python environment file in case you want to run things on your personal computer.

icesat2.pangeo.io is running in the AWS region us-west-2. It is maintained by the [Pangeo project](http://pangeo.io) and is supported by [NASA Grant #17-ACCESS17-0003](https://github.com/pangeo-data/nasa-access-17) and cloud credits from Amazon. Access is currently limited to the [ICESAT-2HackWeek GitHub Organization](https://github.com/ICESAT-2HackWeek). The hub's configuration is stored in this [github repository](https://github.com/pangeo-data/pangeo-cloud-federation). To provide feedback and report any technical problems, please use the [github issue tracker](https://github.com/pangeo-data/pangeo-cloud-federation/issues).

**Why run on AWS?** There are some big advantages to using a common JupyterHub. Everyone has access to ephemeral computational resources, so you are not limited by your laptop CPU and RAM. We can easily share large amounts of data. Many of these tutorials are setup to utilize data that has been staged at `s3://pangeo-data-upload-oregon/`. If you try to download all this data over a typical WiFi connection you risk waiting a very long time and filling up your disk!


## Re-create the same JupyterHub Python environment on your personal computer

The Jupyter project has instructions for capturing the full Python environment from a Hub for re-use. See: https://mybinder.readthedocs.io/en/latest/tutorials/reproducibility.html

Run the following code to re-create the environment locally:

1) Install miniconda if you don't have it already:
```
https://docs.conda.io/en/latest/miniconda.html
```

2) Create a conda environment (**NOTE:** on a Mac replace `environment.yml` with `environment-mac.yml` in the command below)
```
conda env create -f environment.yml
```

3) Activate the environment and install jupyter lab extensions
```
conda activate icesat2-hackweek
jupyter serverextension enable --py nbserverproxy --sys-prefix
jupyter labextension install @jupyter-widgets/jupyterlab-manager \
                             @jupyterlab/hub-extension \
                             @pyviz/jupyterlab_pyviz \
                             jupyter-matplotlib \
                             jupyter-leaflet \
                             dask-labextension
```

4) Launch Jupyter Lab
```
jupyter lab
```


#### Why are there separate files for mac and linux?

There are some incompatibilities with conda packages on linux versus osx. 

For example, the following are linux-specific and therefore won't install on a mac laptop
```
ResolvePackageNotFound:
  - libgfortran-ng=7.3.0
  - libstdcxx-ng=7.3.0
  - libgcc-ng=7.3.0
```

#### Docker image
The docker image of the environment used during the hackweek can be found here:
https://cloud.docker.com/u/uwhackweeks/repository/docker/uwhackweeks/icesat2




