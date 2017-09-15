---
title: 添加一个 GraphQL 入口端点
order: 202
description: 如何为你的服务器添加一个 GraphQL 入口端点
---

根据你使用的服务器框架，Apollo Server 的 API 有略微的不同，但所有的包都共享相同的核心实现和选项格式。

<h2 id="graphqlOptions">Apollo Server 选项</h2>

Apollo Server 接受一个 `GraphQLOptions` 对象作为其唯一参数。`GraphQLOptions` 对象具有以下属性：

```js
// 选项对象
const GraphQLOptions = {
  schema: GraphQLSchema,

  // 用作解析器中的上下文和 rootValue 的值
  context?: any,
  rootValue?: any,

  // 用于在返回给客户端之前格式化错误的函数
  formatError?: Function,

  // 应用于客户端指定查询的其他验证规则
  validationRules?: Array<ValidationRule>,

  // 应用于批处理中的每个查询，在传递给 `runQuery` 之前格式化参数的函数
  formatParams?: Function,

  // 应用于将数据返回给客户端之前的每个响应的函数
  formatResponse?: Function,

  // 一个布尔选项，如果执行发生错误将触发额外的调试日志记录
  debug?: boolean
}
```

<h3 id="options-function">以函数形式传递选项</h3>

作为另一种选择，Apollo Server 可以接受一个函数作为参数，此函数将 request 作为输入参数，并返回一个 GraphQLOptions 对象或是可以 resolve 到一个 GraphQLOptions 对象的 promise：

```js
// 示例选项函数（以 express 为例）
graphqlExpress(request => ({
  schema: typeDefinitionArray,
  context: { user: request.session.user }
}))
```

如果你需要根据每个不同的请求将对象附加到上下文，例如初始化用户数据、缓存工具（如 `dataloader`）或是设置一些 API 密钥，这将非常有用。

<h2 id="importingESModules">导入 ES6 模块</h2>

目前，以下示例中使用的 ES6 模块导入语法未在 Nodejs 6.x、7.x 和更低版本中实现。要使用这些示例，你将需要配置一个外部工具（如 [Babel](https://babeljs.io/)），来将 import 语句转换为标准的 require 语句。例如，`import express from 'express';` 将被转换为 `var express = require('express');`。如果你不想使用外部转译器，你也可以参照示例格式手动将 import 转换为 require。

<h2 id="graphqlExpress">配合 Express 使用</h2>

以下代码片段显示了如何配合 Express 使用 Apollo Server：

```js
import express from 'express';
import bodyParser from 'body-parser';
import { graphqlExpress } from 'apollo-server-express';

const PORT = 3000;

var app = express();

app.use('/graphql', bodyParser.json(), graphqlExpress({ schema: myGraphQLSchema }));

app.listen(PORT);
```

<h2 id="graphqlConnect">配合 Connect 使用</h2>

由于 Connect 与 Express 非常类似，因此被集成在同一个包中。以下代码片段显示了如何配合 Connect 使用 Apollo Server：

```js
import connect from 'connect';
import bodyParser from 'body-parser';
import { graphqlConnect } from 'apollo-server-express';
import http from 'http';

const PORT = 3000;

var app = connect();

app.use('/graphql', bodyParser.json());
app.use('/graphql', graphqlConnect({ schema: myGraphQLSchema }));

http.createServer(app).listen(PORT);
```

传递给 `graphqlConnect` 的参数和传递给 `graphqlExpress` 的参数相同。

<h2 id="graphqlHapi">配合 Hapi 使用</h2>

以下代码片段显示了如何配合 Hapi 使用 Apollo Server：

```js
import hapi from 'hapi';
import { graphqlHapi } from 'apollo-server-hapi';

const server = new hapi.Server();

const HOST = 'localhost';
const PORT = 3000;

server.connection({
    host: HOST,
    port: PORT,
});

server.register({
  register: graphqlHapi,
  options: {
    path: '/graphql',
    graphqlOptions: { schema: myGraphQLSchema },
  },
});
```

`graphqlOptions` 也可以是一个回调函数或是一个 promise：

```js
server.register({
  register: graphqlHapi,
  options: {
    path: '/graphql',
    graphqlOptions: (request) => {
      return { schema: myGraphQLSchema };
    },
  },
});
```

<h2 id="graphqlKoa">配合 Koa 2 使用</h2>

以下代码片段显示了如何配合 Koa 使用 Apollo Server：

```js
import koa from 'koa';
import koaRouter from 'koa-router';
import koaBody from 'koa-bodyparser';
import { graphqlKoa } from 'apollo-server-koa';

const app = new koa();
const router = new koaRouter();
const PORT = 3000;

app.use(koaBody());

router.post('/graphql', graphqlKoa({ schema: myGraphQLSchema }));
app.use(router.routes());
app.use(router.allowedMethods());
app.listen(PORT);
```

`graphqlOptions` 也可以是一个返回 GraphQLOptions 的回调函数或是一个 resolve 到 GraphQLOptions 的 promise。此函数需要一个 koa 2 的 `ctx` 作为其输入参数。

```js
router.post('/graphql', graphqlKoa((ctx) => {
  return { 
    schema: myGraphQLSchema,
    context: { userId: ctx.cookies.get('userId') }
  };
}));
```
