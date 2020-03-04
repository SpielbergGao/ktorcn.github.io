---
title: 流媒体
caption: 处理数据流
category: clients
permalink: /clients/http-client/quick-start/streaming.html
redirect_from:
- /clients/http-client/calls/streaming.html
ktor_version_review: 1.3.0
---


大多数响应类型都在内存中完成。 但是你也可以获取数据流。

## 作用域流

There are multiple ways of doing streaming. The safest way is using [HttpStatement](https://api.ktor.io/{{ site.ktor_version }}/io.ktor.client.statement/-http-statement/) with scoped `execute` block:
有多种执行流式传输的方法。 最安全的方法是将 [HttpStatement](https://api.ktor.io/{{ site.ktor_version }}/io.ktor.client.statement/-http-statement/) 与范围为 `execute` 的块一起使用：

```kotlin
client.get<HttpStatement>.execute { response: HttpResponse ->
    // Response is not downloaded here.
    val channel = response.receive<ByteReadChannel>()
}
```

After `execute` block is finished, network resources is released.
执行完 `execute` 块后，释放网络资源。

You can also point different type for `execute` method:
您还可以为 `execute` 方法指定不同的类型：

```kotlin
client.get<HttpStatement>.execute<ByteReadChannel> { channel: ByteReadChannel ->
    // ...
}
```
