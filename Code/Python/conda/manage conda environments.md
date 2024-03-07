mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
related:: [[Conda]]

## Create a new environment
`conda create --name my_new_env python=3.8`

## Create a new environment based on an existing one
`conda create --name boa_jupyterlab --clone boa`

## Create a new environment based on a requirements.txt file
`conda create --name voila --file requirements.txt python=3.8`

## Check which conda channels are being indexed for new packages
`conda config --show channels`

## Set conda-forge to be the priority channel
`conda config --add channels conda-forge`
`conda config --set channel_priority strict`

## Install and upgrade pip
`conda install pip`
`pip install --upgrade pip`

## Installing plotly so that it can render in jupyterlab
install plotly
`conda install plotly=5.7.0`

ensure you're using jupyterlab>=3 and ipywidgets>=7.6
`conda install "jupyterlab>=3" "ipywidgets>=7.6"`

if you want to build dash apps in jupyterlab, install jupyter-dash
`conda install -c conda-forge jupyter-dash`
`conda install -c conda-forge nodejs`
`jupyter lab build`

ensure that jupyterlab-plotly (and jupyterlab-dash, if you added it) is installed in jupyterlab as an extension
`jupyter labextension list`

If not, go here: [https://plotly.com/python/troubleshooting/](https://plotly.com/python/troubleshooting/)

## Remove an environment
`conda remove --name myenv --all`



##### for running jupyterlab
"plotly=5.7.0" "jupyterlab>=3" "ipywidgets>=7.6"

##### for environments that use Boa or PyConnect:
retrying
pyarrow
dask
pyhive
kazoo
sasl
joblib

##### commonly used packages for analytics/DS
numpy
plotly
pandas
statsmodels
scikit-learn
scipy
pyspark
seaborn
matplotlib
shap


