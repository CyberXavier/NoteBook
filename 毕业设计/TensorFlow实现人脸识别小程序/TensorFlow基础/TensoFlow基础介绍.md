# TensorFlow



## TensorFlow概念介绍



### 目录

* [Graph](#Graph)
* [Session](#Session)
* [Tensor](#Tensor)
* [Operation](#Operation)
* [Feed](#Feed)
* [Fetch](#Fetch)
* [综合小例子](#综合小例子)
* [TensorFlow高层封装与常用接口](#TensorFlow中的核心API)



### 什么是TensorFlow？

* Google开源的基于数据流图的科学计算库，适用于机器学习，深度学习等人工智能领域；
* [TensorFlow源码](https://github.com/tensorflow)
* [TensorFlow现成模型](https://github.com/tensorflow/models)



### Tensorflow特点

* 高度的灵活性
* 真正的可移植性
* 将科研和产品联系在一起
* 自动求微分
* 多语言支持
* 性能最优化
* 社区内容丰富



### Graph

#### 概念

* 图描述了计算过程，可用tensorboard图形化流程结构
  * 声明（单个/多个）
    * 单个：单个网络解决任务声明单个图；多个：多个网络解决任务声明多个图
  * graph保存为pb文件（也就是网络结构保存为pb文件）
    * pb文件包括了网络结构和网络参数
  * 从pb中恢复Graph
  * Tensorboard可视化



#### TensorFlow中实现

* 声明

> ~~~python
> import tensorflow as tf
> g = tf.Graph()
> g = tf.get_default_graph()
> #创建一个常量张量，value=0；
> x = tf.constant(0)
> g = x.graph
> ~~~



* 如何声明和交叉使用多个graph

> ~~~python
> g1 = tf.Graph()
> # 将计算图二设为默认计算图
> with g1.as_defualt():
>     x1 = tf.constant(1.0,name="x1")
> 
> g2 = tf.Graph()
> with g2.as_default():
>     x2 = tf.constant(2.0,name="x2")
> 
> ~~~



* 保存pb

~~~python
g1 = tf.Graph()
tf.train.write_graph(g1.as_graph_def(),'.','graph.pb',False)
~~~



* 从pb中恢复Graph

~~~python
# load graph
with gfile.FastGFile("graph.pb",'rb') as f:
    graph_def = tf.GraphDef()
    graph_def.ParseFromString(f.read())
    tf.import_graph_def(graph_def,name='')
    
sess = tf.Session()
# 节点获取graph.get_tensor_by_name()
c1_tensor = sess.graph.get_tensor_by_name("c1:0")
c1 = sess.run(c1_tensor)
~~~



* 使用tensorboard可视化计算图结构
  * tensorboard是通过中间结果的记录（例如a,b,c,d,e）来可视化计算图结构

~~~python
import tensorflow as tf
a = tf.constant(1,name='input_a')
b = tf.constant(2,name='input_b')
c = tf.multiply(a,b,name='multiply_c')
d = tf.add(a,b,name='add_d')
e = tf.add(d,c,name='add_e')
sess = tf.session()
sess.run(e)
#指定一个文件保存图	tf.summary.FileWritter(path,sess.graph)
writer = tf.summary.FileWriter('graph',sess.graph)
~~~



### Session

#### 概念

* 计算图必须在“会话”的上下文中执行
* 会话将图的operation分发到CPU或GPU之类的设备上执行
* session的操作
  * 创建与关闭
  * 注入机制
  * 指定设备
  * 资源分配



#### tensorflow中实现

* 创建与关闭

~~~python
#直接创建session
sess = tf.session()
#交互式session
sess = tf.InteractiveSession()
#with 定义session作用域
with tf.session as sess:
    #......

sess.close()
~~~



* 注入机制
  * 是具体完成计算图运算的过程
  * 是完成了前端和后端的交互作用

~~~python
#运算
sess.run()
#tf.globle_variables_initializer--获取变量并初始化，通过run--完成初始化
sess.run(tf.globle_variables_initializer())

#占位符
a = tf.placeholder(dtype=tf.float32)
b = tf.placeholder(dtype=tf.float32)
add = a+b
#在进行add计算时才会通过feed_dict{}对a,b进行赋值
# feed其实就是注入数据过程
add_val = sess.run(add,feed_dict={a:1,b:2})
~~~



* 指定资源设备

~~~python
a = tf.placeholder(dtype=tf.float32)
b = tf.placeholder(dtype=tf.float32)
add = a+b
with tf.Session() as sess:
    with tf.device("/cpu:0"):
        print(sess.run(add,feed_dict={a:1,b:2}))
~~~



* 资源分配
  * 通过配置config实现GPU资源的按需分配

~~~python
#将allow_growth设置为true
config = tf.configProto()
config.gpu_option.allow_growth = true
session = tf.Session(config=config,......)
~~~



### Tensor

#### 概念

* TensorFlow中Tensor是“张量”的意思；Flow的意思是“流或者流动”
* 张量可理解为：多为阵列
* 张量中没有真存储数字，它存的是如何得到数字的计算过程
* 一个张量存储了三个属性：名字、维度、型别



#### 定义

* 常量：tf.constant()
* 变量：tf.variable()
* 占位符：tf.placeholder()
* 稀疏张量：tf.SparseTensor()

~~~python
cons = tf.constant(value=[1,2],dtype=tf.float32,shape=(1,2),name='',verify_shape=False)

w = tf.Variable(tf.zeros([3,10]),dtype=tf.float32,name='w')

x = tf.placeholder(dtype=tf.float32,shape=[144,10],name='x')
#不知道具体维度时用none
x = tf.placeholder(dtype=tf.float21,shape=[None,None],name='x')
~~~



### Operation

* TensorFlow Graph中的计算节点，输入输出都是Tensor
* 计算Tensor值：
  * session.run(Tensor)
  * Tensor.eval()



### Feed

* 为计算图注入值

~~~python
a = tf.placeholder(tf.float32)
b = tf.placeholder(tf.float32)
c = tf.add(a,b)
with tf.Session() as sess:
    result = sess.run(c,feed_dict={a:1,b:2})
    print(result)
~~~



### Fetch

* 使用fetch获取计算结果
  * fetch可以是一个张量或者是一个list

~~~python
tf.Session().run(fetches,feed_dict=None)
~~~



### 综合小例子

~~~python
import TensorFlow as tf
x = tf.placeholder(tf.float32,shape=(1,2))
#变量初始化方式
w1 = tf.Variable(tf.random_normal([2,3],stddev=1,seed=1))
w2 = tf.Variable(tf.random_normal([3,1],stddev=1,seed=1))

a = tf.matmul(x,w1)
y = tf.matmul(a,w2)

with tf.Session() as sess:
    #变量运行前必须初始化
    init_op = sess.run(tf.global_variables_initializer())
    sess.run(init_op)
    print(sess.run(y,feed_dict{x:[[0.7,0.5]]}))
~~~



### TensorFlow中的核心API

* 基本运算
* 搭建网络
* 训练优化
* 数据相关



* 基本运算的一些函数

~~~python
#为张量增加维度
tf.expand_dims(Tensor,dim)
#返回张量的形状
tf.shape(Tensor)
#将张量沿着指定维度拼接
tf.concat(concat_dim,values,name="concat")
#沿着value的第一维进行随机重排列
tf.random_shuffle(value,seed=None,name=None)
#找到给定的张量，在其中指定轴axis上的最大值/最小值的位置
tf.argmax(input=tensor,dimention=axis)
tf.argmin(input=tenso,dimention=axis)
#判断两个张量是否每个元素都相等
tf.equal(x,y,name=None)
#将x的数据格式转化成dtype
tf.cast(x,dtype,name=None)
#矩阵乘法
tf.matmul()
#将张量按照新的shape重排列
tf.reshape(tensor,shape,name=None)
#去掉张量维度为一的坐标轴，以及去掉张量中唯一的维度
tf.squeeze()
~~~



#### TensorFlow中的数据操作

* TensorFlow采用TFRecord的格式统一存储数据
  * TFRecord将图像数据和标签一起放到二进制文件（protocol buffer），能更好的利用内存，实现快速的复制、移动、读取、存储
  * 数据读取：tf.train.string_input_producer
  * 数据解析：tf.TFRecordReader、tf.parse_single_example
  * 数据写入：tf.python_io.TFRecordWriter



* 数据写入相关API方法

~~~python
#创建对象
writer = tf.python_io.TFRecordWriter()
#exmaple里存具体的数据：图像的数据、标签、宽高等
example = tf.train.Example()
#将数据序列化写入TFRecord文件
write.write(example.SerializeToString())
write.close()
~~~



## TensorFlow数据读取机制

* 1个Epoch包含所有的训练样本包含n个batchsize
* 文件名队列实现对Epoch更好的管理
  * 假设A、B、C分别表达三个Epoch，并且都包含了所有的文件列表（所有训练样本），通过设置参数对文件列表进行shuffle，即A、B、C都包含的是打乱之后的文件列表，将A、B、C合并 [A,B,C] 最后得到文件名队列
  * 内存队列会从文件名队列中一次读取

![image-20210505151942484](C:\Users\liukun\AppData\Roaming\Typora\typora-user-images\image-20210505151942484.png)



### 数据读取相关的API方法

* 直接从文件中读取图片

* 从TF-Record中解析打包的图片数据

  * > 还可以实现文件名队列构造的方法：
    >
    > tf.train.string_input_producer、tf.train.slice_input_producer
    >
    > 实际获取数据要利用session.run()

  * tf.data库（动态图机制——可以去掉session.run()——所见即所得的方式获取数据 ）



