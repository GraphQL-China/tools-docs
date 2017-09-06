---
title: GraphiQL
order: 205
description: 如何在 Apollo Server 上设置GraphiQL
---

Apollo Server 能够让你轻松的使用 [GraphiQL](https://github.com/graphql/graphiql)，就像这样：

<h2 id="graphiqlOptions">配置 GraphiQL</h2>

`graphiql<Express/Connect/Hapi/Koa>` 接受以下选项对象：

```js
const options = {
  endpointURL: String, // 接收 GraphiQL 当前实例发送请求的 GraphQL POST 入口端点的 URL
  query?: String, // 可选项，预先填入 GraphiQL UI 的 query 区域的内容
  operationName?: String, // 可选项，预先填入 GraphiQL UI 的 operationName 区域的内容
  variables?: Object, // 可选项，预先填入 GraphiQL UI 的 variables 区域的内容
  result?: Object, // 可选项，预先填入 GraphiQL UI 的 result 区域的内容
  passHeader?: String, // 将被添加到输出请求头对象的字符串（如 "'Authorization': 'Bearer lorem ipsum'"）
}
```

Apollo Server 的 `graphiql` 中间件不会运行传递给它的任何查询，而是直接渲染到 UI。要实际执行查询，用户必须通过 GraphiQL UI 提交它，这将会把请求发送到 `endpointURL` 指定的 GraphQL 入口端点。

<h2 id="graphiqlExpress">配合 Express 使用</h2>

如果您正在使用 Express，GraphiQL 可以配置如下：

```js
import { graphiqlExpress } from 'apollo-server-express';

app.use('/graphiql', graphiqlExpress({
  endpointURL: '/graphql',
}));
```


<h2 id="graphiqlConnect">配合 Connect 使用</h2>

如果您正在使用 Connect，GraphiQL 可以配置如下：

```js
import { graphiqlConnect } from 'apollo-server-express';

app.use('/graphiql', graphiqlConnect({
  endpointURL: '/graphql',
}));
```


<h2 id="graphiqlHapi">配合 Hapi 使用</h2>

如果您正在使用 Hapi，GraphiQL 可以配置如下：

```js
import { graphiqlHapi } from 'apollo-server-hapi';

server.register({
  register: graphiqlHapi,
  options: {
    path: '/graphiql',
    graphiqlOptions: {
      endpointURL: '/graphql',
    },
  },
});
```


<h2 id="graphiqlKoa">配合 Koa 2 使用</h2>

如果您正在使用 Koa 2，GraphiQL 可以配置如下：

```js
import { graphiqlKoa } from 'apollo-server-koa';

router.get('/graphiql', graphiqlKoa({ endpointURL: '/graphql' }));
```
