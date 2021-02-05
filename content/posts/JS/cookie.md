---
title: "Cookie"
date: 2021-02-03T14:22:24+08:00
categories: 基礎計算機概論
tags: ['JavaScript', 'cookie']
enableMermaid: false
enableMathJax: false
draft: false
---

## Cookie 是什麼？
Cookie 是儲存在瀏覽器的一小段文字資料。只可儲存 4KB 的資料。

伺服器透過 `Set-Cookie` header 傳遞給瀏覽器，之後會將 cookie 儲存起來，並在發送 request 時夾帶 cookie 至 server。

## Cookie 的用途？
- Session 管理：帳號登入、購物車、遊戲分數，等儲存於 server 上的資訊。
- 個人化：使用者設定、佈景主題，以及其他設定。
- 追蹤：記錄並分析使用者行為，或者廣告應用上。

## 使用 JavaScript 讀取 / 寫入 Cookie
### 讀取
1. Vanilla JavaScript - 內建功能 `document.cookie`

    讀取出來的 `document.cookie` 為一個字串，此字串是將目前網域底下所有的 cookie 以分號串接以後的結果，其中每個 cookie 都是 `[cookie名稱]=[cookie值]` 的形式。

    如果要取得特定的 cookie 的值可以透過 `String.replace()` 加上 RegExp 的方式來取得。[#](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/cookie)
    ```js
    // 將 test 改為要取得的 cookie 名稱
    const getCookie = document.cookie.replace(/(?:(?:^|.*;\s*)test\s*\=\s*([^;]*).*$)|^.*$/, "$1");
    ```
2. Library - 使用套件可以方便快速的取得 cookie 的值。
    - [js-cookie](https://github.com/js-cookie/js-cookie)
    - [cookie](https://github.com/jshttp/cookie)

### 寫入
1. Vanilla JavaScript

    寫入 cookie 的方式是 `document.cookie = 'key=value;'`，只有我們指定的 key 會被更新。

## Cookie 參數
新增參數的方式是用分號區隔各個參數
- `Domain` ：用來指定哪些網域可以存取這個 cookie。

    預設值是當前網域，但是不包含其子網域。

- `Path` ：參數用來指定哪些路徑可以存取這個 cookie。

    預設值是當前的路徑。可以設成 `path=/`，讓全站都可以存取此 cookie。

- `Expires`, `Max-age` ：參數的作用是設定 cookie 的有效期限。

    如果沒有設定 `expires` 或 `max-age` 參數，當瀏覽器關閉之後，儲存在瀏覽器的 cookie 便會消失，這就是所謂的 session cookie。
    反之如果設定了`expires` 或 `max-age` 參數，當瀏覽器關閉之後， cookie 便會儲存於瀏覽器中。
    - `expires` ： 以 UTC 格式表示的有效期限。 `new Date().toUTCString()`
    - `max-age` ： 從設定開始算幾秒之內 cookie 是有效的。

- `Secure` ：參數的作用是讓 cookie 只能透過 https 傳遞。

    Cookie 預設是不區分 http 或是 https。

- `HttpOnly` ：參數的作用是防止 JavaScript 存取 cookie。

    防止受到 XSS Attack (Cross-Site Scripting，跨站腳本攻擊) 的風險。

- `SameSite` ：作用是防止 cookie 以跨站方式傳送，可以幫助避免 CSRF (Cross-Site Request Forgery，跨站請求偽造) 攻擊。