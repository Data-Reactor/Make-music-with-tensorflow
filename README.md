Google的[Magenta项目](https://github.com/tensorflow/magenta)用tensorflow让神经网络作曲，让我们来尝试用一下吧！
图片里显示的步骤基于ubuntu16.04LTS
## 步骤
### 第一步 安装magent
#### 自动安装
如果你是Mac OS X 或Ubuntu系统，可以直接复制下面这段代码到终端中
```
curl https://raw.githubusercontent.com/tensorflow/magenta/master/magenta/tools/magenta-install.sh > /tmp/magenta-install.sh
bash /tmp/magenta-install.sh
```
安装成功之后，在进行下一步之前，记得要激活magenta 
```
source activate magenta
```

如果不能用上面的方式安装，那么就手动安装吧～
#### 手动安装
##### 1.下载并安装[Python 2.7 Miniconda installer](https://conda.io/miniconda.html)
##### 2. 安装magenta
```
conda create -n magenta python=2.7 jupyter
source activate magenta
pip install magenta
```
每次打开一个新终端使用magenta之前，都需要激活magenta 
```
source activate magenta
```
### 第二步 配置环境(基于python2.7)
#### 1. git clone magenta
```
git clone https://github.com/tensorflow/magenta.git
```
#### 2. 安装[bazel](https://docs.bazel.build/versions/master/install.html)(一定要到官网安装)

#### 3.安装 python dependencies
```
pip install matplotlib scipy bokeh IPython pandas
```
#### 4. 安装[tensorflow](https://www.tensorflow.org/install/)(一定要到官网安装)



