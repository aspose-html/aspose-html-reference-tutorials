---
category: general
date: 2026-02-10
description: カスタムリソースハンドラを使用すると、C#でHTMLをZIPに変換できます。HTMLをZIPとして保存し、HTMLリソースを効率的にストリーミングする方法をご紹介します。
draft: false
keywords:
- custom resource handler
- convert html to zip
- save html as zip
- create zip with html
- stream html resources
language: ja
og_description: カスタムリソースハンドラを使用すると、C#でHTMLをZIPに変換できます。このステップバイステップガイドに従って、HTMLをZIPとして保存し、HTMLリソースをストリーミングしましょう。
og_title: C# のカスタムリソースハンドラ – HTML を ZIP に変換
tags:
- Aspose.HTML
- C#
- ZIP archive
- file streaming
title: C# のカスタムリソースハンドラ – HTML を ZIP に変換するチュートリアル
url: /ja/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# カスタムリソースハンドラ – C# で HTML を ZIP に変換

生の HTML から直接 ZIP ファイルへ **カスタムリソースハンドラ** で変換したいと思ったことはありませんか？同じ悩みを抱える開発者は多いです。HTML ページとそのアセットを一時ファイルをディスクに残さずにまとめたいとき、壁にぶつかります。良いニュースは、Aspose.HTML を使えばすべてメモリ上で完結でき、その鍵となるのがカスタムリソースハンドラです。

このチュートリアルでは、**HTML を ZIP に変換**、**HTML を ZIP として保存**、そして **HTML リソースをオンザフライでストリーム** する完全な実行可能サンプルを順を追って解説します。最後まで読めば、HTML 文字列を受け取り、ページとすべてのリンクリソースを含む `result.zip` を即座にダウンロードできる単一メソッドが手に入ります。

> **Prerequisites** – .NET 6+（または .NET Framework 4.6+）、Aspose.HTML for .NET がインストール済み、そしてストリームの基本的な知識があれば OK。外部ツールは不要です。

---

## カスタムリソースハンドラ – 基本概念

Aspose.HTML における *リソースハンドラ* は、ドキュメントの各要素が **どこに出力されるか** を決定するオブジェクトです。ディスク上のファイル、メモリバッファ、あるいは今回示すように ZIP アーカイブ内のエントリへと出力先を選べます。`ResourceHandler` を継承すれば、メイン HTML ファイル **と** すべての補助リソース（CSS、画像、フォント等）の出力先を完全にコントロールできます。

これをドキュメント資産の交通整理係と考えてください。`HandleResource` メソッドがメイン HTML 用の `Stream` を提供し、`ResourceSaving` イベントが各依存ファイルを書き込む直前に割り込むことを可能にします。

---

## 手順 1: カスタムリソースハンドラの実装

まず、`ResourceHandler` を継承したクラスを作成します。`HandleResource` をオーバーライドして、メイン HTML 出力用に新しい `MemoryStream` を Aspose に渡します。リンクされたアセットについては後ほど `ResourceSaving` でフックします。

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using System.IO;

/// <summary>
/// Supplies a stream for every resource the HTML document needs to save.
/// </summary>
class MyHandler : ResourceHandler
{
    /// <summary>
    /// Returns a new stream for the main HTML content.
    /// </summary>
    public override Stream HandleResource(ResourceInfo info)
    {
        // In real life you might return a FileStream or a ZipEntry stream.
        // Here we just hand back a clean MemoryStream.
        return new MemoryStream();
    }
}
```

**重要ポイント:** 新しい `MemoryStream` を返すことで、HTML がファイルシステムに触れることはありません。これが後述のクリーンなインメモリ ZIP 作成の土台となります。

---

## 手順 2: HTML を単一の MemoryStream に保存

ハンドラが用意できたので、HTML ドキュメントを生成し、完全にメモリ上にキャプチャします。このステップは ZIP が必要ない場合は省略可能ですが、ハンドラの単体動作を確認するのに役立ちます。

```csharp
using Aspose.Html;

// Sample HTML – replace with your own markup or load from a file.
string htmlContent = "<html><head><title>Demo</title></head><body>Hello world!</body></html>";

// Create the document from a string.
HTMLDocument htmlDocument = new HTMLDocument(htmlContent);

// Instantiate our custom handler.
MyHandler memoryHandler = new MyHandler();

using (MemoryStream htmlStream = new MemoryStream())
{
    // Save triggers HandleResource and writes the HTML into htmlStream.
    htmlDocument.Save(htmlStream, memoryHandler);

    // Reset position for potential reading.
    htmlStream.Position = 0;

    // For demo purposes, dump the HTML to console.
    using (StreamReader reader = new StreamReader(htmlStream))
    {
        Console.WriteLine("Generated HTML:");
        Console.WriteLine(reader.ReadToEnd());
    }
}
```

**期待される出力**（可読性のため整形）:

```
Generated HTML:
<html><head><title>Demo</title></head><body>Hello world!</body></html>
```

このスニペットを実行すると、HTML が RAM のみで保持され、一時ファイルは作成されません。

---

## 手順 3: HTML とリソースを ZIP アーカイブにパッケージ化

いよいよ本題です。HTML **と** すべての参照アセットを、ディスクに中間ファイルを書き込むことなく ZIP ファイルにまとめます。`System.IO.Compression.ZipArchive` と `ResourceSaving` イベントを組み合わせます。

```csharp
using Aspose.Html;
using System.IO;
using System.IO.Compression;

// Re‑use the same HTMLDocument from the previous step.
HTMLDocument htmlDocument = new HTMLDocument("<html><body>Hello world!</body></html>");

// Path where the final ZIP will be written.
string zipPath = Path.Combine(Environment.CurrentDirectory, "result.zip");

// Open a FileStream for the ZIP file.
using (FileStream zipFile = new FileStream(zipPath, FileMode.Create))
using (ZipArchive zipArchive = new ZipArchive(zipFile, ZipArchiveMode.Update))
{
    // Create a fresh handler for the ZIP operation.
    MyHandler zipHandler = new MyHandler();

    // Hook the ResourceSaving event – this fires for every resource.
    zipHandler.ResourceSaving += (sender, e) =>
    {
        // Ensure we don't create leading folder entries like "/css/style.css".
        string entryName = e.ResourceInfo.Path.TrimStart('/');

        // Create a new entry inside the ZIP.
        ZipArchiveEntry entry = zipArchive.CreateEntry(entryName);

        // Provide the stream that Aspose will write into.
        e.Stream = entry.Open();
    };

    // Save the document; the handler will fill the ZIP for us.
    htmlDocument.Save(zipHandler);
}

// Verify the ZIP exists.
Console.WriteLine($"ZIP created at: {zipPath}");
```

### 背後で何が起きているか？

1. **`ResourceSaving` が** メイン HTML と各リンクアセットごとに発火  
2. ラムダ式で開いている ZIP 内に対応するエントリを `CreateEntry` で作成  
3. `e.Stream = entry.Open()` により、Aspose に対して ZIP エントリへ直接書き込むストリームを提供  
4. `htmlDocument.Save` が完了すると、ZIP には完全な HTML ページと、マークアップが参照する CSS、画像、フォントがすべて格納されます  

**結果:** `result.zip` という単一ファイルが生成され、ブラウザへ配信したり、メールに添付したり、Blob ストレージに保存したりできます。一時ファイルは一切残りません。

---

## ボーナス: Web API で ZIP を利用する

ASP.NET Core のエンドポイントでオンデマンドに ZIP を返したい場合も同様のロジックが使えます。以下はコンパクトなコントローラアクションです。

```csharp
[ApiController]
[Route("api/[controller]")]
public class HtmlZipController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult DownloadZip()
    {
        // Build the document (could be loaded from a DB, etc.).
        var html = "<html><body><h1>Dynamic report</h1></body></html>";
        var doc = new HTMLDocument(html);
        var handler = new MyHandler();

        // Prepare an in‑memory ZIP.
        using var zipStream = new MemoryStream();
        using (var archive = new ZipArchive(zipStream, ZipArchiveMode.Create, true))
        {
            handler.ResourceSaving += (s, e) =>
            {
                var entry = archive.CreateEntry(e.ResourceInfo.Path.TrimStart('/'));
                e.Stream = entry.Open();
            };
            doc.Save(handler);
        }

        zipStream.Position = 0;
        return File(zipStream, "application/zip", "report.zip");
    }
}
```

これで `/api/HtmlZip/download` への GET リクエストは、生成された ZIP をクライアントへ直接ストリーム配信します。レポートをその場で生成するシナリオに最適です。

---

## よくある落とし穴とプロのコツ

| 問題 | 発生理由 | 対策 |
|------|----------|------|
| **ZIP 内に空フォルダができる** | `ResourceInfo.Path` が先頭に `/` を含むためエントリが `/` になる | イベントハンドラ内で `TrimStart('/')` を使用 |
| **画像が欠落する** | 絶対 URL で参照された画像は自動取得されない | `htmlDocument.Options.ResourceLoading = ResourceLoadingMode.Stream` を設定し、リモート資産を取得するカスタム `ResourceHandler` を提供 |
| **大容量ファイルでメモリ圧迫** | すべてのストリームが ZIP が閉じるまでメモリに保持される | `ZipArchiveMode.Update` ではなく `Create` を使用し、各エントリをバッファせずに直接書き込むか、サイズが RAM を超える場合はディスクストリームへ切り替える |
| **例外 “The stream does not support seeking”** | 非シーク可能ストリームを複数リソースで再利用しようとした | 各リソースに対して常に新しい `MemoryStream` または `entry.Open()` を提供 |

---

## 結論

**カスタムリソースハンドラ** を使えば、**HTML を ZIP に変換**、**HTML を ZIP として保存**、そして **HTML リソースをストリーム** しながらファイルシステムに触れずに処理できることを実証しました。`HandleResource` のオーバーライドと `ResourceSaving` へのフックにより、Aspose.HTML が出力するすべてのバイトを細かく制御できます。

このパターンはスケールします。インメモリ `MemoryStream` をクラウドの BLOB ストリームに置き換えたり、圧縮設定を追加したり、資産のパッケージングを監査するロギング層を組み込んだりと、リソースパイプラインを所有すれば可能性は無限です。

次のステップに進む準備はできましたか？HTML に CSS と画像を埋め込んでみたり、リモートリソースの読み込みを試したり、Azure Function に組み込んでオンデマンドで ZIP を返すフローを構築したりしてください。Happy coding!

--- 

*カスタムリソースハンドラが HTML を ZIP ファイルに変換する流れを示す画像。*

![カスタムリソースハンドラのワークフロー](https://example.com/placeholder-image.png "カスタムリソースハンドラのワークフロー")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}