---
category: general
date: 2025-12-29
description: C#でHTMLドキュメントを作成し、フォントファミリーやフォントサイズの設定方法を学び、最後にAspose.HTMLを使用してHTMLをPDFとして保存またはHTMLをPDFに変換します。
draft: false
keywords:
- create html document
- set font family
- set font size
- save html as pdf
- convert html to pdf
language: ja
og_description: C#でHTMLドキュメントを作成し、フォントファミリーやフォントサイズの設定方法をすぐに確認し、HTMLをPDFとして保存またはAspose.HTMLでHTMLをPDFに変換します。
og_title: HTMLドキュメントを作成 – スタイル付きテキストとPDFエクスポート
tags:
- aspnet
- csharp
- pdf-generation
title: スタイル付きテキストでHTMLドキュメントを作成しPDFにエクスポートする完全ガイド
url: /ja/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# スタイル付きテキストのHTMLドキュメントを作成しPDFへエクスポート

C#コードから離れることなく、**create HTML document**をその場で作成してPDFに変換する必要がありますか？レポートエンジンや請求書ジェネレータ、あるいはユーザー向けのクイックプレビューを作っているかもしれません。良いニュースは、Aspose.HTMLを数行で使用すれば、フォントファミリー、フォントサイズ、さらには太字・斜体のスタイルまでフルコントロールできることです。

このチュートリアルでは、インメモリのHTMLドキュメントを作成し、PDFファイルとして保存するまでの全プロセスを順に解説します。最後までで、**set font family**、**set font size**、そして**save HTML as PDF**（別名 **convert HTML to PDF**）をクリーンで本番環境向けのコードサンプルと共に正確に実装できるようになります。

## 必要なもの

- .NET 6+（APIは.NET Coreおよび.NET Frameworkでも動作）
- Aspose.HTML for .NET NuGet パッケージ（`Aspose.Html`） – `dotnet add package Aspose.Html` でインストール
- 生成されたPDFを書き込めるディスク上のフォルダー

余計なHTMLテンプレートや外部コンバータは不要で、純粋にC#だけです。

![HTMLドキュメント作成イラスト](/images/create-html-document.png){alt="HTMLドキュメント作成例"}

## ステップ 1: HTMLドキュメントの作成

まず、空のHTMLドキュメントオブジェクトが必要です。後でスタイル付き段落を描くための真っ白なキャンバスと考えてください。

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

// Step 1 – initialize a new HTML document in memory
HTMLDocument htmlDocument = new HTMLDocument();

// Grab a reference to the <body> element for later use
HTMLBodyElement body = htmlDocument.Body;
```

**Why this matters:** `HTMLDocument` は、プログラムから操作できるDOMに似た構造を提供します。最終段階まで生の文字列やファイルI/Oに触れる必要はありません。

## ステップ 2: 段落を追加しフォントファミリーとフォントサイズを設定

ここで `<p>` 要素を作成し、テキストを挿入してフォントファミリーとサイズを明示的に定義します。ここが **set font family** と **set font size** キーワードが登場するポイントです。

```csharp
// Step 2 – create a <p> element with some sample text
HtmlElement paragraph = htmlDocument.CreateElement("p");
paragraph.InnerHtml = "Bold & Italic text";

// Define the base font style
paragraph.Style.FontFamily = "Arial";   // set font family
paragraph.Style.FontSize = "18px";      // set font size

// Attach the paragraph to the document body
body.AppendChild(paragraph);
```

**Pro tip:** Webセーフなフォールバックが必要な場合は、`"Arial, Helvetica, sans-serif"` のようにカンマ区切りのリストを指定できます。ブラウザー（またはAspose）が最初に利用可能なフォントを選択します。

## ステップ 3: WebFontStyle フラグで太字と斜体のスタイルを適用

Aspose.HTML は便利な列挙型 `WebFontStyle` を提供しており、ビット単位の OR でスタイルを組み合わせられます。テキストを太字 **かつ** 斜体にしてみましょう。

```csharp
// Step 3 – apply bold and italic using WebFontStyle flags
paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

**What’s happening under the hood?** `FontStyle` プロパティは CSS の `font-weight` と `font-style` 宣言に変換されます。フラグを OR することで、CSS を別々に2行書く必要がなくなります。

## ステップ 4: HTMLをPDFに変換（HTMLをPDFとして保存）

最終ステップは実際の変換です。`Save` を一度呼び出すだけで、Aspose.HTML が DOM をレンダリングし、PDFファイルをディスクに書き出します。これで **save html as pdf** と **convert html to pdf** の両方の要件を満たします。

```csharp
// Step 4 – save the HTML document as a PDF file
string outputPath = @"C:\Temp\styled.pdf";
htmlDocument.Save(outputPath, new PDFSaveOptions());

// Optional: open the PDF automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Expected result:** `styled.pdf` を開くと、18px の Arial で「Bold & Italic text」と表示された単一の段落が太字かつ斜体でレンダリングされているのが確認できます。PDF のサイズは標準的な A4 ページに合わせられ、テキストはベクターレンダリングのおかげで選択可能です。

## 完全な動作例

すべてをまとめると、以下が完全で実行可能なプログラムです：

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new HTML document
        HTMLDocument htmlDocument = new HTMLDocument();
        HTMLBodyElement body = htmlDocument.Body;

        // 2️⃣ Add a styled paragraph
        HtmlElement paragraph = htmlDocument.CreateElement("p");
        paragraph.InnerHtml = "Bold & Italic text";

        // Set font family and size
        paragraph.Style.FontFamily = "Arial";
        paragraph.Style.FontSize = "18px";

        // 3️⃣ Apply bold + italic
        paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // Append to body
        body.AppendChild(paragraph);

        // 4️⃣ Save as PDF (convert HTML to PDF)
        string outputFile = @"C:\Temp\styled.pdf";
        htmlDocument.Save(outputFile, new PDFSaveOptions());

        Console.WriteLine($"PDF generated at: {outputFile}");
    }
}
```

### コードの実行

1. Aspose.HTML NuGet パッケージをインストール：  
   ```bash
   dotnet add package Aspose.Html
   ```
2. `C:\Temp\styled.pdf` を、書き込み権限のあるフォルダーに置き換えてください。  
3. ビルドして実行：`dotnet run`。  

コンソールにファイルの場所が表示され、PDF にはスタイル付き段落が含まれているはずです。

## よくある質問とエッジケース

- **What if I need a custom web font?**  
  段落を作成する前に `HTMLFontFaceRule` でフォントをロードするか、リモートの `@font-face` CSS ファイルを参照してください。

- **Can I add images before converting?**  
  もちろんです。`HTMLImageElement img = (HTMLImageElement)htmlDocument.CreateElement("img");` を使用し、`img.Source` にローカルパスまたはデータURIを設定します。

- **What about multi‑page PDFs?**  
  さらに要素（テーブル、div など）を追加すれば、コンテンツがページ高さを超えたときに Aspose.HTML が自動的にページ分割します。

- **Is there a way to control PDF metadata?**  
  `PdfSaveOptions` インスタンスを渡し、`Author`、`Title`、`PdfAConformanceLevel` などのプロパティを設定します。

## まとめ

C# で **create HTML document** を行い、**set font family**、**set font size** を設定し、太字・斜体スタイルを適用、最終的に **save HTML as PDF** する方法、すなわち Aspose.HTML を使った **convert HTML to PDF** を解説しました。このコードスニペットは .NET プロジェクトに簡単に組み込めるほど短く、かつ複雑なレポートシナリオの基盤として十分な内容です。

## 次のステップ

- 再利用可能なスタイルのために CSS クラスを試す。  
- 複数の段落、テーブル、画像を組み合わせて、よりリッチな PDF を作成する。  
- アーカイブ向け文書が必要な場合は PDF/A 準拠を検討する。  

フォントやサイズ、色を自由に調整してください。プログラムで生成できるものに制限はありません。コーディングを楽しんで、作成した PDF が常に思い通りにレンダリングされますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}