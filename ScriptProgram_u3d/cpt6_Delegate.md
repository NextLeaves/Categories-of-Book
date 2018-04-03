# Delegate in Unity3d

* **Date:**4/2/2018 7:21:54 PM 
* **Author:**NextLeaves
* **Expression:** 
	* 在C#中的委托机制
	* 在unity3d中的委托方式

---

**Comtent：**

1. 回调函数机制-委托
2. 委托链的实现
3. 委托的底层实现方式
4. 使用事件实现消息系统（掉血演示）
5. 委托的语法糖
6. 匿名方法-闭包问题
7. lambda表达式

---

## 6.1 回调函数机制-委托

### 对SendMessage()和BoardMessage()说拜拜

* 缺点：
	1. 过于依赖反射机制，导致性能下降
	2. 重构代码对于修改函数名称的问题（当然此问题，在VS2017解决，可以通过ctrl+r,ctrl+r来一次修改所有引用的函数名称）

---

* c/c++实现委托的机制是，通过函数指针，但是只是引用而已，属于类型不安全方式
* c#属于安全机制

`

	delegate void MyDelegate(string name);
	MyDelegate myDelegate = new MyDelegate();
	myDelegate=Print;
	myDelegate("Xiaoming");

	void Print(string name)
	{
		pirnt(name);
	}

* C#中的**协变(covariance)与抗变(variance)**
	* 协变针对：返回值；父类，可以使用子类
	* 抗变针对：参数；子类，可以使用基类

## 委托的底层实现

* 程序员的的语句 **delegate void MyDelegate()**
	* 其实编译器在后面处理了很多工作
	* 生成一个完整的MyDelegate类
		* Constructor
		* Invoke()
		* BeginInvoke()
		* EndInvoke()
* 继承链：
	* System.Delegate
		* System.MulticastDelegate
			* System.MyDelegate
	* 所以所有的委托类型，都是继承自MulticastDelegate类
* 【要求】：
	1. 任何定义类的位置，都可以定义委托
	2. 委托也可以使用访问修饰符

* 【针对】：MulticastDelegate类
	* _target：对非静态方法的对象的引用
	* _methodPtr：对访问的唯一的标志
	* _invocationList：委托链保存方式

* 【注意】：
	1. 调用委托的时候，请注意委托是否为null
	2. 可以使用显性的方式调用，也可以使用隐式的
		* myDelegate()：隐式
		* myDelegate.Invoke()：显式

## 委托链的使用

1. 第一种方式：
	* Delegate.Combine()静态方法
	* Delegate.Remove()静态方法
2. 第二种方法：
	* myDelegate+=方法
	* myDelegate-=方法

## 使用事件实现消息系统

* 【目的】：
	* 对象掉血的时候，通知掉血单位，进行掉血消息显示
* 【相关】：
	* delegate:OnSubHpHandler
	* event:OnSubHpEventHandler
	* class:
		* BaseUnit
			* OnBeAttacked()
			* BeAttacked()
		* BattleInfomationCompnent

## 委托的简化语法（略）

## 匿名方法

`

	Action<string> PrintMethod = delegate(string name){
		string intro="Xiaoming";
	};

* 四种委托方式：
	* Action<T>
	* Func<T>
	* Predicate<T>
	* Comparison<T>

### 闭包概念

* 一个函数除了可以和传递给他的参数交互外，还可以最大程度的和上下文数据进行交互

### Lambda表达式（略）