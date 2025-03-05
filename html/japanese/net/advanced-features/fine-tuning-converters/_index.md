---
title: Aspose.HTML を使用した .NET のコンバーターの微調整
linktitle: .NET でのコンバーターの微調整
second_title: Aspose.HTML .NET HTML 操作 API
description: Aspose.HTML for .NET を使用して HTML を PDF、XPS、画像に変換する方法を学びます。コード例と FAQ を含むステップバイステップのチュートリアルです。
type: docs
weight: 16
url: /ja/net/advanced-features/fine-tuning-converters/
---

## 導入

Aspose.HTML for .NET は、開発者がさまざまな形式の HTML ドキュメントを操作および変換できるようにする強力なライブラリです。HTML を PDF、XPS、または画像に変換する必要がある場合でも、その他の HTML 関連のタスクを実行する必要がある場合でも、Aspose.HTML は作業を完了するのに役立つ強力なツール セットを提供します。

このチュートリアルでは、Aspose.HTML for .NET の重要な機能をいくつか紹介し、各例についてステップごとに説明します。このチュートリアルを完了すると、.NET アプリケーションで Aspose.HTML for .NET を使用する方法をしっかりと理解できるようになります。

## 前提条件

例に進む前に、次の前提条件が満たされていることを確認してください。

-  Aspose.HTML for .NET: Aspose.HTML for .NETライブラリがインストールされている必要があります。[ダウンロードリンク](https://releases.aspose.com/html/net/).

- 一時ライセンス（オプション）：有効なライセンスをお持ちでない場合は、一時ライセンスを取得できます。[ここ](https://purchase.aspose.com/temporary-license/).

ここで、Aspose.HTML for .NET の一般的な使用例をいくつか見てみましょう。

## 名前空間のインポート

C# コードでは、まず必要な名前空間をインポートします。

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Xps;
using Aspose.Html.Rendering.Pdf.Encryption;
using Aspose.Html.Drawing;
```

## HTMLをPDFに変換する

### ステップ1: HTMLコードを準備する

```csharp
var code = @"<span>Hello World!!</span>";
```

### ステップ2: HTMLドキュメントを初期化する

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ステップ3: PDFデバイスを作成し、出力ファイルを指定する

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### ステップ4: HTMLをPDFにレンダリングする

```csharp
document.RenderTo(device);
```

この例では、HTML スニペットを PDF ドキュメントに変換します。必要に応じて、HTML コードと出力ファイルをカスタマイズできます。

## カスタムページサイズを設定する

### ステップ1: HTMLコードを準備する

```csharp
var code = @"<span>Hello World!!</span>";
```

### ステップ2: HTMLドキュメントを初期化する

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ステップ3: PDFレンダリングオプションを作成する

```csharp
var options = new PdfRenderingOptions()
{
    PageSetup =
    {
        AnyPage = new Page(
            new Size(
                Length.FromInches(5),
                Length.FromInches(2)))
    }
};
```

### ステップ4: PDFデバイスを作成し、オプションと出力ファイルを指定する

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### ステップ5: HTMLをPDFにレンダリングする

```csharp
document.RenderTo(device);
```

この例では、生成される PDF ドキュメントのカスタム ページ サイズを設定する方法を示します。

## 解像度を調整する

### ステップ1: HTMLコードを準備してファイルに保存する

```csharp
var code = @"
    <style>
    p
    { 
        background: blue; 
    }
    @media(min-resolution: 300dpi)
    {
        p 
        { 
            /* high-resolution screen color */
            background: green
        }
    }
    </style>
    <p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### ステップ2: HTMLドキュメントを初期化する

```csharp
using (var document = new HTMLDocument("document.html"))
```

### ステップ3: 低解像度用のPDFレンダリングオプションを作成する

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### ステップ4: PDFデバイスを作成し、低解像度のオプションと出力ファイルを指定する

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### ステップ5: 低解像度用にHTMLをPDFにレンダリングする

```csharp
document.RenderTo(device);
```

### ステップ6: 高解像度のPDFレンダリングオプションを作成する

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### ステップ7: PDFデバイスを作成し、高解像度のオプションと出力ファイルを指定する

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### ステップ8: 高解像度のHTMLをPDFにレンダリングする

```csharp
document.RenderTo(device);
```

この例では、低解像度と高解像度の両方の画面を考慮して、HTML を PDF にレンダリングするときに解像度を調整する方法を示します。

## 背景色を指定する

### ステップ1: HTMLコードを準備してファイルに保存する

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### ステップ2: HTMLドキュメントを初期化する

```csharp
using (var document = new HTMLDocument("document.html"))
```

### ステップ3: 背景色でPDFレンダリングオプションを初期化する

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### ステップ4: PDFデバイスを作成し、オプションと出力ファイルを指定する

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### ステップ5: HTMLをPDFにレンダリングする

```csharp
document.RenderTo(device);
```

この例では、HTML を PDF に変換するときに背景色を指定する方法を示します。

## 左ページと右ページのサイズを設定する

### ステップ1: HTMLコードを準備する

```csharp
var code = @"<style>div { page-break-after: always; }</style>
    <div>First Page</div>
    <div>Second Page</div>
    <div>Third Page</div>
    <div>Fourth Page</div>";
```

### ステップ2: HTMLドキュメントを初期化する

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ステップ3: 左ページサイズと右ページサイズでPDFレンダリングオプションを作成する

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### ステップ4: PDFデバイスを作成し、オプションと出力ファイルを指定する

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### ステップ5: HTMLをPDFにレンダリングする

```csharp
document.RenderTo(device);
```

この例では、HTML を PDF に変換するときに、左ページと右ページに異なるページ サイズを設定する方法を示します。

## コンテンツに合わせてページサイズを調整する

### ステップ1: HTMLコードを準備する

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### ステップ2: HTMLドキュメントを初期化する

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ステップ3: PDFレンダリングオプションを作成する

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### ステップ4: PDFデバイスを作成し、オプションと出力ファイルを指定する

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### ステップ5: HTMLをPDFにレンダリングする

```csharp
document.RenderTo(device);
```

この例では、HTML を PDF に変換するときに、最も幅の広いコンテンツに合わせてページ サイズを調整する方法を示します。

## PDF権限を指定する

### ステップ1: HTMLコードを準備する

```csharp
var code = @"<div>Hello World!!</div>";
```

### ステップ2: HTMLドキュメントを初期化する

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ステップ3: 権限付きのPDFレンダリングオプションを作成する

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### ステップ4: PDFデバイスを作成し、オプションと出力ファイルを指定する

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### ステップ5: HTMLをPDFにレンダリングする

```csharp
document.RenderTo(device);
```

この例では、HTML を保護された PDF に変換するときに権限と暗号化を指定する方法を示します。

## 画像固有のオプションを指定する

### ステップ1: HTMLコードを準備する

```csharp
var code = @"<div>Hello World!!</div>";
```

### ステップ2: HTMLドキュメントを初期化する

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ステップ3: 画像レンダリングオプションを作成する

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### ステップ4: イメージデバイスを作成し、オプションと出力ファイルを指定する

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### ステップ5: HTMLを画像にレンダリングする

```csharp
document.RenderTo(device);
```

この例では、形式、解像度、スムージング モードなどの特定のレンダリング オプションを使用して HTML を画像に変換する方法を示します。

## XPS レンダリング オプションを指定する

### ステップ1: HTMLコードを準備する

```csharp
var code = @"<span>Hello World!!</span>";
```

### ステップ2: HTMLドキュメントを初期化する

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ステップ3: ページサイズでXPSレンダリングオプションを作成する

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### ステップ4: XPSデバイスを作成し、オプションと出力ファイルを指定する

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### ステップ5: HTMLをXPSにレンダリングする

```csharp
document.RenderTo(device);
```

この例では、カスタム ページ サイズとレンダリング オプションを使用して HTML を XPS に変換する方法を示します。

## 複数の HTML ドキュメントを PDF に結合する

### ステップ1: 複数のドキュメントのHTMLコードを準備する

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### ステップ2: マージするHTMLドキュメントを作成する

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### ステップ3: HTMLレンダラーを初期化する

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### ステップ4: マージ出力用のPDFデバイスを作成する

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### ステップ5: HTML文書をPDFに結合する

```csharp
renderer.Render(device, document1, document2, document3);
```

この例では、Aspose.HTML for .NET を使用して複数の HTML ドキュメントを 1 つの PDF ファイルに結合する方法を示します。

## レンダリングタイムアウトを設定する

### ステップ1: JavaScriptを使用してHTMLコードを準備する

```csharp
var code = @"
    <script>
        var count = 0;
        setInterval(function()
        {
            var element = document.createElement('div');
            var message = (++count) + '. ' + 'Hello World!!';
            var text = document.createTextNode(message);
            element.appendChild(text);
            document.body.appendChild(element);
        }, 1000);
    </script>";
```

### ステップ2: HTMLドキュメントを初期化する

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ステップ3: HTMLレンダラーを初期化する

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### ステップ4: PDFデバイスを作成し、レンダリングタイムアウトを設定する

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### ステップ5: タイムアウト付きでHTMLをPDFにレンダリングする

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

この例では、HTML を PDF に変換するときにレンダリング タイムアウトを設定する方法を示します。これは、動的なコンテンツや長時間実行されるスクリプトを処理する場合に役立ちます。

## 結論

Aspose.HTML for .NET は、開発者が HTML ドキュメントを効率的に操作できるようにする多目的ライブラリです。このチュートリアルでは、基本的な HTML から PDF への変換から、カスタム ページ サイズ、解像度、権限などのより高度な機能まで、さまざまな例を取り上げました。これらの例に従うことで、.NET アプリケーションで Aspose.HTML for .NET の潜在能力を最大限に活用できます。

ご質問やさらなるサポートが必要な場合は、お気軽に[Aspose.HTML フォーラム](https://forum.aspose.com/)サポートとガイダンスのため。

## よくある質問

### Q1. Aspose.HTML for .NET とは何ですか?
   
A1: Aspose.HTML for .NET は、開発者が HTML ドキュメントをプログラムで操作および変換できるようにする .NET ライブラリです。HTML から PDF、XPS、画像への変換、高度なレンダリング オプションなど、HTML コンテンツを操作するための幅広い機能を提供します。

### Q2. Aspose.HTML for .NET はどこからダウンロードできますか?

 A2: Aspose.HTML for .NETは以下からダウンロードできます。[ダウンロードリンク](https://releases.aspose.com/html/net/).

### Q3. Aspose.HTML for .NET を使用するにはライセンスが必要ですか?

A3: Aspose.HTML for .NET はライセンスがなくても使用できますが、すべての機能のロックを解除し、透かしや制限を削除するには、実稼働環境で使用するライセンスを取得することをお勧めします。

### Q4. Aspose.HTML for .NET で生成された PDF ファイルをどのように保護できますか?

A4: Aspose.HTML for .NET を使用して HTML を PDF にレンダリングするときに、PDF のアクセス許可と暗号化設定を指定できます。これにより、結果の PDF ファイルに誰がアクセスして変更できるかを制御できます。

### Q5. HTML を XPS や画像などの他の形式に変換できますか?

A5: はい、Aspose.HTML for .NET は、HTML を PDF、XPS、画像 (JPEG など) を含むさまざまな形式に変換することをサポートしています。特定の要件に合わせて変換設定をカスタマイズできます。