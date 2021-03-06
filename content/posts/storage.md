---
title: "儲存空間單位"
date: 2021-01-29T19:40:41+08:00
draft: false
categories: "基礎計算機概論"
enableMathJax: true
---

## 基本名詞

- **Bit** / 位元
    >儲存的最小單位，只能儲存 0 、 1 。
- **Byte** / 位元組
    >一個位元組代表八個位元。
- **KB** / Kilobyte
    >Kilo + byte 。 1KB = 1024 bytes
- **MB** / Megabyte
    >Mega + byte 。 1MB = 1024 KB
- **GB** / Gigabyte
    >Giga + byte 。 1GB = 1024 MB

## 數字的儲存方式

### 正整數
通常數字使用 32 個 bit 來儲存，也就是 4 bytes。

範圍：$2^{32} = 4,294,967,296 $

```
假設數字使用 8 bit 儲存。
0000 1010 = 10
```

### 負數
負數的儲存定義為：**將正數的所有位元顛倒後 + 1**
```
假設數字使用 8 bit 儲存。
1111 0110 = -10
```
1. 第一個 bit 代表正負。 0：正數 、 1：負數。
1. 運算方便

```
假設數字使用 8 bit 儲存。
   0000 1010
 + 1111 0110
 -------------
 1 0000 0000
將超過 8 bit 的部分捨去，結果為 0 。
```

### 正負數範圍
範圍：$-2^{31}$ ~ $2^{31} - 1$

### overflow / 溢位
當目前儲存的數字超過可以表示的範圍，會出現一些奇怪的情況。

```
假設數字使用 8 bit 儲存。
目前數字可以表示的範圍為： -2^7 ~ 2^7 - 1
```

## 浮點數的儲存方式
![Float Binary Data](/images/floatBinary.png)

前提：因電腦空間限制，無法以有限的空間來表示無限的數字，無法非常精準。

而小數使用 64 個 bit 來儲存並將之分為 3 個部分。
- sign / 符號： 正負值。
- exponent / 指數： $10^{-n}$。
- fraction / 數字： 儲存數字的部分。