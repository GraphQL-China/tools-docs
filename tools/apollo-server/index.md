---
title: 安装
order: 201
description: 如何安装 Apollo Server
---

Apollo Server 是一个用于 Node.js 的、灵活的、社区驱动的、生产级别的 HTTP 服务端插件。

它适用于任何使用 [GraphQL.js](https://github.com/graphql/graphql-js)（Facebook 的参考 JavaScript 执行库）构建的 GraphQL schema，你可以将 Apollo Server 与所有流行的 JavaScript HTTP 服务器（包括 Express、Connect、Hapi、Koa、Restify 和 Lambda）一起使用。

可以从任何流行的 GraphQL 客户端（如 [Apollo](http://dev.apollodata.com) 或 [Relay](https://facebook.github.io/relay)）查询此服务器，因为就像 [graphql.org 上的文档](http://graphql.cn/learn/serving-over-http/) 所描述的那样，它支持通过 HTTP 提供 GraphQL 服务所需的所有常用语义。Apollo Server 还支持协议的一些小扩展，例如在一个请求中发送多个 GraphQL 操作。你可以在 [发送请求](/tools/apollo-server/requests.html) 页面了解更多。

用以下代码安装它：

```bash
# 选择与你的服务器框架相匹配的那个
npm install graphql apollo-server-express  # 适用于 Express 或 Connect
npm install graphql apollo-server-hapi
npm install graphql apollo-server-koa
npm install graphql apollo-server-restify
npm install graphql apollo-server-lambda
npm install graphql apollo-server-micro
```

以下的特性将 Apollo Server 与 Facebook 的参考 HTTP 服务器实现 [express-graphql](https://github.com/graphql/express-graphql) 区分开来：

- Apollo Server 具有更简单的接口，并允许更少的发送查询的方式，这使得它更容易被理解发生了什么。
- Apollo Server 将 GraphiQL 提供在单独的路径上，可以使你更灵活地决定何时以及如何开启这一服务。
- Apollo Server 支持 [查询批处理](https://medium.com/apollo-stack/query-batching-in-apollo-63acfd859862)，可以有助于减少服务器的负载。
- Apollo Server 内置了对持久化查询的支持，可以使您的应用更快，并使服务器更安全。
