---
title: Virtual Environment
date: 2024-06-26 11:47:07
tags:
  - python
  - virtualenv
  - jupyter-notebook
categories:
  - python
---

今天來分享如何應用 virtual env 來提高工作環境等效率。如果使用 python library 我想信很多時候都會用 pip 來安裝他的 library 等 module。如果某些套件版本跟你專安不 match 造成無法 code 無法運行怎麼呢?這時你只有降版本，也就是可能要先移除再安特殊版本。另一種方式就是建立一個 virtual env 也就是類似虛擬環境，這裡可以安裝任何 package or library 跟主環境分離不會有相關。

我覺得這個很好用，如果你原本主環境安裝太多 library 你有時還要 debug，你可以一開就建立在乾淨環境，再安裝你要安裝個 library or module 等 package。

可以用這兩終方式建立 virtualenv，如:

- `virtualenv` : 需要安裝套件
- `venv`:內建就有無須安裝特建

## venv

> Syntax: `python -m  venv <my_env_name>`
> EX: `python -m  venv venv`

- 如何用

```
#create new directory
mkdir newproject
cd newproject

#create virtual env
py -m  venv env_apitest

#activate
.\.env_apitest\Scripts\activate

#deactivate
deactivate

# upgrade python version
python -m venv /path/to/venv --upgrade
```

{% asset_img venv_usage.png  venv_example %}

## virtualenv

> 安裝: pip3 install virtualenv
> Syntax: `virtualenv <my_env_name>`

> 指令 python `-p`: virtualenv -p /path/to/python3 my_env_name
>
> > 用　`which` to check your python path

```
#create new directory
mkdir newproject
cd newproject

#default method
virtualenv my_env_name

# activate it
cd /python_env/bin/activate
#deactive
deactivate
```

{% asset_img virtualenv_usage.png  virtualenv_example %}

## 匯出匯入 libary

上面方式是我們學會如何建立 virtual env，現在來介紹如何匯出我們當下個 library 然後匯入

> - 匯出:
>   > `pip freeze > requirements.txt`
> - 出入:
>   > `pip install -r requirements.txt`
> - list all library
>   > `pip list` > > `pip3 list`

## virtual environments with Jupyter notebooks

我們也可以將我們 virtual environment 用在 jupter notebooks or labs，用下方法:

- 安裝: `pip install ipykernel`
- 建立 virtual env: `python -m ipykernel install --user --name=myenv `
- list env: `jupyter kernelspec list`

{% asset_img jupyter_virtual.png jupyter-notebook-virtualenv %}

- 移除: `jupyter kernelspec uninstall <myenv>`

{% asset_img jupyter_removeenv.png jupyter-remove-env %}

## Create Virtual Environment with Anaconda

- create virtualenv under conda: `conda create -n myenv`
- activate: `conda activate myenv`
- remove/uninstall: `conda env remove -n myenv`

## reference

- https://www.infoworld.com/article/3239675/virtualenv-and-venv-python-virtual-environments-explained.html
- https://janakiev.com/blog/jupyter-virtual-envs/
