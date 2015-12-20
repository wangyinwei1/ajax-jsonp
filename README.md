
this is ajax-jsonp summary

jsonp 的工作原理：

它是利用<script>标签的没有跨域限制的漏洞（历史遗址），与第三方达成通讯的目的。

著作权归作者所有。
商业转载请联系作者获得授权，非商业转载请注明出处。
作者：贺师俊
链接：

http://www.zhihu.com/question/19966531/answer/13502030
来源：知乎

当需要通讯时，本站脚本创建一个<script>
元素，地址指向第三方的API网址，形如：     <script src="http://www.example.net/api?
param1=1&param2=2"></script>     并提供一个回调函数来接收数据（函数名可约定，或通过地址参数传递）。    
 第三方产生的响应为json数据的包装（故称之为jsonp，即json padding），形如：     callback
({"name":"hax","gender":"Male"})     这样浏览器会调用callback函数，并传递解析后json对象作为参数。本站
脚本可在callback函数里处理所传入的数据。

jQuery 只支持get方式的jsonp实现

jsonp的缺点：

如果返回的数据格式有问题或返回失败了，并不会报错。

2.ajax原理和XmlHttpRequest对象
 
　　Ajax的原理简单来说通过XmlHttpRequest对象来向服务器发异步请求，从服务器获得数据，然后用javascript来
操作DOM而更新页面。这其中最关键的一步就是从服务器获得请求数据。要清楚这个过程和原理，我们必须对 
XMLHttpRequest有所了解。

　XMLHttpRequest是ajax的核心机制，它是在IE5中首先引入的，是一种支持异步请求的技术。简单的说，也就是
javascript可以及时向服务器提出请求和处理响应，而不阻塞用户。达到无刷新的效果。

所以我们先从XMLHttpRequest讲起，来看看它的工作原理。

首先，我们先来看看XMLHttpRequest这个对象的属性。

  　　它的属性有：
  　　onreadystatechange  每次状态改变所触发事件的事件处理程序。
  　　responseText     从服务器进程返回数据的字符串形式。
  　　responseXML    从服务器进程返回的DOM兼容的文档数据对象。
  　　status           从服务器返回的数字代码，比如常见的404（未找到）和200（已就绪）
  　　status Text       伴随状态码的字符串信息
  　　readyState       对象状态值
　　　
　0 (未初始化) 对象已建立，但是尚未初始化（尚未调用open方法）

　1 (初始化) 对象已建立，尚未调用send方法
　　　　
  2 (发送数据) send方法已调用，但是当前的状态及http头未知
　　　　
  3 (数据传送中) 已接收部分数据，因为响应及http头不全，这时通过responseBody和responseText获取部分数据会出现错误，
　　　
　4 (完成) 数据接收完毕,此时可以通过通过responseXml和responseText获取完整的回应数据