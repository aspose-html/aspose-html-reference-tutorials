---
category: general
date: 2025-12-29
description: Aspose.HTML を使用して C# で HTML を素早く Zip する方法 – カスタム ZipResourceHandler で
  HTML を zip に保存する。ステップバイステップで学ぶ。
draft: false
keywords:
- how to zip html
- save html to zip
- create zip archive c#
- Aspose HTML zip
- C# resource handling
language: ja
og_description: Aspose.HTML を使用して C# で HTML を迅速に zip する方法。このガイドに従って HTML を zip に保存し、カスタムリソース処理で
  zip アーカイブを作成します。
og_title: C#でHTMLをZIPに圧縮する方法 – HTMLをZIPに保存
tags:
- C#
- Aspose.HTML
- ZipArchive
- File I/O
title: C#でHTMLをZIPに圧縮する方法 – HTMLをZIPに保存
url: /ja/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で HTML を Zip に圧縮する方法 – HTML を Zip に保存

C# で HTML を Zip に圧縮することは、オフラインで利用できるように Web ページをパッケージ化したいときに一般的に必要とされます。単一ページとその画像をまとめる場合でも、サイト全体をエクスポートする場合でも、**HTML を Zip に保存**することで、すべてが整頓され持ち運びやすくなります。このチュートリアルでは、HTML マークアップを Zip に圧縮するだけでなく、参照されているすべてのリソースを直接アーカイブにストリームする、完全に実行可能なソリューションを順を追って解説します。

学べること:

* .NET の `System.IO.Compression` を使ってプログラムから Zip アーカイブを作成する方法
* Aspose.HTML にカスタム `ResourceHandler` を組み込んで、リソースを直接 Zip に流し込む方法
* 既存の Zip ファイルや大容量バイナリ資産といったエッジケースの取り扱い

外部ツールは不要です — C#、Aspose.HTML、数行のコードだけで完結します。

## 必要なもの

本題に入る前に、以下が揃っていることを確認してください。

* **.NET 6+**（コードは .NET Framework 4.6.2 以降でも動作します）
* **Aspose.HTML for .NET** – Aspose の公式サイトから無料トライアルを取得するか、ライセンス版を使用してください
* 開発環境（Visual Studio、VS Code、Rider などお好みのもの）

以上です。`System.IO.Compression`（.NET に同梱）と `Aspose.HTML` 以外に追加の NuGet パッケージは不要です。

## Step 1: プロジェクトとインポートの設定

新しいコンソールプロジェクトを作成するか、既存プロジェクトにコードを貼り付けます。ファイルの先頭に必要な `using` ディレクティブを追加してください。

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;
```

> **プロのコツ:** Visual Studio を使用している場合、IDE が `Aspose.Html` の不足している NuGet パッケージを自動で提案します。提案を受け入れればすぐに使用可能です。

## Step 2: カスタム ZipResourceHandler の実装

Aspose.HTML はリソース（画像、CSS、スクリプトなど）を書き込む必要があるたびに `ResourceHandler` を呼び出します。`HandleResource` をオーバーライドすることで、各リソースの保存先を自由に決められます。以下のハンドラは、リソースの論理パスに対応した Zip エントリを作成し、そのエントリに直接書き込めるストリームを返します。

```csharp
/// <summary>
/// Streams each HTML resource straight into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;

    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // Ensure the entry's directory structure exists inside the zip.
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        // The returned stream writes directly into the zip entry.
        return entry.Open();
    }
}
```

**この実装が重要な理由:**  
リソースを一時フォルダーに書き出してから Zip にまとめる代わりに、ハンドラはデータをリアルタイムでストリームし、ディスク I/O を削減しメモリ使用量を抑えます。また、Zip 内のフォルダー構造が HTML の相対パスと一致するため、解凍後にブラウザーでページを開いたときに正しく表示されます。

## Step 3: Zip アーカイブの準備

次に、対象となる Zip ファイルを開く（または作成する）処理を書きます。`FileMode.Create` フラグは既存ファイルを上書きするため、ビルドを繰り返すシナリオに最適です。既存のアーカイブを保持したい場合は `FileMode.OpenOrCreate` に変更し、重複エントリの処理を追加してください。

```csharp
string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");

// Ensure the directory exists (useful if you run the code from a nested folder)
Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);

using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);
```

> **エッジケース:** `using` ブロックが破棄される前にプロセスがクラッシュすると、破損した Zip が残る可能性があります。`try/catch` で囲み、失敗時に途中で作成されたファイルを削除することで簡易的に対策できます。

## Step 4: 埋め込みリソース付き HTML ドキュメントの作成

デモ用に、`image.png` を参照する小さな HTML ページを作成します。実際のシナリオでは、ファイルやデータベースから取得した HTML をロードすることになるでしょう。

```csharp
// Sample HTML containing an <img> tag.
// Aspose.HTML will ask the ResourceHandler for "image.png".
string htmlContent = @"
<html>
<head><title>Sample Zip</title></head>
<body>
    <h1>Hello, zipped world!</h1>
    <img src='image.png' alt='Demo image'>
</body>
</html>";

// Create the document from the string.
var html = new HTMLDocument(htmlContent);
```

ディスク上に実際の画像ファイルがある場合は、HTML を保存する前に手動で Zip に追加するか、ハンドラに任せて URL から取得させることができます。今回実装したハンドラはローカルパスとリモート URL の両方に対応しています。

## Step 5: ZipResourceHandler を使用するように保存オプションを構成

ここで、Aspose.HTML にカスタムハンドラを使用させる設定を行います。`HTMLSaveOptions` クラスでは、Zip 内の出力ファイル名（デフォルトは `index.html`）も指定できます。

```csharp
var saveOptions = new HTMLSaveOptions
{
    // The HTML file itself will be saved as "index.html" inside the zip.
    OutputFileName = "index.html",
    // Plug in our handler so resources go straight into the archive.
    OutputStorage = new ZipResourceHandler(zip)
};
```

## Step 6: ドキュメントを保存 – すべてが Zip にストリームされる

最後に `Save` を呼び出します。Aspose.HTML はマークアップを解析し、`<img>` タグを検出して `image.png` 用に `HandleResource` を呼び出し、HTML ファイルと画像の両方を同じ Zip アーカイブに書き込みます。

```csharp
html.Save(saveOptions);
Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
```

`using` ブロックが終了すると、`ZipArchive` がファイルを確定させ、配布可能な状態になります。

### 完全動作サンプル

以下は全体をまとめたプログラムです。`Program.cs` に貼り付けて実行すれば、追加の修正は不要です。

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;
    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare the zip file.
        string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");
        Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);
        using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
        using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);

        // 2️⃣ Build a simple HTML document with an image reference.
        string htmlContent = @"
        <html>
        <head><title>Sample Zip</title></head>
        <body>
            <h1>Hello, zipped world!</h1>
            <img src='image.png' alt='Demo image'>
        </body>
        </html>";
        var html = new HTMLDocument(htmlContent);

        // 3️⃣ Set save options to stream resources into the zip.
        var saveOptions = new HTMLSaveOptions
        {
            OutputFileName = "index.html",
            OutputStorage = new ZipResourceHandler(zip)
        };

        // 4️⃣ Save – everything ends up in output.zip.
        html.Save(saveOptions);
        Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
    }
}
```

**期待される結果:** 実行後、`output.zip` には次の 2 つのエントリが含まれます。

```
index.html
image.png
```

ファイルを解凍し、ブラウザーで `index.html` を開くと、相対パスが保持されているため画像が正しく表示されます。

## Frequently Asked

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}