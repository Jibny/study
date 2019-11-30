---
title: 数据结构(二)(三)栈和队列
date: 2019-09-15 22:14:20
categories: 
    Data-Structure
tags:
    数据结构栈和队列
cover: http://r.photo.store.qq.com/psb?/V13Zm3q236IRIM/Gu4kHxFBVkBcYJaJv9iugn8oXunLSNWefPmYJgDmiPY!/r/dLYAAAAAAAAA
mp3: https://api.uomg.com/api/rand.music
---

# 堆栈

 

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/lX6WTEH86F31G7g9AJX*ZXxn3WpR6G70m*BVlXhq628!/r/dMQAAAAAAAAA)

# 1 定义

## 1.1 具有一定操作约束线性表，只能在一端（栈顶，Top）做插入删除

 插入数据：入栈Push

 删除数据：出栈Pop

 后入先出：LIFO

 先入后出：FILO

## 1.2 Stack

 1.2.1 一个或者多个有穷线性表

 1.2.2 操作集：长度MaxSize，堆栈元素ElementType

 Stack CreateStack(int MaxSize);

 int IsFull(Stack S,int MaxSize); 判断栈是否满

 void Push(Stack S,ElementType item); 压栈

 int IsEmpty(Stack S); 判断堆栈S是否为空

 ElementType Pop(Stack S); 删除并返回栈顶元素

## 1.3 FILO,LIFO

 1.3.1 可用于表达式求职，迷宫求解等深广度优先搜索

 1.3.2 表达式求值后缀例:62/3-42*+=？

 1.3.3 相当6/2-3+4*2=8

 将计算运算符压入符号栈中遇到优先级比栈顶元素低的则弹出

 括号需要注意左右括号的匹配，同级运算符按照从左往右的优先级

# 2 实现

## 2.1 顺序存储

 2.1.1 初始化

 Top=-1表示栈空

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/axN6h793IKN9jLPHIAeeB9v0c0AdcI4EjZ1*l*6NYMU!/r/dLYAAAAAAAAA)

 2.1.2 入栈

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/Gy8s0VDQOatAAm4iyEarSDcKG.CZMvhSEt3D3ysxdI8!/r/dAYBAAAAAAAA)

 2.1.3 出栈

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/FGkVR4exOtX0bgPm*wzpg3jE91TV1EzjZVLXCQh2PzQ!/r/dFQBAAAAAAAA)

 

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/8pbcNxVKitanA0GFbqev6BeDMsiyHG90o8*SMSZ2InA!/r/dAQBAAAAAAAA)

 2.1.4 一个数组实现两个堆栈

 建栈

 Top1和Top2相遇栈满

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/uQ**4y*p5k*r829lp9sWXchQojdSonIZ382fUaXgzKA!/r/dLYAAAAAAAAA)

 入栈

 压栈判断栈满，通过Tag标识区分对哪个栈的操作

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/aCIXHU2AcYSmFQPsfZKeSf8p6VKxyOu9Ji5cnDn*Txk!/r/dL4AAAAAAAAA)

 出栈

 出栈判断栈空

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/gWPO7Ry9quQ3kDDz*P*FCaToh36X1ci7yZqaO5ETqbY!/r/dFQBAAAAAAAA)

## 2.2 链式存储

 2.2.1 建栈

 单链表链栈，栈顶应该在表头

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/M1EjoHLDl7A0zqFn70ZY2pTdfMp28vCVgdMzcOXfGFA!/r/dD4BAAAAAAAA)

 2.2.2 入栈

 入栈可以不用判断栈满，链表大小动态分配

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/AB5c2D8rfo8ND2H5bugn6H59TxF8cH4hN.82k*46Dn4!/r/dL8AAAAAAAAA)

 2.2.3 出栈

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/muqvhhpjtk5pj6qlOB8GlMPHa0kEbwNfz6.E.6YgSCQ!/r/dLYAAAAAAAAA)



# 队列

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/pVQ3AFdI40zKWEy1n76nAKXmXZxoGcDhdqJncWmkPHM!/r/dLYAAAAAAAAA)

# 1 定义

## 1.1 具有一定操作约束的线性表FIFO(先进先出表)

## 1.2 只能在一段进行插入在另一端进行删除

## 1.3 数据对象集：一个有0个或者多个元素的又穷线性表

## 1.4 操作集：长度为MaxSize的队列Q，和队列元素ElementType

 Queue Create(int MaxSize); //生成长度为MaxSize的空队列

 int IsFullQueue(Queue Q,int MaxSize); //判断队列Q是否已满

 void AddQueue(Queue Q,ElementType item); //将数据元素item插入队列Q中

 int IsEmptyQueue(Queue Q); //判断队列是否为空

 ElementType OutDeleteQueue(Queue Q); //将对头数据元素从队列中删除并返回

# 2 队列顺序存储

## 2.1 创建

 front记录对头元素前一个位置rear记录队尾，浪费一个位置判断队列满情况

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/U7ewSAMHJu4cL0xc40dZCxmXG29GV3LLkwH6i5.fDuc!/r/dIMAAAAAAAAA)

## 2.2 初始化空间

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/4mp2PNYUN7NngPbxA0n*kXZvXKL.ZkXkxd0jtX3Nw2E!/r/dL8AAAAAAAAA)

## 2.3 判断队满

 队尾位置加一模队最大存储空间==队头元素

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/W8X83ADNKXdRHrZDe*7HTQA6r3l3CZB7fW7Zp6fARYg!/r/dL4AAAAAAAAA)

## 2.4 将数据元素插入队列

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/fHxq5nyrwGvJ0oDX4xhCp6b3kgr1FBlj74Y3Y9LqHQc!/r/dL8AAAAAAAAA)

 如图

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/.rYRVWQ5DUbhu.zWd3MG4ffxyFMleWQITYTwWkdadtE!/r/dL8AAAAAAAAA)

## 2.5 判断队空

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/D*LrYMKFfvlly8D66SxA9hZqbYC4C.QnVbqOJTE6GRY!/r/dLgAAAAAAAAA)

## 2.6 出队删除

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/KSu.MhaCh6p74zheMBLmSBfivzlzRmIB1JK*A27Z*Aw!/r/dLgAAAAAAAAA)

# 3 队列的链式存储

## 3.1 创建

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/ut1qzxfTD*yHa3bTiABGPlXCcMqgHvBuYrSbHvuv5yU!/r/dL4AAAAAAAAA)

## 3.2 判断队空

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/Tfj37LICt**sZKvLxRCIYkS0GdTSUgnX80j2dUQr7gE!/r/dL8AAAAAAAAA)

## 3.3 入队

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/HnaLPnAEXLhggpzUnlqipeLjP2C7PgaMAHplRArSk78!/r/dLgAAAAAAAAA)

 忘记计数队列中元素的个数了，立个flag每次添加时候++，删除时候--

## 3.4 出队

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/yfgEjRkhbCfrGd2tg7vky.qtLDayPbXTGUBAJupZ93g!/r/dLYAAAAAAAAA)