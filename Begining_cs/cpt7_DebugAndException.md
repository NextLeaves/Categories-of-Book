# DebugAndException

* **Date:**4/10/2018 1:26:34 PM 
* **Author:**NextLeaves
* **Expression:** 

---

**Comtent：**

* vs中的调试
* 非中断模式
* 中断模式

---

## 1. vs中调试

* Debug模式下：
	* 包含应用程序的符号信息（机器码为二进制，便于跟踪数据的值，用于匹配机器码中的数据值，存储在.pdb文件中）.pdb(program database file)
* Release模式下：
	* 运行速度更快，没有符号信息存在

## 2. 非中断模式

* namespace:
	* using System.Diagnostics;
* **代码方式**
	* Debug.WriteLine()
	* Trace.WriteLine()
	* 区别：
		* 前者，在realse模式下，甚至不会写入文件，文件大小减小
		* 后者，在realse模式下，依然会有数据写入output窗口

* **vs模式**
	* 跟踪点（trace point） 

`

	$FUNCTION:x,y值{x,y};

## 3. 中断模式

* **Pase按钮**
* **断点（break point）**
	* 发布模式忽略所有断点操作
* **代码方式：**
	* Debug.Asset()
	* Trace.Asset()
	* 若为false则触发断点操作

## 4. Immediate And Command窗口

* Command手动执行vs操作（菜单和工具栏操作）
* Immediate执行与代码相关的数据操作
* 【技巧】，输入immed切换到immediate窗口，cmd切换到command窗口

## 5. Call Stack窗口

* 查看当前逻辑的调用层次，便于发现错误的位置情况

## 6. 错误处理

* try..catch()when()..finally
* 列出配置异常操作：
	* （本身vs就是一个巨大的exception控制的容器）
	* 列出配置操作，就是选择vs中对于exception的错误操作方式
