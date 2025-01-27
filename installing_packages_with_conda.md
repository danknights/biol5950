# Installing packages with Conda/Mamba
Sometimes MSI will not have the software you need. Installing your own software can be quite tricky,
but a subset of bioinformatics tools can be installed and used easily using a package management tools called _conda_.
There is also a package installer tool, _mamba_ that works with _conda_ and is much faster and more reliable
for the installation step and for creating environments. 

This tutorial shows how to install a package using these tools.

### Load the _conda_ module
You have to do this every time you log in to MSI and want to use conda.
```bash
module load conda
```

### Initialize _conda_ (first time only)
On MSI you may have to initialize _conda_ one time before you start using it. Run this command:
```bash
conda init
```
Now exit MSI completely and log back in.

### Create a new _conda_ environment
It is good practice to create a new _conda_ environment to install your software. This
way the installations won't mess up anything in your normal log-in environment.
```bash
mamba create -n aibio
```

### List your conda environments
In case you forget what they are called
```bash
conda info --envs
```
### Activate the new environment
You will have to do this every time you log in and want to use this environment. 
```bash
conda activate aibio
```

### Install a package
We will install the _roary_ package for pangenome analysis. Not all packages can be installed with _conda_/_mamba_, 
but a quick internet search for "install roary with conda" gives me this command: `conda install bioconda::roary`. 
We will use _mamba_ instead of _conda_.

Note: it's often necessary to include the "conda-forge" channel when installing packages. This is a collection of
many common packages. This may take about 5 minutes.
```bash
mamba install bioconda::roary -c conda-forge
```

### Test the installation
```bash
roary --version
```

### Alternative installation with `pip`
Many bioinformatics tools can be installed with mamba/conda, but there is an even easier method for 
common scientifice python packages. For example, _pip_ can install _pandas_ (used for using data tables in _python_),
or _numpy_ (for arrays and matrices in _python_).
You can always try pip first to see if a package is available there:
```bash
pip install pandas
```

However, it is still a good idea to create and activate a _conda_ environment before installing something with 
_pip_, so that you don't overwrite anything important in your base python environment.
### Exit the conda environment when done
```bash
conda deactivate
```

This is a very powerful process that can install otherwise tricky tools. For example, this same process can be used to install the _prokka_ genome annotation pipeline tool, which is missing from MSI.
