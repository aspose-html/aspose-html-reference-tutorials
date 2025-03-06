---
title: 在 .NET 中透過 Aspose.HTML 使用 HTML 模板
linktitle: 在 .NET 中使用 HTML 模板
second_title: Aspose.HTML .NET HTML 操作 API
description: 了解如何使用 Aspose.HTML for .NET 從 JSON 資料動態產生 HTML 文件。在 .NET 應用程式中利用 HTML 操作的強大功能。
weight: 17
url: /zh-hant/net/advanced-features/using-html-templates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中透過 Aspose.HTML 使用 HTML 模板


如果您希望在 .NET 應用程式中使用 HTML 文件和模板，那麼您來對地方了！ Aspose.HTML for .NET 是一個多功能函式庫，可讓開發人員輕鬆操作 HTML 文件和範本。在本教程中，我們將深入研究使用 Aspose.HTML for .NET 的基本知識，分解每個步驟並提供清晰的解釋。

## 先決條件

在我們深入了解 Aspose.HTML for .NET 的本質之前，請確保您具備以下先決條件：

1. Visual Studio：確保您的電腦上安裝了 Visual Studio。如果您還沒有，可以從網站下載。

2.  Aspose.HTML for .NET：您需要在 Visual Studio 專案中安裝 Aspose.HTML for .NET。您可以從[文件](https://reference.aspose.com/html/net/).

3. JSON 資料：準備要用於填入 HTML 範本的 JSON 資料來源。在本教程中，我們將使用以下 JSON 資料：

```json
{
    'FirstName': 'John',
    'LastName': 'Smith',
    'Address': {
        'City': 'Dallas',
        'Street': 'Austin rd.',
        'Number': '200'
    }
}
```

4. HTML 範本：建立要使用 JSON 資料填入的 HTML 範本。這是一個簡單的例子：

```html
<table border=1>
    <tr>
        <th>Person</th>
        <th>Address</th>
    </tr>
    <tr>
        <td>{{FirstName}} {{LastName}}</td>
        <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
    </tr>
</table>
```

## 導入命名空間

首先，讓我們在 .NET 專案中導入必要的命名空間：

```csharp
using Aspose.Html.Converters;
using Aspose.Html.Loading;
```

現在我們已經介紹了先決條件並導入了所需的命名空間，讓我們詳細分解每個步驟。

## 第1步：準備JSON資料來源

首先建立一個 JSON 資料來源，其中包含要插入到 HTML 範本中的資訊。在此範例中，我們已經準備好先決條件中提到的 JSON 資料來源。將其儲存到文件中，例如“data-source.json”。

```csharp
var data = @"{
    'FirstName': 'John',
    'LastName': 'Smith',
    'Address': {
        'City': 'Dallas',
        'Street': 'Austin rd.',
        'Number': '200'
    }
}";
System.IO.File.WriteAllText("data-source.json", data);
```

此程式碼片段讀取 JSON 資料並將其寫入名為「data-source.json」的檔案。

## 第 2 步：準備 HTML 模板

現在，讓我們建立一個要使用 JSON 資料填入的 HTML 範本。將此模板儲存到文件中，例如“template.html”。

```csharp
var template = @"
<table border=1>
    <tr>
        <th>Person</th>
        <th>Address</th>
    </tr>
    <tr>
        <td>{{FirstName}} {{LastName}}</td>
        <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
    </tr>
</table>
";
System.IO.File.WriteAllText("template.html", template);
```

此 HTML 範本包含以下佔位符`{{FirstName}}`, `{{LastName}}`, `{{Address.Street}}`, `{{Address.Number}}`， 和`{{Address.City}}`，我們將用實際數據替換它。

## 第 3 步：填入 HTML 模板

最後，調用`Converter.ConvertTemplate`方法使用 JSON 來源中的資料填入 HTML 範本。

```csharp
Aspose.Html.Converters.Converter.ConvertTemplate(
"template.html", new Aspose.Html.Converters.TemplateData("data-source.json"), new Aspose.Html.Loading.TemplateLoadOptions(), "document.html"
);
```

此程式碼採用「template.html」文件，以對應的 JSON 值取代佔位符，並將結果儲存於「document.html」中。

恭喜！您已成功利用 Aspose.HTML for .NET 的強大功能從 JSON 資料動態產生 HTML 文件。

## 結論

在本教程中，我們探討了使用 Aspose.HTML for .NET 動態建立 HTML 文件的基礎知識。我們介紹了先決條件、導入命名空間，並詳細分解了每個步驟。透過執行這些步驟，您可以將 HTML 文件產生無縫整合到您的 .NET 應用程式中。

## 常見問題解答

### Q1.什麼是 .NET 的 Aspose.HTML？

A1：Aspose.HTML for .NET 是一個功能強大的函式庫，使 .NET 開發人員能夠以程式設計方式使用 HTML 文件和範本。它簡化了 HTML 生成、轉換和操作等任務。

### Q2。在哪裡可以找到 Aspose.HTML for .NET 的文檔？

 A2：您可以存取 Aspose.HTML for .NET 的文檔[這裡](https://reference.aspose.com/html/net/)。它提供了全面的信息，包括 API 參考和程式碼範例。

### Q3。如何下載 .NET 版 Aspose.HTML？

A3：您可以從下載頁面下載Aspose.HTML for .NET[這裡](https://releases.aspose.com/html/net/).

### Q4。 Aspose.HTML for .NET 是否有免費試用版？

 A4：是的，您可以透過下載免費試用版來嘗試 Aspose.HTML for .NET[這裡](https://releases.aspose.com/).

### Q5.我需要 Aspose.HTML for .NET 的臨時授權嗎？

 A5：如果您需要臨時許可證用於評估目的，您可以從以下位置取得一份：[這裡](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
