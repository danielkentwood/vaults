# ç Installing Python Packages from a Jupyter Notebook
title:: ç Installing Python Packages from a Jupyter Notebook
created:: 2022-08-31 05:17
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
related:: [[Jupyter]], [[Conda]], [[Pip]]
***

See [this article](http://jakevdp.github.io/blog/2017/12/05/installing-python-packages-from-jupyter/) by Jake van der Plaas for a great discussion.

#### If you want to install a package to the current notebook kernel, there are two ways to do it. 

1. Using a magic command

		%conda install numpy

	or

		%pip install numpy

2. Using `sys`

		import sys
		!conda install --yes --prefix {sys.prefix} numpy

	or

		import sys
		!{sys.executable} -m pip install numpy

#### If you want to install a package to the shell environment that launched Jupyter, you can do this:

	!conda install --yes numpy

or 

	!pip install numpy


