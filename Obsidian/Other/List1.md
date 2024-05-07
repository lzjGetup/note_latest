## 查找端口占用情况
==CMD命令==

*末尾数字为端口号*

![[Pasted image 20231001141738.png]]


==Maven==

*设置资源和跳过测试*


![[Pasted image 20231001205305.png]]

==SpringMVC乱码处理==

>![[Pasted image 20231002111346.png]]


# 状态码

**500——服务器产生内部错误**
**501——服务器不支持请求的函数**
**502——服务器暂时不可用，有时是为了防止发生系统过载**
**503——服务器过载或暂停维修**
**504——关口过载，服务器使用另一个关口或服务来响应用户，等待时间设定值较长**
**505——服务器不支持或拒绝支请求头中指定的HTTP版本**

# XmlHttpRequest

**XMLHttpRequest**对象有以下常用方法：

**open**(method, url, async, user, password)：初始化一个请求。参数method表示请求的类型（GET、POST等），url表示请求的URL，async表示是否异步发送请求，user和password表示可选的用户名和密码。

**send**(data)：发送请求。参数data表示要发送的数据，通常在POST请求中使用。

**setRequestHeader**(header, value)：设置HTTP请求头部。参数header表示要设置的头部名称，value表示头部的值。

XMLHttpRequest对象的参数列表和返回值如下：
参数列表：

**method**：请求的类型（GET、POST等）
**url**：请求的URL
**async**：是否异步发送请求
**user**：可选的用户名
**password**：可选的密码
**data**：要发送的数据
**header**：要设置的头部名称
**value**：头部的值
返回值：
无特定返回值，通常通过事件处理函数来处理请求的结果。

# setRequestHeader方法

setRequestHeader(header, value) 方法用于设置HTTP请求头部。这个方法通常在使用XMLHttpRequest对象发送请求时用到。header 参数表示要设置的头部名称，value 参数表示头部的值。

以下是一些常见的 HTTP 请求头部：

1. Content-Type：指定请求发送的数据类型，例如 "application/json" 表示发送 JSON 数据。
2. Accept：指定客户端能够接收的内容类型，例如 "application/json" 表示客户端希望接收 JSON 格式的数据。
3. Authorization：用于发送身份验证信息，例如 "Bearer token" 表示使用 Bearer 令牌进行身份验证。
4. User-Agent：发送请求的用户代理信息，通常包含浏览器或应用程序的相关信息。

```javascript
xhr.setRequestHeader("Content-Type", "application/json");
xhr.setRequestHeader("Accept", "application/json");
```


