# datamining_algorithms
用python3实现数据挖掘领域十大经典算法。十大经典算法如下：    
  
  ![image](http://s16.sinaimg.cn/middle/551d7bffg80cbb284ca7f&690)
           
>### <a href="#c4.5">1. C4.5</a>
>### <a href="#kmeans">2. K-Means</a>
>### <a href="#svm">3. SVM</a>
>### <a href="#apriori">4. Apriori</a>
>### <a href="#em">5. EM</a>
>### <a href="#pagerank">6. PageRank</a>
>### <a href="#adaboost">7. AdaBoost</a>
>### <a href="#knn">8. kNN</a>
>### <a href="#naïve bayes">9. Naïve Bayes</a>
>### <a href="#cart">10. CART</a>
>### <a href="#relation">相关术语</a>             
         

## <a name="kmeans">2. K-Means</a>
### 简介
又叫**K-均值算法**，是非监督学习中的聚类算法。  

### 基本思想 
在k-means算法中，用cluster来表示簇；且容易证明k-means算法收敛等同于所有质心不再发生变化。基本的k-means算法流程如下：

>选取k个初始质心（作为初始cluster，每个初始cluster只包含一个点）；  
>**repeat**：  
>    &nbsp;&nbsp;&nbsp;&nbsp;对每个样本点，计算得到距其最近的质心，将其类别标为该质心所对应的cluster；  
>    &nbsp;&nbsp;&nbsp;&nbsp;重新计算k个cluster对应的质心（质心是cluster中样本点的均值）；  
>**until** 质心不再发生变化

repeat的次数决定了算法的迭代次数。实际上，k-means的本质是最小化目标函数，目标函数为每个点到其簇质心的距离的平方和：
>![image](http://img.blog.csdn.net/20140419234515937)  

N是元素个数，x表示元素，c(j)表示第j簇的质心

### 算法复杂度  
时间复杂度是O(nkt) ,其中n代表元素个数，t代表算法迭代的次数，k代表簇的数目

### 优缺点  
#### 优点
1. 简单、快速；
2. 对大数据集有较高的效率并且是可伸缩性的；
3. 时间复杂度近于线性，适合挖掘大规模数据集。

#### 缺点
1. k-means是局部最优，因而对初始质心的选取敏感；
2. 选择能达到目标函数最优的k值是非常困难的。

## <a name="knn">8. kNN</a>
### 简介  
又叫**K-邻近算法**，是监督学习中的一种分类算法。目的是根据已知类别的样本点集求出待分类的数据点类别。

### 基本思想 
kNN的思想很简单：在训练集中选取离输入的数据点最近的k个邻居，根据这个k个邻居中出现次数最多的类别（最大表决规则），作为该数据点的类别。kNN算法中，所选择的邻居都是已经正确分类的对象。
>e.g：下图中，绿色圆要被决定赋予哪个类，是红色三角形还是蓝色四方形？如果k=3，由于红色三角形所占比例为2/3，绿色圆将被赋予红色三角形那个类，如果k=5，由于蓝色四方形比例为3/5，因此绿色圆被赋予蓝色四方形类。  
&nbsp;&nbsp;&nbsp;&nbsp;![image](https://gss2.bdstatic.com/-fo3dSag_xI4khGkpoWK1HF6hhy/baike/w%3D268/sign=fc3731ea0ad162d985ee651a29dfa950/bf096b63f6246b60f20ccd5aebf81a4c510fa29a.jpg)  

### 算法复杂度  
kNN是一种lazy-learning算法，分类器不需要使用训练集进行训练，因此训练时间复杂度为0；kNN分类的计算复杂度和训练集中的文档数目成正比，也就是说，如果训练集中文档总数为n，那么kNN的分类时间复杂度为O(n)；因此，最终的时间复杂度是O(n)。

### 优缺点  
#### 优点
1. 理论成熟，思想简单，既可以用来做分类也可以用来做<a href="#regression">回归</a> ；
2. 适合对稀有事件进行分类（例如：客户流失预测）；
3. 特别适合于多分类问题(multi-modal,对象具有多个类别标签，例如：根据基因特征来判断其功能分类)， kNN比SVM的表现要好。

#### 缺点
1. 当样本不平衡时，如一个类的样本容量很大，而其他类样本容量很小时，有可能导致当输入一个新样本时，该样本的K个邻居中大容量类的样本占多数；
2. 计算量较大，因为对每一个待分类的文本都要计算它到全体已知样本的距离，才能求得它的K个最近邻点；
3. 可理解性差，无法给出像决策树那样的规则。

## <a name="naïve bayes">9. Naïve Bayes</a>
### 简介  
又叫**朴素贝叶斯算法**，**朴素：特征条件独立；贝叶斯：基于贝叶斯定理。**属于监督学习的生成模型，实现简单，没有迭代，并有坚实的数学理论（即贝叶斯定理）作为支撑。在大量样本下会有较好的表现，不适用于输入向量的特征条件有关联的场景。

### 基本思想 
#### (1)病人分类的例子
某个医院早上收了六个门诊病人，如下表：
>症状　　职业　　　疾病
打喷嚏　护士　　　感冒 
打喷嚏　农夫　　　过敏 
头痛　　建筑工人　脑震荡 
头痛　　建筑工人　感冒 
打喷嚏　教师　　　感冒 
头痛　　教师　　　脑震荡

现在又来了第七个病人，是一个打喷嚏的建筑工人。请问他患上感冒的概率有多大？	
根据**贝叶斯定理**：
　	**`P(A|B) = P(B|A) P(A) / P(B)`**
可得
>P(感冒|打喷嚏x建筑工人) 
= P(打喷嚏x建筑工人|感冒) x P(感冒) / P(打喷嚏x建筑工人)

假定"打喷嚏"和"建筑工人"这两个特征是独立的，因此，上面的等式就变成了
>P(感冒|打喷嚏x建筑工人) 
= P(打喷嚏|感冒) x P(建筑工人|感冒) x P(感冒) / P(打喷嚏) x P(建筑工人)

这是可以计算的。
>P(感冒|打喷嚏x建筑工人) 
= 0.66 x 0.33 x 0.5 / 0.5 x 0.33 
= 0.66

因此，这个打喷嚏的建筑工人，有66%的概率是得了感冒。同理，可以计算这个病人患上过敏或脑震荡的概率。比较这几个概率，就可以知道他最可能得什么病。
                                     
这就是贝叶斯分类器的基本方法：**在统计资料的基础上，依据某些特征，计算各个类别的概率，从而实现分类。**
#### (2)朴素贝叶斯分类器的公式
假设某个体有n项特征（Feature），分别为F1、F2、...、Fn。现有m个类别（Category），分别为C1、C2、...、Cm。贝叶斯分类器就是计算出概率最大的那个分类，也就是求下面这个算式的最大值：
　**`P(C|F1F2...Fn) = P(F1F2...Fn|C)P(C) / P(F1F2...Fn)`**
由于 P(F1F2...Fn) 对于所有的类别都是相同的，可以省略，问题就变成了求
　**`P(F1F2...Fn|C)P(C)`**
的最大值。
朴素贝叶斯分类器则是更进一步，假设所有特征都彼此独立，因此
　**`P(F1F2...Fn|C)P(C) = P(F1|C)P(F2|C) ... P(Fn|C)P(C)`**
上式等号右边的每一项，都可以从统计资料中得到，**8由此就可以计算出每个类别对应的概率，从而找出最大概率的那个类。**
虽然”所有特征彼此独立"这个假设，在现实中不太可能成立，但是它可以大大简化计算，而且有研究表明对分类结果的准确性影响不大。

参见[朴素贝叶斯分类器-阮一峰的网络日志](http://www.ruanyifeng.com/blog/2013/12/naive_bayes_classifier.html)

### 实际应用场景  
- 文本分类
- 病人分类
- 拼写检查

## <a name="relation">相关术语</a>  
### 监督学习 （supervised learning）
>(wipipedia)是一个机器学习中的方法，可以由训练资料中学到或建立一个模式（函数 / learning model），并依此模式推测新的实例。训练资料是由输入物件（通常是向量）和预期输出所组成。函数的输出可以是一个连续的值（称为回归分析），或是预测一个分类标签（称作分类）。 
                      
### 非监督学习（unsupervised learning）  
>(wipipedia)是一种机器学习的方式，并不需要人力来输入标签。它是监督式学习和强化学习等策略之外的一种选择。在监督式学习中，典型的任务是分类和回归分析，且需要使用到人工预先准备好的范例(base)。
               
### 聚类与分类的区别  
简单说就是分类分为有监督——半监督——无监督，对应标签为有——部分有——无，无监督就是聚类，只给数据不给标签，现实中用的最多的是半监督分类（一般用分类、半监督分类、聚类来替代有监督分类、半监督分类、无监督分类）。具体参见[知乎——聚类与分类有什么区别？徐凯的回答](https://www.zhihu.com/question/42044303/answer/107836313)
        
### <a name="regression">回归</a>
>通过找出一个样本的k个最近邻居，将这些邻居的属性的平均值赋给该样本，就可以得到该样本的属性。更有用的方法是将不同距离的邻居对该样本产生的影响给予不同的权值(weight)，如权值与距离成反比。

### 分类器(Classifier)
分类的概念是在已有数据的基础上学会一个分类函数或构造出一个分类模型（即我们通常所说的分类器）。总之，分类器是数据挖掘中对样本进行分类的方法的统称。
#### 实际应用中如何选择分类器？
**没有最好的分类器，只有最合适的分类器。**只有多实践才能灵活处理实际生活中面临的分类问题。
#### 如何评价分类器的质量？
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;首先定义，**分类器的正确率**指分类器正确分类的项目占所有被分类项目的比率。
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;通常使用**回归测试**来评估分类器的准确率，最简单的方法是用构造完成的分类器对训练数据进行分类，然后根据结果给出正确率评估。但这不是一个好方法，因为使用训练数据作为检测数据有可能因为过分拟合而导致结果过于乐观，所以一种更好的方法是**在构造初期将训练数据一分为二，用一部分构造分类器，然后用另一部分检测分类器的准确率**。
