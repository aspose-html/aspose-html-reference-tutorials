---
category: general
date: 2026-04-06
description: C#でHTMLをPNGにレンダリングし、メモリ内でZIPを作成します。文字列からHTMLを読み込み、太字スタイルのHTMLを追加し、Aspose.HTMLを使用してHTMLをZIPとして保存する方法を学びます。
draft: false
keywords:
- render html to png
- create zip in memory
- load html from string
- save html as zip
- add bold style html
language: ja
og_description: C#でHTMLをPNGにレンダリングし、メモリ上でZIPを作成します。このチュートリアルでは、文字列からHTMLを読み込み、太字スタイルのHTMLを追加し、HTMLをZIPとして保存する方法を示します。
og_title: HTML をメモリ上で PNG と ZIP にレンダリング – 完全 C# ガイド
tags:
- Aspose.HTML
- C#
- Image Rendering
- ZIP Archives
title: HTML をメモリ上で PNG と ZIP に変換 – 完全 C# ガイド
url: /ja/net/rendering-html-documents/render-html-to-png-and-zip-in-memory-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Render HTML to PNG and ZIP in Memory – Complete C# Guide

HTML をその場で **PNG にレンダリング** し、ソースとアセットを一緒にパッケージ化したいことはありませんか？サムネイルサービス、メールプレビュー生成ツール、自己完結型 HTML パッケージを配布するレポートツールなど、シナリオはさまざまです。どのケースでも共通する課題は、マークアップ文字列があり、スタイルを適用し、ラスタ画像が必要で、ファイルシステムに触れずに ZIP にまとめたい、ということです。

そこで Aspose.HTML を使えば、この一連の作業がとても簡単になります。このガイドでは、文字列から HTML を読み込み、**太字スタイルの HTML を追加**し、ページを PNG にレンダリングし、最後に **メモリ上の ZIP** を作成して HTML と外部リソースの両方を格納します。最終的に `ResultArchive.zip` と鮮明な `final.png` が同時に手に入ります。

カバーする内容:

* 文字列から HTML をロード（ファイル不要）  
* 要素に太字フォントを適用  
* 画像レンダリングオプションの設定（サイズ、アンチエイリアス、ヒンティング）  
* **メモリ上の ZIP アーカイブ** に HTML を保存  
* 同じドキュメントを PNG 画像としてレンダリング  

特別な依存関係は不要、.NET 用 Aspose.HTML と数行の慣用的 C# だけです。さっそく始めましょう。

## Render HTML to PNG – Overview

コードに入る前に、簡単な概念モデルを把握しておきましょう。プロセスは 3 つの層に分かれます。

1. **Document 作成** – 生のマークアップを Aspose.HTML に渡し、`Document` オブジェクトを取得します。  
2. **変換** – DOM を操作して（太字を追加、色を変更など）加工します。  
3. **エクスポート** – PNG にラスタライズする **または** 後で利用できるように ZIP にシリアライズします。

両方のエクスポートは同じ内部ドキュメントを共有するため、DOM の構築は一度だけです。これが効率的で保守しやすい理由です。

> **Pro tip:** 多数のサムネイルを提供する場合は、`Document` インスタンスをキャッシュし、マークアップが実際に変化したときだけ再レンダリングすると CPU サイクルを大幅に削減できます。

## Load HTML from String

最初のステップは、マークアップを直接 `Document` に渡すことです。テンポラリファイルやストリームは不要、単なる文字列です。

```csharp
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

// Step 1: Load an HTML document from a string.
var htmlContent = "<html><body><img src='logo.png'><span id='title'>Demo</span></body></html>";
var doc = new Document(htmlContent);
```

**Why this matters:** 文字列からロードする (`load html from string`) と、メールテンプレートやユーザー生成レポート、Markdown から HTML への変換など、オンザフライでマークアップを生成できます。`Document` コンストラクタはマークアップを解析し、操作可能なインメモリ DOM を構築します。

## Add Bold Style HTML

`Document` が手に入ったので、タイトルを目立たせましょう。`id` で要素を取得し、太字フォントスタイルを適用します。

```csharp
// Step 2: Apply a bold font style to the element with id 'title'.
doc.GetElementById("title").Style.FontStyle = WebFontStyle.Bold;
```

**What’s happening under the hood?** `GetElementById` は `<span id='title'>` を表す `IElement` を返します。`FontStyle` に `WebFontStyle.Bold` を設定すると、要素のインラインスタイルに CSS `font-weight: bold;` が注入されます。外部スタイルシートに触れずに **add bold style HTML** を実現する最もシンプルな方法です。

> **Watch out:** 要素が存在しない場合、`GetElementById` は `null` を返し、次の行で `NullReferenceException` がスローされます。本番コードではチェックを入れるべきですが、このチュートリアルでは要素が確実に存在すると仮定しています。

## Create ZIP in Memory

HTML ファイル *と* `logo.png` のような外部アセットを含むポータブルパッケージが欲しいです。`System.IO.Compression.ZipArchive` を使えば、ディスク I/O を一切行わずにメモリ上で ZIP を構築できます。

```csharp
// Step 3: Prepare a ZIP archive that will hold the HTML and its external resources.
using var zipStream = new MemoryStream();
using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: true);
var resourceHandler = new ZipResourceHandler(zip);
```

**Why a memory‑based ZIP?**  
* **Performance:** 中間ファイルがないためディスク競合が減ります。  
* **Security:** 一時的なアーカイブがファイルシステムに触れないので、サンドボックス環境でも安全です。  
* **Flexibility:** ZIP を直接レスポンスや Azure Blob、その他のストレージへストリームできます。

`ZipResourceHandler` は Aspose のヘルパーで、後で `doc.Save` を呼び出すと自動的に外部リソース（画像など）を同じアーカイブに書き込んでくれます。

## Configure Image Rendering Options

HTML をビットマップにレンダリングするにはいくつかの設定が必要です。幅・高さ・アンチエイリアス・テキストヒンティングを設定して、鮮明な PNG を得ます。

```csharp
// Step 4: Configure image rendering options (size, antialiasing, and hinting).
var imgOptions = new ImageRenderingOptions
{
    Width = 600,
    Height = 400,
    UseAntialiasing = true,
    TextOptions = new TextOptions { UseHinting = true }
};
```

**Explanation:**  
* `Width`/`Height` は出力キャンバスのサイズを決めます。  
* `UseAntialiasing` はエッジを滑らかにし、ギザギザを防ぎます。  
* `TextOptions.UseHinting` は小さなフォントの可読性を向上させ、特に Windows の ClearType 環境で有効です。

UI 要件に合わせてこれらの値を調整してください。高 DPI のサムネイルが必要な場合は、サイズを大きくしてから画像処理ライブラリでダウンスケールすると良いでしょう。

## Save HTML as ZIP and Render PNG

ここからがデュアルエクスポートです。HTML をメモリ上の ZIP にシリアライズし、同時にドキュメントを PNG 画像としてディスクに保存します。

```csharp
// Step 5: Save the HTML into the ZIP and render the document as a PNG image.
doc.Save(zipStream, new HtmlSaveOptions { OutputStorage = resourceHandler });
doc.Save("YOUR_DIRECTORY/final.png", imgOptions);
```

**What `HtmlSaveOptions.OutputStorage` does:** Aspose に対し、外部参照（例: `logo.png`）をすべて `resourceHandler` に書き込むよう指示します。`resourceHandler` はそれらのファイルを `zip` に格納します。HTML ファイル自体もアーカイブに入れられ、元のフォルダ構造が保持されます。

2 回目の `Save` 呼び出しは、先ほど定義したオプションを使って同じ `Document` をラスタ画像に変換します。結果として得られる `final.png` は、ブラウザで表示される HTML とまったく同じ見た目です。

> **Note:** PNG をファイルではなくバイト配列として取得したい場合は、`doc.Save(new MemoryStream(), imgOptions)` を使用し、ストリームからバイト列を読み取ってください。

## Persist ZIP Archive to Disk

最後に、メモリ上の ZIP を物理ファイルに書き出して配布や保存ができるようにします。

```csharp
// Step 6: Persist the ZIP archive (contains HTML + external files) to disk.
zipStream.Position = 0;
File.WriteAllBytes("YOUR_DIRECTORY/ResultArchive.zip", zipStream.ToArray());
```

`Position = 0` でストリームを先頭に戻すことで、全体のアーカイブが正しく書き込まれます。生成された `ResultArchive.zip` には以下が含まれます。

* `index.html`（元のマークアップ）  
* `logo.png`（HTML が参照する画像）  

ZIP を解凍して `index.html` を任意のブラウザで開けば、先ほど生成した PNG と同一の表示が得られます。

---

![render html to png example](render-html-png.png)

*Image alt text: HTMLをPNGにレンダリングする例*

## Full Working Example

すべてをまとめた、すぐに実行できる完全なプログラムです。`YOUR_DIRECTORY` を実際のフォルダパスに置き換えてください。

```csharp
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

class Program
{
    static void Main()
    {
        // 1️⃣ Load HTML from a string.
        var htmlContent = "<html><body><img src='logo.png'><span id='title'>Demo</span></body></html>";
        var doc = new Document(htmlContent);

        // 2️⃣ Add bold style to the title.
        doc.GetElementById("title").Style.FontStyle = WebFontStyle.Bold;

        // 3️⃣ Create a ZIP archive in memory.
        using var zipStream = new MemoryStream();
        using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: true);
        var resourceHandler = new ZipResourceHandler(zip);

        // 4️⃣ Set up image rendering options.
        var imgOptions = new ImageRenderingOptions
        {
            Width = 600,
            Height = 400,
            UseAntialiasing = true,
            TextOptions = new TextOptions { UseHinting = true }
        };

        // 5️⃣ Save HTML into the ZIP and render a PNG.
        doc.Save(zipStream, new HtmlSaveOptions { OutputStorage = resourceHandler });
        doc.Save("C:/Temp/final.png", imgOptions); // Adjust path as needed

        // 6️⃣ Write the ZIP to disk.
        zipStream.Position = 0;
        File.WriteAllBytes("C:/Temp/ResultArchive.zip", zipStream.ToArray());

        // 🎉 Done! You now have a PNG thumbnail and a self‑contained ZIP.
    }
}
```

### Expected Output

* **`final.png`** – 600 × 400 ピクセルの画像で、ロゴと太字の **Demo** という文字が表示されます。  
* **`ResultArchive.zip`** – `index.html`（渡したマークアップ）と `logo.png` を含みます。ブラウザで `index.html` を開くと PNG と同じ表示になります。

---

## Conclusion

**render html to png** のワークフローを、**create zip in memory**、**load html from string**、**add bold style html**、**save html as zip** と同時に実装する方法を解説しました。コードは自己完結型で、Aspose.HTML と .NET 標準ライブラリだけを使用し、ラスタ出力とアーカイブ出力の両方を示しています。

次のステップは？ PNG を JPEG に変えてみる、CSS トランスフォームを試す、ZIP を HTTP レスポンスに直接ストリームしてダウンロードエンドポイントを作る、あるいは同一アーカイブに複数の HTML ページを埋め込む—`Document` オブジェクトを追加で作成し、同じ `resourceHandler` で `doc.Save` すれば実現できます。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}