---
title: 发送请求
order: 203
description: 如何向 Apollo Server 发送请求
---

Apollo Server 可同时接受 GET 和 POST 请求。

<h2 id="postRequests">POST 请求</h2>

Apollo Server 接受带有 JSON 请求体的 POST 请求。一个有效的请求必须包含一个 `query` 或一个 `operationName`（或两者，在命名查询的情况下），并且可能包含 `variables`。以下是一个包含有效请求体的 post 请求的示例：

```js
{
  "query": "query aTest($arg1: String!) { test(who: $arg1) }",
  "operationName": "aTest",
  "variables": { "arg1": "me" }
}
```

变量可以是一个对象或是一个 JSON 编码的字符串。也就是说，下面的查询和前一个查询是等价的：

```js
{
  "query": "query aTest($arg1: String!) { test(who: $arg1) }",
  "operationName": "aTest",
  "variables": "{ \"arg1\": \"me\" }"
}
```

<h3 id="batching">批处理</h3>

可以通过简单地发送一个 JSON 编码的查询数组来发送一批查询，例如：

```js
[
  { "query": "{ testString }" },
  { "query": "query q2{ test(who: \"you\" ) }" }
]
```

如果发送了一批查询，则将会返回一组 GraphQL 响应。

如果 Apollo Server 并非与您的客户端运行在同一个来源上，则需要在服务器上启用 CORS 支持，或者通过主来源上的 Web 服务器代理 GraphQL 请求。


<h2 id="getRequests">GET 请求</h2>

Apollo Server 也可以接受 GET 请求。GET 请求必须在 URL 中传递查询，以及可选的变量和 operationName。

以下发送到 Apollo Server 的格式良好的 GET 请求与上面的查询作用相同：
```
GET /graphql?query=query%20aTest(%24arg1%3A%20String!)%20%7B%20test(who%3A%20%24arg1)%20%7D&operationName=aTest&variables=me
```

注意事项：变更无法通过 GET 请求执行。
