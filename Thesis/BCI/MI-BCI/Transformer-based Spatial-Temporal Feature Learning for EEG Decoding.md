

# Transformer-based Spatial-Temporal Feature Learning for EEG Decoding



## Transformer 框架

编码与解码

> 编码：例如 Z（z1...zn） 其中zt表示的就是第t个词的一个向量表示，这就是编码器的输出（将原始的数据编码成机器学习可以理解的向量）
>
> 解码：得到 Z 以后，输出一个序列 Y（y1...ym）其中n和m可能不一样。解码的时候只能一个词一个词的生成。被称为自回归（你的输入也是你的输出）



layerNorm 和 batchNorm

> 两者通过将batch进行不同方向的切割，来计算每个切片的均值和方差，使得每个切片均值变成0，方差变成1。在预测时还得记录全局的样本均值和方差（图中蓝色表示batchNorm，黄色表示layerNorm）在二维和三维情况下
>
> * batchNorm如果每个样本长度变化过大，每次做mini-batch算出来的均值和方差抖动较大
> * layerNorm是每个样本自己算均值和方差，是对每个样本来做的，所以比较稳定
> * feat×batch×seq ：512个特征、样本数、每个样本的序列
>
> [![LIqjcd.png](https://s1.ax1x.com/2022/04/25/LIqjcd.png)](https://imgtu.com/i/LIqjcd)



> [![LopX36.png](https://s1.ax1x.com/2022/04/25/LopX36.png)](https://imgtu.com/i/LopX36)
>
> * 使用Q、K、V矩阵进行点乘运算，实现并行
> * 除以根号dk是为了避免两极分化，当算出来的数据比较大进入softmax层之后就会更加接近1，而且它的则会更加接近0。这种时候一般是训练快收敛了，梯度比较小，所以跑的比较慢。



## 训练loss变化表示的含义

* 1 train loss 不断下降,test loss 不断下降,说明网络正在学习 
* 2 train loss 不断下降,test loss 趋于不变,说明网络过拟合 
* 3 train loss 趋于不变,test loss 趋于不变,说明学习遇到瓶颈,需要减小学习率或者批处理大小 
* 4 train loss 趋于不变,test loss 不断下降,说明数据集100%有问题 
* 5 train loss 不断上升,test loss 不断上升(最终变为NaN),可能是网络结构设计不当,训练超参数设置不当,程序bug等某个问题引起



## 一些调参策略

* L2-正则化防止过拟合

> ​       weight decay（权值衰减），其最终目的是防止过拟合。在机器学习或者模式识别中，会出现overfitting，而当网络逐渐overfitting时网络权值逐渐变大，因此，为了避免出现overfitting,会给误差函数添加一个惩罚项，常用的惩罚项是所有权重的平方乘以一个衰减常量之和。其用来惩罚大的权值。在损失函数中，weight decay是放在正则项（regularization）前面的一个系数，正则项一般指示模型的复杂度，所以weight decay的作用是调节模型复杂度对损失函数的影响，若weight decay很大，则复杂的模型损失函数的值也就大。
>
> 这个在定义优化器的时候可以通过参数 【weight_decay，一般建议0.0005】来设置：
>
> ~~~python
> opt_Adam = torch.optim.Adam(net_Adam.parameters(), lr=LR, betas=(0.9, 0.99), eps=1e-06, weight_decay=0.0005)
> ~~~



* batch normalization。batch normalization的是指在神经网络中激活函数的前面，将按照特征进行normalization，这样做的好处有三点：

> 1. 提高梯度在网络中的流动。Normalization能够使特征全部缩放到[0,1]，这样在反向传播时候的梯度都是  在1左右，避免了梯度消失现象。
> 2. 提升学习速率。归一化后的数据能够快速的达到收敛。
> 3. 减少模型训练对初始化的依赖。
> 4. 减少参数选择的依赖
> 5. 一些通常的解释：https://blog.csdn.net/hjimce/article/details/50866313



* 加入dropout层：dropout一般设置为0.5
* 集成方法



## 代码

### 多头注意力机制[代码链接](# [multihead-attention slides (d2l.ai)](https://c.d2l.ai/zh-v2/assets/notebooks/chapter_attention-mechanisms/multihead-attention.slides.html#/))

~~~python
import math
import torch
from torch import nn
from d2l import torch as d2l

~~~

选择缩放点积注意力作为每一个注意力头

~~~python
class MultiHeadAttention(nn.Module):
    def __init__(self, key_size, query_size, value_size, num_hiddens,
                 num_heads, dropout, bias=False, **kwargs):
        super(MultiHeadAttention, self).__init__(**kwargs)
        self.num_heads = num_heads
        self.attention = d2l.DotProductAttention(dropout)
        self.W_q = nn.Linear(query_size, num_hiddens, bias=bias)
        self.W_k = nn.Linear(key_size, num_hiddens, bias=bias)
        self.W_v = nn.Linear(value_size, num_hiddens, bias=bias)
        self.W_o = nn.Linear(num_hiddens, num_hiddens, bias=bias)

    def forward(self, queries, keys, values, valid_lens):
        queries = transpose_qkv(self.W_q(queries), self.num_heads)
        keys = transpose_qkv(self.W_k(keys), self.num_heads)
        values = transpose_qkv(self.W_v(values), self.num_heads)

        if valid_lens is not None:
            valid_lens = torch.repeat_interleave(valid_lens,
                                                 repeats=self.num_heads,
                                                 dim=0)

        output = self.attention(queries, keys, values, valid_lens)

        output_concat = transpose_output(output, self.num_heads)
        return self.W_o(output_concat)
~~~

使多个头并行计算

~~~python
def transpose_qkv(X, num_heads):
    X = X.reshape(X.shape[0], X.shape[1], num_heads, -1)

    X = X.permute(0, 2, 1, 3)

    return X.reshape(-1, X.shape[2], X.shape[3])

def transpose_output(X, num_heads):
    """逆转 `transpose_qkv` 函数的操作"""
    X = X.reshape(-1, num_heads, X.shape[1], X.shape[2])
    X = X.permute(0, 2, 1, 3)
    return X.reshape(X.shape[0], X.shape[1], -1)
~~~

测试

~~~python
num_hiddens, num_heads = 100, 5
attention = MultiHeadAttention(num_hiddens, num_hiddens, num_hiddens,
                               num_hiddens, num_heads, 0.5)
attention.eval()
~~~

输出

```python
MultiHeadAttention(
  (attention): DotProductAttention(
    (dropout): Dropout(p=0.5, inplace=False)
  )
  (W_q): Linear(in_features=100, out_features=100, bias=False)
  (W_k): Linear(in_features=100, out_features=100, bias=False)
  (W_v): Linear(in_features=100, out_features=100, bias=False)
  (W_o): Linear(in_features=100, out_features=100, bias=False)
)
```

测试2

~~~python
batch_size, num_queries, num_kvpairs, valid_lens = 2, 4, 6, torch.tensor([
    3, 2])
X = torch.ones((batch_size, num_queries, num_hiddens))
Y = torch.ones((batch_size, num_kvpairs, num_hiddens))
attention(X, Y, Y, valid_lens).shape
~~~

输出

```python
torch.Size([2, 4, 100])
```

