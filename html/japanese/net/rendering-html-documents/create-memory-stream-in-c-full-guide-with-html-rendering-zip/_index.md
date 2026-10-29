---
category: general
date: 2026-03-31
description: C#でメモリストリームを作成し、HTMLをPNGにレンダリングする方法を学び、カスタムリソースハンドラを使用し、HTMLをZIPに保存し、フォントスタイルをプログラムで設定する—すべてを一つのチュートリアルで。
draft: false
keywords:
- create memory stream
- render html to png
- custom resource handler
- save html to zip
- set font style programmatically
language: ja
og_description: C#でメモリストリームを作成し、HTMLを即座にPNGにレンダリングし、カスタムリソースハンドラを使用し、HTMLをZIPに保存し、フォントスタイルをプログラムで設定する。
og_title: C#でメモリストリームを作成する – 完全プログラミングガイド
tags:
- C#
- HTML rendering
- Streams
- ZIP archives
- Image processing
title: C#でメモリストリームを作成する – HTMLレンダリングとZIPエクスポートを含む完全ガイド
url: /ja/net/rendering-html-documents/create-memory-stream-in-c-full-guide-with-html-rendering-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Memory Stream を作成 – HTML レンダリングと ZIP エクスポートの完全ガイド

HTML ドキュメントを PNG 画像や ZIP ファイルに変換したり、実行時にフォントスタイルを変更したりしたいと考えたことはありませんか？ あなただけではありません。多くの開発者が、ドキュメントのインメモリ表現が必要なのにファイルシステムに触れたくないという壁にぶつかります。

このチュートリアルでは、エンドツーエンドの完全なソリューションを順を追って解説します。カスタムリソースハンドラを作成し、HTML を `MemoryStream` に流し込み、同じドキュメントを ZIP に圧縮し、最後にアンチエイリアス付きで画像にレンダリングします。これを終えると、**HTML を PNG にレンダリング**、**HTML を ZIP に保存**、**フォントスタイルをプログラムで設定**できるようになり、ディスクに一時ファイルを書き込む必要がなくなります。

## 前提条件

- .NET 6.0 以降（API は最近のバージョンで安定しています）。  
- `HTMLDocument`、`ImageRenderer` などの型を提供する HTML‑to‑image ライブラリへの参照例：**HtmlRenderer.Core**（使用している実際のパッケージに置き換えてください）。  
- ストリーム、`using` 文、C# のオブジェクト指向パターンに関する基本的な知識。

> **プロのコツ:** Visual Studio を使用している場合は、**nullable 参照型**（`<Nullable>enable</Nullable>`）を有効にして、微妙なバグを早期に検出しましょう。

## 手順 1: カスタムリソースハンドラで Memory Stream を作成

最初に必要なのは、HTML エンジンに対して *どこに* 各リソース（画像、CSS など）を書き込むかを指示するハンドラです。`ResourceHandler` を継承することで、すべての出力を単一の `MemoryStream` に向けることができます。

```csharp
using System;
using System.IO;

// Step 1: Define a handler that writes resources to an in‑memory stream
class MemoryResourceHandler : ResourceHandler
{
    // The stream lives for the whole lifetime of the handler
    public MemoryStream OutputStream = new MemoryStream();

    // The engine calls this for every resource it needs to write
    public override Stream HandleResource(ResourceInfo info) => OutputStream;
}
```

**重要ポイント:**  
`MemoryStream` は完全に RAM 上に存在するためディスク I/O が発生せず、Web サービスやユニットテストなど高パフォーマンスが求められるシナリオに最適です。また、ハンドラはエンジンが各リソースに `Stream` を期待しているため、API も満足します。

## 手順 2: HTML ドキュメントを読み込み Memory Stream に保存

既存の HTML ファイル（または文字列）を読み込み、先ほど作成した `MemoryResourceHandler` を使用するよう指示します。`Save` 呼び出しの後、`OutputStream` には完全な HTML ペイロードが格納されています。

```csharp
using System.IO;

// Assume the HTML file lives under YOUR_DIRECTORY
HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");

// Instantiate the memory handler
MemoryResourceHandler memoryHandler = new MemoryResourceHandler();

// Save the document – all resources flow into the same MemoryStream
htmlDoc.Save(memoryHandler);
```

この時点でストリームの位置は末尾にあるため、内容を読み取る前にシークして巻き戻す必要があります。

```csharp
// Reset the stream position to the beginning
memoryHandler.OutputStream.Position = 0;

// Quick verification (optional)
// string htmlContent = new StreamReader(memoryHandler.OutputStream).ReadToEnd();
// Console.WriteLine(htmlContent);
```

> **注:** 上記の `ReadToEnd` 行はコメントアウトされています。実運用ではストリームを別コンポーネントに渡すことが多く、コンソールに出力するだけではありません。

## 手順 3: カスタム ZIP リソースハンドラで同じ HTML を圧縮

HTML とそのアセットを一緒に配布したいケースがあります。2 つ目のカスタムハンドラを使えば、各リソースをその場で ZIP エントリに変換できます。

```csharp
using System.IO.Compression;

// Step 4: Define a handler that writes each resource into a ZIP archive
class ZipResourceHandler : ResourceHandler, IDisposable
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(string zipPath)
    {
        // Open (or create) the archive in write mode
        _zipArchive = ZipFile.Open(zipPath, ZipArchiveMode.Create);
    }

    // The engine calls this for each resource; we create a ZIP entry with the same name
    public override Stream HandleResource(ResourceInfo info) =>
        _zipArchive.CreateEntry(info.Name).Open();

    // Proper disposal of the underlying ZipArchive
    protected override void Dispose(bool disposing)
    {
        if (disposing) _zipArchive.Dispose();
        base.Dispose(disposing);
    }

    public void Dispose() => Dispose(true);
}
```

同じ `htmlDoc` インスタンスを再利用し、ZIP ファイルに書き込みます。

```csharp
// Step 5: Save the HTML document into a ZIP file
using (var zipHandler = new ZipResourceHandler("YOUR_DIRECTORY/output.zip"))
{
    htmlDoc.Save(zipHandler);
}
```

**エッジケースのヒント:** HTML が同一画像を複数回参照している場合、ZIP ハンドラは重複エントリを作成してしまいます。これを防ぐには、既に追加済みの名前を保持する `HashSet<string>` を用意し、既存エントリのストリームを返すようにします。

## 手順 4: デフォルトスタイルシートでフォントスタイルをプログラム的に設定

ソース HTML を触らずにドキュメントの見た目を変更できるのは便利です。たとえば、PDF プレビュー用にヘッダーを太字にしたい場合などです。ライブラリは `DefaultViewStyleSheet` を公開しているので、ここをいじります。

```csharp
// Step 6: Apply bold and italic styling to the default view stylesheet
htmlDoc.DefaultViewStyleSheet.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

`WebFontStyle` に定義されたフラグを自由に組み合わせられます。変更は即時に反映され、以降のレンダリングや保存に影響します。

## 手順 5: HTML ドキュメントを PNG 画像にレンダリング

最後に、HTML をラスタ画像に変換します。アンチエイリアスとヒンティングを有効にすれば、テキストはくっきり、エッジは滑らかになります。

```csharp
using System.Drawing; // For ImageRenderingOptions if needed

// Step 7: Render the document to an image with antialiasing and hinting
var renderingOptions = new ImageRenderingOptions
{
    UseAntialiasing = true,
    UseHinting = true
};

new ImageRenderer(renderingOptions).Render(htmlDoc, "YOUR_DIRECTORY/out.png");
```

**期待される結果:** `YOUR_DIRECTORY` 配下に `out.png` という名前の PNG が生成され、ブラウザで表示される HTML と同一の見た目になります（先ほど設定した太字‑斜体スタイルが適用されています）。

![メモリストリーム出力のスクリーンショット](placeholder-image.png "メモリストリーム例")

*画像の alt テキストは主要キーワードを含めて SEO 対策を行っています。*

## よくある質問と落とし穴

| 質問 | 回答 |
|----------|--------|
| **`HTMLDocument` を ZIP に保存した後でも再利用できますか？** | はい。ドキュメントオブジェクトはメモリ上に残っているので、異なるハンドラを指定して `Save` を何度でも呼び出せます。 |
| **HTML に大容量のバイナリ資産が含まれる場合は？** | `MemoryStream` はそれに応じてサイズが増大します。非常に大きなファイルの場合は、直接ファイルへストリーミングするか `BufferedStream` の使用を検討してください。 |
| **`MemoryResourceHandler` の `Dispose` は必要ですか？** | 必須ではありません。ハンドラは `MemoryStream` だけを保持しており、ガベージコレクション時に破棄されます。ただし、明示的に `Dispose` を呼び出す習慣は推奨されます。 |
| **画像形式を PNG 以外（例: JPEG）に変更するには？** | `ImageRenderer.Render` に別の拡張子を渡すか、`ImageRenderer.RenderToBitmap` を使用してから `bitmap.Save("out.jpg", ImageFormat.Jpeg)` で保存します。 |
| **ZIP ハンドラはスレッドセーフですか？** | いいえ。`ZipArchive` はスレッドセーフではないため、アクセスをシリアライズするか、スレッドごとに別ハンドラを作成してください。 |

## 完全動作サンプル

以下は、ここまで説明したすべての手順を実装した、コピー＆ペーストだけで動作するプログラムです。`YOUR_DIRECTORY` を実際のパスに置き換えてください。

```csharp
// FullExample.cs
using System;
using System.IO;
using System.IO.Compression;

// Assume these types come from your HTML rendering library
using HtmlRendering; // placeholder namespace

class MemoryResourceHandler : ResourceHandler
{
    public MemoryStream OutputStream = new MemoryStream();
    public override Stream HandleResource(ResourceInfo info) => OutputStream;
}

class ZipResourceHandler : ResourceHandler, IDisposable
{
    private readonly ZipArchive _zipArchive;
    public ZipResourceHandler(string zipPath) =>
        _zipArchive = ZipFile.Open(zipPath, ZipArchiveMode.Create);

    public override Stream HandleResource(ResourceInfo info) =>
        _zipArchive.CreateEntry(info.Name).Open();

    protected override void Dispose(bool disposing)
    {
        if (disposing) _zipArchive.Dispose();
        base.Dispose(disposing);
    }

    public void Dispose() => Dispose(true);
}

class Program
{
    static void Main()
    {
        // 1️⃣ Load HTML
        var htmlDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");

        // 2️⃣ Write to a memory stream
        var memHandler = new MemoryResourceHandler();
        htmlDoc.Save(memHandler);
        memHandler.OutputStream.Position = 0;
        // Optional: verify content
        // Console.WriteLine(new StreamReader(memHandler.OutputStream).ReadToEnd());

        // 3️⃣ Zip the same document
        using (var zipHandler = new ZipResourceHandler("YOUR_DIRECTORY/output.zip"))
        {
            htmlDoc.Save(zipHandler);
        }

        // 4️⃣ Change font style programmatically
        htmlDoc.DefaultViewStyleSheet.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // 5️⃣ Render to PNG with antialiasing & hinting
        var renderOpts = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            UseHinting = true
        };
        new ImageRenderer(renderOpts).Render(htmlDoc, "YOUR_DIRECTORY/out.png");

        Console.WriteLine("All operations completed successfully.");
    }
}
```

このプログラムを実行すると、次の 3 つの成果物が生成されます。

1. `memHandler.OutputStream` に格納された **インメモリ HTML**。  
2. HTML とすべてのリンクリソースを含む **`output.zip`**。  
3. 太字‑斜体スタイルが適用された **`out.png`** – レンダリングされた画像。

## 結論

C# で **Memory Stream を作成**し、HTML のレンダリング、ZIP 圧縮、画像生成とシームレスに統合する方法を示しました。重要なポイントは、単一の `HTMLDocument` を `MemoryStream`、ZIP アーカイブ、PNG ファイルのいずれかに保存できるのは、`ResourceHandler` を差し替えるだけで実現できるということです。

さらに踏み込むなら、次のことに挑戦してみてください。

- **PDF にレンダリング**：`Stream` を受け取る PDF レンダラを使用。  
- **ネットワーク送信前に圧縮**：`GZipStream` などでメモリストリームを圧縮。  
- **複数 HTML ページをまとめて ZIP**：大量エクスポート用に複数ページを一つの ZIP に統合。

ぜひ試してみて、問題があればコメントで教えてください。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}