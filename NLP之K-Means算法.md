---
title: NLP之K-Means聚类算法
date: 2018-11-09 11:28:47
tags:
    - 自然语言处理
---

# K-Means聚类算法

首先谈谈**聚类(Clustering)**和**分类(Classification)**的区别。在机器学习中，分类就是按照某种标准给对象贴标签，再根据标签来区分归类。而聚类是将本身没有类别的样本聚集成不同的组，这样的一组数据对象的集合叫做**簇**，并且对每一个这样的簇进行描述的过程。它的目的是使得属于同一个簇的样本之间应该彼此相似，而不同簇的样本应该足够不相似。

参考资料：**《集体智慧编程》**

**K-均值聚类(K-Means Clustering)**算法不同于**分级聚类**，因为我们会预先告诉算法希望生成的聚类数量，然后算法会根据数据的结构状况来确定聚类的大小。K-均值聚类算法首先会随机确定**k**个中心位置(位于空间中代表聚类中心的点)，然后将各个数据项分配给最临近的中心点。待分配完成后，聚类中心就会移到分配给该聚类的所有节点的平均位置处，然后整个分配过程重新开始。这一过程会一直重复下去，直到分配过程不再产生变化为止。

Python3代码：
```python
	import random
	
	def kcluster(rows,distance=pearson,k=5): 
		#计算每一个单词使用次数的最大值和最小值 
		ranges=[(min([row[i] for row in rows]),max(row[i] for row in rows)) for i in range(len(rows[0]))] 
		#随机创建k个中心点 
		clusters=[[random.random()*(ranges[i][1]-ranges[i][0])+ranges[i][0] for i in range(len(rows[0]))] for j in range(k)] 
		
		lastmatches=None 
		for t in range(100): 
			print("Iteration %d" %t) 
			#存储与中心点最近的实例点的下标 
			bestmatches=[[] for i in range(k)] 
			for j in range(len(rows)): 
				row=rows[j] 
				bestmatch=0 
				for i in range(k): 
					d=distance(clusters[i],row) 
					if(d<distance(clusters[bestmatch],row)): 
						bestmatch=i 
				bestmatches[bestmatch].append(j) 
			if(bestmatches==lastmatches): 
				break 
			lastmatches=bestmatches 
			for i in range(k): 
				avgs=[0.0]*len(rows[0]) 
				if(len(bestmatches[i])>0): 
					for rowid in bestmatches[i]: 
					#先求和 
					for m in range(len(rows[rowid])): 
						avgs[m]+=rows[rowid][m] 
					#再除以实例点的个数 
					for j in range(len(avgs)): 
						avgs[i]/=len(bestmatches[i]) 
					clusters[i]=avgs 
		return bestmatches
```

在调用这个函数时，可以自由设定想要聚类的数量。上述的k=5可以自由设定。

函数参数列表中的*distance=pearson*为计算距离的函数。[皮尔逊算法(Pearson)]([https://shuming9886.github.io/2018/11/09/NLP%E6%96%87%E6%9C%AC%E7%9B%B8%E4%BC%BC%E5%BA%A6%E8%AE%A1%E7%AE%97/](https://shuming9886.github.io/2018/11/09/NLP文本相似度计算/))在之前的博客中可以找到。上述代码在每个变量的值域范围内随机构造了一组聚类。当每次迭代进行的时候，算法会将每一行数据分配给它的所有项的平均位置。当分配情况与前一次结果相同时，迭代过程就结束了，同时算法会返回k组序列，其中每个序列代表一个聚类。

由于函数选用随机的中心点作为开始，所以返回结果的顺序几乎总是不同的。根据中心点初始位置的不同，最终聚类中包含的内容也可能会有所不同。

我把K-Means算法运用在将一堆微博聚类，分成5大类微博，每一类的微博指向特定的事件。