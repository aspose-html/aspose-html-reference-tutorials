---
category: general
date: 2026-02-19
description: C#でドキュメントをPNGに変換し、画像サイズを設定し、画像品質を調整する方法を、シンプルなステップバイステップの例で学びましょう。
draft: false
keywords:
- convert document to png
- set image dimensions
- save rendered image
- adjust image quality
- set custom image size
language: ja
og_description: 画像サイズを設定し、品質を調整し、レンダリングされた画像を保存することで、C#でドキュメントをPNGに変換する—すべてを1つのチュートリアルで。
og_title: ドキュメントをPNGに変換 – 完全C#ガイド
tags:
- C#
- Image Rendering
- Document Processing
title: ドキュメントをPNGに変換 – 完全なC#ガイド
url: /ja/net/generate-jpg-and-png-images/convert-document-to-png-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ドキュメントを PNG に変換 – 完全 C# ガイド

**convert document to PNG** が必要だったことはありますか？しかし、どの設定が鮮明で正しいサイズの出力をもたらすか分からないこともあるでしょう。あなたは一人ではありません。レポート、サムネイル、Web プレビューなど多くのプロジェクトで、適切な画像サイズと品質を確保することは重要であり、以下のコードがその方法を正確に示しています。

このチュートリアルでは、ドキュメントの読み込み、**set image dimensions** の設定、**adjust image quality** の調整、そして最終的に **save rendered image** をディスクに保存する手順を順に解説します。最後には、あらゆるシナリオに対応できる **set custom image size** の方法も確認できます。

## 学べること

- 人気のある .NET レンダリングライブラリ（ここでは Aspose.Words for .NET を使用）でドキュメントをロードする方法（概念は類似の API にも適用できます）。
- 幅・高さ・アンチエイリアシングを制御しながら **convert document to PNG** を行うステップバイステップのプロセス。
- パフォーマンス重視のアプリ向けに **set image dimensions** と **adjust image quality** を設定する方法。
- **save rendered image** を安全に行い、マルチページドキュメントを処理する方法。
- 特定のページだけをレンダリングする、または大容量ファイルを扱うといったエッジケースへのヒント。

> **Prerequisite:** .NET 6+ SDK、Visual Studio 2022（またはお好みの IDE）、および Aspose.Words for .NET の NuGet パッケージ。別のレンダリングエンジンを使用している場合は、`ImageRenderingOptions` クラスをライブラリの同等クラスに置き換えてください。

---

## ステップ 1 – 希望サイズでドキュメントを PNG に変換

最初に行うべきことは、`ImageRenderingOptions` インスタンスを作成し、レンダラーに PNG の希望サイズを正確に指示することです。ここで **set image dimensions** が重要になります。

```csharp
using System;
using System.Drawing.Imaging;               // For ImageFormat
using Aspose.Words;                         // Core document API
using Aspose.Words.Rendering;               // Image rendering helpers

class Program
{
    static void Main()
    {
        // Load the source document (DOCX, PDF, etc.)
        Document document = new Document("YOUR_DIRECTORY/input.docx");

        // Create an ImageRenderingOptions instance
        ImageRenderingOptions imageRenderOptions = new ImageRenderingOptions();

        // Configure the image size, format, and quality
        imageRenderOptions.Width = 1024;                     // width in pixels
        imageRenderOptions.Height = 768;                     // height in pixels
        imageRenderOptions.OutputFormat = ImageFormat.Png;  // PNG output
        imageRenderOptions.UseAntialiasing = true;           // smoother edges

        // Render the first page to a PNG file
        document.RenderToImage("YOUR_DIRECTORY/output.png", imageRenderOptions);
    }
}
```

**これが重要な理由:**  
- **Width & Height** を使用すると、後でリサイズする必要なく **set custom image size** ができ、シャープさが保たれます。  
- **UseAntialiasing** は **adjust image quality** の重要なフラグです。オンにするとエッジが滑らかになり、オフにするとレンダリングが高速になります。  
- 直接 PNG にレンダリングすることでロスレスの色深度が確保され、UI サムネイルに最適です。

> **Pro tip:** より高い DPI（dots per inch）が必要な場合は、レンダリング前に `imageRenderOptions.Resolution = 300;` を設定してください。DPI を上げると印刷品質が向上しますが、ファイルサイズが大きくなります。

## ステップ 2 – 画像サイズの設定と画像品質の調整

デフォルトのページサイズが目的に合わないことがあります。ウェブギャラリー用の横長サムネイルや、モバイルアプリ用の正方形アイコンが必要になることもあります。そのような場合は **set image dimensions** を手動で設定します。

```csharp
// Example: Create a square 500×500 PNG with high quality
imageRenderOptions.Width = 500;
imageRenderOptions.Height = 500;
imageRenderOptions.UseAntialiasing = true;   // high‑quality rendering
imageRenderOptions.OutputFormat = ImageFormat.Png;
```

**内部で何が起きているか:**  
レンダラーは元のページベクターデータを指定したピクセルグリッドにスケーリングします。PNG はロスレスなので、スケーリングによって圧縮アーティファクトは発生しませんが、**adjust image quality** フラグ（アンチエイリアシング）がエッジの滑らかさを決定します。アンチエイリアシングをオフにすると、数百枚のサムネイルを生成するバッチ処理が高速化されます。

### 品質を調整すべきとき

| シナリオ | 推奨設定 |
|----------|----------------------|
| リアルタイムプレビュー（例: UI） | `UseAntialiasing = false` |
| マーケティング用の最終アセット | `UseAntialiasing = true` |
| 大規模バッチ変換 | `Resolution` と `UseAntialiasing` を組み合わせて速度と鮮明さのバランスを調整 |

## ステップ 3 – レンダリング画像をディスクに保存

オプションを設定したら、最後のステップは **save rendered image** です。`RenderToImage` メソッドがファイル作成を行ってくれますが、出力パスを確認し、I/O エラーに対処する必要があります。

```csharp
try
{
    string outputPath = "YOUR_DIRECTORY/output.png";
    document.RenderToImage(outputPath, imageRenderOptions);
    Console.WriteLine($"✅ Successfully saved PNG to {outputPath}");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"❌ Failed to save PNG: {ex.Message}");
}
```

**なぜ try/catch でラップするのか:**  
ファイルの権限、ディスク容量、または無効なパスが例外を引き起こすことがあります。これらを捕捉することで、サービス全体のクラッシュを防げます。特に、ドキュメントをリアルタイムで変換する Web API では重要です。

### 結果の確認

生成されたファイルを任意の画像ビューアで開きます。設定した幅と高さが一致した PNG が表示され、アンチエイリアシングが有効ならエッジが滑らかです。サイズがずれている場合は、`Width` と `Height` を誤って入れ替えていないか再確認してください。

## オプション – シナリオ別にカスタム画像サイズを設定

異なる解像度（例: サムネイル、ミディアム、ラージ）の画像が必要になることがあります。各サイズをハードコーディングする代わりに、次元オブジェクトの配列をループ処理します。

```csharp
var sizes = new (int width, int height)[]
{
    (200, 200),   // tiny thumbnail
    (800, 600),   // medium preview
    (1920, 1080)  // full‑HD preview
};

foreach (var (w, h) in sizes)
{
    imageRenderOptions.Width = w;
    imageRenderOptions.Height = h;
    string outFile = $"YOUR_DIRECTORY/output_{w}x{h}.png";
    document.RenderToImage(outFile, imageRenderOptions);
    Console.WriteLine($"Saved {outFile}");
}
```

**重要なポイント:**  

- このパターンにより、コードを DRY に保ちつつ、**set custom image size** を動的に行えます。  
- `UseAntialiasing` をサイズごとに変更でき、大きな画像は高品質に、小さなサムネイルは高速レンダリングにできます。  
- 使用後は `Document` オブジェクトを必ず破棄（`document.Dispose();`）して、ネイティブリソースを解放することを忘れずに。

---

## マルチページドキュメントの処理

上記のスニペットは最初のページのみをレンダリングします。ソースが複数ページあり、各ページの PNG が必要な場合は `document.PageCount` をループします。

```csharp
for (int pageIndex = 0; pageIndex < document.PageCount; pageIndex++)
{
    // Adjust options if you want per‑page customizations
    imageRenderOptions.PageIndex = pageIndex; // tells the renderer which page

    string outPath = $"YOUR_DIRECTORY/page_{pageIndex + 1}.png";
    document.RenderToImage(outPath, imageRenderOptions);
    Console.WriteLine($"Page {pageIndex + 1} saved as PNG.");
}
```

**なぜ `PageIndex` を使用するのか:**  
`PageIndex` はレンダラーに描画するページを指示します。指定しなければデフォルトはページ 0（最初のページ）です。この方法により、各ページが個別の PNG として出力され、マルチページの PDF、DOCX、ODT ファイルに対する **convert document to png** ワークフローが維持されます。

## 完全な動作例

以下は新しいコンソールアプリにコピー＆ペーストできる完全なプログラムです。ロード、設定、レンダリング、エラーハンドリング、マルチページ対応をすべて一箇所でカバーしています。

```csharp
using System;
using System.Drawing.Imaging;
using Aspose.Words;
using Aspose.Words.Rendering;

class ConvertToPngDemo
{
    static void Main()
    {
        // 1️⃣ Load the source document
        Document doc = new Document("YOUR_DIRECTORY/input.docx");

        // 2️⃣ Prepare rendering options (set image dimensions, quality, format)
        ImageRenderingOptions opts = new ImageRenderingOptions
        {
            Width = 1024,
            Height = 768,
            OutputFormat = ImageFormat.Png,
            UseAntialiasing = true,
            Resolution = 150 // optional DPI tweak
        };

        // 3️⃣ Render each page to its own PNG file
        for (int i = 0; i < doc.PageCount; i++)
        {
            opts.PageIndex = i; // select page
            string outPath = $"YOUR_DIRECTORY/output_page_{i + 1}.png";

            try
            {
                doc.RenderToImage(outPath, opts);
                Console.WriteLine($"✅ Page {i + 1} saved → {outPath}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Error on page {i + 1}: {ex.Message}");
            }
        }

        // Clean up
        doc.Dispose();
    }
}
```

**期待される出力:**  
`output_page_1.png`、`output_page_2.png` … といった名前の PNG ファイルが連続して生成され、各ファイルは 1024 × 768 ピクセルのサイズでアンチエイリアシングが適用されています。任意のファイルを開くと、画像は鮮明で正しい比率になっており、Web でもデスクトップでも使用できる状態です。

## 結論

これで C# で **convert document to PNG** を行い、正確に **set image dimensions**、**adjust image quality**、そして **save rendered image** を効率的に実行する方法が分かりました。単一のサムネイルを生成する場合でも、フルページのギャラリーを作成する場合でも、ここで示したパターンにより出力を完全にコントロールできます。

次のステップは？ ` を入れ替えてみてください

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}