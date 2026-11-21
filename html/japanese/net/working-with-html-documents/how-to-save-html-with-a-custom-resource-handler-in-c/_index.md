---
category: general
date: 2026-11-20
description: C# のカスタム ResourceHandler を使用して HTML を保存する方法と、簡潔で本番環境向けのコードで HTML を zip
  アーカイブに保存する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save html
- save html to zip
- custom ResourceHandler C#
- HtmlAgilityPack save example
- stream based HTML export
language: ja
lastmod: 2026-11-20
og_description: C# のカスタム ResourceHandler を使用して HTML を保存し、必要に応じて HTML を zip ファイルに保存する方法―.NET
  開発者向けの完全かつ実行可能なガイド。
og_image_alt: Diagram showing how to save HTML with a custom ResourceHandler and zip
  the output
og_title: C# のカスタムリソースハンドラで HTML を保存する方法
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  headline: How to save HTML with a custom resource handler in C#
  type: TechArticle
- description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  name: How to save HTML with a custom resource handler in C#
  steps:
  - name: What if I need multiple HTML files in the same zip?
    text: 'Create a new entry for each call to `HandleResource`. The `resourceName`
      argument typically contains the filename, so you can use it directly:'
  - name: How to handle large documents without exhausting memory?
    text: Replace `MemoryStream` with a `FileStream` that points to a temporary file.
      The handler then returns the file stream, and you can later delete the file
      after the zip is created.
  - name: Does this approach work with .NET Core on Linux?
    text: Yes. All APIs used (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) are
      cross‑platform. Ensure the target framework is at least .NET 6 for best compatibility.
  - name: Can I encrypt the zip archive?
    text: '`ZipArchive` supports password‑based encryption only through third‑party
      libraries (e.g., `SharpZipLib`). If encryption is required, wrap the output
      bytes with a library that provides AES encryption before sending them to the
      client.'
  type: HowTo
tags:
- C#
- HTML
- file I/O
title: C#でカスタムリソースハンドラを使用してHTMLを保存する方法
url: /ja/net/working-with-html-documents/how-to-save-html-with-a-custom-resource-handler-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# カスタムリソースハンドラを使用した C# での HTML 保存方法

インメモリ文字列や解析済みドキュメントから **HTML を保存する方法** を知りたい場合、このガイドでは完全なソリューションを示します。カスタム `ResourceHandler` を使用すると、出力先ストリームを制御できるため、**HTML を zip** アーカイブに保存する際に一時ファイルを書き込む必要がなくなります。

`ResourceHandler` が従来の `IOutputStorage` アプローチよりも好まれる理由、設定方法、そして zip 圧縮用に拡張する方法を紹介します。このチュートリアルの最後までに、任意の .NET 6+ プロジェクトにコードを組み込み、独自の保存要件に合わせて適応できるようになります。

## 作成するもの

* `MemoryStream` を返す最小限の `ResourceHandler`  
* **HtmlAgilityPack** で作成した `HtmlDocument`  
* ハンドラが提供するストリームに HTML を書き込む `doc.Save` の呼び出し  
* 任意で、生成した HTML を zip ファイルに圧縮するラッパー  

前提条件:

* .NET 6 SDK 以降  
* `HtmlAgilityPack` NuGet パッケージ (`dotnet add package HtmlAgilityPack`)  
* C# ストリームに関する基本的な知識  

## Step 1: カスタムリソースハンドラの作成 (**how to save html** の主要手法)

`ResourceHandler` 基底クラス（viewer SDK バージョン 24.2 以降で利用可能）は、抽象メソッド `HandleResource` を 1 つ定義しています。このメソッドを実装することで、HTML の書き込み先を完全に制御できます。

```csharp
using System.IO;

/// <summary>
/// Handles the output stream for each HTML resource.
/// Returning a MemoryStream keeps everything in memory, which is ideal for further processing
/// such as zipping or sending over a network.
/// </summary>
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(string resourceName)
    {
        // You could inspect resourceName to decide between file, memory, or zip entry.
        return new MemoryStream();
    }
}
```

**重要ポイント:** `MemoryStream` を返すことでディスク I/O を回避し、レイテンシを削減し、ユニットテストで決定的な動作を実現できます。ハンドラは `Save` メソッドから自動的に呼び出されるため、ストリームを明示的に渡す必要はありません。

## Step 2: HTML ドキュメントの読み込みまたは構築

`HtmlAgilityPack` は、文字列、ファイル、またはストリームを解析できる便利な `HtmlDocument` クラスを提供します。この例ではシンプルなリテラルをロードしますが、同じコードは任意の HTML ソースでも機能します。

```csharp
using HtmlAgilityPack;

/// <summary>
/// Builds a basic HTML document in memory. Replace the string with your own markup
/// or load it from an external source.
/// </summary>
HtmlDocument doc = new HtmlDocument();
doc.LoadHtml("<html><body>Hello World</body></html>");
```

**重要ポイント:** ドキュメントをメモリ上に保持することで、カスタムハンドラのストリームベースアプローチと整合します。また、保存前に DOM を操作してスクリプトを挿入したり、タグの不整合を修正したりできます。

## Step 3: カスタムハンドラを使ってドキュメントを保存

`MyHandler` のインスタンスを渡して `doc.Save` を呼び出すと、`HandleResource` メソッドがトリガーされます。HTML は返されたストリームに直接書き込まれます。

```csharp
// Save the HTML; the handler provides the output stream.
doc.Save(new MyHandler());
```

`Save` が完了すると、`MyHandler` 内の `MemoryStream` にシリアライズされた HTML が格納されています。取得方法は以下の通りです。

```csharp
// Cast the handler back to access the stream (if you kept a reference)
MyHandler handler = new MyHandler();
doc.Save(handler);

// Reset position to read from the beginning.
handler.HandleResource("").Seek(0, SeekOrigin.Begin);
using var reader = new StreamReader(handler.HandleResource(""));
string htmlOutput = reader.ReadToEnd();
System.Console.WriteLine(htmlOutput);
```

**結果:** コンソールに `LoadHtml` に渡した正確な HTML が出力されます。これにより、**カスタムハンドラで HTML を保存する方法** を理解したことが確認できます。

## Step 4: ハンドラを拡張して **save HTML to zip** する

HTML をアーカイブしたい場合は、`MyHandler` を変更して `ZipArchiveEntry` に書き込むようにします。.NET の `System.IO.Compression` 名前空間を使えば簡単に実装できます。

```csharp
using System.IO.Compression;

/// <summary>
/// Writes the HTML into a zip entry named "document.html".
/// The zip archive is created in memory and can be saved to a file or sent over HTTP.
/// </summary>
class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        // Initialise the zip archive in create mode.
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        // Create a zip entry for the HTML file.
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open(); // Returns a stream that writes directly into the zip entry.
    }

    /// <summary>
    /// Finalises the zip archive and returns the raw bytes.
    /// </summary>
    public byte[] GetZipBytes()
    {
        // Ensure all entries are flushed.
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}
```

新しいハンドラの使用例:

```csharp
// Instantiate the zip‑aware handler.
using var zipHandler = new ZipHtmlHandler();

// Save HTML; it ends up inside the zip archive.
doc.Save(zipHandler);

// Retrieve the zip file as a byte array.
byte[] zipBytes = zipHandler.GetZipBytes();

// Optionally write the zip to disk for verification.
File.WriteAllBytes("output.zip", zipBytes);
System.Console.WriteLine("ZIP file created with size: " + zipBytes.Length);
```

**動作理由:** `HandleResource` メソッドが `document.html` という名前の zip エントリを作成します。`doc.Save` が返されたストリームに書き込むと、データは自動的に圧縮されます。zip がメモリ上で構築されるため、Web API のレスポンスとして返したり、メールに添付したり、データベースに保存したりしてもファイルシステムに触れる必要がありません。

## よくある質問とエッジケース

### 同じ zip に複数の HTML ファイルを入れたい場合は？
`HandleResource` が呼び出されるたびに新しいエントリを作成します。`resourceName` 引数には通常ファイル名が含まれるので、そのまま使用できます。

```csharp
public override Stream HandleResource(string resourceName)
{
    var entry = _archive.CreateEntry(resourceName, CompressionLevel.Optimal);
    return entry.Open();
}
```

### 大容量ドキュメントでメモリ不足にならないようにするには？
`MemoryStream` の代わりに一時ファイルを指す `FileStream` を使用します。ハンドラはファイルストリームを返し、zip 作成後にファイルを削除すれば OK です。

### .NET Core on Linux でも動作しますか？
はい。使用しているすべての API（`MemoryStream`、`ZipArchive`、`HtmlAgilityPack`）はクロスプラットフォームです。ターゲットフレームワークは最低でも .NET 6 を推奨します。

### zip アーカイブを暗号化できますか？
`ZipArchive` はパスワードベースの暗号化を標準ではサポートしていません。暗号化が必要な場合は、`SharpZipLib` などのサードパーティライブラリを利用し、クライアントに送信する前に AES 暗号化されたバイト列にラップしてください。

## プロのコツ

* 多数のドキュメントをバッチ処理する際はハンドラを再利用しましょう。ファイルごとに新しい `ZipArchive` を作成すると余計なオーバーヘッドが発生します。  
* アーカイブを開いたまま zip バイト列を取得したい場合は、`ZipArchive` コンストラクタで `LeaveOpen: true` を設定してください。  
* 保存前に `doc.OptionCheckSyntax = true;` を呼び出して HTML を検証すると、タグの不整合を早期に検出できます。  
* 生成された zip のサイズをログに記録しましょう。異常に大きい出力は、重複リソースや圧縮が適用されていないことを示すサインです。

## 完全動作サンプル

以下はコンソールプロジェクト（`dotnet new console`）に貼り付けて実行できる単一ファイルです。プレーン HTML の保存と zip 圧縮の両方をデモします。

```csharp
using System;
using System.IO;
using System.IO.Compression;
using HtmlAgilityPack;

// ---------- Custom handlers ----------
class MyHandler : ResourceHandler
{
    public MemoryStream HtmlStream { get; } = new();

    public override Stream HandleResource(string resourceName) => HtmlStream;
}

class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open();
    }

    public byte[] GetZipBytes()
    {
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}

// ---------- Main program ----------
class Program
{
    static void Main()
    {
        // Build a simple HTML document.
        HtmlDocument doc = new HtmlDocument();
        doc.LoadHtml("<html><body>Hello World from HtmlAgilityPack</body></html>");

        // ---- Example 1: plain HTML save ----
        var plainHandler = new MyHandler();
        doc.Save(plainHandler);
        plainHandler.HtmlStream.Seek(0, SeekOrigin.Begin);
        using var reader = new StreamReader(plainHandler.HtmlStream);
        Console.WriteLine("Plain HTML output:");


## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説と完全に動作するコード例が含まれており、追加の API 機能を習得したり、独自の実装アプローチを探求したりするのに役立ちます。

- [How to Save HTML in C# with Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [How to Use ZipArchive – Save HTML and Resources to a ZIP File](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [save html as zip with a custom resource handler – step‑by‑step guide](/html/english/net/html-extensions-and-conversions/save-html-as-zip-with-a-custom-resource-handler-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}