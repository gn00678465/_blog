---
title: "[Nuxt 學習紀錄] Initial"
date: 2021-02-03T19:03:49+08:00
categories: 'Nuxt 學習紀錄'
tags: ['Nuxt']
featured_image: "/images/Nuxt/index.png"
draft: false
---

## Nuxt.js [#](https://nuxtjs.org/)
Nuxt.js 是基於 Vue.js 的應用框架，支援不同的渲染方式(SSR、SPA 或靜態)。

## install / 安裝
```bash
npx create-nuxt-app <project-name>
# <project-name> 專案名稱
```

安裝時需要確認，且可依照專案需求進行設定
```bash
? Project name: # 專案名稱
? Programming language: # 開發語言：JS or TS
? Package manager: # package 管理器 Npm or Yarn
? UI framework: # UI 框架
? Nuxt.js modules: # 模組
? Linting tools:
? Testing framework: # 測試框架
? Rendering mode: # 渲染模式
  > Universal (SSR / SSG) # 伺服器渲染
    Single Page App # 單頁式應用
? Deployment target: # 部屬方式
  > Server (Node.js hosting)
    Static (Static/JAMStack hosting)
? Development tools: # 部屬工具
? Continuous integration:
? Version control system: # 版控工具
```
### 指令
1. 開發模式
    ```bash
    npm run start
    ```
1. 編譯成產品
    ```bash
    npm run build
    ```
1. 後端執行(SSR)
    ```bash
    npm run start
    ```
1. 發布靜態網頁
    ```bash
    npm run generate
    ```

## 資料夾配置
```bash
 ┬ assets
 │ # 存放會被 webpack 編譯的靜態檔案。如：Sass 等
 ┼ components
 │ # 主要存放可共用或可重複使用的 Vue.js components
 ┼ layouts
 │ # 主要存放網頁布局的地方， default 或者 custom 以及 error page
 ┼ pages
 │ # Nuxt 會依據內部的檔案以及資料夾產生 router
 ┼ static
 │ # 存放不會被編譯的靜態檔案。如：圖片 等
 ┼ plugins
 │ # 注入 vue instance 的套件。
 ┼ middleware
 │ # 自訂進入 layouts 或是 pages 開始渲染的方法，如：驗證登入狀態。
 ┼ store
 │ # 存放 Vuex Store的檔案。
 ┴ nuxt.config.js
   # Nuxt 主要的設定檔案。
```

## `nuxt.config.js` / 設定檔

```js
export default {
  // HTML Header 設定
  // See: https://go.nuxtjs.dev/config-head
  head: {
    title: 'NuxtTodo',
    htmlAttrs: {
      lang: 'en'
    },
    meta: [
      { charset: 'utf-8' },
      { name: 'viewport', content: 'width=device-width, initial-scale=1' },
      { hid: 'description', name: 'description', content: '' }
    ],
    link: [
      { rel: 'icon', type: 'image/x-icon', href: '/favicon.ico' }
    ]
  },
  // 全域載入 CSS 檔案
  // See: https://go.nuxtjs.dev/config-css
  css: [],
  // 對應 plugins 資料夾，載入第 3 方套件。
  // See: https://go.nuxtjs.dev/config-plugins
  plugins: [],
  // 不需要再手動 import components
  // See: https://go.nuxtjs.dev/config-components
  components: true,
  // Modules for dev and build (recommended)
  // See: https://go.nuxtjs.dev/config-modules
  buildModules: [],
  // 加入模組化套件
  // See: https://go.nuxtjs.dev/config-modules
  modules: [],
  // 編譯的設定
  // See: https://go.nuxtjs.dev/config-build
  build: {},
  router: {
    middleware: ['auth']
  },
}

```

### 其他設定
#### **mode**
Nuxt 除了編譯靜態頁面，另外提供兩種模式

- `universal`: 同構架構(Isomorphic)，有SSR+CSR(包含 client-side navigation)
- `spa`: 僅有 CSR (包含 client-side navigation)

#### **env**
此參數可以設定環境變數，當編譯後會自動取代。

```js
export default {
  env: {
    baseURL: process.env.BASE_URL
  }
}
```

#### **router**
此參數會覆蓋 Nuxt.js 預設產生的 router 設定。
```js
export default {
  router: {
    linkExactActiveClass: 'text-primary'
  }
}
```
**官方文檔**：[nuxt.config](https://nuxtjs.org/docs/2.x/directory-structure/nuxt-config)