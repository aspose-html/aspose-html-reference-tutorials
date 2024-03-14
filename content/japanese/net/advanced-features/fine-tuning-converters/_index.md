---
title: Aspose.HTML を使用した .NET のコンバータの微調整
linktitle: .NET でのコンバーターの微調整
second_title: Aspose.HTML .NET HTML 操作 API
description: Aspose.HTML for .NET を使用して HTML を PDF、XPS、および画像に変換する方法を学びます。コード例と FAQ を含むステップバイステップのチュートリアル。
type: docs
weight: 16
url: /ja/net/advanced-features/fine-tuning-converters/
---

## 導入

Aspose.HTML for .NET は、開発者が HTML ドキュメントをさまざまな形式で操作および変換できるようにする強力なライブラリです。 HTML を PDF、XPS、または画像に変換する必要がある場合でも、他の HTML 関連タスクを実行する必要がある場合でも、Aspose.HTML はその作業を支援する強力なツール セットを提供します。

このチュートリアルでは、Aspose.HTML for .NET のいくつかの重要な機能を検討し、各例について段階的に説明します。このチュートリアルを終えると、.NET アプリケーションで Aspose.HTML for .NET を使用する方法をしっかりと理解できるようになります。

## 前提条件

例に入る前に、次の前提条件が満たされていることを確認してください。

-  Aspose.HTML for .NET: Aspose.HTML for .NET ライブラリがインストールされている必要があります。からダウンロードできます。[ダウンロードリンク](https://releases.aspose.com/html/net/).

- 一時ライセンス (オプション): 有効なライセンスをお持ちでない場合は、次のサイトから一時ライセンスを取得できます。[ここ](https://purchase.aspose.com/temporary-license/).

ここで、Aspose.HTML for .NET の一般的な使用例をいくつか見てみましょう。

## 名前空間のインポート

C# コードで、必要な名前空間をインポートすることから始めます。

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Xps;
using Aspose.Html.Rendering.Pdf.Encryption;
using Aspose.Html.Drawing;
```

## HTML を PDF に変換する

### ステップ 1: HTML コードを準備する

```csharp
var code = @"<span>Hello World!!</span>";
```

### ステップ 2: HTML ドキュメントを初期化する

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ステップ 3: PDF デバイスを作成し、出力ファイルを指定する

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### ステップ 4: HTML を PDF にレンダリングする

```csharp
document.RenderTo(device);
```

この例では、HTML スニペットを PDF ドキュメントに変換します。必要に応じて、HTML コードと出力ファイルをカスタマイズできます。

## カスタムページサイズの設定

### ステップ 1: HTML コードを準備する

```csharp
var code = @"<span>Hello World!!</span>";
```

### ステップ 2: HTML ドキュメントを初期化する

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ステップ 3: PDF レンダリング オプションを作成する

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

### ステップ 4: PDF デバイスを作成し、オプションと出力ファイルを指定する

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### ステップ 5: HTML を PDF にレンダリングする

```csharp
document.RenderTo(device);
```

この例では、生成される PDF ドキュメントのカスタム ページ サイズを設定する方法を示します。

## 解像度の調整

### ステップ 1: HTML コードを準備してファイルに保存する

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

### ステップ 2: HTML ドキュメントを初期化する

```csharp
using (var document = new HTMLDocument("document.html"))
```

### ステップ 3: 低解像度用の PDF レンダリング オプションを作成する

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### ステップ 4: PDF デバイスを作成し、オプションと低解像度の出力ファイルを指定する

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### ステップ 5: 低解像度の HTML を PDF にレンダリングする

```csharp
document.RenderTo(device);
```

### ステップ 6: 高解像度用の PDF レンダリング オプションを作成する

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### ステップ 7: PDF デバイスを作成し、高解像度のオプションと出力ファイルを指定する

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### ステップ 8: 高解像度の HTML を PDF にレンダリングする

```csharp
document.RenderTo(device);
```

この例では、低解像度画面と高解像度画面の両方を考慮して、HTML を PDF にレンダリングするときに解像度を調整する方法を示します。

## 背景色の指定

### ステップ 1: HTML コードを準備してファイルに保存する

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### ステップ 2: HTML ドキュメントを初期化する

```csharp
using (var document = new HTMLDocument("document.html"))
```

### ステップ 3: 背景色を使用して PDF レンダリング オプションを初期化する

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### ステップ 4: PDF デバイスを作成し、オプションと出力ファイルを指定する

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### ステップ 5: HTML を PDF にレンダリングする

```csharp
document.RenderTo(device);
```

この例では、HTML を PDF に変換するときに背景色を指定する方法を示します。

## 左右のページサイズを設定する

### ステップ 1: HTML コードを準備する

```csharp
var code = @"<style>div { page-break-after: always; }</style>
    <div>First Page</div>
    <div>Second Page</div>
    <div>Third Page</div>
    <div>Fourth Page</div>";
```

### ステップ 2: HTML ドキュメントを初期化する

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ステップ 3: 左右のページ サイズを使用して PDF レンダリング オプションを作成する

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### ステップ 4: PDF デバイスを作成し、オプションと出力ファイルを指定する

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### ステップ 5: HTML を PDF にレンダリングする

```csharp
document.RenderTo(device);
```

この例では、HTML を PDF に変換するときに、左右のページで異なるページ サイズを設定する方法を示します。

## コンテンツに合わせてページサイズを調整する

### ステップ 1: HTML コードを準備する

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### ステップ 2: HTML ドキュメントを初期化する

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ステップ 3: PDF レンダリング オプションを作成する

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### ステップ 4: PDF デバイスを作成し、オプションと出力ファイルを指定する

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### ステップ 5: HTML を PDF にレンダリングする

```csharp
document.RenderTo(device);
```

この例では、HTML を PDF に変換するときに、最も幅の広いコンテンツに合わせてページ サイズを調整する方法を示します。

## PDF のアクセス許可を指定する

### ステップ 1: HTML コードを準備する

```csharp
var code = @"<div>Hello World!!</div>";
```

### ステップ 2: HTML ドキュメントを初期化する

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ステップ 3: 権限のある PDF レンダリング オプションを作成する

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### ステップ 4: PDF デバイスを作成し、オプションと出力ファイルを指定する

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### ステップ 5: HTML を PDF にレンダリングする

```csharp
document.RenderTo(device);
```

この例では、HTML を保護された PDF に変換するときにアクセス許可と暗号化を指定する方法を示します。

## イメージ固有のオプションを指定する

### ステップ 1: HTML コードを準備する

```csharp
var code = @"<div>Hello World!!</div>";
```

### ステップ 2: HTML ドキュメントを初期化する

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ステップ 3: 画像レンダリング オプションを作成する

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### ステップ 4: イメージ デバイスを作成し、オプションと出力ファイルを指定する

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### ステップ 5: HTML を画像にレンダリングする

```csharp
document.RenderTo(device);
```

この例では、形式、解像度、スムージング モードなどの特定のレンダリング オプションを使用して、HTML を画像に変換する方法を示します。

## XPS レンダリング オプションの指定

### ステップ 1: HTML コードを準備する

```csharp
var code = @"<span>Hello World!!</span>";
```

### ステップ 2: HTML ドキュメントを初期化する

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ステップ 3: ページ サイズを使用した XPS レンダリング オプションを作成する

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### ステップ 4: XPS デバイスを作成し、オプションと出力ファイルを指定する

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### ステップ 5: HTML を XPS にレンダリングする

```csharp
document.RenderTo(device);
```

この例では、カスタム ページ サイズとレンダリング オプションを使用して HTML を XPS に変換する方法を示します。

## 複数の HTML ドキュメントを PDF に結合する

### ステップ 1: 複数のドキュメント用の HTML コードを準備する

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### ステップ 2: 結合する HTML ドキュメントを作成する

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### ステップ 3: HTML レンダラーを初期化する

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### ステップ 4: 結合出力用の PDF デバイスを作成する

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### ステップ 5: HTML ドキュメントを PDF に結合する

```csharp
renderer.Render(device, document1, document2, document3);
```

この例では、Aspose.HTML for .NET を使用して複数の HTML ドキュメントを 1 つの PDF ファイルに結合する方法を示します。

## レンダリングタイムアウトの設定

### ステップ 1: JavaScript を使用して HTML コードを準備する

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

### ステップ 2: HTML ドキュメントを初期化する

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ステップ 3: HTML レンダラーを初期化する

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### ステップ 4: PDF デバイスを作成し、レンダリング タイムアウトを設定する

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### ステップ 5: タイムアウトを指定して HTML を PDF にレンダリングする

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

この例では、HTML を PDF に変換するときにレンダリング タイムアウトを設定する方法を示します。これは、動的コンテンツや長時間実行されるスクリプトを処理する場合に役立ちます。

## 結論

Aspose.HTML for .NET は、開発者が HTML ドキュメントを効率的に操作できるようにする多用途ライブラリです。このチュートリアルでは、基本的な HTML から PDF への変換から、カスタム ページ サイズ、解像度、権限などのより高度な機能まで、さまざまな例を取り上げました。これらの例に従うことで、.NET アプリケーションで Aspose.HTML for .NET の可能性を最大限に活用できます。

ご質問がある場合、またはさらにサポートが必要な場合は、お気軽に次のサイトにアクセスしてください。[Aspose.HTML フォーラム](https://forum.aspose.com/)サポートと指導のために。

## よくある質問

### Q1. Aspose.HTML for .NET とは何ですか?
   
A1: Aspose.HTML for .NET は、開発者がプログラムで HTML ドキュメントを操作および変換できるようにする .NET ライブラリです。 HTML から PDF、XPS、画像変換など、HTML コンテンツを操作するための幅広い機能と、高度なレンダリング オプションを提供します。

### Q2. .NET 用の Aspose.HTML はどこでダウンロードできますか?

 A2: Aspose.HTML for .NET は、[ダウンロードリンク](https://releases.aspose.com/html/net/).

### Q3. Aspose.HTML for .NET を使用するにはライセンスが必要ですか?

A3: Aspose.HTML for .NET はライセンスなしで使用できますが、すべての機能のロックを解除し、ウォーターマークや制限を削除するには、運用環境で使用するライセンスを取得することをお勧めします。

### Q4. Aspose.HTML for .NET で生成された PDF ファイルを保護するにはどうすればよいですか?

A4: Aspose.HTML for .NET を使用して HTML を PDF にレンダリングするときに、PDF のアクセス許可と暗号化設定を指定できます。これにより、作成された PDF ファイルにアクセスして変更できるユーザーを制御できます。

### Q5. HTML を XPS や画像などの他の形式に変換できますか?

A5: はい、Aspose.HTML for .NET は、PDF、XPS、画像 (JPEG など) を含むさまざまな形式への HTML の変換をサポートしています。特定の要件に合わせて変換設定をカスタマイズできます。