---
title: "Using Conda manage package from some language"
date: 2022-10-29
author: Jianqi Huang
---

### Conda is What

conda and environment based on different environments

the command is about how to install miniconda.

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
sh Miniconda3-latest-Linux-x86_64.sh -b -p ${HOME}/software/miniconda3
rm -f Miniconda3-latest-Linux-x86_64.sh
echo "export PATH=${HOME}/software/miniconda3/bin:\$PATH" >> ~/.bashrc
source ~/.bashrc
conda --version
```

Of course, you can install from the conda website.



### using conda Install R and R package

#### adding R resource

```bash
conda config --add channels r
```

we can find out where is R

```bash
which R
```

using conda to search R

```
conda search r-base
```

check the environment currently

```
conda info -e     
```

create the environment

```bash
conda create -n env_name [python=<version>] # 创建环境，并指定python版本，或者安装包等；
```

创建的过程中会显示创建目录的位置，Proceed ([y]/n)? 选择y即可，下图为环境创建成功后的结果：

also the uninstall environment .

```bash
conda remove -n env_name --all  # 删除指定环境
```

list the package in conda 

```
conda list 
```



### A example

```bash
conda create -n R4.1.0
source activate R4.1.1
```

now the environment we created had activated and transfer into this env. Next we need to install some package in here.

```bash
conda install -c conda-forge r-base
```

the package is `r-base` so the other package could install by this way.

When we want to exit the current environment we just make the `deactivate`. Inputting the command below:

```
conda deactivate # 退出当前的conda环境；
```

