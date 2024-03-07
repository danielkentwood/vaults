# Package installation with conda-pack

##### Metadata
created:: 2023-05-15 10:42
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis #aetna 
kind:: #code
status:: #status/seed
language:: [[ç Python]], [[Linux]]
platform:: [[Conda]]
***

Sometimes the Aetna mirrors for conda and pip won't have the package (or package version) that you need. There are several solutions to this problem. Here are a few:
* *Ask IT*: Open a ticket with IT and request that the package be added to the mirror. 
* *Install from local repo*: Clone the repo locally and install the package by pointing to the local repo
* *Use conda-pack*: Install the package in an environment that has access (as long as this source environment has the same OS as the target environment), then use conda-pack to transfer the entire conda environment to your edge node as a pre-built conda environment.

Here are instructions for using the conda-pack method:

1. Create new conda environment in RStudio Workbench (for example, `healthycode`)
2. Install the package you need
3. Install conda-pack at the user level with pip: `pip install --user conda-pack`
4. Run conda pack to package the binaries into a tarball: `conda pack -n healthycode -o healthycode.tar.gz`
5. Move the compressed file to the home directory on your edge node
6. Delete the compressed file from your RStudio Workbench directory with `rm healthycode.tar.gz`
7. Run the following from the home directory on your edge node:

```bash
mkdir ~/.conda/envs/healthycode
tar -xzf healthycode.tar.gz -C ~/.conda/envs/healthycode
conda activate healthycode
conda unpack
ipython kernel install --user --name=healthycode
rm healthycode.tar.gz
```

You should be ready to go.

### Resources
- https://ckmanalytix.com/moving-conda-environments-with-conda-pack/
- https://www.anaconda.com/blog/moving-conda-environments
- https://conda.github.io/conda-pack/

