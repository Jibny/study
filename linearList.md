---
title: 数据结构(一)线性表
date: 2019-09-08 22:14:02
categories: 
    Data-Structure
tags:
    数据结构线性表
cover: http://r.photo.store.qq.com/psb?/V13Zm3q236IRIM/unStEpIFd.yg2bTiK8CigXUVkTvg1XZRBS.JbSzbyIc!/r/dDABAAAAAAAA
mp3: https://api.uomg.com/api/rand.music
---

线性表

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/wBQA49aBxuo9SOC5hnS38zZovp5ZvBYi77t744hKj4k!/r/dE0BAAAAAAAA)

# 1 顺序表

## 1.1 连续存储空间顺序存放

## 1.2 定义

线性表的顺序存储是指用一组地址连续的存储单元依次存储线性表中的各个元素、使得线性表中在逻辑结构上相邻的数据元素存储在相邻的物理存储单元中

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/y0Ym5n*TuC2WsiGoGa6VMnJYWYBmA037orWKoVXaS*s!/r/dDYBAAAAAAAA)

### 1.2.2 初始化



![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/7F7CMrVHTtMeu6dRGvVPEzABoOz4U8Zi3e6R8ckz5gc!/r/dDUBAAAAAAAA)

### 1.2.3 查找



![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/*iNYq40IK*w5E27jN5WsvSDw.27Km4f3NtrAEVNFd*0!/r/dFQBAAAAAAAA)

### 1.2.4 插入



![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/seXsFQCiJ9RHTVQXyJPPfe26AWoqTDJ*PdJgljxFxH0!/r/dL8AAAAAAAAA)

### 1.2.5 删除



![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/mfjNZYRt3aR4heDr0n9Ab65.EGjTQn77Rt7a24vz5HE!/r/dMUAAAAAAAAA)

插入后移，删除前移([*插入*](#_1_2_4___), [*删除*](#_1_2_5___))

# 2 链式表

## 2.1 随机分配空间随机存放

## 2.2 定义

非顺序的存储结构，数据元素的逻辑顺序是通过链表中的指针链接次序实现的



![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/Kr2IGpEz0C*cV7dLfvtXHNSDXeqdhRwkWwyGC5CpAXA!/r/dFMBAAAAAAAA)

### 2.2.2 求表长

####  

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/ZeyF7EPh6ObP759VPQJ56sJeyuNyRDl1ebEsVi1gtm0!/r/dL8AAAAAAAAA)

### 2.2.3 序号，按值查找

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/33WbCkQwn1rwfr2W5suhDo62pKE56rJpRZAg4eMjj5k!/r/dFIBAAAAAAAA)

### 2.2.4 插入

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/zStrYCW3mVF5StOJ.fpdGhMql0XlMAdUeAQRqAoPnqc!/r/dEABAAAAAAAA)

### 2.2.5 删除

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/TRtmYZEeq9tK8A*NhUpKK.mB4BjOEg7dWammzjDSNzU!/r/dLYAAAAAAAAA)

# 3 线性表定义

## 3.1 可以由多种同类型的数据元素构成有序序列

## 3.2 表中同类数据元素个数-长度

## 3.3 表中没有元素-空表

## 3.4 表起始位置表头，结束位置表末尾



# 4 广义表

## 4.1 线性表的推广，表中元素可以是另一个表

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/57tUkGnhHUFpGUQ2kL1PTUOgnqBvRTgijpO6E1nMnSA!/r/dIMAAAAAAAAA)

# 5 多重链表

## 5.1 含有多个指针域（双向链表不是多重链表），可以实现树，图等复杂数据存储结构

## 5.2 十字链表稀疏矩阵

### 5.2.1  行列指针，行列头结点，Term入口4行5列7个非零项

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/kD*xcnzgMhGorw7daPDKsz5wW9R7ylP4nAaNdkALvXM!/r/dLgAAAAAAAAA)

该十字链表表示的矩阵为

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/1NQVvlu9VHu8*Uhl2.ARn.jbzpyJPw4qgv1Xm1x9I0M!/r/dIQAAAAAAAAA)

节点结构

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/TS4gw4**2S6lLzGPdbNBqpmcKofZJoULKcwZTEFMM6k!/r/dFQBAAAAAAAA)