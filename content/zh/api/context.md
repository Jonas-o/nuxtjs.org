---
title: 'API: 上下文对象'
description: 上下文是从Nuxt额外提供的对象（参数），而不是传统上可用的VUE组件，在"asyncData"、"plugins"、"middlewares"、"modules"和"store/nuxtServerInit"等特殊的 Nuxt 生命周期区域中可以使用"context"。
menu: context
category: essential
position: 1
---

## 上下文对象

context 变量的可用属性一览:

| 属性字段 | 类型 | 可用 | 描述 |
| --- | --- | --- | --- |
| `app` | Vue 根实例 | 客户端 & 服务端 | 包含所有插件的 Vue 根实例。例如：在使用 `axios` 的时候，你想获取 `$axios` 可以直接通过 `context.app.$axios` 来获取 |
| `isClient` | `Boolean` | 客户端 & 服务端 | 是否来自客户端渲染（废弃。请使用 `process.client` ） |
| `isServer` | `Boolean` | 客户端 & 服务端 | 是否来自服务端渲染（废弃。请使用 `process.server` ） |
| `isStatic` | `Boolean` | 客户端 & 服务端 | 是否来自 `nuxt generate` 静态化（预渲染）（废弃。请使用 `process.static` ） |
| `isDev` | `Boolean` | 客户端 & 服务端 | 是否是开发 dev 模式，在生产环境的数据缓存中用到 |
| `isHMR` | `Boolean` | 客户端 & 服务端 | 是否是通过模块热替换 `webpack hot module replacement` (_仅在客户端以 dev 模式_) |
| `route` | [Vue Router 路由](https://router.vuejs.org/zh/api/#%E8%B7%AF%E7%94%B1%E5%AF%B9%E8%B1%A1%E5%B1%9E%E6%80%A7) | 客户端 & 服务端 | Vue Router 路由实例 |
| `store` | [Vuex 数据](https://vuex.vuejs.org/zh/api/) | 客户端 & 服务端 | `Vuex.Store` 实例。**只有[vuex 数据流](/guide/vuex-store)存在相关配置时可用** |
| `env` | `Object` | 客户端 & 服务端 | `nuxt.config.js` 中配置的环境变量，见 [环境变量 api](/api/configuration-env) |
| `params` | `Object` | 客户端 & 服务端 | `route.params` 的别名 |
| `query` | `Object` | 客户端 & 服务端 | `route.query` 的别名 |
| `req` | [`http.Request`](https://nodejs.org/api/http.html#http_class_http_incomingmessage) | 服务端 | Node.js API 的 Request 对象。如果 Nuxt 以中间件形式使用的话，这个对象就根据你所使用的框架而定。_`nuxt generate` 不可用_ |
| `res` | [`http.Response`](https://nodejs.org/api/http.html#http_class_http_serverresponse) | 服务端 | Node.js API 的 Response 对象。如果 Nuxt 以中间件形式使用的话，这个对象就根据你所使用的框架而定。_`nuxt generate` 不可用_ |
| `redirect` | `Function` | 客户端 & 服务端 | 用这个方法重定向用户请求到另一个路由。状态码在服务端被使用，默认 302 `redirect([status,] path [, query])` |
| `error` | `Function` | 客户端 & 服务端 | 用这个方法展示错误页：`error(params)` 。`params` 参数应该包含 `statusCode` 和 `message` 字段 |
| `nuxtState` | `Object` | 客户端 | Nuxt 状态，在使用 `beforeNuxtRender` 之前，用于客户端获取 Nuxt 状态，仅在 `universal` 模式下可用 |
| `beforeNuxtRender(fn)` | `Function` | 服务端 | 使用此方法更新 `__NUXT__` 在客户端呈现的变量，`fn` 调用 (可以是异步) `{ Components, nuxtState }` ，参考 [示例](https://github.com/nuxt/nuxt.js/blob/cf6b0df45f678c5ac35535d49710c606ab34787d/test/fixtures/basic/pages/special-state.vue) |