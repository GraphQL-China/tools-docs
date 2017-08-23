---
title: 综述
order: 0
---

除了一整套功能齐全的 GraphQL 客户端之外，Apollo 社区还维护了一套用于构建 GraphQL 服务器的工具，以及一些让使用 GraphQL 变得更加方便的实用程序。

如果你正在寻找一种简单的方法来启动并运行一台 GraphQL.js 服务器，请从 [graphql-tools](/tools/graphql-tools/) 开始吧。

## Apollo Server & tools

这里是一些设计用于使构建 JavaScript GraphQL 服务器变得更加简单的库，基于 [GraphQL.js](https://github.com/graphql/graphql-js) 和 Facebook 的 GraphQL 类型系统和执行引擎的参考实现。

- [graphql-tools](/tools/graphql-tools)，使你能够使用 GraphQL schema language 构建生产可用的 GraphQL.js schema，而不是直接使用 GraphQL.js 类型构造函数。使用这个包构建的 schema 可以与任何 GraphQL 服务器兼容，包括我们自己的 `apollo-server` 和 Facebook 的 `express-graphql`。这允许你基于 [GraphQL.js 入门指南](http://graphql.cn/graphql-js/) 进行构建，并为解析器、联合、接口、自定义标量、schema 模块化等提供额外的支持。
- [apollo-server](/tools/apollo-server)，一个生产可用的 Node.js GraphQL 服务端库，支持 **Express**、**Connect**、**Hapi**、**Koa** 以及其它流行的 Node HTTP 服务器，包含持久化查询、批处理等内置功能。Apollo Server 可以与任何 GraphQL 客户端（如 Apollo、Relay、Lokka 等）协同工作。

[Launchpad](https://launchpad.graphql.com/new) 是一款能够在浏览器中使用的 GraphQL 服务端演示环境。它使用了上面提到的库，你可以把它当成一个服务端的 JSFiddle。想获取更多信息，请参阅 [公告](https://dev-blog.apollodata.com/introducing-launchpad-the-graphql-server-demo-platform-cc4e7481fcba) 和 [文档](https://github.com/apollographql/launchpad/blob/master/docs.md)。

## GraphQL 订阅

使人们能够为应用程序添加实时功能是 Apollo 社区感到兴奋的一件事，而 GraphQL 订阅是在这条路上的第一步。你可以使用以下的包为任何 Node.js GraphQL 服务器添加订阅支持。

- [graphql-subscriptions](https://github.com/apollostack/graphql-subscriptions)，一个与传输无关的 JavaScript 实用程序集合，包括 `PubSub`、通道映射和过滤器。
- [subscriptions-transport-ws](https://github.com/apollostack/subscriptions-transport-ws)，一个 GraphQL 的 WebSocket 服务端和客户端，可与 `AsyncIterable` 一起使用，且可以简单地直接在 JavaScript 应用程序中使用，或连接到功能齐全的 GraphQL 客户端，如 Apollo 或 Relay。

你可以在 [了解](/tools/graphql-subscriptions/) 阅读更多关于订阅服务器的内容。

## GraphQL 客户端工具

- [graphql-anywhere](https://github.com/apollostack/graphql-anywhere)，Apollo JavaScript Client 的 schema-less GraphQL 核心执行引擎，可让你构建自己强大的GraphQL 工具和缓存实现，并且能够在任何可以运行 JavaScript 代码的地方工作。
- [graphql-tag](https://github.com/apollostack/graphql-tag)，一个简单的用于解析和打印 GraphQL 查询的库，并能够将多个片段合并到一个查询中。它有助于增强 [apollo-client](https://github.com/apollostack/apollo-client)，且能够与 [eslint-plugin-graphql](https://github.com/apollostack/eslint-plugin-graphql) 完美结合。

## 开发者工具

- [eslint-plugin-graphql](https://github.com/apollostack/eslint-plugin-graphql)，一个 ESLint 插件，它将检查你的 GraphQL 查询字符串的语法错误和 schema 符合性，并能够与任何 JavaScript GraphQL 客户端（包括 Apollo、Relay、Lokka 等）一起使用。
