# Conda, Mamba and Jupyterlab

# Conda

[Conda](https://docs.conda.io/en/latest/) is a package management mainly for Python but can basically used for any language. There are 2 installers, namely [miniconda](https://docs.conda.io/en/latest/miniconda.html) and [Anaconda](https://www.anaconda.com/). Miniconda is basically the minimal installer for conda while Anaconda is miniconda plus all the additional conda packages that are frequently used by data scientist.

## Installation of Conda
```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
sh Miniconda3-latest-Linux-x86_64.sh
```

If the installation is successful, an indicator `(base)` will be shown in your terminal (reopen a new terminal after installation). This indicate that the current active environment is the `(base)` environment.

## Usage

Refer to the [cheat sheet](https://docs.conda.io/projects/conda/en/latest/user-guide/cheatsheet.html) for all usage. 

### Create and Activate
Basically to create and use (activate) an environment:

```bash
conda create -n ENVNAME
conda activate ENVNAME
```

Note that after `conda activate ENVNAME`, your terminal should show `(ENVNAME)`. 

### Search and Install
To search/install a particular package(s):

```bash
conda search PACKAGENAME
conda install PACKAGENAME1 [PACKAGENAME2]
```

I do not recommend installing any package in the `(base)` environment (except `mamba`, see below), create a new environment for any new project or workflow.

### Remove a package (or an environment)
To delete a package(s) or an entire environment:

```bash
conda remove PACKAGENAME1 [PACKAGENAME2]
conda remove -n ENVNAME --all
```

Note that `-n` is used to specify the environment for `conda` to act on, otherwise `conda` will act on the current active environment.

### Info
To show how many environments are currently managed by `conda`:

```bash
conda info --env
```

# Mamba

[Mamba](https://mamba.readthedocs.io/en/latest/index.html) is a drop-in replacement for `conda` but faster. We will need conda for using mamba installation. A conda-independent mamba ([micromamba](https://mamba.readthedocs.io/en/latest/user_guide/micromamba.html)) is also available but will not be discussed here.

## Installation of Mamba

```bash
conda install -n base -c conda-forge mamba
```

## Conda vs Mamba
Basically mamba is a drop-in replacement for conda, so you can use mamba as you are using conda with few exception.

- To use `mamba activate` , it need to be initialized by `mamba init`.
- Instead of `conda search`, we need to `mamba repoquery search`.
- Mamba has yet to support `conda config`.

From here onward, this tutorial will assume `mamba` is installed and use `mamba` command instead of `conda` 

### Channels

If you notice, during `mamba` installation, we supply a `-c` flag. This is to indicate which channel (=repository) to look for a particular package. Conda only have defaults channel initially, but we might need more packages that are not in the defaults channel.

There are 2 channels that are useful in addition to the defaults channel. To add the channel:

```bash
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
conda config --set channel_priority strict
```

The first three line add the channels and the last line activate the strict channel priority (see [here](https://conda-forge.org/docs/user/tipsandtricks.html) for more). The sequence of channel addition is important as the channel added last will be the first channel `conda` look for packages. In this case, `conda-forge` -> `bioconda` -> `defaults`. This setting is saved in the file `~/.condarc`.

### Update

We can update package or all packages via:

```bash
mamba update PACKAGENAME1 [PACKAGENAME2]
mamba update --all
```

However, for `(base)` environment, I recommend not to do so but only update `mamba` to avoid package conflict.

```bash
mamba update mamba
```

# Jupyter
*To be added*