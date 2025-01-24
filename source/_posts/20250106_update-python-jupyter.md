---
title: update_python_jupyter
date: 2025-01-06 10:52:26
tags:
  - python
  - jupyter-notebook
categories:
  - python
---

This is a note for change your python version in jupyter Notebook. 今天想要分享如何換在 jupyter Notebook 換不同 python 般本

Please Install latest python for example python 3.13 which is the latest version, if you are going to switch to python 3.13. You don't have to install latest version, it's because I want to switch to python3.13, please be noted.

請務必先安裝最新的 python 3.13，由於我要切換到 python 3.13，因此必須要先安裝 python 3.13。

# Changing python version in jupyter

## Step changing python version

### Step1: Install package

- Install Jupyter (optional): `pip install jupyter`

- Install ipkernel: `pip install ipykernel`

You can also install under virtual environment

```
#1. create virtual env with conda
#syntax: conda create -n <virtual env name> python=3.13
conda create -n py313 python=3.13


#2. Activate the new environment
conda activate py313
```

you can also use conda command `conda env list` to list virtual env.

### Step2: Register the kernel

Install the Python kernel for the desired Python version.

```
python -m ipykernel install --user --name <python313> --display-name <"Python 3.13">

or

py -m ipykernel install --user --name py3.13
```

- `--user`: This installs the kernel for the current user, not system-wide.
- `--name python313`: This specifies the name of the kernel that will appear in Jupyter Notebook.
- `--display-name "Python 3.13"`: This sets the display name for the kernel in Jupyter Notebook, making it easier to identify.

### Step3: open jupyter Notebook

Open Jupyter notebook and change your kernel: ` kernel>change kernel` picture as below:

{% asset_img jupyter_kernel.PNG %}

or use this command:
`jupyter notebook --kernel python313`

# Other Jupyter Setting

Note: You can install jupyter notebook independent without need to anaconda.　可以獨立安裝 jupyter 等工具 不需要透過 anaconda

anaconda 安裝檔案又大，又吃資源，因此可以選擇獨立安裝。意下是最常在 anaconda 用的工具。

- Jupyter Notebook: `pip install jupyter`
- Jupyter Lab: `pip install jupyterlab`
- Spyder: `pip install spyder `

## Jupyter command

- launch jupyter-notebook: `jupyter notebook`
- Generate jupyter-notebook configure: `jupyter notebook --generate-config`
- check jupyter config location path: `jupyter --paths`
- check python version on notebook:

```
from platform import python_version
print(python_version())
```

- list all kernel: `jupyter kernelspec list`
- remove kernel: `jupyter kernelspec remove <kernel_name>`

## conda command

- list all package install in conda: `conda list`
- create virtual : `conda create -n <venv name> python=3.13`
- list all virtual env: `conda env list`
