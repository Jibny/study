---
title: 数据结构(四)二叉树
date: 2019-09-23 22:51:07
categories: 
    Data-Structure
tags:
    数据结构二叉树
cover: http://r.photo.store.qq.com/psb?/V13Zm3q236IRIM/OtY0OKSV3oqfrgmOT0RxvEK*egJ7CsaQD.J2HM0QeVU!/r/dLYAAAAAAAAA
mp3: https://api.uomg.com/api/rand.music
---

# 数据结构(三)树

 <a href="https://shmly.top/temp/download/coding.rar" target="_blank">C语言代码下载</a>

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/CFr4aqAHhKH*spGWSJ8qyNgehlO7UZ6jOUVqB4akmDQ!/r/dLYAAAAAAAAA)

# 1 定义

## 1.1 用于描述事物与事物之间的层次关系，由N个结点构成的有限集合

 对于任意N>0的非空树

 包含根节点（Root）

 其余节点可分为M个互不相交的有限集，其中每个集合本身又是原来树的子树



## 1.2 基本概念术语

 结点的度（Degree）：结点的子树个数

 树的度：树的所有结点中最大的度数

 叶结点：度数为零的结点

 父结点，子结点

 兄弟结点（Sibling）：具有同一父结点的各结点彼此是兄弟结点

 祖先结点（Ancestor）：沿根结点到某一结点的所有结点都是这个结点的祖先结点

 子孙结点（Descendant）：某一结点子树中的所有结点

 结点的层次（Level）：根节点在1层，其他结点层数是父结点层数+1

 树的深度(Depth）：树的所有节点中最大层次是这棵树的深度



## 1.3 二分查找判定树

 判定树上每个节点需要查找的次数刚好是该节点所在层数

 查找次数不会超过判定树的深度，N个节点的判定树深度[Log₂N]+1

 四层满二叉树的平均查找成功次数：ASL=(8*4+4*3+2*2+1)/15=3



## 1.4 表示方法

 1.4.1 右边顺时针旋转45°就是一课二叉树

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/HHH*TvteIlmLs06.BYecJUl9Z.Dyzch0tYZVgJlDjT8!/r/dLYAAAAAAAAA)

# 2 二叉树（Binary Tree）

## 2.1 子树左右有顺序之分

## 2.2 几种特殊的二叉树

 斜二叉树

 完美二叉树/满二叉树

 完全二叉树



## 2.3 重要性质

 深度为k的二叉树有最大结点总数

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/fvhjaWXI*YDB2EDIJvSg8hieo2rksnNHxgzLZS4iDxc!/r/dL8AAAAAAAAA)

 第i层最大结点树是

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/qUrXM2wZLlgJCIhjSY0Q0Pr9nZhg8YTCLRzVYjPdA9Y!/r/dFIBAAAAAAAA)

 任何非空二叉树【 叶结点的个数 = 度为2的非叶节点的个数+1 】

  

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/XfyW.a1XhrAuWzqGqKXgPn5zvM2Vgw2khL9T0SH*FeA!/r/dLYAAAAAAAAA)

 边数=n。+ n₁ + n₂  - 1

 2.3.4 二叉树的高度

 一个二叉树的高度等于其左右子树中的最大高度的+1：Height=max(H左，H右)+1

 用后序遍历递归取得左右子树的高度

 由两种遍历序列可以确定二叉树，已知中有中序

## 2.4 基本操作集

 二叉树BinTree，树结点元素ElementType

 Boolean IsEmpty(BinTree BT); //判断BT是否为空

 BinTree CreatBinTree(); //创建一个二叉树

 void OverTraversal(BinTree BT); //遍历，按某种顺序访问每个结点

 常用的遍历方法有先序，中序，后序，层次遍历（上到下，左到右）

## 2.5 完全二叉树顺序结构表示

 第i个元素的父结点下标i/2

 第i个元素的左子节点下标2*i，右儿子结点的下标2*i+1

 缺点：二叉树需要构建成完全二叉树，会造成大量空间浪费

 静态链表表示方法

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/JX*hNjQ0IwNllDJ67N.JF7XExudYCPHM5avpw0gIELY!/r/dMMAAAAAAAAA)

 根在T[1]：判断left和right中没用到的下标(1)

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/tJnMb8Ue8qOyebGmku3ejggqucYe4jVlro33HD0xbMs!/r/dMMAAAAAAAAA)

######  

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/xeBfsYlsSfi2E1PjkP.VzheZ6NjhpQU.EuHmW5uw*Q4!/r/dL8AAAAAAAAA)

## 2.6 二叉树的遍历

 2.6.1 前中后序遍历

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/aYmAxi26g2dwb8f7RsjAjwUZTm6WstK9kVZlW4c7WdA!/r/dL8AAAAAAAAA)



 2.6.2 非递归堆栈实现前中后序遍历

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/uZMkF*u8FCQO9Uw3kfKeKlMHw7NfMRY6FQ0ivvtcV7k!/r/dLYAAAAAAAAA)



 2.6.3 队列实现层序遍历

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/5LKvsu8qGHuwuG8KejexfWn.UnaJgF5TF6oC5mCcKcw!/r/dFQBAAAAAAAA)

若是按层输出则还需判断每一层的最右节点，如下

```C++
void LevelorderTraversal ( BinTree BT )//队列实现二叉树层序遍历 
{ 
    Queue Q; 
    BinTree T;
 	BinTree last=BT;
 	BinTree nolast=BT;
    if ( !BT ) return; // 若是空树则直接返回 
     
    Q = CreateQueue(MAXSIZE); // 创建空队列Q
    AddQ( Q, BT );
	//每次循环从队列里出队一个元素并且把这个元素的左右儿子放入队列，重复这过程 
    while ( !IsEmpty(Q) ) 
	{
        T = DeleteQ( Q );
        printf("%d ", T->Data); //访问取出队列的结点
        if ( T->Left ) 
		{
			AddQ( Q, T->Left );
			nolast=T->Left;
		} 
        if ( T->Right )
		{
			AddQ( Q, T->Right );	
			nolast = T->Right;
		} 
		if(last == T)
		{
			printf("\n");
			last=nolast;
		}
        
    }
}
```



## 2.7 二元运算表达式树

 2.7.1 叶结点运算数非叶结点运算符号

 2.7.2 中序受运算符优先级影响不准（输出左右子树时加括号）



# 3 二叉搜索树（Binary search Tree）

## 3.1 左子树所有结点都小于根结点，右子树所有结点都大于根结点

 3.1.1 定义结构



![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/HzRQCAGqoteZsq*51R4pcn.HAUgF5t98Lngenn.JLsQ!/r/dL4AAAAAAAAA)



## 3.2 Position Find(ElementType X,BinTree BST);

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/o*9kS6soQ*Rl5mhaETSe86ugxvDZIwWqpR5v3RlFATg!/r/dMMAAAAAAAAA)

 3.2.1 FindMin

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/Wz47bhR27ajV02jgTJ7*kwe.*zW26lAvHHSC.skDT.Q!/r/dL8AAAAAAAAA)



 3.2.2 FindMax

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/MVqsEMgoHK19pzNpwYujJaPnS6nVMFi3Dwmze42LGRw!/r/dLYAAAAAAAAA)



## 3.3 BinTree Insert(ElementType X,BinTree BST);

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/S17IvlynDVmFVkbw.Dy9xSdjiZhNB2bnCLBt0imxgZ0!/r/dLYAAAAAAAAA)



## 3.4 BinTree Delete(ElementType X,BinTree BST);

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/fuOwox1zvRSuSYgbcKKLQaAtJi.HgbXKHD8.E.O0Wjk!/r/dL8AAAAAAAAA)



## 3.5 堆栈实现二叉树前中后序的非递归遍历

## 3.6 队列实现二叉树的层序遍历（层次输出还需要在当前遍历最有结点加换行）

# 4 平衡二叉树（AVLTree）

## 4.1 不同的插入次序导致不同的深度， 平均查找次数ASL也不同

## 4.2 AVL树左右子树高度差绝对值不超过1

## 4.3 高度=层数-1  高度H的最小结点数为斐波那契数+1

![img](http://r.photo.store.qq.com/psb?/V13Zm3q235lv98/Ns6ypFlTftyZs3HFChHIeMl6.CEOerRWa*e.Ptm2zmY!/r/dMMAAAAAAAAA)

## 4.4 插入删除时候要保证二叉树高度差平衡因子绝对值不超过1

 4.4.1 LL旋转，LR旋转，RR旋转，RL旋转等一系列保持平衡操作

# 5 红黑树RB-Tree

## 5.1 和平衡二叉树类似都是通过插入删除时通过一系列操作保持二叉查找树的平衡

## 5.2 STL和Linux都采用红黑树作为平衡树的实现

## 5.3 五个性质

 结点是红色或黑色

 根节点是黑色

 每个叶节点（也叫NIL结点，空节点）是黑色的

 每个红色结点的两个子结点都是黑色的

 从任意结点到其每个叶子（子孙叶节点）的所有路径都包含相同数目的黑色结点

 总结：有红必有黑，有黑不一定有红([*每个红色结点的两个子结点都是黑色的*](#_5_3_4__________________), [*从任意结点到其每个叶子（子孙叶节点）的所有路径都包含相同数目的黑色结点*](#_5_3_5____________________________________))

## 5.4 与平衡二叉树的区别

 最坏运行时间也良好O(LogN)

 插入相同于AVL最多两次旋转，删除优于AVL最多三次旋转，大量插入删除时不用频繁rebalance

 虽然AVL高度平衡，查找效率更高，大量插入删除频繁rebalance