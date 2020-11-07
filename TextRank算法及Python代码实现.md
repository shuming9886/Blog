---
title: TextRank算法及Python代码实现
date: 2019-03-04 09:57:43
tags:
mathjax: true
	- 自然语言处理
---

# TextRank算法及Python代码实现

## TextRank算法是什么？

文本自动摘要分为两种方法，一种是抽取式，另一种是生成式。其中TextRank方法就是抽取式方法，即从原文抽取重要的句子来生成摘要。可以从下文的论文链接进一步了解该论文的研究目的。

[论文TextRank: Bringing Order into Texts](<https://www.aclweb.org/anthology/W04-3252>)

## 算法详解

TextRank的打分思想是从PageRank的迭代思想衍生过来的。首先我们可以构建一个有向有权图**G=（V，E）**，其种**V**是点的集合，**E**是边的集合，**w<sub>ji</sub>**是图中任意两点**V<sub>i</sub>**,**V<sub>j</sub>**之间边的权重，即句子**V<sub>i</sub>**,**V<sub>j</sub>**之间的相似度。**In(V<sub>i</sub>)**为指向该节点的节点集合，**Out(V<sub>j</sub>)**为节点**V<sub>j</sub>**指向的节点集合。节点*V<sub>i</sub>*的评分计算公式如下：
$$
WS(V_i)=(1-d)+d*\sum_{V_j\in{In(V_i)}}{\frac{w_{ji}}{\sum_{V_k\in{Out(V_j)}}{w_{jk}}}WS(V_j)}
$$
![](https://gitee.com/shuming9886/pic-go/raw/master/img/2020-10-24-latex.svg)

等式左边表示一个句子的权重，右侧的求和表示每个相邻句子对本句子的贡献度。一般认为全部句子都是相邻的。

**d**是阻尼系数，表示从图中某一点指向其他任意点的概率。阻尼系数过大会使需要迭代次数骤增且算法的排序不稳定。一般取0.85。

句子相似度计算我使用的是余弦相似度（Coine）。

[Python3代码](<https://github.com/shuming9886/textrank_for_patent>)

