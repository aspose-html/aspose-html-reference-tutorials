---
category: general
date: 2026-03-26
description: 即時示範中展示頂層 await 範例，包含 await 延遲 JavaScript、遞增計數器類別與公共類別欄位 JavaScript。
draft: false
keywords:
- top level await example
- await delay javascript
- increment counter class
- public class fields javascript
- javascript class public field
language: zh-hant
og_description: 頂層 await 範例，示範 await 延遲 JavaScript、遞增計數器類別及公共類別欄位 JavaScript 的簡潔教學。
og_title: 頂層 await 範例 – 在 JavaScript 中使用 await 延遲
tags:
- JavaScript
- ES2022
- async‑await
- classes
title: 頂層 await 範例 – 在 JavaScript 中使用 await 延遲
url: /zh-hant/java/advanced-usage/top-level-await-example-using-await-delay-in-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# top level await 範例 – 在 JavaScript 中使用 await delay

有沒有想過在不把所有程式碼包在 async IIFE 裡的情況下，暫停模組執行？這正是 **top level await 範例** 能做到的事。在本教學中，我們會一步步示範一個小型網頁，使用 `await delay javascript` 來延遲工作，接著建立一個利用 **public class fields javascript** 的 **increment counter class**。完成後，你將得到一段可直接複製貼上的程式碼，能在任何現代瀏覽器中執行。

我們會從定義帶有 public 欄位的 class 開始，接著串接一個簡易的基於 Promise 的 delay 輔助函式。全程不需要外部函式庫、建置步驟——只要純 HTML、`<script type="module">`，以及最新的 ECMAScript 功能。若你已熟悉 async 函式，會發現 top‑level await 是自然的延伸；若你剛接觸 **javascript class public field** 語法，也別擔心，我們會說明每一行背後的原因。

## 你將學到

- **top level await 範例** 在模組腳本中的運作方式  
- `await delay javascript` 輔助函式的寫法（模擬 `setTimeout` 並回傳 Promise）  
- 如何撰寫使用 public 欄位 (`count`) 與 static 初始化區塊的 **increment counter class**  
- 預期的 console 輸出，以及如何驗證 static 區塊會在其他程式碼之前執行  
- 常見問題的排除技巧，例如不支援 top‑level await 的舊版瀏覽器  

> **Pro tip:** 現代瀏覽器（Chrome 106+、Firefox 102+、Edge 106+）已支援 top‑level await。若需相容較舊環境，可考慮使用 Vite 或 Babel 等工具進行打包。

## Step 1 – 定義帶有 Public 欄位與 Static 區塊的 Class

示範的第一段是儲存數值計數器的 class。注意 `count = 0;` 這一行——這是 ES2022 引入的 **public class fields javascript** 語法，讓我們在不寫 constructor 的情況下直接建立實例屬性。

```html
<!DOCTYPE html>
<html>
<head>
    <title>ECMAScript 2022 Demo</title>
</head>
<body>
<img src="placeholder.png" alt="top level await example screenshot" title="top level await example">

<script type="module">
    // Step 1: Class definition
    class Counter {
        // Public field holds the current count
        count = 0;

        // Static block runs once when the class is first evaluated
        static {
            console.log('Counter class initialized');
        }

        // Simple method that increments the public field
        increment() {
            this.count++;
        }
    }
```

**為什麼要使用 static 區塊？** 它讓我們能在模組被解析的瞬間（*在* 任何 top‑level await 執行之前）執行一次性的初始化邏輯（例如寫入日誌）。這樣可以保證訊息最先出現在 console，證明 class 已提前評估。

## Step 2 – 建立 `await delay javascript` 輔助函式

接下來需要一個小型的基於 Promise 的 delay 函式。它本質上是 `setTimeout` 的包裝，但回傳 Promise 後即可使用 `await`。

```javascript
    // Step 2: Promise‑based delay helper
    const delay = ms => new Promise(resolve => setTimeout(resolve, ms));
```

**邊緣情況：** 若 `ms` 為負數或不是數字，`setTimeout` 會視為 `0`。雖然可以加入驗證，但為了示範簡潔，我們就保留單行寫法。

## Step 3 – 使用 Top‑Level Await 暫停執行

現在輪到主角登場：top‑level await。因為我們的腳本是模組（`type="module"`），可以直接在最外層使用 `await`。這會讓模組在 Promise 解決前暫停，從而控制副作用的執行順序。

```javascript
    // Step 3: Top‑level await – delay half a second
    await delay(500);   // Wait 500 ms so the static block logs first
```

**常見問題：** 「可以在普通的 `<script>` 標籤裡使用 top‑level await 嗎？」不行——只有模組腳本支援。若忘記加 `type="module"`，會拋出語法錯誤。

## Step 4 – 實例化 Class、遞增並輸出結果

最後把所有部件組合起來：建立實例、呼叫 `increment()`，然後印出最終計數。這樣即可看到 **increment counter class** 的實際運作。

```javascript
    // Step 4: Work with the Counter instance
    const counterInstance = new Counter();
    counterInstance.increment();               // count becomes 1
    console.log('Final count:', counterInstance.count);
</script>
</body>
</html>
```

### 預期的 Console 輸出

```
Counter class initialized
Final count: 1
```

在 DevTools 開啟此頁面時，應先看到 static‑block 訊息 **先於** 延遲結束的輸出，證明 class 先被評估。

## Step 5 – 為什麼使用 Public Class Fields 而不是 Constructor？

你可能會想，為什麼不直接寫成：

```javascript
class Counter {
    constructor() {
        this.count = 0;
    }
}
```

兩種寫法都可行，但 **public class fields javascript** 提供了更簡潔、宣告式的語法。欄位只會定義一次，而不是在每次 constructor 呼叫時重複寫入，當 class 變得較大時更易閱讀。此外，static 區塊無法放在 constructor 內，因此將初始化邏輯分離會更自然。

## Step 6 – 將範例套用到實務應用

在正式環境中，往往不只需要一個計數器。以下提供幾個快速擴充的想法：

- **多個計數器：** 使用 `Map` 以 identifier 為鍵儲存多個實例。  
- **持久化狀態：** 把 `console.log` 換成寫入 `localStorage`。  
- **非同步初始化：** 在 static 區塊中先向伺服器取得設定，確保所有實例建立前已完成。

這些模式同樣受惠於 top‑level await，因為你可以在模組載入時一次取得資料，保證所有消費者都能即時使用。

## 常見問答

**Q: top‑level await 會阻塞其他模組嗎？**  
A: 不會。每個模組獨立執行。只有包含 await 的模組會暫停，其他模組仍會平行載入。

**Q: 若 delay 的 Promise 被 reject 會怎樣？**  
A: 未處理的 reject 會中止模組評估，並在 console 顯示錯誤。若需要優雅的回退，請將 await 包在 `try…catch` 中。

**Q: `static` 關鍵字是必須的嗎？**  
A: 對計數器本身不是必須，但 static 區塊是一個方便的方式，示範程式碼在載入時只執行一次——非常適合寫日誌或做功能偵測。

## 結論

你剛完成一個 **top level await 範例**，展示了 `await delay javascript`、**increment counter class**，以及 **public class fields javascript** 的威力。完整、可執行的程式碼已在上方提供，Console 輸出也證明 static 區塊會在延遲程式碼之前觸發。

接下來，你可以嘗試更複雜的 async 流程、把 delay 換成真實的 API 呼叫，或為 class 加入更多方法。記住，現代 JavaScript 讓模組本身就能作為第一級的 async 實體——不需要額外的包裝。

祝開發順利，歡迎在留言區分享你的變化。如果本教學對你有幫助，別忘了分享給仍在與 async 模式奮戰的同事！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}