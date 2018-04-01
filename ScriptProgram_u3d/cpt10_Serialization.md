# Serialization in Unity3d

* **Date:**4/1/2018 1:56:58 PM
* **Author:**NextLeaves
* **Expression:** 
	* 前面介绍C#中的序列化、反序列化内容
	* 后面介绍序列化、反序列化在Unity3d中的内容

---

**Comtent：**

1. 初识序列化机制
2. 选择可序列化的类型，以及标记不序列化的类型，序列化之中的处理函数
3. unity3d与序列化相关的机制
4. 脚本序列化时的注意事项
5. prefab机制

---

## 10.1 初识序列化机制

* namespace:
 	* using System.IO;
	* using System.Runtime.Serialization;
	* using System.Runtime.Serialization.Formatters;
	* using System.Runtime.Serialization.Formatters.Binary;
* class:
	* BinaryFormatter
		* Serialize()
		* Deserialize()
	* MemoryStream
* 【扩展】：
	1. 针对于XML的序列化：
		* class:
			* XmlSerializer
			* DataContactSerializer
	2. 针对于另一个格式化器
		* namespace:
			* using System.Runtime.Serialization.Formatters.Soap;
		* class:
			* SoapFormatter
* 【细节】：
	1. BinaryFormatter
		* 检查对象的元数据，保证每个对象只序列化一次（即使引用的同一个栈中对象，也只序列化一次对象的数据）
	2. FileStream
		* 句柄的引用，记得释放！！！
* 【小结】：
	1. 序列化可以同时序列化多个对象，再进行数据流保存
	2. 序列化与反序列化必须保证使用的是同一种格式化器
	3. 针对于序列化中，是根据元数据进行判断的标准，若名称空间不一样，或者其他的细节导致元数据不符合，会导致序列化立即终止，序列化失败

## 10.2 序列化标记

* namespace:
	* using System;
* attribute:
	* SerializableAttribute
	* NonSerializedAttribute
* 【注意】：
	1. 只能标记**class/struct/enumerate/delegate**类型，后两者可不必显性标记
	2. 标记的[Serializable]没有继承的效果
		* 基类修饰、子类未修饰；基类能序列化，子类不行
		* 基类未修饰、子类修饰；都不能序列化
	3. 标记的[NonSerialized]具有继承的效果
		* 基类修饰，子类自动继承
	4. fileStream.Posion=0;设置流的位置，在反序列化之前的考虑

---

* namespace:
	* using System.Runtime.Serialization;
* attribute:
	* OnDeserializedAttribute
	* OnDeserialingAttribute
	* OnSerializedAttribute
	* OnSerializingAttribute

`

	//1.must to add a parameter:StreamingContext
	//2.must to returnValue:void
	//3.suggest modifier:private
	[OnDesrialized]
	private void CalculatePowerRank(StreamingContext context)
	{
		//calculate power value
	}

---

* 针对深度clone操作**StreamingContext**类型
* class:
	* StreamingContext
		* 值类型
		* struct类型
* 【步骤】：
	1. 生成BinaryFormatter对象
	2. 修改上述对象的字段：bf.Context=New StreamingContext()
	3. 设置格式化方式：StreamingContextStates
		1. CrossProcess:	同一电脑、不同进程
		2. CrossMachine:	不同机器
		3. File:			来源于文件，不承认是同一进程
		4. Remoting:		来源于远程服务
		5. Other:			来源未知
		6. Clone:			克隆对象，同一进程的操作
		7. CrossAppDomain	来源是不同的AppDomain([https://msdn.microsoft.com/zh-cn/subscriptions/downloads/system.appdomain.aspx](https://msdn.microsoft.com/zh-cn/subscriptions/downloads/system.appdomain.aspx "AppDomain Expression"))
		8. All				包含以上各种可能（默认设置）

## 10.3 Unity3d中的序列化相关的机制

1. Inspector数值
2. Prefab机制：（可选择两种序列化方式）
	* Edit->ProjectSetting->Editor
		* Force text
		* force binary
3. Instantiate()
4. 存储场景：
	* 文本型：YMAL
	* 二进制类型：.dat
5. 场景的载入
6. 重载代码编辑器
7. Resource.GarbageCollectShardAssets()
	* 切换场景时，判断不必要的资源的数量即位置等，释放资源

## 10.4 脚本序列化的注意事项

* 注意点：
	1. 字段最好为public，修饰特性
	2. 不要为const/static/readonly
	3. 字段类型可被可序列化的
		* 自定义**类、结构**类型，非抽象类
		* 派生自UnityEngine.Object类型
		* C#的基本类型
		* 数组类型
* 【细节】：
	1. 在unity3d中，若多次引用相同类型，会造成序列化很多次，资源浪费（只针对于自定义类型，不包括继承自Object类型）
	2. 针对于字段类型为null的序列化，会导致死循环序列化（729次，循环次数上限）
	3. **多态类型的限制，序列化为Animal基类的DOg子类、Cat子类；但是反序列化只是Animal类型**
	4. 针对于自定义类型的序列化的重复序列化，可以针对变成Unity类型，再反序列化回来的效果（具体p305）