---
title: "[Nuxt 學習紀錄] Router"
date: 2021-02-04T13:21:39+08:00
categories: 'Nuxt 學習紀錄'
tags: ['Nuxt']
draft: false
---

在 Nuxt.js 專案中，不需要透過 `VueRouter` 設定各個頁面的 URL 以及各種畫面結構安排。

而是會依據 `pages` 的目錄結構會自動對應出 `VueRouter` 的設定。

## Router
```
pages
  ├ login
  │   └ index.vue
  └ admin
      ├ index.vue
      └ profile.vue
```

|路由 (URL)|page component|路由名稱 (Route Name)|
|---|---|---|
|/login|pages/login/index.vue|login|
|/admin|pages/admin/index.vue|admin|
|/admin/profile|pages/admin/profile.vue|admin-profile|

`<NuxtLink to="/">Home page</NuxtLink>`
而跳轉路由使用上與 VueRouter 相同。
如果要

## Dynamic Router
在 Nuxt.js 中路由設定是以資料夾結構來設定，而要使用動態路由並傳遞參數時。

需要建立一個以**下底線** 開頭的資料夾 `_<變數名稱>` 或者 Vue 檔案 `_<變數名稱>.vue`。

- 單參數：
    ```
    pages 
      └ _id
          └ profile.vue
    ```

- 多組參數時：
    ```
    pages 
      └ _id
          ├ profile.vue
          └ _detial.vue
    ```

|路由 (URL)|page component|路由名稱 (Route Name)|
|---|---|---|
|/`id`/profile|pages/`_id`/profile.vue|`id`-profile|
|/`id`/`detial`|pages/`_id`/`_detial`.vue|`id`-`detial`|

此方式所傳遞的參數會儲存在

```js
$route: {
  params: {
    id: '',
    detial: ''
  },
  query:Object (empty)
}
```
調用時： `$route.params.<變數名稱>`

> 如果要傳遞 `query` 的參數，則需要在 URL 的末端加上 `?<query變數名稱>=<query值>`。

調用時： `$route.query.<變數名稱>`


## Nested Router
當在頁面中，需要更改當前頁面的某些內容時，可以使用 nested router。

1. 建立一個 `<nested>.vue` template ，並同時建立一個與 template 同名的資料夾，此資料夾的內部檔案就是 `/<nested>` 的子路由。
1. template 與資料夾需要同層。
1. template `<nested>.vue` 內要使用 `<nuxt-child />` 來指定子路由 template 要插入的位置。
1. 預設載入的為 `index.vue`，搭配路由切換顯示的路由。

```
pages 
  ├ nested
  │   ├ index.vue
  │   └ second.vue
  └ nested.vue
```
```
/nested                               /nested/second
+------------------+                  +-----------------+
| nested           |                  | nested          |
| +--------------+ |                  | +-------------+ |
| | index        | |  +------------>  | | second      | |
| |              | |                  | |             | |
| +--------------+ |                  | +-------------+ |
+------------------+                  +-----------------+
```

## Properties
```js
export default {
  // Vue option API
  // Nuxt page properties：
  head () {
      return {};
  },
  // 透過 `vue-meta` 設定此頁面 head 相關資訊。
  loading: true,
  // 設定載入的時候，是否要顯示載入進度條，可於 nuxt.config.js 的 loading 設定(全域設定)。
  layout: 'darkMode',
  // 要套用 layouts 底下的哪個樣版。
  transition: '',
  // 透過 <transition> 設定轉場和動畫效果。
  scrollToTop: false,
  // 希望讓畫面回到最頂端可以將此屬性設為 true。
  middleware: 'auto',
  // 要套用 middleware 底下檔案。
  // 套用多個可以使用陣列。
  validate (context) {
      return true;
  },
  // 用來檢查 URL 上的變數或是 vuex store 裡的資料。
  async asyncData(context) {
      return {};
  },
  // 串接 API 取得資料的地方，藉此達到 SSR 的效果，
  // 需回傳物件且會自動 mapping、覆蓋 data 物件。
  async fetch(context) {},
  // 與 asyncData 幾乎一樣，只差在沒有回傳物件。
  // 建議將要存入 vuex store 的資料在這裡取得。
}
```
### **context**

**context** 是 Nuxt.js 新增的 objects/params ，主要作用於 Nuxt.js 本身的 lifecycle 區域，如：asyncData, fetch, plugins, middleware and nuxtServerInit 等。 [#](https://nuxtjs.org/docs/2.x/internals-glossary/context)
- app： Vue 實例的根屬性包含所有 `nuxt.config.js` 中註冊的所有 plugin。
- store： Vuex Store 的實例。
- route： Vuex Router 的實例。
- params： URL 中的變數資料，同於 `this.$route.params`。
- query： URL 中的 query string，同於 `this.$route.query`。
- env： 設定於 `nuxt.config.js` 內的環境變數。 [#](https://nuxtjs.org/docs/2.x/configuration-glossary/configuration-env)
- isDev： 是否為開發模式。`[boolean]`
- isHMR： 
- redirect： 跳轉路由的方法。
- error：
- $config： [runtime config](https://nuxtjs.org/docs/2.x/configuration-glossary/configuration-runtime-config)