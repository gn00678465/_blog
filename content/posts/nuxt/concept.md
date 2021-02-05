---
title: "[Nuxt 學習紀錄] Concept"
date: 2021-02-04T13:12:53+08:00
categories: 'Nuxt 學習紀錄'
tags: ['Nuxt']
draft: false
---

## Views
Nuxt.js Application 是由，app template, layout, 以及 page 等 component 所組合而成。

在不同的 component 中有對應的屬性以及方法可以使用。

比如：可以在每個 page component 內的 head 中自訂 meta tag 來優化 SEO。
![](/images/Nuxt/views.png)

## Nuxt Lifecycle
官方文件：[Nuxt Lifecycle](https://nuxtjs.org/docs/2.x/concepts/nuxt-lifecycle)

- `nuxtServerInit`：用於在服務端操作 store 的，實質上就是一個 Action。

    只能被定義於 `store/index.js`。

    可以帶入 2 個參數。
    - 第一個：**Vuex context**。
    - 第二個：**Nuxt.js context**。
        ```js
        // store/index.js
        export const actions = {
          nuxtServerInit(Vuex, Nuxt) {
            // ...
          }
        }
        ```
- `Middleware`：頁面渲染之前執行的一個函式，這個函式可以使用在 nuxt.config.js、layouts 、 pages 中
    ```js
    // middleware/auth.js
    export default function({store, route, redirect}) {
      // ...
    }
    ```
    - `nuxt.config.js`： 當每個路由改變時被調用。
        ```js
        module.exports = {
          router: {
            middleware: 'auth'
          }
        }
        ```
    - `pages`： 當進入設定 middleware 的頁面時才會調用。
        ```js
        <script>
          export default {
            middleware: 'auth'
          }
        </script>
        ```
    - `layout`： 與 pages 應用上相同。
- `validate`：通常使用於驗證動態路由的參數
    ```js
    async validate({ params, query, store }) {
      // await operations
      return true // 如果參數有效
      return false // 將停止Nuxt.js呈現頁面並顯示錯誤頁面
    }
    ```

- `asyncData`：
    - 只可定義於 pages 內，並會在 pages 渲染前調用。
    - 可以將資料寫入 store 內。
    - 回傳物件會**取代**當前 component 的 data。
    - 帶入的第一個參數是當前 component 的 context。
    - [Sample](https://nuxtjs.org/examples/data-fetching-async-data)
    ```js
    async asyncData({store, route, params}) {
      return {
        // ...
      }
    }
    ```
- `fetch`：
    - 只可定義於 pages 內，並會在 pages 渲染前調用。
    - 與 `asyncData` 幾乎同時觸發。
    - 可以使用 `this`。
    - 可以獲取資料並寫入 data 或者 store 內。
    - 需 return Promise 物件，或者使用 `async/await`。
    - [Sample](https://nuxtjs.org/examples/data-fetching-fetch-hook)