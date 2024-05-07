# DSL

DSL_query的分类

>![[Pasted image 20240202133108.png]]

查询DSL的基本语法

`GET /索引库名/_search`
`{"query":{"查询类型":{"FIELD":"TEXT"}}}`


# 查询
## 全文检索查询

>![[Pasted image 20240202134045.png]]


如果你知道要搜索的内容只在一个字段中，使用match查询可能会有更好的性能。但如果你需要在多个字段上执行搜索，multi_match查询提供了便利的方式，尽管在性能上可能会有一些损失。



## 精确查询


>![[Pasted image 20240202134840.png]]

## 地理查询

>![[Pasted image 20240202135247.png]]


>![[Pasted image 20240202135401.png]]


## 相关性得分算法

当涉及到信息检索和文本分析时，TF（词项频率）、TF-IDF（词项频率-逆文档频率）和BM25（BM25算法）是常用的算法和概念。

1. **TF（词项频率）**：TF是指在一个文档中某个词项出现的频率。它是用来衡量一个词项在文档中的重要性的指标。TF越高，表示该词项在文档中的重要性越高。TF可以通过简单地计算某个词项在文档中出现的次数来得到。
2. **TF-IDF（词项频率-逆文档频率）**：TF-IDF是一种用于信息检索和文本挖掘的常用加权技术。它结合了词项频率（TF）和逆文档频率（IDF）。TF-IDF的核心思想是，一个词项在文档中的重要性与它在整个文集中的频率成反比。即在当前文档中词项频率高，但在整个文集中出现频率低的词项，其重要性较高。TF-IDF可以通过以下公式计算：TF-IDF = TF * IDF。
3. **BM25算法**：BM25是一种用于信息检索的概率模型，它是TF-IDF的改进版本。BM25考虑了文档长度对词项频率的影响，并引入了一个调节参数来平衡词项频率和文档长度的影响。BM25在实践中被广泛应用，特别是在搜索引擎中。它的公式相对复杂，但是它的性能在很多情况下都比传统的TF-IDF要好。


### Founction Score Query

>![[Pasted image 20240202141017.png]]


### 复合查询

>![[Pasted image 20240202141837.png]]


# 排序

#### 地理坐标
假设我们有一个索引包含了商店的地理位置信息，并且我们想要按照距离给定地理坐标（纬度 40.7128，经度 -74.0060）的远近对商店进行排序，可以使用以下查询：

```json
{
  "query": {
    "match_all": {}
  },
  "sort": [
    {
      "_geo_distance": {
        "location": {
          "lat": 40.7128,
          "lon": -74.0060
        },
        "order": "asc",
        "unit": "km",
        "mode": "min",
        "distance_type": "arc"
      }
    }
  ]
}
```

在这个示例中，我们使用了sort来指定排序规则。在sort中，我们使用了_geo_distance来指定按照地理距离进行排序。具体来说：

- "location" 是包含商店地理位置信息的字段。
- "lat" 和 "lon" 分别指定了给定地理坐标的纬度和经度。
- "order" 设置为 "asc" 表示按照距离给定地理坐标的远近进行升序排序。
- "unit" 设置为 "km" 表示距离的单位是公里。
- "mode" 设置为 "min" 表示使用最近的点到给定坐标的距离进行排序。
- "distance_type" 设置为 "arc" 表示使用球面距离进行计算。


# 分页

>![[Pasted image 20240202160916.png]]


#### 三种分页方式对比

  
当涉及到Elasticsearch中的分页和滚动查询时，from+size、search_after和scroll是常用的方法。以下是它们的简单介绍以及各自的优缺点和使用场景：

1. **from+size**：
    - **优点**：简单直观，适用于小型数据集和较小的偏移量。
    - **缺点**：对于大型数据集，性能可能会受到影响，因为每次查询都需要跳过一定数量的文档。
    - **使用场景**：适用于小型数据集或者需要精确控制分页的情况。
2. **search_after**：
    - **优点**：适用于大型数据集，性能较好，不需要跳过大量文档。
    - **缺点**：需要提供上一页结果中最后一个文档的排序值作为游标，不太适合实时性要求高的场景。
    - **使用场景**：适用于大型数据集的分页查询，适合需要快速滚动浏览数据的情况。
3. **scroll**：
    - **优点**：适用于大型数据集，可以保持查询结果的快照，适合需要长时间保持游标的情况。
    - **缺点**：不适合实时性要求高的场景，需要额外的资源来维护滚动上下文。
    - **使用场景**：适用于需要长时间保持游标或者需要对大量数据进行批量处理的情况。

# 高亮

>![[Pasted image 20240202203212.png]]

# RestClient查询文档
## API

```java
void testMatchAll() throws IOException {  
    //创建请求  
    SearchRequest request = new SearchRequest("hotel");  
    //设置请求参数  
    request.source().query(QueryBuilders.matchAllQuery());  
    //获取响应结果  
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);  
    //解析响应  
    SearchHits searchHits = response.getHits();  
    //总记录数  
    long value = searchHits.getTotalHits().value;  
    SearchHit[] hits = searchHits.getHits();  
    //结果集  
    for (SearchHit hit : hits) {  
        String json = hit.getSourceAsString();  
        System.out.println(json);  
    }  
}
```


## 解析文档

>![[Pasted image 20240202204301.png]]


## Match&MultiMatch

```java
QueryBuilders.matchQuery("all","如家")
QueryBuilders.multiMatchQuery("如家","name","brand")
```

与普通查询仅在查询条件中改变

## Term&Range
```java
QueryBuilders.termQuery("city","赣州")
QueryBuilders.rangeQuery("price").gte(100).lte(250)
```


## boolQuery

>![[Pasted image 20240202220328.png]]

## 分页
>![[Pasted image 20240202220758.png]]




## 高亮

>![[Pasted image 20240202223659.png]]

![[Pasted image 20240504172647.png]]

当搜索字段与高亮匹配的字段不一致时,如上,es将默认不显示高亮字段

此部分的`requireFieldMatch`配置,则可以拒绝该策略


>![[Pasted image 20240202224215.png]]









