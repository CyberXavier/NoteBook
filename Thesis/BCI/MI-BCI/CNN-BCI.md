# CNN-BCI



## 目录

* [互信息特征选择](# 互信息)
* [Parzen Window](# Parzen Window)
* [希尔伯特变换](# 希尔伯特变换)
* [scipy butter](# scipy butter)
* [end](# end)



## 知识扩充

1.Channel-wise Conv 

出自论文: ChannelNets: Compact and Efficient Convolutional Neural Networks via Channel-Wise Convolutions论文地址:https://arxiv.org/abs/1809.01330
论文代码:https://github.com/HongyangGao/ChannelNets

2.交叉熵验证（Cross Validation Values）

3.十倍交叉验证(ten-fold cross validation)

4.感受野

5.drop out层

6.批标准化



# 互信息

## 一、算法思想

### 1、[特征选择](https://so.csdn.net/so/search?q=特征选择&spm=1001.2101.3001.7020)

特征选择是去除**无关紧要**或**庸余**的特征，仍然还保留其他**原始特征**，从而获得**特征子集**，从而以最小的性能损失更好地描述给出的问题。

特征选择方法可以分为三个系列：过滤式选择、包裹式选择和[嵌入式](https://so.csdn.net/so/search?q=嵌入式&spm=1001.2101.3001.7020)选择的方法 。

本文介绍的互信息（mutual information）即为过滤式的特征选择算法。

关于过滤式的特征算法系列，可参考我的其他文章。
[特征选择之卡方检验](https://blog.csdn.net/qq_39923466/article/details/105520015)
[特征选择之Fisher Score](https://blog.csdn.net/qq_39923466/article/details/105539153)

### 2、互信息

#### 互信息介绍

定义：**两个随机变量的互信息（mutual information）是变量间相互依赖性的量度。**

如何理解相互依赖性的量度？

**互信息度量两个随机变量共享的信息——知道随机变量X,对随机变量Y的不确定性减少的程度（或者知道随机变量Y，对随机变量X的不确定性减少的程度），用 I(X;Y)表示。**

还是很抽象？举个例子吧。

**随机变量X表示一个均衡的六面骰子投掷出的点数，Y表示X的奇偶性。这里我们设X是偶数时，Y=0；X是奇数时，Y=1。**

**如果我们知道X，如X=1，则可以判断Y=1。(失去Y=0这一信息的可能性，Y的不确定性信息减少了)**

**同样的，如果我们知道Y=0,则可以判断X=2或4或6。（失去X=1或3或5这一信息的可能性，X的不确定性信息减少了）**

因此，我们说随机变量X和Y之间存在互信息。

ok，这里我们还需要理解什么叫做**随机变量的不确定性**。
因此，我们需要引入**熵**的概念。

熵的概念起源于物理学，用于度量一个热力学系统的无序程度。在信息论中，**熵是对不确定性的测量**，用*H*表示。对于随机变量X:
[![qjSUwd.png](https://s1.ax1x.com/2022/04/06/qjSUwd.png)](https://imgtu.com/i/qjSUwd)

我们可以通过下面这张互信息的韦恩图来形象的理解互信息和熵的关系与区别：
![互信息的韦恩图](https://img-blog.csdnimg.cn/20200414230329244.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM5OTIzNDY2,size_16,color_FFFFFF,t_70#pic_center)
关于这张图的理解：
![互信息韦恩图的理解](https://img-blog.csdnimg.cn/20200414230551490.PNG#pic_center)
可参考这个视频↓
[参考视频](https://www.bilibili.com/video/BV194411X7Jg?from=search&seid=12612297557725952605)

[![qHAjII.png](https://s1.ax1x.com/2022/04/03/qHAjII.png)](https://imgtu.com/i/qHAjII)

#### 特征选择中的互信息

由上文所述， 特征选择是去除**无关紧要**或**庸余**的特征，仍然还保留其他**原始特征**，从而获得**特征子集**，从而以最小的性能损失更好地描述给出的问题。

[![qHAG28.png](https://s1.ax1x.com/2022/04/03/qHAG28.png)](https://imgtu.com/i/qHAG28)

## 二、代码实现

### 1、python调用sklearn包

python里面的sklearn包里面有metrics.mutual_info_score（）函数。

它的参数为两个列表sample,label。由上文互信息的对称性可知，sample与label是对称的，可互换。且这个函数的log以自然底数e为底。

```python
from sklearn import metrics
label=[0,0,1]
sample=[1,1,0]
print(metrics.mutual_info_score(label,sample))
1234
```

输出为互信息的值：`0.6365141682948129`

### 2、自己实现的代码

话不多说，上代码。

```python
# 针对标签样本都是二值(0和1)的互信息,label和sample是对称的
#eg:label=[0,1,0]   sample=[1,0,1]
#return 0.6365141682948128
import numpy as np
import math
def binary_mutula_information(label, sample):
    # 用字典来计数
    d = dict()
    # 统计其中00,01,10,11各自的个数
    binary_mi_score = 0.0
    label = np.asarray(label)
    sample = np.asarray(sample)
    if label.size != sample.size:
        print('error！input array length is not equal.')
        exit()

    # np.sum(label)/label.size表示1在label中的概率,
    # 前者就是0在label中的概率
    # 这里需要用总的数目减去1的数目再除以总的数目，提高精度
    x = [(label.size - np.sum(label)) / label.size, np.sum(label) / label.size]

    y = [(sample.size - np.sum(sample)) / sample.size, np.sum(sample) / sample.size]

    for i in range(label.size):
        if (label[i], sample[i]) in d:
            d[label[i], sample[i]] += 1
        else:
            d[label[i], sample[i]] = 1

    # 遍历字典，得到各自的px,py,pxy，并求和
    for key in d.keys():
        px = x[key[0]]
        py = y[key[1]]
        pxy = d[key] / label.size
        binary_mi_score = binary_mi_score + pxy * math.log(pxy / (px * py))

    return binary_mi_score
label=[0,0,1]
sample=[1,1,0]
print(binary_mutula_information(label,sample))
1234567891011121314151617181920212223242526272829303132333435363738394041
```

输出互信息值：`0.6365141682948129`

以上代码只是简单的实现了当特征值和标签值为二值0和1的情况，因此输入的参数的值请读者注意。

其实值的大小并不重要，只要能区分是不同的值就行。其实对于sklearn包里面的metrics.mutual_info_score（）函数来说，

```python
label=[0,0,1]
sample=[1,1,0]
12
```

与

```python
label=[666,666,999]
sample=[999,999,666]
12
```

执行

```python
metrics.mutual_info_score(label,sample)
1
```

得到的答案是一样的，读者可自行验证。

后续我会再更新出一般的对于n个值都适用的互信息python实现。

链接：[(8条消息) 特征选择之互信息（mutual information）算法思想及其python代码实现_亨少德小迷弟的博客-CSDN博客_互信息代码](https://blog.csdn.net/qq_39923466/article/details/118809611)



# Parzen Window

[Parzen Window详解](https://blog.csdn.net/Nianzu_Ethan_Zheng/article/details/79211861)



# 希尔伯特变换

[希尔伯特变换](# [希尔伯特变换学习笔记 - 哔哩哔哩 (bilibili.com)](https://www.bilibili.com/read/cv2793412/))



# scipy butter

[滤波](# https://blog.csdn.net/weixin_41521681/article/details/108262389)



# end

[目录](# 目录)
