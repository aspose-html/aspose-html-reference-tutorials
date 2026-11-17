---
category: general
date: 2026-06-22
description: C#でHTMLからPDFを素早く作成—HTMLをPDFに変換する方法、HTMLをPDFとして保存する方法、シンプルなライブラリでHTMLをPDFにエクスポートする方法を学びましょう。
draft: false
keywords:
- create pdf from html
- convert html to pdf
- save html as pdf
- export html as pdf
- how to convert html to pdf
language: ja
og_description: C#で軽量コンバータを使用してHTMLからPDFを作成します。このガイドでは、HTMLをPDFに変換し、HTMLをPDFとして保存し、クリーンなコードでHTMLをPDFにエクスポートする方法を示します。
og_title: C#でHTMLからPDFを作成する – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create PDF from HTML in C# quickly—learn how to convert HTML to PDF,
    save HTML as PDF, and export HTML as PDF with a simple library.
  headline: Create PDF from HTML in C# – Complete Programming Guide
  type: TechArticle
- description: Create PDF from HTML in C# quickly—learn how to convert HTML to PDF,
    save HTML as PDF, and export HTML as PDF with a simple library.
  name: Create PDF from HTML in C# – Complete Programming Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 SDK or later (the code works on .NET Core and .NET Framework
      alike). - Basic familiarity with C# and the command line. - An HTML file you
      want to turn into a PDF (we’ll call it `input.html`).'
  - name: How It Works
    text: 1. **Reading the HTML** – We pull the raw HTML string from `input.html`.
      This step is crucial for the **save html as pdf** part because the converter
      works with a string, not a file handle. 2. **Creating a `PdfDocument`** – Think
      of this as the blank canvas where each page will be painted. 3. **`Pdf
  - name: Handling CSS and Images
    text: '```csharp // Load HTML with a base URL so relative paths resolve correctly.
      string baseUrl = Path.GetDirectoryName(htmlPath) ?? ""; PdfGenerator.AddPdfPages(pdf,
      htmlContent, PageSize.A4, new PdfGenerateConfig { BaseUrl = new Uri($"file:///{baseUrl}/")
      }); ```'
  - name: Large Documents & Pagination
    text: 'If your HTML creates many pages, the library automatically adds them. However,
      you might want to control page breaks manually:'
  type: HowTo
tags:
- C#
- HTML
- PDF
- Conversion
title: C#でHTMLからPDFを作成する – 完全プログラミングガイド
url: /ja/net/html-extensions-and-conversions/create-pdf-from-html-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で HTML から PDF を作成 – 完全プログラミングガイド

何十ものコマンドラインツールと格闘せずに **HTML から PDF を作成** したことはありませんか？ あなたは一人ではありません。動的なウェブページを印刷可能なレポートや請求書、ダウンロード可能なパンフレットに変換する必要があるとき、多くの開発者がこの壁にぶつかります。

このチュートリアルでは、数行の C# コードだけで **HTML を PDF に変換**、**HTML を PDF として保存**、さらには **HTML を PDF としてエクスポート** できるシンプルでエンドツーエンドなソリューションを順を追って解説します。最後まで読むと、任意の .NET プロジェクトに組み込める再利用可能なメソッドが手に入り、謎の依存関係や隠されたマジックは一切ありません。

## 学べること

- HTML‑to‑PDF 変換のための最小限の C# コンソールアプリのセットアップ方法。  
- 人気の *HtmlRenderer.PdfSharp* ライブラリ（または類似ライブラリ）を使用して **HTML から PDF を作成** するために必要な正確なコード。  
- 同期呼び出しと非同期呼び出しのどちらを好むか、そしてそれぞれが適切なシーンはいつか。  
- 一般的な落とし穴—CSS が欠如、画像が大きすぎる、相対パス—とそれらを回避する方法。  
- 出力が期待通りかを確認できる簡単なテスト。  

### 前提条件

- .NET 6.0 SDK 以降（コードは .NET Core と .NET Framework の両方で動作します）。  
- C# とコマンドラインの基本的な知識。  
- PDF に変換したい HTML ファイル（ここでは `input.html` と呼びます）。  

これらが揃っているなら、さっそく始めましょう。

## HTML から PDF を作成 – プロジェクトのセットアップ

まず、フレッシュなコンソールプロジェクトを作成します。ターミナルを開いて次のコマンドを入力してください。

```bash
dotnet new console -n HtmlToPdfDemo
cd HtmlToPdfDemo
```

次に、変換ライブラリを追加します。この例では **HtmlRenderer.PdfSharp** を使用します。これは PdfSharp をラップし、ほとんどの HTML/CSS をデフォルトで処理します。

```bash
dotnet add package HtmlRenderer.PdfSharp --version 1.7.2
```

> **プロのコツ:** .NET Framework を対象にしている場合でも、同じ NuGet パッケージを使用できます。プロジェクトファイルが適切なフレームワーク バージョンを対象としていることを確認してください。

これで **HTML を PDF に変換** するために必要なものはすべて揃いました。

## HTML を PDF に変換 – HtmlToPdfConverter の使用

`PdfConverter.cs` という新しいクラスファイルを作成します（またはデモ用にすべてを `Program.cs` に入れても構いません）。以下は **完全かつ実行可能** な例で、HTML ドキュメントを読み込み、変換し、結果をディスクに書き出します。

```csharp
using System;
using System.IO;
using TheArtOfDev.HtmlRenderer.PdfSharp;   // Namespace from HtmlRenderer.PdfSharp
using PdfSharp.Pdf;

namespace HtmlToPdfDemo
{
    /// <summary>
    /// Simple helper that encapsulates the HTML → PDF conversion logic.
    /// </summary>
    public static class PdfConverter
    {
        /// <summary>
        /// Converts the specified HTML file to a PDF and saves it.
        /// </summary>
        /// <param name="htmlPath">Full path to the source HTML file.</param>
        /// <param name="pdfPath">Full path where the PDF should be written.</param>
        public static void ConvertHtmlToPdf(string htmlPath, string pdfPath)
        {
            // Validate inputs early – helps you avoid vague exceptions later.
            if (!File.Exists(htmlPath))
                throw new FileNotFoundException($"HTML file not found: {htmlPath}");

            // Read the HTML content. Using UTF‑8 ensures you keep any special characters.
            string htmlContent = File.ReadAllText(htmlPath);

            // Create a new PDF document. This is the container that will hold our pages.
            using PdfDocument pdf = new PdfDocument();

            // The HtmlRender library does the heavy lifting. It parses the HTML and draws it onto a PDF page.
            PdfGenerator.AddPdfPages(pdf, htmlContent, PageSize.A4);

            // Finally, write the PDF to the destination path.
            pdf.Save(pdfPath);
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to match your environment.
            string inputHtml = Path.Combine(Environment.CurrentDirectory, "input.html");
            string outputPdf = Path.Combine(Environment.CurrentDirectory, "output.pdf");

            try
            {
                PdfConverter.ConvertHtmlToPdf(inputHtml, outputPdf);
                Console.WriteLine($"✅ Success! PDF created at: {outputPdf}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Failed to create PDF: {ex.Message}");
            }
        }
    }
}
```

### 動作概要

1. **HTML の読み取り** – `input.html` から生の HTML 文字列を取得します。このステップは **HTML を PDF として保存** の部分で重要です。コンバータはファイルハンドルではなく文字列で動作するためです。  
2. **`PdfDocument` の作成** – 各ページが描かれる空白のキャンバスと考えてください。  
3. `PdfGenerator.AddPdfPages` – ライブラリの核心部分です。HTML を解析し、基本的な CSS を適用し、1枚以上の A4 ページにレンダリングします。  
4. **ファイルの保存** – `pdf.Save` 呼び出しでバイナリ PDF がディスクに書き込まれ、実質的に **HTML を PDF としてエクスポート** されます。  

プログラムを実行します:

```bash
dotnet run
```

すべてが正しく設定されていれば、緑のチェックマークが表示され、実行ファイルの横に `output.pdf` が生成されます。

## HTML を PDF として保存 – ファイル処理の詳細

「なぜ PDF を直接レスポンスにストリームしないのか？」と疑問に思うかもしれません。良い質問です。多くの Web API シナリオではバイト列をストリームしますが、デスクトップやバッチジョブでは物理的なファイルが必要になることが多いです。上記のコードは `pdf.Save(pdfPath)` を呼び出すことで既に **HTML を PDF として保存** しています。  

いくつかの注意点があります：

- **上書き保護** – `pdf.Save` は既存のファイルを黙って上書きします。安全にしたい場合は、先に `File.Exists(pdfPath)` を確認し、リネームするかユーザーに確認してください。  
- **フォルダーの権限** – 特に Linux コンテナではデフォルトユーザーが制限されることがあるため、対象フォルダーへの書き込み権限があることを確認してください。  
- **エンコーディング** – HTML ファイルは UTF‑8 であるべきです。そうでないと最終的な PDF に文字化けが発生する可能性があります。  

## HTML を PDF としてエクスポート – 高度なオプション

シンプルな例はほとんどの静的ページで機能しますが、実際の HTML では外部 CSS、画像、さらには JavaScript が含まれることが多いです。以下に、そうしたケースに対応するためにコンバータを拡張する方法を示します。

### CSS と画像の取り扱い

```csharp
// Load HTML with a base URL so relative paths resolve correctly.
string baseUrl = Path.GetDirectoryName(htmlPath) ?? "";
PdfGenerator.AddPdfPages(pdf, htmlContent, PageSize.A4, 
    new PdfGenerateConfig
    {
        BaseUrl = new Uri($"file:///{baseUrl}/")
    });
```

- **BaseUrl** は、`src="images/logo.png"` や `href="styles/main.css"` などのリソースを探す場所をレンダラに指示します。  
- リモート資産の場合、`BaseUrl` を HTTP URL に設定できますが、ネットワーク遅延に注意してください。  

### 大規模ドキュメントとページング

HTML が多数のページを生成する場合、ライブラリは自動的にページを追加します。ただし、ページ区切りを手動で制御したいこともあります：

```html
<div style="page-break-after: always;"></div>
```

C# では HTML をセクションに分割し、`AddPdfPages` を繰り返し呼び出すことで、ヘッダーやフッターをより細かく制御できます。

## HTML を PDF に変換する方法 – よくある落とし穴

| 問題 | 発生理由 | 対策 |
|------|----------|------|
| フォントが欠如 | PdfSharp は標準フォントのみをデフォルトで使用します。 | `PdfFontResolver` を使用して TrueType フォントを埋め込む。 |
| 画像が表示されない | 相対パスが壊れているか、サポートされていない形式です。 | `BaseUrl` を使用するか、画像を Base64 で埋め込む。 |
| CSS が適用されない | ライブラリは CSS のサブセットしかサポートしていません。 | スタイルをシンプルに保つか、ヘッドレスブラウザ（例: Puppeteer）で HTML を事前処理する。 |
| 大きなページでメモリ不足 | `Save` まで全ページがメモリに保持される。 | チャンク単位で変換するか、利用可能ならストリーミング API を使用する。 |

## 期待される出力

サンプルを実行したら、任意の PDF ビューアで `output.pdf` を開きます。`input.html` の忠実なレンダリングが表示されるはずです—見出し、段落、画像（ある場合）すべてが A4 ページに配置されます。ファイルサイズは、プレーンテキストで約 50 KB、画像が多いページで数百キロバイト程度です。

![create pdf from html example output](https://example.com/assets/create-pdf-from-html.png "create pdf from html example output")

*上のスクリーンショットは、シンプルな HTML ページがきれいな PDF に変換された様子を示しています。*

## まとめ & 次へ

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [HTML から PDF を作成 – C# ステップバイステップガイド](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)
- [.NET で Aspose.HTML を使用して HTML を PDF に変換](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [スタイル付きテキストで HTML ドキュメントを作成し PDF にエクスポート – 完全ガイド](/html/english/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}