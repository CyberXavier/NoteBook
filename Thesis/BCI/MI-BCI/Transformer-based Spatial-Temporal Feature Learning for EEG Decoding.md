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
