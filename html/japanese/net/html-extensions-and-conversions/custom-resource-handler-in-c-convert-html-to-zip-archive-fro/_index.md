---
category: general
date: 2026-02-13
description: C#でカスタムリソースハンドラを構築し、HTMLをZIPアーカイブに変換する方法を学び、Aspose.HTMLを使用してメモリ上でZIPを作成するステップバイステップガイド。
draft: false
keywords:
- custom resource handler
- convert html zip archive
- create zip from memory
- Aspose HTML
- in‑memory streaming
- C# zip compression
language: ja
og_description: カスタムリソースハンドラを使用して、HTML をメモリ上で直接 ZIP アーカイブに変換する完全な C# ソリューションをご紹介します。
og_title: カスタムリソースハンドラ – メモリ上のHTMLをZIPに変換
tags:
- C#
- Aspose.HTML
- ZipArchive
- MemoryStream
title: C# のカスタムリソースハンドラ – メモリ上の HTML を ZIP アーカイブに変換
url: /ja/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-archive-fro/
---

< blocks/products/products-backtop-button >}}

All preserved.

Make sure we keep markdown formatting, code block placeholders unchanged.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# カスタムリソースハンドラ – メモリ上で HTML を ZIP アーカイブに変換

Ever needed a **custom resource handler** to grab every image, CSS file, or script that an HTML page pulls in, and then zip everything up without touching the disk? You're not the only one. In many web‑automation or email‑templating scenarios you want the whole page bundled as a single, portable package, and you’d rather keep everything in RAM for speed and security.

HTML ページが取得するすべての画像、CSS ファイル、スクリプトを取得し、ディスクに触れずにすべてを zip したい **custom resource handler** が必要になったことはありませんか？ あなただけではありません。多くのウェブ自動化やメールテンプレートのシナリオでは、ページ全体を単一のポータブルパッケージとしてまとめ、速度とセキュリティのためにすべてを RAM 上に保持したいものです。

In this tutorial we’ll walk through a complete, runnable example that shows you exactly how to **convert HTML zip archive** using a **custom resource handler** and then **create zip from memory** with .NET’s `System.IO.Compression`. By the end you’ll have a self‑contained method that you can drop into any C# project that uses Aspose.HTML.

このチュートリアルでは、**custom resource handler** を使用して **convert HTML zip archive** を行い、.NET の `System.IO.Compression` で **create zip from memory** を実現する、完全で実行可能なサンプルを順に解説します。最後まで読むと、Aspose.HTML を使用する任意の C# プロジェクトに組み込める自己完結型メソッドが手に入ります。

## 必要なもの

- .NET 6+（または .NET Framework 4.7.2+）  
- Aspose.HTML for .NET（NuGet パッケージ `Aspose.HTML`）  
- ストリームと `ZipArchive` クラスに関する基本的な知識  

外部ツールや一時ファイルは不要で、純粋にメモリ上で処理します。

## ステップ 1: カスタムリソースハンドラの定義

The heart of the solution is a class that inherits from `Aspose.Html.ResourceHandler`. Its job is to supply a fresh `Stream` for each external resource the HTML engine requests. By returning a new `MemoryStream` each time we keep the data isolated and ready for later packaging.

このソリューションの核心は `Aspose.Html.ResourceHandler` を継承したクラスです。このクラスは、HTML エンジンが要求する外部リソースごとに新しい `Stream` を提供する役割を担います。毎回新しい `MemoryStream` を返すことで、データを分離し、後でパッケージ化できる状態に保ちます。

```csharp
using System.IO;
using Aspose.Html;

// Step 1 – Custom handler that stores resources in memory
class MemoryResourceHandler : ResourceHandler
{
    // The framework calls this method for every external resource (images, CSS, etc.)
    public override Stream HandleResource(Resource resource)
    {
        // We give the engine an empty stream; later we’ll fill it with the actual bytes.
        // Using MemoryStream means everything stays in RAM.
        return new MemoryStream();
    }
}
```

**この点が重要な理由:**  
Aspose.HTML にリソースを書き込ませると、後でそれらをクリーンアップする必要があります。インメモリハンドラを使用すれば I/O のオーバーヘッドがなくなり、サンドボックス環境（例: Azure Functions）でも安全にコードを実行できます。

## ステップ 2: HTML ドキュメントの読み込み

Next, point Aspose.HTML at the HTML file you want to package. The document can be on disk, a URL, or even a raw string. Here we use a file path for simplicity.

次に、パッケージ化したい HTML ファイルを Aspose.HTML に指定します。ドキュメントはディスク上のファイル、URL、あるいは生の文字列でも構いません。ここでは簡単のためファイルパスを使用します。

```csharp
using Aspose.Html;

// Step 2 – Load the source HTML
HtmlDocument document = new HtmlDocument("YOUR_DIRECTORY/input.html");
```

> **プロ・チップ:** HTML が相対リソースを参照している場合、`input.html` がそれらのアセットと同じフォルダーにあることを確認してください。そうでないとハンドラがリソースを見つけられません。

## ステップ 3: ハンドラを設定し、MemoryStream に保存

Now we instantiate the handler and tell Aspose.HTML to use it via `HtmlSaveOptions.OutputStorage`. The resulting HTML (including rewritten resource URLs) lands in a `MemoryStream`.

ここでハンドラのインスタンスを作成し、`HtmlSaveOptions.OutputStorage` を介して Aspose.HTML に使用させます。結果として得られる HTML（リライトされたリソース URL を含む）は `MemoryStream` に格納されます。

```csharp
using Aspose.Html.Saving;
using System.IO;

// Step 3 – Prepare the handler and an in‑memory buffer for the final HTML
var resourceHandler = new MemoryResourceHandler();

using (MemoryStream htmlMemoryStream = new MemoryStream())
{
    document.Save(htmlMemoryStream, new HtmlSaveOptions
    {
        OutputStorage = resourceHandler // redirects all resources to the handler
    });

    // At this point htmlMemoryStream contains the full HTML file,
    // while each external resource resides in the streams returned by the handler.
```

**内部で何が起きているか:**  
`document.Save` が実行されると、Aspose.HTML は各リソースに対して `MemoryResourceHandler` にストリームを要求します。空の `MemoryStream` を返すので、エンジンは生のバイト列を直接メモリに書き込みます。一時ファイルは作成されません。

## ステップ 4: ZIP アーカイブを完全にメモリ上で組み立てる

Now comes the fun part: we’ll create a `ZipArchive` that lives inside another `MemoryStream`. This lets us **create zip from memory** without ever touching the file system.

さあ楽しいパートです: 別の `MemoryStream` 内に `ZipArchive` を作成します。これにより、ファイルシステムに触れることなく **create zip from memory** が可能になります。

```csharp
    // Step 4 – Build the ZIP archive in memory
    using (MemoryStream zipMemoryStream = new MemoryStream())
    using (var zipArchive = new ZipArchive(zipMemoryStream, ZipArchiveMode.Create, leaveOpen: true))
    {
        // 4a – Add the main HTML file
        var htmlEntry = zipArchive.CreateEntry("index.html");
        using (var entryStream = htmlEntry.Open())
        {
            // Reset the position of the HTML stream before copying
            htmlMemoryStream.Position = 0;
            htmlMemoryStream.CopyTo(entryStream);
        }

        // 4b – Add each resource that the handler captured
        // The handler stored each resource in a fresh MemoryStream, which we can enumerate.
        // For demonstration, assume we kept a list of those streams (you could store them in a dictionary).
        // Example placeholder – replace with your actual collection:
        // foreach (var kvp in capturedResources)
        // {
        //     var resourceEntry = zipArchive.CreateEntry(kvp.Key); // kvp.Key = relative path
        //     using var entry = resourceEntry.Open();
        //     kvp.Value.Position = 0;
        //     kvp.Value.CopyTo(entry);
        // }

        // When we’re done, flush everything
        zipArchive.Dispose(); // optional because of using, but makes intent clear
    }

    // At this stage zipMemoryStream holds the complete ZIP file.
    // You can return it, write it to a response stream, or save it to disk if you wish.
}
```

> **注:** コメントアウトされた部分は、`MemoryResourceHandler` 内でストリームを収集する方法の例です。本番環境では、各 `MemoryStream` を元のリソース URL をキーとした辞書に保存し、ここで反復処理してアーカイブに追加します。

**ZIP をメモリ上に保持する理由:**  
アーカイブを `MemoryStream` に保存すれば、HTTP クライアント（ASP.NET Core の `FileResult` など）へ直接送信したり、途中のファイルを介さずにクラウドストレージへアップロードしたりするのが非常に簡単になります。

## ステップ 5: (オプション) ZIP をディスクに保存

If you still need a physical file—maybe for debugging—just write the `zipMemoryStream` to disk:

デバッグなどで物理ファイルが必要な場合は、`zipMemoryStream` をディスクに書き出すだけです。

```csharp
// Optional: write the in‑memory ZIP to a file for inspection
File.WriteAllBytes("YOUR_DIRECTORY/output.zip", zipMemoryStream.ToArray());
```

## 完全な動作例

Putting everything together, here’s a single, copy‑paste‑ready program that **converts HTML to a ZIP archive** entirely in memory.

すべてを組み合わせた、メモリ上だけで **converts HTML to a ZIP archive** を実現する、コピー＆ペースト可能な単一プログラムをご紹介します。

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class MemoryResourceHandler : ResourceHandler
{
    // Capture each resource in a dictionary for later retrieval
    public static readonly System.Collections.Generic.Dictionary<string, MemoryStream> Captured = new();

    public override Stream HandleResource(Resource resource)
    {
        var ms = new MemoryStream();
        // Store the stream using the resource's absolute URL as the key
        Captured[resource.Uri.AbsoluteUri] = ms;
        return ms;
    }
}

class Program
{
    static void Main()
    {
        // Load the HTML file
        HtmlDocument doc = new HtmlDocument("YOUR_DIRECTORY/input.html");

        // Attach the custom handler
        var handler = new MemoryResourceHandler();

        // Save HTML + resources to memory
        using var htmlStream = new MemoryStream();
        doc.Save(htmlStream, new HtmlSaveOptions { OutputStorage = handler });

        // Create the ZIP archive in memory
        using var zipStream = new MemoryStream();
        using (var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, true))
        {
            // Add the HTML file
            var htmlEntry = zip.CreateEntry("index.html");
            using (var entry = htmlEntry.Open())
            {
                htmlStream.Position = 0;
                htmlStream.CopyTo(entry);
            }

            // Add each captured resource
            foreach (var kvp in MemoryResourceHandler.Captured)
            {
                // Derive a sane relative path from the URL
                var uri = new Uri(kvp.Key);
                var relativePath = uri.AbsolutePath.TrimStart('/');
                var resEntry = zip.CreateEntry(relativePath);
                using var entry = resEntry.Open();
                kvp.Value.Position = 0;
                kvp.Value.CopyTo(entry);
            }
        }

        // The ZIP is ready – write it out or return it from a web API
        File.WriteAllBytes("YOUR_DIRECTORY/output.zip", zipStream.ToArray());

        Console.WriteLine("HTML successfully packaged into output.zip");
    }
}
```

### 期待される結果

Running the program creates `output.zip` containing:

- `index.html` – the rewritten HTML that points to the bundled resources.  
- All images, CSS, and JavaScript files that the original page referenced, stored using their original relative paths.

プログラムを実行すると、以下を含む `output.zip` が作成されます：

- `index.html` – バンドルされたリソースを指すように書き換えられた HTML。  
- 元のページが参照していたすべての画像、CSS、JavaScript ファイルが、元の相対パスのまま保存されます。

Open `index.html` from the ZIP in any browser and you’ll see the page render exactly as it did when it was on the file system.

ZIP 内の `index.html` を任意のブラウザで開くと、ファイルシステム上にあったときと同じようにページが正しく表示されます。

## よくある質問とエッジケース

| Question | Answer |
|----------|--------|
| **リソースが非常に大きい（例: ビデオ）場合はどうしますか？** | すべてがメモリ上にあるため、非常に大きなファイルは `OutOfMemoryException` を引き起こす可能性があります。その場合は、一時ファイルに直接ストリームするか、受け入れるサイズを制限してください。 |
| **重複するリソース URL を処理する必要がありますか？** | ハンドラの辞書は重複を上書きします。1 つだけ保持したい場合は、追加前に `Captured.ContainsKey` を確認してください。 |
| **ASP.NET Core のコントローラで使用できますか？** | もちろんです。アクションメソッドから `File(zipStream.ToArray(), "application/zip", "page.zip")` を返せば利用できます。 |
| **HTTPS リソースはどう扱いますか？** | ランタイムが SSL 証明書を信頼している限り、Aspose.HTML は自動的にダウンロードします。自己署名証明書の場合は、`ServicePointManager.ServerCertificateValidationCallback` を設定してください。 |
| **カスタムハンドラはスレッドセーフですか？** | この例では static 辞書を使用しており、*スレッドセーフではありません*。多数のドキュメントを同時に処理する場合は、ロックで保護するか `ConcurrentDictionary` を使用してください。 |

## 本番環境でのプロ・ティップ

- **Reuse the handler** は単一のドキュメントに対してのみ再利用してください。リクエストごとに新しいインスタンスを作成し、ユーザー間のクロストークを防ぎます。  
- **Dispose streams** を速やかに行いましょう。`using` ブロックで多くの場合は対応できますが、辞書に保存したストリームは ZIP 作成後に必ず破棄してください。  
- **Validate the HTML** を事前に実行し、ハンドラが予期しないリソースを要求する原因となる不正なマークアップを検出します。  
- ファイルサイズが重要な場合は、`ZipArchiveEntry.CompressionLevel = CompressionLevel.Optimal` を設定して圧縮率を高めましょう。

## 結論

ここまでで、HTML ページを通じて **custom resource handler** を活用し、すべてのリンクされたアセットを取得し、ディスクに触れることなく **create zip from memory** を実現するために必要なすべてを説明しました。このパターンは、ウェブサービス、バックグラウンドジョブ、あるいは自己完結型 HTML バンドルを配布するデスクトップユーティリティなど、さまざまなシナリオに柔軟に対応できます。

ぜひ試してみてください。`YOUR_DIRECTORY/input.html` を任意のページに置き換え、ハンドラを `ConcurrentDictionary` にリソースを保存するよう調整すれば、本番環境でも使える堅牢なインメモリ HTML‑to‑ZIP パイプラインが手に入ります。

---

*レベルアップの準備はできましたか？* 次は Aspose.HTML を使って **convert HTML to PDF** を試したり、ZIP を暗号化してセキュリティを高める実験をしてみましょう。C# でインメモリストリーミングをマスターすれば、可能性は無限です。コーディングを楽しんでください！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}