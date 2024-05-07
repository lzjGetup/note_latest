# 初识微服务

## 微服务技术栈

>![[Pasted image 20240124204703.png]]

>![[Pasted image 20240124211314.png]]


## 运程服务调用

springboot启动类注册restTemplate

```java
@Bean  
public RestTemplate restTemplate(){  
    return new RestTemplate();  
}
```

```java
在Spring框架中，RestTemplate类提供了许多用于发起HTTP请求的API。一些常用的API包括：

getForObject(String url, Class<T> responseType, Object... uriVariables)：发送一个GET请求，并将响应转换为指定类型的对象。

postForObject(String url, Object request, Class<T> responseType, Object... uriVariables)：发送一个POST请求，并将请求体转换为指定类型的对象。

exchange(String url, HttpMethod method, HttpEntity<?> requestEntity, Class<T> responseType, Object... uriVariables)：发送一个自定义HTTP方法的请求，并可以设置请求头和请求体。

delete(String url, Object... uriVariables)：发送一个DELETE请求。
```


# eureka

>![[Pasted image 20240124214038.png]]

>![[Pasted image 20240124214133.png]]


# Eureka配置

## 服务端

>![[Pasted image 20240124234127.png]]


## 客户端

>![[Pasted image 20240124234823.png]]

用于多次启动同一个服务

>![[Pasted image 20240124235256.png]]

负载均衡配置

>![[Pasted image 20240124235529.png]]

# Ribbon负载均衡

>![[Pasted image 20240125000851.png]]

>![[Pasted image 20240125001056.png]]

>![[Pasted image 20240125001154.png]]

`修改负载均衡的策略`

>![[Pasted image 20240125001547.png]]

>![[Pasted image 20240125001834.png]]


## 饥饿加载与懒加载

>![[Pasted image 20240125002514.png]]









