---
title: NLP文本相似度计算及Python代码实现（余弦相似度和皮尔逊相似度）
date: 2018-11-09 11:20:33
tags:
    - 自然语言处理
---

# NLP文本相似度计算及Python代码实现

## 前言

之前一直在学习自然语言处理，项目的一个功能是计算文本相似度，很久之前就做好了，现在准备再系统的温习一遍。

## 方法

最近学习了两种计算文本相似度的方法，分别是**余弦相似度**和**皮尔逊相似度**。

### 余弦相似度(cosine similiarity)

来看看维基百科的定义：
>**余弦相似性**通过测量两个**向量**的夹角的余弦值来度量它们之间的相似性。0度角的余弦值是1，而其他任何角度的余弦值都不大于1；并且其最小值是-1。从而两个向量之间的角度的余弦值确定两个向量是否大致指向相同的方向。两个向量有相同的指向时，余弦相似度的值为1；两个向量夹角为90°时，余弦相似度的值为0；两个向量指向完全相反的方向时，余弦相似度的值为-1。这结果是与向量的长度无关的，仅仅与向量的指向方向相关。

我们可以通过夹角的大小，来判断向量的相似性。夹角越小，就代表越相似。

![](https://gitee.com/shuming9886/pic-go/raw/master/img/2020-10-24-nlp-01.png)

![](https://gitee.com/shuming9886/pic-go/raw/master/img/2020-10-24-nlp-02.png)

假定a向量是[x1,y1]，b向量是[x2,y2],那么可以将余弦定理改写成下面的形式：

![3](https://gitee.com/shuming9886/pic-go/raw/master/img/2020-10-24-nlp-03.png)



假定A和B是两个n维向量，A是[A1,A2,...,An]，B是[B1,B2,...,Bn]，则A与B的夹角θ的余弦等于：

![](https://gitee.com/shuming9886/pic-go/raw/master/img/2020-10-24-nlp-04.png)

参考资料：http://www.ruanyifeng.com/blog/2013/03/cosine_similarity.html 阮一峰


python3代码如下：

```python
    def cosine_similarity(vector1, vector2):
    dot_product = 0.0
    normA = 0.0
    normB = 0.0
    for a, b in zip(vector1, vector2):
        dot_product += a * b
        normA += a ** 2
        normB += b ** 2
    if normA == 0.0 or normB == 0.0:
        return 0
    else:
        return round(dot_product / ((normA**0.5)*(normB**0.5)) * 100, 2)
    #round() 方法返回浮点数x的四舍五入值
```

### 皮尔逊相似度(pearson)



在《集体智慧编程》中**K-Means**聚类算法中有运用。

![5](https://gitee.com/shuming9886/pic-go/raw/master/img/2020-10-24-nlp-05.gif)

参考资料：http://lobert.iteye.com/blog/2024999

python3代码如下：

```python
    def pearson(v1,v2):
    #简单求和
    sum1=sum(v1)
    sum2=sum(v2)

    #求平方和
    sum1Sq=sum([pow(v,2) for v in v1])
    sum2Sq=sum([pow(v,2) for v in v2])

    #求乘积之和
    pSum=sum([v1[i]*v2[i] for i in range(len(v1))])

    #计算r(Pearson score)
    num=pSum-(sum1*sum2/(len(v1)))
    den=sqrt((sum1Sq-pow(sum1,2)/len(v1))*(sum2Sq-pow(sum2,2)/len(v1)))

    if(den==0):
        return 0

    return 1.0-num/den
```

