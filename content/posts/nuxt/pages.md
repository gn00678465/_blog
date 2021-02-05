---
title: "[Nuxt 學習紀錄] Router"
date: 2021-02-04T13:21:39+08:00
categories: 'Nuxt 學習紀錄'
tags: ['Nuxt']
draft: true
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

```
pages
  └ users
      ├ _id.vue
      └ profile.vue
```

接收參數的方式為： `this.$route.params.變數名稱`

## Nested Router

## Properties
```js
export default {
  // Vue option API
  // Nuxt page properties：
  head () {
      return {};
  },
  loading: true,
  layout: 'ManagerLayout',
  transition: '',
  scrollToTop: false,
  middleware: 'ManagerAuth',
  validate (context) {
      return true;
  },
  async asyncData(context) {
      return {};
  },
  async fetch(context) {},
}
```

- `head`：透過 `vue-meta` 設定此頁面 head 相關資訊。
- `loading`：