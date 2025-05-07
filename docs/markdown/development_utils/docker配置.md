# 配置docker
[docker教程](https://www.runoob.com/docker/docker-container-usage.html)

## docker使用步骤
### 安装docker
具体可以参考docker教程 
### 修改docker镜像源
[修改docker镜像源](https://blog.csdn.net/qq_73162098/article/details/145014490)
* 需要注意的是，macos上docker的daemon.json的路径应该在：/Users/<user_name>/.docker/daemon.json
* 找到daemon.json后，使用修改docker镜像源教程的方法添加多个镜像源即可。
* 目前我使用的镜像源：<br>
"registry-mirrors": [
    "http://hub-mirror.c.163.com",
    "https://mirror.ccs.tencentyun.com",
    "https://docker.m.daocloud.io",
    "https://docker.imgdb.de",
    "https://docker-0.unsee.tech",
    "https://docker.hlmirror.com",
    "https://docker.1ms.run",
    "https://func.ink",
    "https://lispy.org",
    "https://docker.xiaogenban1993.com"
  ]
* 或者，在Docker Desktop中，打开Setting-Docker Engine，添加上述registry-mirrors到配置文件中也可以

## 实战：DeepRec的部署
[DeepRec](https://deeprec.readthedocs.io/zh/latest/DeepRec-Compile-And-Install.html#id1)
DeepRec的部署需要用到docker。在我自己的MacBook m1上尝试部署。部署有两种方式：通过Docker部署（推荐）、手动部署。
首先，介绍第一种方式：通过docker部署：
### 安装docker
### 拉取镜像
拉取适配arm64版本且使用cpu的DeepRec镜像 `docker pull alideeprec/deeprec-release:deeprec2302-cpu-py38-ubuntu22.04-arm64`
### 创建容器
基于拉取的镜像，创建docker容器，可通过--name自定义名称`docker run -it --name deeprec-dev alideeprec/deeprec-release:deeprec2302-cpu-py38-ubuntu22.04-arm64 /bin/bash`
### clone code
在终端运行docker目录，然后在docker内，运行`git clone https://github.com/alibaba/DeepRec` 目的是将DeepRec的代码clone到docker容器中，然后在docker容器中直接运行代码
* 理解：我们拉取了代码的镜像，然后使用这个镜像，创建了一个docker容器。这样，在容器中就有代码运行所需的环境。只需要在容器中运行代码即可。
### 运行训练代码
以Wide & Deep模型为例。
* 首先，cd到模型数据目录：`cd /home/workdir/DeepRec/modelzoo/wide_and_deep/data`，并且下载数据集：<br>
`wget https://storage.googleapis.com/dataset-uploader/criteo-kaggle/large_version/train.csv` <br>
`wget https://storage.googleapis.com/dataset-uploader/criteo-kaggle/large_version/eval.csv`
* 然后，cd到模型目录：`cd /home/workdir/DeepRec/modelzoo/wide_and_deep`
* 运行训练脚本`python train.py --parquet_dataset False`（使用的是csv data，不是parquet data）<br>
顺利的话，模型就可以开始训练了。

<br>
另外，也可以手动部署。手动部署是在本地python环境中使用`pip install $DEEPREC_WHL`安装DeepRec运行依赖的package，然后手动下载数据集，在环境中运行`python train.py`即可。


