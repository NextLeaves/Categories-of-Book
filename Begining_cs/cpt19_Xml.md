# XML & JSON

* **Date:**3/26/2018 8:53:02 AM 
* **Author:**NextLeaves
* **Expression:** 

---

**Comtent：**

* XML基础
* JSON基础
* XML模式
* XML文档对象模型
* 把XML转换为JSON
* 使用XPath搜索XML文档

---

## 1. XML基础 ##

* W3C标准格式，类似于HTML
* **特性和元素**：统称为结点（element）

`

	<book>
		<title>Beginning Visual C# 2015</title>
		<author>Benjamin</author>
		<code>0987632</code>
	</book>

## 2. JSON基础 ##

* JSON(JavaScript Object Notation),也是一个标准(www.json.org)

`

	"book":[{
			"titile":"Begining Visual c# 2015",
			 "author":"Benjamin",
			 "code":"09876231"
			}]

## 3. XML模式 ##

* 用于C#的标准模式XML格式是XSD（XML Schema Definition）

`

	<?xml version="1.0" encoding="utf-8"?>

* 创建XML文件的方式：
	* 创建文件
	* 保存为XSD文件，用于Intellisense

## 4. XML文档对象模型 ##

* XML的DOM(Document Object Model)是一组直观的访问XML的类
* DOM不是读取XML数据最快捷的方式
* 引用类库：
	* using System.Xml;
	* XmlNode
	* XmlDocument
	* XmlElement:派生于XmlLinkedNode,XmlLinkedNode派生于XmlNode
	* XmlAttribute
	* XmlText
	* XmlComment
	* XmlNodeList

### XmlDocument类 ###

* 用于创建，引用，保存，删除等功能为一体的操作XML文件的类
* 属性：
	* **DocumentElement**：返回根节点（XmlElement类型）

### XmlElement类 ###

* FirstChild
* LastChild
* ParentNode
* NextSibling
* HasChildNodes：bool
* 迭代XML文档中所有结点：p529

### 修改结点的值 ###

* InnerText
* InnerXml
* Value：
	* XmlText
	* XmlAttribute
	* XmlComment

### 插入新节点 ###

* XmlDocument和XmlNode类：可以创建相应的节点
	* CreateNode()
	* CreateElement()
	* CreateAttibute()
	* CreateTextNode()
	* CreateComment()
* 插入数据：
	* AppendChild()
	* InsetAfter()
	* InsertBefore()

### 删除节点 ###

* RemoveAll()
* RemoveChild()：返回删除的节点

### 选择节点 ###

* 使用XPath来查询节点
* XmlNode类：
	* SelectSingleNode()
	* SelectNodes()

## 5. 把XML转换为JSON ##

* NuGet库里面使用第三方库：**NewtonSoft JSON.NET**
	* 帮助文档：[www.json.net](www.json.net "第三方库帮助文档地址")
* **Newtonsoft类**
	* Json类
		* JsonConvert
			* SerializeXmlNode(XmlDocument类型);

`

	string jsonmessage=Newtonsoft.Json.JsonConvert.SerializeXmlNode(xmlDocument)
	string

	//value:
		//Type:System.String
		//The JSON string.
	 xmlmessage=NeWTONSOFT.Json.JsonConvert.DeserialzeXmlNode(string value):

## 6. 用XPath搜索XML ##

* XPath相当复杂，只是简要介绍一下
* 帮助文档：[www.w3.org/TR/xpath](www.w3.org/TR/xpath "XPath")
*