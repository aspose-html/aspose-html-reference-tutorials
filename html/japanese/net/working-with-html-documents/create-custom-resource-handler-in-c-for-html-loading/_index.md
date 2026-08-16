---
category: general
date: 2026-08-15
description: C#でカスタムリソースハンドラを作成し、画像やCSSなどのHTMLリソースを管理します。HTMLLoadOptions、メモリストリーム、HTMLDocumentのロード方法を学びます。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom resource handler
- C# resource handler
- HTMLLoadOptions
- HTMLDocument loading
- memory stream for resources
language: ja
lastmod: 2026-08-15
og_description: C#でカスタムリソースハンドラを作成し、HTMLリソースのストリーミング方法を制御します。このチュートリアルでは、HTMLLoadOptionsの設定、メモリストリームの処理、カスタムロジックによるHTMLDocumentのロード方法を示します。
og_image_alt: Screenshot of C# code defining a custom resource handler class for HTML
  loading
og_title: C#でカスタムリソースハンドラを作成 – HTMLリソース管理の完全ガイド
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  headline: Create custom resource handler in C# for HTML loading
  type: TechArticle
- description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  name: Create custom resource handler in C# for HTML loading
  steps:
  - name: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
    text: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
  - name: Configure `HTMLLoadOptions` to use the handler.
    text: Configure `HTMLLoadOptions` to use the handler.
  - name: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
    text: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
  - name: (Optional) Store received resources to disk for verification.
    text: (Optional) Store received resources to disk for verification.
  type: HowTo
tags:
- C#
- HTML
- resource handling
title: HTML読み込みのためのC#カスタムリソースハンドラを作成する
url: /ja/net/working-with-html-documents/create-custom-resource-handler-in-c-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で HTML 読み込み用カスタムリソースハンドラを作成する

HTML ファイル用に **カスタムリソースハンドラを作成** する必要がある場合、このガイドで手順をすべて示します。`HTMLLoadOptions` とメモリベースのストリームを使用して、HTML ドキュメントの読み込み中に画像、CSS、その他のアセットをインターセプトする方法を学びます。

このチュートリアルでは、再利用可能なハンドラの実装、ロードオプションの設定、リソースが正しく取得されているかの検証に必要なすべてを網羅しています。外部ドキュメントは不要です—以下のコードと解説だけで完了します。

## 前提条件

- .NET 6.0 以降
- C# の基本的な知識
- `HTMLDocument`、`HtmlLoadOptions`、`ResourceHandler` を提供する HTML 処理ライブラリへの参照（例: GroupDocs.Viewer for .NET）

## ソリューションの概要

以下を行います。

1. `ResourceHandler` を継承して **カスタムリソースハンドラを作成** する。
2. ハンドラを使用するように `HTMLLoadOptions` を設定する。
3. `HTMLDocument` で HTML ファイルを読み込み、ハンドラが各リソースに対してストリームを提供するようにする。
4. （オプション）取得したリソースをディスクに保存して検証する。

各ステップには完全なソースコードとその背後にある考え方を示します。

## 手順 1: カスタムリソースハンドラ クラスを定義する

カスタムハンドラを作成するには `HandleResource` をオーバーライドし、ライブラリがリソースバイトを書き込むストリームを自分で制御できるようにします。`MemoryStream` を使用すればデータはメモリ内に保持され、テストや追加処理に最適です。

```csharp
using System;
using System.IO;
using GroupDocs.Viewer.Handler;   // Adjust namespace to match your library

namespace HtmlResourceDemo
{
    /// <summary>
    /// Provides a memory stream for each HTML resource (images, CSS, etc.).
    /// </summary>
    public class MyHandler : ResourceHandler
    {
        /// <summary>
        /// Called by the viewer for every external resource referenced in the HTML.
        /// </summary>
        /// <param name="info">Information about the resource (name, MIME type, etc.).</param>
        /// <returns>A writable stream that receives the resource data.</returns>
        public override Stream HandleResource(ResourceInfo info)
        {
            // A fresh MemoryStream ensures the viewer can write the resource bytes.
            // You could replace this with a FileStream to save directly to disk.
            return new MemoryStream();
        }
    }
}
```

**重要ポイント:**  
`HandleResource` をオーバーライドすることで、リソースデータの保存先を完全にコントロールできます。後で画像をキャッシュしたり、CSS を変換したり、リソース使用状況をログに記録したりしたい場合は、`MemoryStream` を任意のカスタムストリーム実装に置き換えるだけです。

## 手順 2: ハンドラを使用するように `HTMLLoadOptions` を設定する

`HTMLLoadOptions` ではハンドラをロード パイプラインに差し込むことができます。`ResourceHandler` プロパティにハンドラを設定すると、ビューアは外部アセットごとに `MyHandler` を呼び出します。

```csharp
using GroupDocs.Viewer.Options;   // Namespace for HtmlLoadOptions

// ...

var loadOptions = new HtmlLoadOptions
{
    // Attach the custom handler defined in Step 1
    ResourceHandler = new MyHandler()
};
```

**重要ポイント:**  
`ResourceHandler` を設定しない場合、ビューアはデフォルトの場所（多くの場合一時フォルダ）にリソースを書き込みます。独自のハンドラを指定することで、**カスタムリソースハンドラ** の動作をアプリケーションの保存戦略に合わせて実装できます。

## 手順 3: 設定したオプションで HTML ドキュメントを読み込む

ここで HTML ファイルを読み込みます。ビューアは検出した各リソースに対して `MyHandler.HandleResource` を呼び出します。

```csharp
using GroupDocs.Viewer;           // Namespace for HTMLDocument

// Path to the source HTML file
string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// Load the document using the custom load options
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);
```

この時点で HTML コンテンツは解析され、外部リソースはすべて `MyHandler` が提供したメモリ バッファにストリームされました。

## 手順 4（オプション）: 取得したリソースにアクセスする

リソースを確認または永続化したい場合は、`MyHandler` を変更して各 `MemoryStream` をリソース名をキーとしたディクショナリに格納します。

```csharp
public class MyHandler : ResourceHandler
{
    // Stores streams for later retrieval
    public Dictionary<string, MemoryStream> Resources { get; } = new();

    public override Stream HandleResource(ResourceInfo info)
    {
        var stream = new MemoryStream();
        Resources[info.Name] = stream;
        return stream;
    }
}
```

読み込み後、`handler.Resources` を走査して各ストリームをディスクに書き出すことができます。

```csharp
var handler = new MyHandler();
var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);

// Save each captured resource
foreach (var kvp in handler.Resources)
{
    string fileName = Path.Combine("output_resources", kvp.Key);
    File.WriteAllBytes(fileName, kvp.Value.ToArray());
    Console.WriteLine($"Saved resource: {fileName}");
}
```

**重要ポイント:**  
リソースを保存すると、画像最適化や CSS 圧縮、アーカイブなどの後処理が可能になります。また、**カスタムリソースハンドラを作成** するロジックが期待通りに動作していることを目に見えて確認できます。

## 手順 5: クリーンアップ

`HTMLDocument` とすべてのストリームは、アンマネージド リソースを解放するために必ず破棄してください。

```csharp
doc.Dispose();                     // Releases internal buffers
foreach (var stream in handler.Resources.Values)
{
    stream.Dispose();              // Flushes and releases memory
}
```

## 完全な実行可能サンプル

以下はクラス定義からリソース抽出までのすべての手順を示す、自己完結型プログラムです。

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Viewer;
using GroupDocs.Viewer.Handler;
using GroupDocs.Viewer.Options;

namespace HtmlResourceDemo
{
    public class MyHandler : ResourceHandler
    {
        public Dictionary<string, MemoryStream> Resources { get; } = new();

        public override Stream HandleResource(ResourceInfo info)
        {
            var stream = new MemoryStream();
            Resources[info.Name] = stream;
            return stream;
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare paths
            string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");
            string outputDir = Path.Combine("output_resources");
            Directory.CreateDirectory(outputDir);

            // 2️⃣ Create handler and load options
            var handler = new MyHandler();
            var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };

            // 3️⃣ Load the HTML document
            using (HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions))
            {
                // Document is now loaded; resources are in handler.Resources
            }

            // 4️⃣ Persist captured resources
            foreach (var kvp in handler.Resources)
            {
                string filePath = Path.Combine(outputDir, kvp.Key);
                File.WriteAllBytes(filePath, kvp.Value.ToArray());
                Console.WriteLine($"Saved: {filePath}");
            }

            // 5️⃣ Clean up streams
            foreach (var stream in handler.Resources.Values)
                stream.Dispose();

            Console.WriteLine("All resources processed.");
        }
    }
}
```

**期待される出力**

```
Saved: output_resources/logo.png
Saved: output_resources/styles.css
Saved: output_resources/banner.jpg
All resources processed.
```

コンソールには、ビューアがカスタムハンドラを通してストリームした各リソースが一覧表示され、**カスタムリソースハンドラの作成** ワークフローが正常に完了したことが確認できます。

## よくある質問とエッジケース

| 質問 | 回答 |
|----------|--------|
| *リソースが大きい（例: 高解像度画像）場合はどうすべきですか？* | `MemoryStream` の代わりに一時フォルダを指す `FileStream` を使用します。これによりメモリ使用量を抑えられます。 |
| *リソースを種類でフィルタリングできますか？* | `HandleResource` 内で `info.MimeType` または `info.Extension` を確認し、不要なタイプに対して `null` を返します。`null` を返すとビューアはそのリソースをスキップします。 |
| *スレッドセーフは必要ですか？* | 同一ハンドラ インスタンスを複数の同時ロードで使う場合は、`Resources` ディクショナリをロックで保護するか、`ConcurrentDictionary` などのスレッドセーフコレクションを使用してください。 |
| *相対 URL をサポートするには？* | `ResourceInfo` に元の URL が含まれるので、HTML ファイルのベースパスと組み合わせて相対参照を解決し、保存前に調整できます。 |

## 結論

これで **C# で HTML 読み込み用カスタムリソースハンドラを作成** し、`HTMLLoadOptions` を設定してストリーミングされたアセットを取得し、適切にクリーンアップする方法が分かりました。このパターンを使えば、オンザフライの画像処理、CSS の書き換え、セキュアな保存など、リソース管理をフルコントロールできます。

次は、**HTMLDocument の読み込み** をさまざまなレンダリングオプションで試したり、ハンドラを拡張して **C# リソースハンドラ** がクラウドストレージに直接書き込む実装に挑戦したりしてください。`HandleResource` メソッドをプロジェクト固有のリソースフローに合わせてカスタマイズしてみましょう。

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには完全な動作サンプルとステップバイステップの解説が含まれており、API の追加機能習得や代替実装アプローチの探求に役立ちます。

- [Create HTML from String in C# – Custom Resource Handler Guide](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Custom Resource Handler in C# – Convert HTML to ZIP Tutorial](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}