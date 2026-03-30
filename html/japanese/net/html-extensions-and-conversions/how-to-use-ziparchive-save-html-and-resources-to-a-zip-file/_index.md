---
category: general
date: 2026-03-29
description: C# の ZipArchive の使い方を学び、HTML を ZIP に変換し、HTML を ZIP に保存し、HTML 画像を圧縮する方法を、すべてひとつの分かりやすいチュートリアルで解説します。
draft: false
keywords:
- how to use ziparchive
- convert html to zip
- save html to zip
- create zip archive c#
- compress html images
language: ja
og_description: C# の ZipArchive を使用して HTML を ZIP に変換し、HTML を ZIP に保存し、HTML 画像を圧縮する方法を、完全な実行可能サンプルとともに紹介します。
og_title: ZipArchive の使い方 – HTML とリソースを ZIP ファイルに保存する
tags:
- C#
- .NET
- Aspose.Html
- ZipArchive
title: ZipArchive の使い方 – HTML とリソースを ZIP ファイルに保存する
url: /ja/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ZipArchive の使い方 – HTML とリソースを ZIP ファイルに保存する

HTML ページとその画像、CSS、その他のアセットをまとめて ZIP にする方法を **ZipArchive の使い方** で考えたことがありますか？ あなただけではありません。ページが外部リソースを参照している場合、自己完結型の HTML パッケージを配布しようとして壁にぶつかる開発者は多いです。良いニュースは、C# と Aspose.HTML の数行で **HTML を ZIP に変換**、**HTML を ZIP に保存**、さらには **HTML 画像を圧縮** でき、IDE を離れる必要がないことです。

このチュートリアルでは、シンプルな `HTMLDocument` の作成からカスタム `ResourceHandler` を使ったすべてのリンクリソースの処理まで、全工程を順に解説します。最後まで実行すれば、任意の Web サーバーやメール添付にそのまま投入できる、すぐに使える ZIP ファイルが手に入ります。外部スクリプト不要、手動コピー不要――純粋な .NET だけです。

## 前提条件

- **.NET 6+**（または .NET Framework 4.6+）。使用する API は `System.IO.Compression` の一部です。
- **Aspose.HTML for .NET** がインストール済み（NuGet パッケージ `Aspose.Html`）。
- C# の基本的な構文が分かっていること。
- Visual Studio や VS Code などの IDE。

以上です。余計なツールやサードパーティ製の zip ユーティリティは不要です。準備はできましたか？さっそく始めましょう。

## 手順 1: プロジェクトの設定と依存関係の追加

新しいコンソールプロジェクトを作成します：

```bash
dotnet new console -n HtmlToZipDemo
cd HtmlToZipDemo
dotnet add package Aspose.Html
```

`Aspose.Html` パッケージは `HTMLDocument` クラスと、後で拡張する `ResourceHandler` 基底クラスを提供します。組み込みの `System.IO.Compression` 名前空間は `ZipArchive` と `ZipArchiveEntry` を提供します。

> **Pro tip:** .NET 6 を対象にする場合、トップレベルステートメントを使って `Main` メソッドをすっきりさせることができます。このコード例は分かりやすさのために従来の `Program` クラスを使用しています。

## 手順 2: カスタム Resource Handler の作成

Aspose.HTML がドキュメントを保存するとき、外部ファイル（画像、CSS、フォントなど）ごとに `ResourceHandler` に `Stream` の提供を求めます。`HandleResource` をオーバーライドすることで、すべてのリソースを直接 zip エントリに流し込むことができます。

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Writes each HTML resource (image, CSS, etc.) directly into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        // Ensure a folder hierarchy inside the zip (optional but tidy)
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open(); // Aspose streams the content into this entry.
    }
}
```

**Why this matters:** リソースを一度ディスクに書き出してから zip にまとめるのではなく、ハンドラが直接ストリームを zip エントリに渡すため、I/O のオーバーヘッドが減り、HTML コンテンツと zip の同期が保証されます。

## 手順 3: HTML ドキュメントの構築

デモ用に、外部画像 `logo.png` を参照する小さな HTML スニペットを埋め込みます。実際のプロジェクトではファイルやデータベースから HTML を読み込むことになるでしょう。

```csharp
// Create a simple HTML document with an external image reference.
HTMLDocument htmlDocument = new HTMLDocument(
    "<html><body><h1>Welcome!</h1><img src='logo.png' alt='Demo logo'></body></html>"
);
```

**HTML 画像を圧縮**したい場合は、画像ファイルを実行ファイルの隣に置くか、リソースとして埋め込んでください。`ZipResourceHandler` が自動的に画像をアーカイブに追加します。

## 手順 4: ZIP ファイルを開く（または作成）して保存

ここで全体を結びつけます。出力用 zip の `FileStream` を開き、*Update* モードで `ZipArchive` をインスタンス化し、カスタムハンドラを `HTMLDocument.Save` に渡します。

```csharp
using (var fileStream = new FileStream("output.zip", FileMode.Create))
using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
{
    // Initialise the handler with the open ZipArchive.
    var zipHandler = new ZipResourceHandler(zipArchive);

    // Save the HTML document; the handler writes HTML, images, CSS, etc. into the zip.
    htmlDocument.Save(zipHandler);
}
```

`using` ブロックが終了すると zip が自動的に確定・クローズされます。生成された `output.zip` には以下が含まれます：

- `index.html`（シリアライズされた HTML ドキュメント）
- `logo.png`（HTML が参照している画像）

任意のファイルエクスプローラで zip を開いて内容を確認できます。

## 手順 5: 結果の検証（任意）

zip が正しく機能するか二重チェックするのは常に良い考えです。以下のスニペットを前のコードの後に実行すれば、エントリ一覧が表示されます：

```csharp
using (var zip = ZipFile.OpenRead("output.zip"))
{
    Console.WriteLine("Contents of output.zip:");
    foreach (var entry in zip.Entries)
        Console.WriteLine($"- {entry.FullName} ({entry.Length} bytes)");
}
```

次のような出力が得られるはずです：

```
Contents of output.zip:
- index.html (1234 bytes)
- logo.png (45678 bytes)
```

抽出したフォルダーから `index.html` を開くと、画像が正しく表示されます――**HTML を ZIP に保存** が期待通りに動作した証拠です。

## 共通のバリエーションとエッジケース

### 1. HTML ファイルのエントリ名を変更する

デフォルトでは Aspose が HTML を `index.html` として書き出します。カスタム名が必要な場合は、保存前に `htmlDocument.FileName` を設定します：

```csharp
htmlDocument.FileName = "myPage.html";
htmlDocument.Save(zipHandler);
```

### 2. 追加ファイルを手動で追加する

README などの余分なファイルを同梱したいときは、`htmlDocument.Save` を呼び出す前に `ZipArchive` に直接追加できます：

```csharp
var readme = zipArchive.CreateEntry("README.txt", CompressionLevel.Optimal);
using (var writer = new StreamWriter(readme.Open()))
{
    writer.WriteLine("This ZIP contains an HTML page generated with Aspose.HTML.");
}
```

### 3. 大容量画像を効率的に扱う

HTML が非常に大きな画像を参照している場合は、事前にリサイズして zip サイズを抑えることを検討してください。`System.Drawing.Common` パッケージが役立ちます：

```csharp
// Example: Resize logo.png to a max width of 800px before zipping.
using (var img = System.Drawing.Image.FromFile("logo.png"))
{
    int maxWidth = 800;
    if (img.Width > maxWidth)
    {
        var ratio = (double)maxWidth / img.Width;
        var newHeight = (int)(img.Height * ratio);
        using var thumb = img.GetThumbnailImage(maxWidth, newHeight, () => false, IntPtr.Zero);
        thumb.Save("logo_resized.png");
    }
}
```

その後、HTML 内の `<img src='logo_resized.png'>` を指すようにします。

## 完全な実行可能サンプル

以下は `Program.cs` にそのまま貼り付けてビルド・実行できる完全プログラムです。Aspose.HTML の NuGet パッケージがインストールされていればそのまま動作します。

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Custom handler that streams each resource into a zip entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;
    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Create an HTML document that references an external image.
        HTMLDocument htmlDocument = new HTMLDocument(
            "<html><head><title>Demo</title></head>" +
            "<body><h2>Hello, ZipArchive!</h2>" +
            "<img src='logo.png' alt='Demo logo'></body></html>"
        );

        // 2️⃣ Open (or create) the output zip file.
        using (var fileStream = new FileStream("output.zip", FileMode.Create))
        using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
        {
            // 3️⃣ Initialise the custom handler.
            var zipHandler = new ZipResourceHandler(zipArchive);

            // 4️⃣ Save the HTML; resources get streamed into the zip.
            htmlDocument.Save(zipHandler);
        }

        Console.WriteLine("✅ HTML document and its resources have been saved to output.zip");
    }
}
```

**期待される出力:** コンソールに成功メッセージが表示され、プロジェクトフォルダーに `output.zip` が生成されます。中身は `index.html` と `logo.png` です。

## Frequently Asked Questions

- **Does this work on .NET Core?**  
  Yes. `System.IO.Compression.ZipArchive` is part of .NET Standard, so the same code runs on .NET 5, .NET 6, and .NET 7.

- **What if I need to **compress HTML images** more aggressively?**  
  You can pre‑process images (resize, change format to WebP, etc.) before they are added to the zip. The handler itself just streams whatever data it receives.

- **Can I encrypt the zip?**  
  `ZipArchive` supports AES encryption only via third‑party libraries (e.g., `SharpZipLib`). If you need encryption, create the zip with that library and then feed the stream to Aspose as a custom `ResourceHandler`.

- **Is there a way to set the root folder inside the zip?**  
  Yes—prepend a folder name to `resourceName` inside `HandleResource`, e.g., `var entry = _zipArchive.CreateEntry($"site/{resourceName}", ...)`.

## 結論

これで **ZipArchive の使い方** をマスターし、**HTML を ZIP に変換**、**HTML を ZIP に保存**、そして **HTML 画像を圧縮** する一連のクリーンなワークフローが実現できました。`ResourceHandler` を拡張することで一時ファイルを作らずにメモリ効率の高い処理が可能です。このパターンはスケーラブルで、生成した zip を Web サーバーに配置したり、メールで送ったり、クラウドストレージに保存したりできます。

次に試してみると良いこと：

- **Create ZIP archives programmatically** for entire website folders (`create zip archive c#`)。
- **Add PDF or DOCX conversions** before zipping for richer documentation packages。
- **Integrate with ASP.NET Core** to stream the zip directly to a client browser (`FileStreamResult`)。

HTML の zip 化、フォントの取り扱い、画像サイズの最適化についてさらに質問があれば、コメントや Stack Overflow で ping してください。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}