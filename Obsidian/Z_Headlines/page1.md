# 大文本展示方案

>![[Pasted image 20240210155851.png]]


# FreeMarker

>![[Pasted image 20240210160359.png]]

## 模板对比
>![[Pasted image 20240210160332.png]]


## 基础语法


>![[Pasted image 20240210162613.png]]

### list
>![[Pasted image 20240210163011.png]]

其中`stu_index`用于获取索引,从0开始

### map

>![[Pasted image 20240210163437.png]]


## if

>![[Pasted image 20240210163634.png]]

### 运算符
==算术运算符,比较运算符,逻辑运算符与java基本一致,不赘述==


>![[Pasted image 20240210163949.png]]

### 空值处理

>![[Pasted image 20240210164510.png]]

### 内置函数

>![[Pasted image 20240210164751.png]]

>![[Pasted image 20240210165001.png]]



# MinIO
MinIO是一个开源的对象存储服务器，它允许用户在私有云环境中构建高性能的分布式存储。MinIO专注于提供高可用性、可扩展性和安全性，同时保持简单易用的特点。它兼容Amazon S3 API，因此可以轻松地与现有的S3应用程序和工具集成。MinIO还支持Erasure Code和分布式存储等先进的功能，使其成为构建现代数据基础设施的理想选择。


# FreeMarker&MinIO
freemarker将文本数据转换为静态资源文件,再将文件上传到分布式文件系统,然后再返回文本url路径供前端使用

```java
//文章内容通过freemarker生成html文件  
StringWriter out = new StringWriter(); 
//获取模板
Template template = configuration.getTemplate("article.ftl");  
//用map存储参数传向模板
Map<String, Object> params = new HashMap<>();  
params.put("content", JSONArray.parseArray(apArticleContent.getContent()));  

template.process(params, out);  
InputStream stream = new ByteArrayInputStream(out.toString().getBytes());

//上传文件
//3.把html文件上传到minio中
String path = fileStorageService.uploadHtmlFile("", apArticleContent.getArticleId() + ".html", stream);
```

其中flieStorageService是封装好了的工具类,apArticleContent为mp从数据库查询的数据

