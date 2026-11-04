---
category: general
date: 2026-03-29
description: C#でAspose.HTMLを使用してHTMLからPDFを作成します。フォントの埋め込み方法、HTMLをPDFに変換する方法、HTMLをPDFとして保存する方法を数ステップで学びましょう。
draft: false
keywords:
- create pdf from html
- how to embed font
- convert html to pdf
- save html as pdf
- how to create pdf
language: ja
og_description: Aspose.HTMLでHTMLからPDFを作成します。このガイドでは、フォントの埋め込み方法、HTMLをPDFに変換する方法、そしてHTMLを迅速にPDFとして保存する方法を示します。
og_title: C#でHTMLからPDFを作成 – フォントを埋め込んでPDFに変換
tags:
- Aspose.HTML
- C#
- PDF generation
title: C#でHTMLからPDFを作成 – フォントを埋め込んでPDFに変換
url: /ja/net/html-extensions-and-conversions/create-pdf-from-html-in-c-embed-fonts-convert-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で HTML から PDF を作成 – フォント埋め込みと PDF 変換

**HTML から PDF を作成**したいけど、カスタムフォントをきれいに保つ方法が分からない…という経験はありませんか？同じ悩みを抱える開発者は多いです。Aspose.HTML を使えば、ウェブフォントを埋め込み、HTML を PDF に変換し、さらに **HTML を PDF として保存** するのが数行の C# で可能です。

本チュートリアルでは、HTML ドキュメントの設定、**フォント埋め込み方法**、マークアップの PDF 変換、そして結果の保存までを順を追って解説します。最後には、任意の .NET プロジェクトにそのまま貼り付けられる完全なサンプルが手に入ります。

## 必要な環境

- .NET 6.0 以上（API は .NET Core や .NET Framework でも動作）  
- Aspose.HTML for .NET（無料トライアルの NuGet パッケージ `Aspose.HTML` を取得）  
- カスタムフォントファイル（例: `OpenSans.woff2`）を実行ファイルと同じフォルダーに配置  
- お好みの IDE（Visual Studio、Rider、VS Code など）

追加設定や外部サービスは不要です。NuGet 参照を数個追加すればすぐに始められます。

---

## 手順 1: PDF を作成 – HTMLDocument の初期化

まず最初に、PDF に変換したいページを表す `HTMLDocument` オブジェクトが必要です。これは、スタイルやスクリプト、あるいは生の HTML を注入できる仮想ブラウザキャンバスと考えてください。

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Dom;

class FontStyleDemo
{
    static void Main()
    {
        // 1️⃣ Create a fresh HTMLDocument – this is the starting point for conversion
        var htmlDocument = new HTMLDocument();
```

> **ポイント:** `HTMLDocument` クラスは、ブラウザと同様にマークアップを解析するため、レイアウトや CSS、フォントが PDF エンジンに引き渡される前に正しく処理されます。

---

## 手順 2: フォント埋め込み – `@font-face` を含む `<style>` ブロックの追加

カスタムフォントの埋め込みは 2 段階の作業です。まず `@font-face` でフォントを宣言し、次に対象要素に適用します。以下のコードは、実行ファイルと同じフォルダーにあるフォントファイルを読み込み、スタイル要素を動的に生成します。

```csharp
        // 2️⃣ Build a <style> element that defines the custom web font and applies it
        var styleElement = htmlDocument.CreateElement("style");
        styleElement.InnerHTML = @"
            @font-face {
                font-family: 'OpenSans';
                src: url('OpenSans.woff2') format('woff2');
                font-weight: normal;
                font-style: normal;
            }
            body {
                font-family: 'OpenSans';
                font-weight: " + ((int)WebFontStyle.Bold) + @";
                font-style: " + ((int)WebFontStyle.Italic) + @";
            }";

        // Insert the style into the <head> so the browser engine sees it
        htmlDocument.Head.AppendChild(styleElement);
```

> **プロのコツ:** 複数のウェイトやスタイルが必要な場合は、`font-weight: 700` や `font-style: italic` を付加した `@font-face` ルールを追加してください。Aspose.HTML は各バリエーションを正しくレンダリングします。

---

## 手順 3: コンテンツの追加 – Body に HTML を設定

フォントが準備できたら、ドキュメントの Body に HTML を投入します。ここに書いた内容は、埋め込んだフォントで描画されます。

```csharp
        // 3️⃣ Add some content that will use the defined font style
        htmlDocument.Body.InnerHTML = "<p>Styled text using WebFontStyle.</p>";
```

> **もっと複雑なマークアップが必要な場合は？** `new HTMLDocument("file.html")` で外部 HTML ファイルを読み込むか、プログラムで DOM ツリーを構築できます。Aspose.HTML はテーブル、画像、SVG まで対応しています。

---

## 手順 4: HTML を PDF に変換し、HTML を PDF として保存

ここまでで、メモリ上に完全にスタイルが適用された HTML ドキュメントが完成しました。次の行で Aspose.HTML に PDF ファイルへ直接レンダリングさせます。これが **convert html to pdf** の核心です。

```csharp
        // 4️⃣ Choose an output path and save the document as PDF
        string outputPath = "styled.pdf"; // change to your desired folder
        htmlDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

> **`Save` が機能する理由:** 背後で Aspose.HTML は DOM を PDF キャンバスにラスタライズし、ベクターテキスト（フォントは選択可能）とレイアウトの忠実さを保持します。画像への中間変換が不要なため、ファイルサイズも抑えられます。

---

## 手順 5: 結果の確認 – PDF を開いてフォントをチェック

プログラム実行後、`styled.pdf` を任意の PDF ビューアで開きます。段落が *OpenSans* の太字・斜体で表示されていれば成功です。フォントが代替表示になる場合は、以下を再確認してください。

1. `OpenSans.woff2` が実行ファイルと同じフォルダーにあること。  
2. ファイル名が完全に一致していること（Linux では大文字小文字を区別）。  
3. `@font-face` の `src` URL が正しい相対パスになっていること。

---

## HTML から PDF を作成する際の一般的な落とし穴

| 問題 | 発生原因 | 簡単な対処法 |
|------|----------|--------------|
| フォントが表示されない | パスのタイプミスまたはファイル欠損 | 絶対パス (`Path.Combine(Directory.GetCurrentDirectory(), "OpenSans.woff2")`) を使用 |
| テキストが画像として出力される | `WebFontStyle` 列挙体の誤用 | 示した通り `int` にキャストするか、CSS で直接 `font-weight: bold;` を指定 |
| PDF が空白になる | `Body.InnerHTML` が空または不正な HTML | HTML 文字列が空でないか、構文エラーがないか確認 |
| ファイルサイズが大きい | 高解像度画像を埋め込んでいる | 画像を圧縮するか、`srcset` 属性付き `Image` 要素を使用 |

---

## ボーナス: カスタムページサイズで HTML を PDF として保存

A4 縦など特定のページレイアウトが必要な場合は、`PdfSaveOptions` を渡して `Save` を呼び出します。これにより、**save html as pdf** を細かく制御できます。

```csharp
using Aspose.Html.Rendering.Pdf;

// ...

        // 4️⃣ (Alternative) Save with custom page dimensions
        var pdfOptions = new PdfSaveOptions
        {
            PageSetup = new PageSetup
            {
                Width = 595,   // A4 width in points
                Height = 842   // A4 height in points
            }
        };
        htmlDocument.Save("styled-a4.pdf", pdfOptions);
```

> **エッジケース:** ページサイズを指定すると、Aspose.HTML はコンテンツを再フローさせて収めます。その結果、改行位置が変わることがあります。実際の HTML でレイアウトを確認してください。

---

## 完全動作サンプル（コピペで使用可能）

以下はコンパイル可能な全プログラムです。`OpenSans.woff2` を `.csproj` と同じフォルダーに置き、Aspose.HTML NuGet パッケージをインストールしたら **Run** してください。

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Dom;
using Aspose.Html.Rendering.Pdf; // Needed for PdfSaveOptions (optional)

class FontStyleDemo
{
    static void Main()
    {
        // Step 1 – Initialize the HTML document
        var htmlDocument = new HTMLDocument();

        // Step 2 – Embed the custom font via @font-face
        var styleElement = htmlDocument.CreateElement("style");
        styleElement.InnerHTML = @"
            @font-face {
                font-family: 'OpenSans';
                src: url('OpenSans.woff2') format('woff2');
                font-weight: normal;
                font-style: normal;
            }
            body {
                font-family: 'OpenSans';
                font-weight: " + ((int)WebFontStyle.Bold) + @";
                font-style: " + ((int)WebFontStyle.Italic) + @";
            }";
        htmlDocument.Head.AppendChild(styleElement);

        // Step 3 – Add HTML content that uses the font
        htmlDocument.Body.InnerHTML = "<p>Styled text using WebFontStyle.</p>";

        // Step 4 – Convert HTML to PDF (basic save)
        string outputPath = "styled.pdf";
        htmlDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");

        // Optional: Save with custom page size (demonstrates save html as pdf)
        var pdfOptions = new PdfSaveOptions
        {
            PageSetup = new PageSetup { Width = 595, Height = 842 } // A4
        };
        htmlDocument.Save("styled-a4.pdf", pdfOptions);
        Console.WriteLine("PDF with custom page size saved as styled-a4.pdf");
    }
}
```

**期待される出力:** 実行フォルダーに `styled.pdf` と `styled-a4.pdf` の 2 つの PDF が生成されます。どちらも CSS で指定した通り、OpenSans の太字・斜体で段落が表示されます。

---

## まとめ

本稿では Aspose.HTML を用いた **HTML から PDF の作成** 方法、**フォント埋め込み** の手順、シンプルな **convert html to pdf** ワークフロー、そしてカスタムページサイズを伴う高度な **save html as pdf** シナリオを紹介しました。基本的な流れはシンプルです: `HTMLDocument` を作成し、`@font-face` ルールを注入し、マークアップを追加、最後に Aspose に任せて PDF を生成するだけです。

次のステップとしては、フォントを差し替えたり画像を追加したり、マルチページレポートを生成したりしてみてください。CSS のメディアクエリを活用すれば、画面表示と印刷用レイアウトを分けることも可能です。請求書、証明書、電子書籍など、さまざまな文書を C# の快適さのまま PDF に変換できます。

問題が発生したら、フォントパスと NuGet パッケージのバージョンが対象の .NET ランタイムと合っているかを再確認してください。コーディングを楽しみながら、HTML を美しい PDF に変換しましょう！

<img src="assets/create-pdf-from-html-diagram.png" alt="Create PDF from HTML example with embedded font">

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}