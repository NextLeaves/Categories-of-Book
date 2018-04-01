# Linq

* **Date:**3/25/2018 15:48:00 PM 
* **Author:**NextLeaves
* **Expression:** 

---

**Comtent：**

* Linq to XML
* Linq提供程序
* Linq查询语法
* Linq方法语法
* Lambda表达式
* 对查询结果排序
* 聚合函数
* SelectDistinctQuery
* 组合查询
* 连接

---

## 1. Linq to XML ##

* using System.Xml.Linq;
* using System.Linq;
* 相关处理类：
	* XDocument
	* XElement
	* XAttribute
	* 不常用类：XDeclaration;XComment;XProcessingInstruction
* 处理片段XML文档，即不适用XDocument即可
* XElement类：
	* Save(string path：绝对路径)
	* static Load(string path：绝对路径)
* XDocument和XElement都继承与Linq to XML的**XContainer**类

## 2. Linq 提供程序 ##

* Linq to Objects
* Linq to XML
* Linq to Entities
* Linq to Data Set：对旧的.NET进行支持
* Linq to SQL：取代Linq to Entities
* PLINQ：并行处理Linq操作
* Linq to Json：Newtonsoft包，支持json到xml的转化

## 3. LInq 查询语法 ##

`

	strng[] names = {"xiaoming","Bob"};
	var query = from n in names
				where n.StartsWith("s")
				select n;
				
* 用**var**关键字声明结果变量；（看起来像是一个集合，从技术上讲其实不是）
	* 返回值实现：IEnumerable<T>
* **from**关键字用于声明查询的数据源（必须是可枚举的，数组或者集合）
	* 可枚举：支持IEnumerable
* **where**关键字用于筛选需要的数据，判断为bool值
* **select**关键字选择对于数据有趣的部分（必须存在）
* **foreach**实现对数据的输出，称为延迟查询

## 4. LINQ 方法语法 ##

* 实际上Linq的**查询语法**就是间接的使用**方法语法**来实现数据查询的
	* 建议尽量使用**查询语法**，需要的时候使用**方法语法**
* **Lambda表达式**一词来源于微积分

`

	n => n>2
	(a,b) => a+b;
	
	var query = name.Where(n=>n.StartsWith("S"));
	
## 5. 排序查询结果 ##

* **orderby**关键字，用于排序
	* orderby n ; orderby n descending

## 6. 查询大型数据集 ##

* 生成大数据进行查询语法，查询数据

## 7. 聚合运算符 ##

* 用于分析大数据的内容，而不必全部显示出来
* 相关函数：
	* Count()，LongCount()
	* Max()
	* Min()
	* Average()
	* Sum()
	* 高级聚合函数：
		* Aggregate
	* 针对于改变类型（防止溢出）：numbers.Sum(n=>(long)n);

## 8. 单值查询 ##

* Distinct()：实现对重复值的删除，只输出未重复的值
* Select()：实现对感兴趣的数据的选择

`

	var query = customers.Select(c=>c.Region).Distinct();
	
## 9. 多级排序 ##

`

	var query = from c in customers
				orderby c.Name,c.Region,c.Sex
				select new {c.ID,c.Region,c.County};
				
## 10. 组合查询 ##

`

	var queryResult = from c in customers
						group c by c.Region into cg
						select new {TotalSales=cg.Sum(s=>s.Sales),Region=cg.Key};
						
	var queryOrder = from cg in queryResult
						orderby cg.TotalSales descending
						select cg;
						
* 组的结果集实现了Linq接口IGrouping，支持Key属性

## 11. Join查询 ##

`

	var queryResult = from c in customers
						join o in orders on c.ID equals o.ID
						select new {c.Name,c.Amount,o.ID,o.Price};