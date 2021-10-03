# anaconda3 常用命令



## 目录

* [conda 命令](# conda 命令)

* [启动jupyter notebook](# 启动jupyter notebook)

* [jn安装代码自动补全包](# 安装代码自动补全)

* [查看当前环境下使用的Python](# 查看当前环境下使用的Python)

  



### conda 命令

~~~bash
# 查看conda环境变量路径
conda info --envs
conda info -e

# 查看所有envs
conda env list

# 版本 
conda -V

#激活环境
conda activate [环境路径]

#停止激活
conda deactivate

#查看conda的python版本
python -V

#查看当前环境下已安装的包
conda list 

#新建一个envs,安装到默认环境路径下
## conda create -n [envs_name] [python=版本号] [anaconda]
conda create -n BCI python=3.8
## 创建虚拟环境时就把基于python3.8版本的anaconda中的其他库一次性安装好
conda create -n BCI python=3.8 anaconda

#新建一个envs，安装到指定路径下
conda create --prefix=D:\Anaconda3\envs\BCI python=3.8
~~~



### 启动jupyter notebook

~~~bash
# 命令行启动jupyter notebook
jupyter notebook [工作空间路径]

#或者先转到工作目录，在执行
jupyter notebook
~~~



### 安装代码自动补全

~~~bash
# 安装代码自动补全
## 1,关闭Jupyter notebook
## 2.pip 安装一个包

pip install jupyter_contrib_nbextensions
jupyter contrib nbextension install --user

## 3.安装nbextensions_configurator

pip install jupyter_nbextensions_configurator
jupyter nbextensions_configurator enable --user

## 4.重启jupyter notebook 在主页新增的Nbextensions标签页中勾选Hinterland
~~~



### 查看当前环境下使用的Python

~~~python
import sys
sys.path
~~~

