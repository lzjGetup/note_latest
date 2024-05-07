# ES


>![[Pasted image 20240201174920.png]]

## 倒排索引

  
倒排索引（Inverted Index）是一种用于快速查找文档中特定词语的数据结构。它将文档集合中每个词语的出现位置记录下来，然后以这些词语作为键，它们所在文档的编号或其他相关信息作为值，构建一个索引表。这样，当需要查找某个词语时，只需在倒排索引中查找该词语，就能快速找到包含该词语的文档列表，从而实现高效的信息检索。倒排索引在搜索引擎和文本检索系统中被广泛应用。


## MySQL_ES

>![[Pasted image 20240201193925.png]]

## IK分词器

IK分词器采用了先进的中文分词算法，能够较好地识别中文文本中的词语边界，对于中文分词有着较高的准确性和效率。

### 分词模式
1. 细粒度切分模式（ik_smart）：该模式会尽可能多地切分词语，适合对文本进行细粒度的分词处理。
2. 搜索引擎模式（ik_max_word）：该模式会将词语尽可能多地切分，适合作为搜索引擎使用。


### 简单配置

已知IK分词器装配在ES的插件目录中
配置词典:

1. 配置自定义词典：在IK分词器的插件目录中，可以找到一个名为"ext_dict"的目录，你可以将自定义的词典文件（如sensitive.txt）放置在这个目录中，IK分词器会自动加载这些自定义词典文件。
2. 配置停用词词典：类似地，在IK分词器的插件目录中，可以找到一个名为"ext_stopword"的目录，你可以将停用词词典文件（如stopwords.txt）放置在这个目录中，IK分词器会自动加载这些停用词词典文件。





## 索引库

### Mapping

在Elasticsearch的mapping中，常见的属性包括：

1. **类型（type）**：指定字段的数据类型，如text、keyword、date等。
2. **分词器（analyzer）**：用于指定处理文本字段的分词器，例如standard、ik_smart等。
3. **索引选项（index）**：控制字段是否被索引，可选值包括true、false和"not_analyzed"。
4. **存储（store）**：指定是否将字段的原始值存储在索引中，可选值包括true和false。
5. **复制到（copy_to）**：允许将一个或多个字段的内容复制到指定字段中，用于全文搜索等需求。
6. **动态模板（dynamic_templates）**：允许根据字段名或类型自动应用映射规则。
7. **字段属性（fields）**：允许在同一字段上应用多个不同的分析器或数据类型。


### 索引库操作


 ==创建==
 例如:
```json
PUT /my_index
{
  "mappings": {
    "properties": {
      "content": {
        "type": "text"/"keyword",
        "index": "true"/"false",
        "analyzer": "ik_smart"
      }
    }
  }
}
```

==查询==
GET  /索引库名
==删除==
DELETE  /索引库名
==修改==
PUT /索引库名/mapping
```json
PUT /my_index/_mapping
{
  "properties": {
    "new_field": {
      "type": "integer"
    }
  }
}
```


###  ES文档操作
当使用Elasticsearch进行文档的增删查操作时，可以使用以下简单的示例：

1. **增加文档**：

```json
POST /my_index/_doc
{
  "title": "Sample Document",
  "content": "This is a sample document for Elasticsearch."
}
```

2. **删除文档**：
```json
DELETE /my_index/_doc/1
```
这将删除索引为"my_index"中ID为1的文档。

3. **查询文档**：
```json
GET /my_index/_search
{
  "query": {
    "match": {
      "content": "sample"
    }
  }
}
```

这将在索引为"my_index"中搜索包含"sample"关键词的文档。
4. **修改文档**：

>![[Pasted image 20240201204952.png]]


## geo_piont以及copy_to

ES中的geo_point是一种特殊的数据类型，用于存储地理坐标，比如经度和纬度。这使得你可以在地图上准确地表示位置信息，并执行基于地理位置的搜索和分析。

而copy_to是一个属性，它允许你将一个字段的值复制到另一个字段中。这在搜索和分析时非常有用，因为它可以让你在不同的字段中存储相同的信息，以便于不同的查询需求。例如，你可以将多个字段的内容复制到一个专门用于全文搜索的字段中，以便于执行全文搜索操作。


## RestClient操作索引库

>![[Pasted image 20240202110538.png]]

>![[Pasted image 20240202111136.png]]

>![[Pasted image 20240202111638.png]]


## 文档操作
#### 新增文档

```java
@Test
void createDoc() throws IOException {
    // 1. 创建request对象,设置文档的ID
IndexRequest request = new IndexRequest("hotel").id("2");
    // 2. 准备文档数据，采用Key-Value结构
    Map<String, Object> jsonMap = new HashMap<>();
    jsonMap.put("age", 25);
    jsonMap.put("name", "Emily");
    request.source(jsonMap, XContentType.JSON);
    // 3. 发送请求
    IndexResponse indexResponse = client.index(request, RequestOptions.DEFAULT);
}
```

#### 更新文档
部分更新
```java
@Test  
void updateDoc() throws IOException {  
    //1.创建request对象  
    UpdateRequest request = new UpdateRequest("hotel", "1");  
    //2.准备参数,采用Key_Value结构  
    request.doc(  
        "age", 18,  
        "name", "jack"  
    );  
    //3.发送请求  
    client.update(request, RequestOptions.DEFAULT);  
}
```

>![[Pasted image 20240202120556.png]]


### 批量插入文档

>![[Pasted image 20240202122028.png]]





