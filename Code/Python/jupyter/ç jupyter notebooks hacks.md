# jupyter notebooks hacks

mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
related:: [[Jupyter]], [[Conda]]

# if you are exceeding data rate limits

jupyter notebook --NotebookApp.iopub_data_rate_limit=10000000000

# managing python kernels in jupyter notebooks

From:

[https://stackoverflow.com/questions/30492623/using-both-python-2-x-and-python-3-x-in-ipython-notebook](https://stackoverflow.com/questions/30492623/using-both-python-2-x-and-python-3-x-in-ipython-notebook)

The idea here is to install multiple ipython kernels. Here are instructions for anaconda. If you are not using anaconda, I recently added [instructions](https://stackoverflow.com/a/34464003/2272172) using pure virtualenvs.

## Anaconda 4.1.0

Since version 4.1.0, anaconda includes a special package nb_conda_kernels that detects conda environments with notebook kernels and automatically registers them. This makes using a new python version as easy as creating new conda environments:

```bash
conda create -n py27 python=2.7 ipykernel
conda create -n py36 python=3.6 ipykernel
```

After a restart of jupyter notebook, the new kernels are available over the graphical interface. Please note that new packages have to be explicitly installed into the new enviroments. The [Managing environments](http://conda.pydata.org/docs/using/envs.html) section in conda's docs provides further information.

## Manually registering kernels

Users who do not want to use nb_conda_kernels or still use older versions of anaconda can use the following steps to manually register ipython kernels.

configure the python2.7 environment:

```bash
conda create -n py27 python=2.7
source activate py27
conda install notebook ipykernel
ipython kernel install --user
```

configure the python3.6 environment:

```bash
conda create -n py36 python=3.6
source activate py36
conda install notebook ipykernel
ipython kernel install --user
```

After that you should be able to choose between python2 and python3 when creating a new notebook in the interface.

Additionally you can pass the --name and --display-name options to ipython kernel install if you want to change the names of your kernels. See ipython kernel install --help for more nformation.