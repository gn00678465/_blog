---
title: "[Nuxt 學習紀錄] 錯誤頁面"
date: 2021-02-24T13:33:21+08:00
categories: 'Nuxt 學習紀錄'
tags: ['Nuxt']
draft: false
---

## 錯誤頁面

當 Nuxt 碰到**不可預期的錯誤**

或者於頁面中使用 `validate` callback 驗證權限等出現錯誤時

Nuxt 皆會顯示錯誤預設頁面

可以於 layout 資料夾內建立一個 `error.vue` 檔案來處理錯誤的頁面

```
layout
  ├ default.vue
  └ error.vue
```

error.vue 內可以設定 props 接收 error 的資料
```js
// error.vue
export default {
  props: ['error'],
  layout: 'error' // you can set a custom layout for the error page
}
```
可以於 `error.vue` 內設定專屬 error 的樣式。

## 404 頁面

在網址輸入不存在的路徑希望可以轉址到首頁等路徑。

在 pages 建立一個 `_.vue` 檔案。

這如同於 Vue-router 內設定 * 來匹配所有的路徑。

```
pages
  └ _.vue
```
並在 `_.vue` 內設定當進入不存在路徑後要轉址的路徑。
```js
// _.vue
export default {
  asyncData ({ redirect }) {
    return redirect('/')
  }
}
```
