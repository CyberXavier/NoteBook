
###  1.Logistic Regression

* 逻辑回归也叫做对数几率回归（见西瓜书讲解）

### 2.Logistic Regression lost function(逻辑回归损失函数)

如图1-1：

![损失函数](https://github.com/CyberXavier/NoteBook/blob/main/%E6%AF%95%E4%B8%9A%E8%AE%BE%E8%AE%A1/DeepLearning/image/lostfunction.PNG)

【解析】：损失函数误差平方法：L(pre_y , rel_y) = 1/2(pre_y^2 - rel_y^2)^2	{梯度下降法不太好用所以再逻辑回归中用一个不同的损失函数，它看起来与误差平方相似的作用（见图1-1）并且损失函数只适用于单个训练样本}

---

### 3.Logistic Regression cost function

图1-2：

<img src="E:\MySoftware\LearningRelated\Markdown\TheDocument\MyNotes\毕业设计\DeepLearning\image\成本函数.png" alt="成本函数" style="zoom: 25%;" />

【解析】：成本函数基于参数的总成本。

#### 3-1.损失函数由来

图1-2.1：

![1-2.1损失函数由来](E:\MySoftware\LearningRelated\Markdown\TheDocument\MyNotes\毕业设计\DeepLearning\image\1-2.1损失函数由来.PNG)

【解析】：单个训练样本的损失函数

* 绿色箭头通过等效替换得到“P(y|x)”函数
* 目标：训练模型求解“P(y|x)”函数的最大值
* 由于log函数单调增因此求解P(y|x)函数的最大值等价于log(P(y|x))函数的最大值
* 虽然在我们学习训练模型时希望得到概率最大的值，但是我们的损失函数的值肯定是越小越好因此我们可以通过添加一个负号来完成损失函数的建立"-L(pre_y,y)"。

#### 3-2成本函数的由来

图1-2.2：

![1-2.2成本函数由来](E:\MySoftware\LearningRelated\Markdown\TheDocument\MyNotes\毕业设计\DeepLearning\image\1-2.2成本函数由来.PNG)

【解析】：m个训练样本的总体成本函数

* 第一点：log函数中连续相乘等于log函数相加
* 第二点：最大似然估计：求出一组参数使这个式子取最大值（也就是第二点所指的函数）
* 第三点：通过前里面两点就可以推导出图1-2.1给出的logistic回归的成本函数“J(w,b)”。由于训练模型时目标是让成本函数最小化，所以我们不是直接用最大似然概率因此我们去掉了负号。最后为了方便可以对成本函数进行适当缩放于是就在前面加了一个额外的常数因子（1/m）
* 总结：我们从logistic回归模型的最大似然估计角度出发，假设训练集中的样本都是独立同分布的条件下。

---

### 4.Gradient Descent

图1-3

![逻辑回归梯度下降](E:\MySoftware\LearningRelated\Markdown\TheDocument\MyNotes\毕业设计\DeepLearning\image\逻辑回归梯度下降.PNG)

【解析】：使用梯度下降找到使得代价最小的w、b的值。（因为我们要找到全局最优的解所以我们没有选择平方误差法因为这种方法会产生许多局部最优解。它不是一个凹函数）

---

### 5.Logistic regression derivatives

如下图1-4：

![链式求导法](E:\MySoftware\LearningRelated\Markdown\TheDocument\MyNotes\毕业设计\DeepLearning\image\逻辑回归梯度下降链式求导法.PNG)

【解析】：这就是单个样本一次使用链式求导法则梯度下降的过程。[其中a代表pre_y；a=pre_y=德尔塔(z)=1/(1+e^-z)；L(a,y)=-(yloga+(1-y)log(1-a))]

---

### 6.SIMD

* juputer notebook 是使用的cpu而不是用gpu。

* > * CPU和GPU都有并行化指令有时会叫作SIMD（a single instruction multiple data）。
  >
  > * 【SIMD】：一条指令多个数据。
  >
  > > * SIMD：如果你使用了这样的内置函数np.function或者其他能让你去掉显示for loop的函数。
  > >
  > > * 这样python的numpy能够充分利用 并行化去更快计算。这一点对GPU和CPU上面计算都是成立的。只是GPU更加擅长SIMD计算但是CPU也不差。
  > > * 向量化能够加速你的代码。
  > > * 经验法则：只要有其他可能就不要使用显示for循环。

---

### 7.Vectorizing Logistic Regression（向量化逻辑回归）

如下图1-5：

![向量化](E:\MySoftware\LearningRelated\Markdown\TheDocument\MyNotes\毕业设计\DeepLearning\image\向量化逻辑回归week2.PNG)

【解析】：通过python的np.dot方法实现向量化去代替for loop。在求Z的式子中最后一项”+b“，在python中会自动转化成1×m的矩阵（通过python的广播（Broadcasting））。

---

### 8.向量化logistic回归的梯度输出

如下图1-6：

![](E:\MySoftware\LearningRelated\Markdown\TheDocument\MyNotes\毕业设计\DeepLearning\image\向量化logistic归回梯度输出.PNG)

【解析】：同时计算m个训练数据的梯度，得到一个高效率的逻辑回归的实现（如下图1-7右边部分消除了for loop）。

图1-7：

![逻辑回归实现](E:\MySoftware\LearningRelated\Markdown\TheDocument\MyNotes\毕业设计\DeepLearning\image\高效logistic回归实现.PNG)

【解析】：如果你需要很多次梯度下降可能还需要在右边部分加上一个for loop。

---

