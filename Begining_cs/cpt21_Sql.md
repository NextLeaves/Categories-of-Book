# SQL

* **Date:**3/23/2018 15:56:00 PM 
* **Author:**NextLeaves
* **Expression:** 

---

**Comtent：**

* 使用数据库
* 理解Entity Framework
* 用Code First创建数据
* 使用LINQ和数据库
* 导航数据库关系
* 在数据库中创建和查询XML

---

## 1. 使用数据库 ##

* 数据库是**长久的，结构化**的数据仓库
* 存储和查询的数据库用的较多的是关系型数据库
* CodeFirst方法写对象；LINQ方法查询对象；而可以不用使用SQL语言
* 安装Microsoft SQL Server express，初学阶段使用LocalDB

—

* Entity Framework(EF)：实体数据库，来源于数据库的关系存在实体关系数据库；实现**C#中的对象映射到实体关系的过程**
* Entity Framework实际上是ADO.NET在.NET代码的底层实现
* LINQ to Entities，用于查询数据内容

## 2. Code First 数据库 ##

* 安装Entity Framework，在NuGet包中下载
* 使用逻辑：
	* 创建前提：
		* using System.Data.Entity;
		* using System.ComponentModel.DataAnnotations;
		* using System.Linq;
		* [Key]：描述主键
		* 创建数据库上下文：
			* DbContext：父类
			* BookContext：类
			* DbSet<T>：对应的保存数据集
	* 操作逻辑：
		* 创建数据库对象：var db=new BookContext();
		*  存储数据后···
		*  SaveChange()：保存数据内容
	*  LINQ操作：
		*  var query = from b in db.Books orderby b.Title select b;
		*  foreach操作query
*  连接数据库操作：
	*  位置：(localdb)/MSSQLLocalDB
		*  若安装以前的VS版本则位置为：(localdb)/v11.0

## 3. 导航数据库关系 ##

* Entity Framework较强大的地方在于：linq自动生成数据对象，帮助查询数据（延迟查询）
* 当一个类需要存储另一个类的数据时，需要使用**virtual**修饰前者类的存储属性

`

	public class Store
	{
		public string Name{get;set;}
		public virtual List<Stock> Inventory{get;set;}
	}
	
	public class Stock
	{
		public string ID{get;set;}
		public vitrual Book item{get;set;}
	}
	
	publlic class Book
	{
		public string Name{get;set;}
		public string Author{get;set;}
	}
	
## 4. 处理迁移 ##

* 当需要改变之前数据库的关系图时，再次运行会出现，Invalid Operation Exception
* 处理步骤：
	1. 安装NuGet包，**Code First Migrations**
	2. 在Console界面输入：Enable-Migrations -EnableAutomaticMigrations
	3. 需要更新的时候，输入：Update-Database

## 5. 在已有的数据库中创建和查询XML ##

* xml多用于，客户端和服务器之间的数据传输，同时也用作不同层之间传输数据的方式
* **Linq to Entities**:延迟保存数据；**Linq to XML:**查询的数据翻译成xml
* 学习步骤：
	1. add item project : ADO.NET Entities Data Model
	2. using System.Xml.Linq;using System.Linq;
	3. 针对于Xml的类对象
		* XElement
		* XAttribute

`

	using(var db = new BookContext())
	{
		var result = from s in db.Stores
					orderby s.Name
					select s;
		foreach(var item in result)
		{
			XElement storeElement = new XElement("Store",
				new XAttribute("Name",item.Name),
				new XAttribute("Address",item.Address),
				from s in item.Inventory
				select new Element("stock",
					new XAttribute("Name",s.Name),
					new XAttribute("OnHand",s.OnHand)
					)//end stock
				)//end store
		}			
		
	}		