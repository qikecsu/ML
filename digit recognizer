#encoding:utf-8
'''
Created on Juan 16, 2016
kNN: k Nearest Neighbors
'''
from numpy import *
import operator
from os import listdir
import csv

def classify0(inX, dataSet, labels, k): #kNN分类器
    dataSetSize = dataSet.shape[0]     #获得dataSet的行数
    diffMat = tile(inX, (dataSetSize,1)) - dataSet      #tile(A,(n,m))扩展数组A，得到的为一个n行，m列的数组
    sqDiffMat = diffMat**2         #对每一个元素（坐标值之差）求平方
    sqDistances = sqDiffMat.sum(axis=1)  #axis=0为普通相加，axis=1为每一行的元素进行相加
    distances = sqDistances**0.5   #求平方根得到欧式距离
    sortedDistIndicies = distances.argsort()     #对距离进行排序，返回的是同类型的按从小到大的元素索引值
    classCount={}          
    for i in range(k):
        voteIlabel = labels[sortedDistIndicies[i]]    #将前k个种类提取出来 
        classCount[voteIlabel] = classCount.get(voteIlabel,0) + 1  #计算每个种类的个数
    sortedClassCount = sorted(classCount.iteritems(), key=operator.itemgetter(1), reverse=True) #排序逆序
    return sortedClassCount[0][0]

def handwritingTest():
	f=open('train.csv','rb')
	reader=csv.reader(f)
	train_labels=[]
	train_vector=zeros((42000,784))
	i=0
	for line in reader:
		if(line[0]=='label'):
			continue
		else:
			num=line[0]
			train_labels.append(int(num))
			j=0
			while(j<784):
				train_vector[i,j]=int(line[j+1])
				j=j+1
			i=i+1
	f.close()
	ft=open('test.csv','rb')
	readert=csv.reader(ft)
	test_vector=zeros((1,784))
	fw=file("results.txt","w")
	result=0
	for li in readert:
		if(li[0]=='pixel0'):
			continue
		else:
			j=0
			while(j<784):
				h=int(li[j])
				test_vector[0,j]=h
				j=j+1
			result=classify0(test_vector,train_vector,train_labels,3)
			print result
			print >>fw,result 
	ft.close()
	print '算法已经执行完毕！'		
	

