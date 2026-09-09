---
category: general
date: 2025-12-30
description: カスタムリソースハンドラを使用してHTMLを迅速にZIPとして保存します。数ステップでウェブページをZIPに変換し、画像やCSSを抽出する方法を学びましょう。
draft: false
keywords:
- save html as zip
- custom resource handler
- convert webpage to zip
- extract images css
language: ja
og_description: カスタムリソースハンドラでHTMLをZIPとして保存します。このガイドに従って、ウェブページをZIPに変換し、画像やCSSを簡単に抽出しましょう。
og_title: HTMLをZIPとして保存 – 完全なC#チュートリアル
tags:
- Aspose.HTML
- C#
- File Compression
title: HTML を ZIP に保存 – 完全 C# チュートリアル
url: /ja/net/html-extensions-and-conversions/save-html-as-zip-complete-c-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML を ZIP として保存 – 完全 C# チュートリアル

サードパーティツールを使わずに **HTML を ZIP として保存** したいと思ったことはありませんか？ 同じ悩みを抱える開発者は多いです。画像、CSS、スクリプトを含む完全なウェブページをアーカイブして、配布したり、保存したり、後で解析したりしたいことがよくあります。朗報です！ Aspose.HTML を使えばプログラムで実現でき、その鍵となるのが **カスタムリソースハンドラ** で、取得した各アセットを直接 ZIP エントリに書き込むことができます。

このガイドでは、プロジェクトのセットアップからハンドラの実装、ウェブページを ZIP に変換する方法、そして必要に応じて画像や CSS を個別に抽出する手順まで、すべてを詳しく解説します。外部スクリプトや手動のコピーペーストは不要です。どの .NET ソリューションにもすぐに組み込めるクリーンな C# コードだけです。

## 学べること

- すべてのリソースリクエストをインターセプトする **カスタムリソースハンドラ** の作り方  
- Aspose.HTML の `HTMLDocument.Save` メソッドを使って **ウェブページを ZIP に変換** する正確な手順  
- 生成されたアーカイブから **画像や CSS を抽出** してさらに処理する方法  
- 重複ファイル名などの一般的な落とし穴と、ZIP をきれいに保つためのプロのコツ  

**前提条件** – 以下が必要です：

- .NET 6 以上（または .NET Framework 4.7.2 以上）  
- 最新版の Aspose.HTML for .NET NuGet パッケージ  
- C# のストリームと `System.IO.Compression` 名前空間に関する基本的な知識  

準備はできましたか？ それでは始めましょう。

![HTML を ZIP として保存するフローを示す図、URL から ZIP ファイルまでの流れ](save-html-as-zip-diagram.png "HTML を ZIP として保存するプロセス")

## HTML を ZIP として保存 – 概要

全体の流れは次のようになります：

1. **Initialize** 出力先の `.zip` ファイルを指す `FileStream` を作成する。  
2. **Instantiate** カスタムハンドラ `ZipResourceHandler` を作成し、ストリームを渡す。  
3. `HTMLDocument` で対象のウェブページを **Load** する。  
4. ドキュメントを **Save** し、ハンドラが各リソースをアーカイブに書き込む。

ハンドラが各リソースに対して書き込み可能なストリームを返すため、Aspose.HTML が画像、CSS、JavaScript などを取得し、ZIP 内の正しい場所に埋め込む重い処理をすべて担ってくれます。

## Step 1: Set Up the Project

まずは新しいコンソールアプリを作成する（既存のサービスに組み込んでも構いません）。次に Aspose.HTML の NuGet パッケージを追加します：

```bash
dotnet add package Aspose.HTML
```

`System.IO.Compression` も参照してください。これはベースクラスライブラリに含まれているため、追加のパッケージは不要です。

## Step 2: Create a Custom Resource Handler

**カスタムリソースハンドラ** が本ソリューションの核心です。各リクエストされたアセットに対して `ResourceInfo` オブジェクトが渡され、Aspose.HTML がデータを書き込む `Stream` を返します。URL パスを ZIP エントリ名にマッピングし、元のフォルダー構造を保持します。

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using System.IO;
using System.IO.Compression;

/// <summary>
/// Writes every fetched resource directly into a ZIP entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    /// <summary>
    /// Opens a ZIP archive in "Create" mode. The archive stays open
    /// until the handler is disposed.
    /// </summary>
    /// <param name="zipStream">The underlying stream for the ZIP file.</param>
    public ZipResourceHandler(Stream zipStream)
    {
        // leaveOpen:true lets us close the handler without closing the file stream.
        _zipArchive = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    /// <summary>
    /// Called for each resource (image, CSS, script, etc.).
    /// </summary>
    /// <param name="resourceInfo">Info about the requested resource.</param>
    /// <returns>A writable stream that points to a new ZIP entry.</returns>
    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // Trim leading '/' to avoid creating an empty top‑level folder.
        var entryName = resourceInfo.Url.PathAndQuery.TrimStart('/');
        // Ensure a valid entry name; duplicate names are overwritten.
        var entry = _zipArchive.CreateEntry(entryName, CompressionLevel.Optimal);
        // Return the stream that Aspose.HTML will write into.
        return entry.Open();
    }

    protected override void Dispose(bool disposing)
    {
        if (disposing)
        {
            _zipArchive?.Dispose();
        }
        base.Dispose(disposing);
    }
}
```

**ポイント**：各リソースに対して新しい `ZipArchiveEntry` ストリームを返すことで、一時ファイルを作らずメモリ使用量を抑えられます。また、ハンドラ側で名前付けを完全に制御できるため、後で **画像や CSS を抽出** したい場合に便利です。

## Step 3: Prepare the ZIP Output Stream

次に、最終的な ZIP ファイルを指す `FileStream` を開きます。このストリームを先ほど作成したハンドラに渡します。

```csharp
// Adjust the path to wherever you want the ZIP to land.
string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");

// Using statement ensures the stream is closed even if an exception occurs.
using var zipFileStream = new FileStream(zipPath, FileMode.Create, FileAccess.Write);
```

> **プロのコツ**：HTTP 応答として ZIP を返す必要がある場合は、`FileStream` の代わりに `MemoryStream` を使用し、バイト配列をレスポンスボディに書き込んでください。

## Step 4: Load and Convert the Webpage

ハンドラの準備ができたら、任意の公開 URL をロードできます。Aspose.HTML は相対リンクを自動的に解決し、アセットをダウンロードし、ハンドラを呼び出します。

```csharp
// Step 4: Instantiate the handler with the ZIP stream.
var zipHandler = new ZipResourceHandler(zipFileStream);

// Step 5: Load the target HTML page.
var url = "https://example.com"; // Change to the page you want to archive.
var htmlDoc = new HTMLDocument(url);

// Step 6: Save the document – the handler writes everything into the ZIP.
htmlDoc.Save(zipHandler, new SaveOptions(SaveFormat.Html));

// Dispose the handler to flush the ZIP archive.
zipHandler.Dispose();

Console.WriteLine($"✅ Webpage saved as ZIP at: {zipPath}");
```

**内部で何が起きているか**  
- `HTMLDocument` が HTML を解析し、`<img>`、`<link rel="stylesheet">`、`<script>` タグを検出する。  
- 各リソースに対して `ZipResourceHandler.HandleResource` が呼び出される。  
- ハンドラは対応するエントリ（`images/logo.png`、`css/site.css` など）を作成し、ダウンロードされたバイトを直接アーカイブにストリームする。

## Step 5: Verify the ZIP Contents

生成された `output.zip` を任意のアーカイブマネージャで開きます。元サイトと同じフォルダー階層が表示されるはずです：

```
/index.html
/images/logo.png
/css/site.css
/js/app.js
...
```

**画像や CSS をさらに分析したい** 場合は、エントリを列挙すれば簡単です：

```csharp
using (var zip = ZipFile.OpenRead(zipPath))
{
    foreach (var entry in zip.Entries)
    {
        if (entry.FullName.EndsWith(".png") || entry.FullName.EndsWith(".jpg"))
        {
            Console.WriteLine($"Image: {entry.FullName}");
        }
        else if (entry.FullName.EndsWith(".css"))
        {
            Console.WriteLine($"CSS: {entry.FullName}");
        }
    }
}
```

このスニペットはハンドラが保存したすべての画像と CSS ファイルを出力します。CSS のリントやサムネイル生成が必要な自動パイプラインに便利です。

## Common Pitfalls and Tips

| 問題 | 発生理由 | 対策 |
|------|----------|------|
| 重複ファイル名（例：異なるフォルダーに同名の `logo.png` がある） | `CreateEntry` が同名エントリを上書きしてしまう | `resourceInfo.Url.PathAndQuery` でフル相対パスを保持するか、GUID を前置して一意にする |
| 大規模ページでメモリ使用量が増える | Aspose.HTML がリソースをバッファリングすることがある | `CompressionLevel.Optimal` を使用し、ハンドラを速やかに `Dispose` する |
| 認証が必要なリソースが取得できない | ライブラリがログイン後の資産にアクセスできない | `HTMLDocument` のコンストラクタオーバーロードで認証情報付き `HttpClient` を渡す |
| 実行後に ZIP ファイルがロックされる | `zipHandler.Dispose()` が呼ばれていない | `using` ブロックでハンドラを囲むか、手動で `Dispose` を呼び出す |

## Conclusion

これで **カスタムリソースハンドラ** を使って **HTML を ZIP として保存** する完全な手法が手に入りました。このアプローチにより、1 回のパスで **ウェブページを ZIP に変換** でき、さらに **画像や CSS を抽出** して downstream の処理に活用できます。ウェブアーカイブサービス、静的サイトのバックアップツール、オフライン閲覧用のページバンドルなど、さまざまなシナリオでスケーラブルに利用でき、.NET エコシステム内に収まります。

次のステップは、`FileStream` を `MemoryStream` に置き換えて ASP.NET Core API エンドポイントから直接 ZIP を返すことです。また、抽出した CSS をミニファイしてからアーカイブに保存するなど、ポストプロセッシングにも挑戦してみてください。可能性はほぼ無限で、基本コンセプトは変わりません：Aspose.HTML に取得させ、ハンドラに書き込ませるだけです。

問題が発生したらコンソール出力の警告を確認し、上記のヒントを活用してください。アーカイブ作業、楽しんでください！ 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}