mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
related:: [[Jupyter]], [[Conda]]

[https://medium.com/@nrk25693/how-to-add-your-conda-environment-to-your-jupyter-notebook-in-just-4-steps-abeab8b8d084](https://medium.com/@nrk25693/how-to-add-your-conda-environment-to-your-jupyter-notebook-in-just-4-steps-abeab8b8d084)

[https://danielkentwood.gitbook.io/wiki/data-science/devops/make-conda-environments-available-as-kernels-in-jupyterlab](https://danielkentwood.gitbook.io/wiki/data-science/devops/make-conda-environments-available-as-kernels-in-jupyterlab)

### Adding Kernels
	conda activate myenv
	conda install ipykernel
	ipython kernel install --user --name=myenv_kernel

### Removing Kernels
	conda activate myenv
	jupyter kernelspec uninstall myenv_kernel

How to remove the default python3 kernel (which sometimes makes it hard for jupyter to use the correct kernel)
[https://stackoverflow.com/questions/65954044/jupyterlab-how-to-remove-hide-default-python-3-kernel](https://stackoverflow.com/questions/65954044/jupyterlab-how-to-remove-hide-default-python-3-kernel)

### See list of available kernels
If you want to see a list of currently available kernels:

```bash
$ jupyter kernelspec list
```

### Installing packages to a specific kernel from Jupyter
Using the `!pip install` command will install the package to the instance of python that launched the jupyter instance. But we want to install the package to the kernel, not the jupyter version of python. You can do this with the magic commands `%conda install` or `%pip install`.




