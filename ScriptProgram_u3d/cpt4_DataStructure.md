# DataStructure in Unity3d

* **Date:**4/3/2018 4:21:37 PM 
* **Author:**NextLeaves
* **Expression:** 
	* 针对于unity3d常使用的数据结构类型介绍

---

**Comtent：**

1. Array类型
2. ArrayList类型
3. List<T>类型
4. Queue<T>和Stack<T>类型
5. HashTable类型
6. Dictionary类型

---

## 4.1 Array类型

* 一维数组
* 二维数组
* ragged array

## 4.2 ArrayList数组

* namespace:
	* using System.Collections;
* 缺点：
	1. 装箱、拆箱操作
	2. 类型不安全

## 4.3 List<T>类型

* 泛型类型
* 类型安全

## 4.4 LinkedList<T>链表方式（略）

## 4.5 Queue<T>和Stack<T>

* Queue<T>
	* 初始分配的容量为32字节
	* Enqueue()
	* Dequeue()
	* FIFO
* Stack<T>
	* Push()
	* Pop()
	* FILO
	* 栈顶、栈低；只能在一端进行数据操作

## 4.6 HashTable和Dictionary

* 哈希表：又名散列表
* 哈希转换
* 哈希函数
* 哈希冲突：
	* 冲突避免机制
		* 提前预算存储数据的表示方式
	* 冲突解决机制
		* 开放寻址法
			* 线性探查
			* 二次探查
	* C#中的HashTable的解决机制：
		* using System.Collections;
		* 二度哈希

## 4.7 Dictionary<K,V>

* 解决冲突机制：链接技术；创建一个桶的方式
* 遍历字典的方式：
	1. foreach(var d in dict)
	2. foreach(KeyValuePair<k,v> d in dict)
	3. foreach(K k in dict.Keys)
	4. foreach(V v in dict.Values)
	5. List<V> list = dict.ToArray(dict);for()机制
* 缺点：
	* 以空间换时间
	* 实现是间接的实现索引，一个桶的数组，然后实际数据的数组；
	* 是以**初始化值的不小于初始化值的最小质数**，若数据不是太多，不适合使用字典来存储数据