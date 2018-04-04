# File

* **Date:**4/4/2018 7:29:24 PM  
* **Author:**NextLeaves
* **Expression:** 

---

**Comtent：**

* 使用输出与输入的类
* Stream类、FileStream类
* 存储中的压缩方式
* 文件监控系统

---

## 1. 用于输入与输出的类 ##

* namespace:
	* using System.IO;
	* using System.Compression;
* Compression class:
	* DeflateStream
	* GZipStream

### File类、Directory类

* 对于Directory类，**GetXXX()**比**EnumerateXXX()**性能差

* 【**FileInfo**类】（略）
* windows中的路径为反斜杠的方式

### DirectoryInfo类（略）

* 路径名和相对路径
	* 相对路径
	* 绝对路径：**"..\log.txt"**；表示上一个文件的位置
* Directory.GetCurrentDirectory()
* Directory.SetCurrentDirectory()

## 18.2 流Stream

* 序列化设备的抽象表示
	* 1. 线性读写对象
	* 2. 文件流可以忽略设备的物理机制
* 流相关的类：
	* FileStream：操作字节和字节数组
	* MemoryStream
	* StreamWriter
	* StreamReader
* Stream：操作字符数据
* **FileMode:**
	* Append
	* Create
	* CreateNew
	* Open
	* OpenOrCreate
	* Truncate
* **FileAccess:**
	* Read
	* Write
	* ReadWrite
* **【小技巧：】**
	* File和FileInfo具有OpenRead()，OpenWrite()，易于创建FileStream类
* **文件位置：**
	* FileStream类
		* Seek(int,SeekOrigin)
			* SeekOrigin.Start
			* SeekOrigin.Current
			* SeekOrigin.End
* **读取数据：**
	* FileStream类
		* Read()
* **写入数据：**
	* FileStream类
		* Write()
* **【StreamWriter：】**
	* Write()
	* WriteLine()
* **【StreamReader：】**	
	* Read()：返回值为-1，读取到流结尾
	* ReadLine()
	* ReadToEnd()
	* ReadLines()：返回为IEnumerater<T>数据
* **异步文件访问**（略）

### 读写压缩文件

* using System.IO.Compression;;
	* GZipStream：适合重复数据的压缩方式
	* DeflateStream

`

	FIleStream fs = File.Open(path);
	DeflateStream ds = new DeflateStream(fs,CompressMode.Compress);
	StreamWriter sw = new StreamWriter(ds);

## 18.3 文件监控系统

* namespace:
	* using System.IO;
	* using Microsoft.win32;
* class:
	* FileSystemWatcher
* Property:
	* Path
	* NotifyFilter
	* Filter
* evnet:
	* Changed
	* Created
	* Deleted
	* Renamed
* watcher.EnableRaisingEvents=true;开启监控系统