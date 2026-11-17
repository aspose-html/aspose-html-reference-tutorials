---
category: general
date: 2026-04-01
description: C# を使用して HTML で太字と斜体を組み合わせる。HTML のフォントスタイルの変更方法、変更した HTML の保存方法、そして C#
  でフォントスタイルを変更する方法を簡単な手順で学びましょう。
draft: false
keywords:
- combine bold and italic
- save modified html
- modify html font style
- change font style c#
language: ja
og_description: C#でHTMLの太字と斜体を組み合わせる。このガイドでは、HTMLのフォントスタイルを変更し、変更したHTMLを保存し、C#でフォントスタイルをすばやく変更する方法を示します。
og_title: C#でHTMLの太字と斜体を組み合わせる – ステップバイステップ
tags:
- C#
- Aspose.Html
- HTML manipulation
title: C#でHTMLの太字と斜体を組み合わせる – 完全ガイド
url: /ja/net/html-document-manipulation/combine-bold-and-italic-in-html-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML で太字と斜体を組み合わせる C# – 完全ガイド

動的なメールやレポートを生成する際に、**太字と斜体を組み合わせ**た HTML スニペットをプログラムで作成したいと思ったことはありませんか？同じ問題に直面している開発者は多いです。Aspose.HTML ライブラリと数行の C# だけで、任意のドキュメントに太字‑斜体のフォントスタイルを適用し、**変更した HTML を保存**して後で使用できます。

このチュートリアルでは、次の手順を順に解説します。小さな HTML フラグメントの読み込み、**HTML フォントスタイルの変更**、**太字と斜体の組み合わせ**効果の適用、そして最終的に**変更した HTML をディスクに保存**する方法です。最後まで読めば、**C# でフォントスタイルを変更**する方法がドキュメントを掘り下げることなく理解できます。

## 必要なもの

- .NET 6 以降（コードは .NET Core でも動作します）  
- Aspose.HTML for .NET – NuGet から取得できます（`Install-Package Aspose.HTML`）  
- テキストエディタまたは IDE（Visual Studio、VS Code、Rider などお好みのもの）  

他の依存関係は不要です。既存のプロジェクトがある場合は、NuGet パッケージを追加するだけで使用できます。

![Screenshot showing combined bold and italic text in a browser – combine bold and italic](https://example.com/combine-bold-italic.png)

*Image alt text: combine bold and italic*

## Step 1: Load the HTML Snippet and Create a Document

まず、操作対象となる HTML を表す `Aspose.Html.Document` オブジェクトを作成します。以下のスニペットは `<b>` と `<i>` タグを含む小さなフラグメントを読み込みます。

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;

// The raw HTML we’ll transform
string htmlContent = "<html><body><b>Bold</b> <i>Italic</i></body></html>";

// Create a Document instance from the string
Document document = new Document(htmlContent);
```

**Why this matters:**  
`Document` を作成すると、ブラウザと同様にスタイルを操作できる完全な DOM ライクなモデルが得られます。また、後で **変更した HTML を保存** できるようオブジェクトが準備されるため重要です。

## Step 2: Combine Bold and Italic Font Style

チュートリアルの核心部分です。一度に太字 **かつ** 斜体になるスタイルを適用します。Aspose.HTML は `WebFontStyle` 列挙体を提供しており、`BoldItalic` メンバーは `FontStyle.Bold | FontStyle.Italic` のショートハンドです。

```csharp
// Retrieve the default viewport style (covers the whole document)
var defaultStyle = document.DefaultViewPort.Style;

// Apply the combined bold‑and‑italic style
defaultStyle.FontStyle = WebFontStyle.BoldItalic; // same as FontStyle.Bold | FontStyle.Italic
```

**Explanation:**  
`DefaultViewPort.Style` は、上書きされない限りすべての要素に適用されるグローバル CSS ルールです。`FontStyle` を `BoldItalic` に設定することで、**HTML フォントスタイルの変更** が均一に適用され、個々の `<b>` や `<i>` タグを個別に操作する必要がなくなります。

> *Pro tip:* 特定の要素だけを太字‑斜体にしたい場合は、`document.QuerySelectorAll("p.special")` で取得し、各ノードに対してスタイルを設定するとグローバルビューポートを変更せずに済みます。

## Step 3: Verify the Change (Optional but Helpful)

ディスクに書き出す前に、生成されたマークアップを確認すると安心です。コンソールやデバッグウィンドウに HTML を出力できます。

```csharp
// Output the transformed HTML for quick verification
string transformedHtml = document.ToString();
Console.WriteLine(transformedHtml);
```

`<head>` 内に `<style>` ブロックが挿入され、`font-weight: bold; font-style: italic;` が全体に適用されているはずです。これにより **太字と斜体の組み合わせ** が正しく行われたことが確認できます。

## Step 4: Save Modified HTML

最後に、更新されたドキュメントを永続化します。`Save` メソッドは、外部リソースを保持したまま、整形式の HTML ファイルを書き出します。

```csharp
// Choose an output path that makes sense for your project
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.html");

// Save the document – this is the “save modified html” step
document.Save(outputPath);
Console.WriteLine($"Modified HTML saved to: {outputPath}");
```

**What you get:**  
`output.html` を任意のブラウザで開くと、元のテキストが **太字かつ斜体** で表示されます。これは Aspose.HTML を使用して **C# でフォントスタイルを変更** した具体的な結果です。

## Step 5: Common Variations & Edge Cases

### a) Targeting Only Specific Elements

特定の要素だけ **HTML フォントスタイルを変更** したい場合、たとえばクラス `highlight` を持つすべての段落に対しては次のようにセレクタを使用します。

```csharp
var highlights = document.QuerySelectorAll("p.highlight");
foreach (var node in highlights)
{
    node.Style.FontStyle = WebFontStyle.BoldItalic;
}
```

### b) Keeping Original `<b>` / `<i>` Tags

意味論的に元の `<b>` / `<i>` タグを残したまま、組み合わせスタイルを適用したいことがあります。その場合は、グローバルスタイルを上書きせずに CSS クラスを追加します。

```csharp
// Add a CSS class to the head
var style = document.CreateElement("style");
style.InnerHtml = ".bold-italic { font-weight: bold; font-style: italic; }";
document.Head.AppendChild(style);

// Apply the class to the body (or any element you like)
document.Body.ClassName = "bold-italic";
```

### c) Saving to a Different Encoding

Aspose.HTML のデフォルトは UTF‑8 ですが、下流システムが別のエンコーディングを要求する場合は明示的に指定できます。

```csharp
var saveOptions = new HtmlSaveOptions()
{
    Encoding = System.Text.Encoding.ASCII // or any other Encoding
};
document.Save("output-ascii.html", saveOptions);
```

## Full Working Example

すべてをまとめた、コンソールアプリに貼り付け可能な完全なプログラムです。

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the HTML snippet
        string htmlContent = "<html><body><b>Bold</b> <i>Italic</i></body></html>";
        Document document = new Document(htmlContent);

        // 2️⃣ Apply combined bold‑and‑italic style
        var defaultStyle = document.DefaultViewPort.Style;
        defaultStyle.FontStyle = WebFontStyle.BoldItalic; // combine bold and italic

        // 3️⃣ (Optional) Verify by printing to console
        Console.WriteLine("Transformed HTML:");
        Console.WriteLine(document.ToString());

        // 4️⃣ Save the modified HTML
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.html");
        document.Save(outputPath);
        Console.WriteLine($"✅ Modified HTML saved to: {outputPath}");
    }
}
```

**Expected output:**  
`output.html` をブラウザで開くと「Bold Italic」という文字列が **太字かつ斜体** で表示されます。またコンソールにも生成された HTML が出力され、`<style>` タグで組み合わせスタイルが強制されていることが確認できます。

## Conclusion

これで C# を使って HTML ドキュメントに **太字と斜体を組み合わせ**る方法が分かりました。`Aspose.Html.Document` に HTML を読み込み、`WebFontStyle.BoldItalic` をデフォルトビューポートに設定し、**変更した HTML を保存**することで、あらゆる自動化タスクに対してクリーンで再利用可能なソリューションが得られます。グローバルに **HTML フォントスタイルを変更**したり、特定ノードだけを対象にしたり、**C# でフォントスタイルを変更**したりする場合でも同じ原則が適用できます。

次は何をしますか？`WebFontStyle` の他の値（`Underline`、`StrikeThrough`、あるいはカスタム CSS クラス）を試して、スタイリングツールキットを拡張してみましょう。また、Aspose.HTML の画像処理や PDF 変換機能を利用して、同じスタイルのドキュメントをその場で PDF に変換することも可能です。

質問や難しいケースがあればコメントで教えてください。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}