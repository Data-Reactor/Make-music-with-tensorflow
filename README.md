Google的[Magenta项目](https://github.com/tensorflow/magenta)用tensorflow让神经网络作曲，让我们来尝试用一下吧！
## 步骤
### 第一步 安装magent
#### 自动安装
如果你是Mac OS X 或Ubuntu系统，可以直接复制下面这段代码到终端中
```
curl https://raw.githubusercontent.com/tensorflow/magenta/master/magenta/tools/magenta-install.sh > /tmp/magenta-install.sh
bash /tmp/magenta-install.sh
```

安装成功之后，每次打开一个新终端使用magenta之前，都需要激活magenta 
```
source activate magenta
```

如果不能用上面的方式安装，那么就手动安装吧～
#### 手动安装
##### 下载并安装[Python 2.7 Miniconda installer](https://conda.io/miniconda.html)
##### 安装magenta
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
#### git clone magenta
```
git clone https://github.com/tensorflow/magenta.git
```

#### 安装[bazel](https://docs.bazel.build/versions/master/install.html)(一定要到官网安装)

#### 安装 python dependencies
```
pip install matplotlib scipy bokeh IPython pandas
```
#### 安装[tensorflow](https://www.tensorflow.org/install/)(一定要到官网安装)

#### 配置完成之后测试一下能不能正常运行：
```
bazel test //magenta/...
```
### 第三步 正式开始！
#### 获取.mid文件
首先，你需要一些.mid格式的歌曲，你可以[到网站上下载](http://www.midishow.com)，也可以把[.mp3转化为.mid](https://www.ofoct.com/audio-converter/convert-wav-or-mp3-ogg-aac-wma-to-midi.html)。

打开终端，激活magenta:
```
source activate magenta
```
进入你git clone 得到的magenta文件夹，建立一个名为```notesequences.tfrecord```的空白文件

#### 创建NoteSequences
```
convert_dir_to_note_sequences \
 --input_dir=/home/manyue/magenta/train/mid \　　　　
 --output_file=/home/manyue/magenta/train/notesequences.tfrecord \　
 --recursive  
```
```--input_dir```是存储.mid文件的文件夹地址，```--output_file```是```notesequences.tfrecord```的地址，把上面的换为你的存储地址即可

记得前面的```--```和后面的反斜杠```\```

#### 创建SequenceExamples
建立一个名为```SequenceExamples```的空白文件夹，下面的代码运行外之后，```SequenceExamples```里会生成两个文件：```training_melodies.tfrecord ``````eval_melodies.tfrecord ```
```
melody_rnn_create_dataset \
--config=lookback_rnn \
--input=/home/manyue/magenta/train/notesequences.tfrecord \
--output_dir=/home/manyue/magenta/train/SequenceExamples \
--eval_ratio=0.10 
```
```--input```是```notesequences.tfrecord```的地址，```--output_dir```是```SequenceExamples```的地址，换为你的地址即可
#### 训练模型
创建一个名为```run1```的文件夹
```
melody_rnn_train \
--config=lookback_rnn \
--run_dir=/home/manyue/magenta/train/run1 \
--sequence_example_file=/home/manyue/magenta/train/SequenceExamples/training_melodies.tfrecord \
--hparams="batch_size=64,rnn_layer_sizes=[64,64]" \
--num_training_steps=1000 
```
```--run_dir```是```run1```文件夹的地址，```--sequence_example_file```是上一步生成的文件```training_melodies.tfrecord```的地址
