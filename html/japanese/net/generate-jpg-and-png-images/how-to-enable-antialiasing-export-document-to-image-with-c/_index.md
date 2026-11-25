---
category: general
date: 2026-04-06
description: C#でアンチエイリアスを有効にし、画像の幅と高さを設定し、ドキュメントをPNGとして保存する方法を学びましょう – ドキュメントを画像にエクスポートするための簡単ガイド。
draft: false
keywords:
- how to enable antialiasing
- save document as png
- set image width
- set image height
- export document to image
language: ja
og_description: ドキュメントを画像としてエクスポートする際にアンチエイリアスを有効にする方法。このガイドでは、画像の幅と高さの設定方法、およびドキュメントを
  PNG 形式で保存する手順を示します。
og_title: アンチエイリアシングを有効にする方法 – ドキュメントを画像としてエクスポート
tags:
- C#
- ImageRendering
- Antialiasing
title: アンチエイリアスの有効化方法 – C#でドキュメントを画像としてエクスポート
url: /ja/net/generate-jpg-and-png-images/how-to-enable-antialiasing-export-document-to-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# アンチエイリアシングの有効化方法 – C#でドキュメントを画像としてエクスポート

ドキュメントを画像に変換するときに **アンチエイリアシングを有効にする方法** を疑問に思ったことはありませんか？ `Save` を手早く呼び出してみて、特に斜めの線がギザギザに見えることがあったかもしれません。良いニュースは、グラフィックの専門家は必要なく、C# の数行と適切なオプションさえあればできる、ということです。

このチュートリアルでは、画像の幅を設定し、画像の高さを設定し、最後に **save document as PNG** して **export document to image** を滑らかなエッジで実現する手順を解説します。最後まで読むと、アンチエイリアシングが有効な 800 × 600 PNG を生成する、すぐに実行できるコードスニペットが手に入ります。

## 前提条件

- .NET 6.0 以降（コードは .NET Framework 4.7+ でも動作します）  
- `ImageRenderingOptions` をサポートするレンダリングライブラリへの参照（例: Aspose.Words、Syncfusion、または同様のプロパティを公開する任意の API）  
- C# 文法の基本的な理解  

重いセットアップは不要です。NuGet パッケージを追加すればすぐに始められます。

## ステップ 1: レンダリングライブラリのインストール

まず、パッケージをプロジェクトに追加します。Aspose.Words を使用している場合は、次のコマンドを実行してください。

```bash
dotnet add package Aspose.Words
```

> **Pro tip:** ライブラリのバージョンは常に最新に保ちましょう。2026 年 4 月時点の最新リリースでは、アンチエイリアシング向けのパフォーマンス改善が含まれています。

## ステップ 2: Document オブジェクトの作成

レンダリングしたいドキュメントを読み込むか作成します。以下は、シンプルな段落だけで構成された 1 ページのドキュメントを作る最小例です。

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Create a new blank document
Document doc = new Document();

// Add a paragraph with some text
Paragraph para = new Paragraph(doc);
Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
para.AppendChild(run);
doc.FirstSection.Body.AppendChild(para);
```

`Document` クラスがエントリーポイントです。レンダリングされるすべてはこのオブジェクトから取得します。実際のプロジェクトでは既存の .docx を読み込むことが多いでしょう。

```csharp
// Document doc = new Document("input.docx");
```

## ステップ 3: レンダリングオプションの定義（幅、高さ、アンチエイリアシング）

ここで核心の質問に答えます: **アンチエイリアシングを有効にする方法**。`ImageRenderingOptions` オブジェクトを使うと、平滑化の切り替えやサイズの制御が可能です。

```csharp
// Step 3: Define rendering options (size and antialiasing)
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Set the desired output size
    Width = 800,               // set image width
    Height = 600,              // set image height

    // Turn on antialiasing for smoother edges
    UseAntialiasing = true
};
```

コメントに注目してください。**set image width**、**set image height**、そして **UseAntialiasing** が明示的に記載されており、きれいな PNG を得るために最も重要な 3 つの設定です。

### アンチエイリアシングが重要な理由

アンチエイリアシングが無いと、斜め線や曲線は階段状に見えてしまいます。これはレンダラが各ピクセルを「オン」か「オフ」かでしか判断しないためです。アンチエイリアシングを有効にすると、エッジピクセルがブレンドされ、写真編集ソフトで見られるような柔らかな見た目になります。処理時間は僅かに増加しますが、ほとんどの UI 向けエクスポートでは無視できる程度です。

## ステップ 4: Document を PNG として保存（ドキュメントを画像としてエクスポート）

オプションが整ったら、いよいよ **save document as PNG** です。`Save` メソッドはファイルパスと先ほど設定したオプションを受け取ります。

```csharp
// Step 4: Render the document to a PNG file using the configured options
doc.Save("output.png", imageOptions);
```

これで完了です。ドキュメントはアンチエイリアシングが適用された 800 × 600 PNG になります。`output.png` を開くと、文字がクリアで線が滑らかになり、ギザギザのアーティファクトがありません。

### 結果の検証

任意の画像ビューアでファイルをすぐに確認できます。チェックすべきポイントは次の通りです。

- 正しいサイズ (800 × 600)  
- テキストや図形に階段状のエッジが見えないこと  
- ドキュメントに背景色が設定されていない場合は透明背景（多くのライブラリはデフォルトで白）

画像がギザギザしている場合は、`UseAntialiasing = true` が他の箇所で上書きされていないか再確認してください。

## ステップ 5: エッジケースとバリエーション

### 出力形式の変更

PNG の代わりに JPEG が欲しいですか？ ファイル拡張子を変更し、必要に応じて圧縮設定を調整するだけです。

```csharp
imageOptions.JpegQuality = 90; // only works for JPEG output
doc.Save("output.jpg", imageOptions);
```

### 複数ページのエクスポート

ソースドキュメントに複数ページがある場合、レンダラはデフォルトでページごとに別々の画像ファイルを生成します。ページをループして処理できます。

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string fileName = $"page_{i + 1}.png";
    doc.Save(fileName, imageOptions);
}
```

### ストリームへの保存（例: HTTP レスポンス）

Web API を構築している場合、PNG を直接クライアントに返すことができます。

```csharp
using (MemoryStream ms = new MemoryStream())
{
    doc.Save(ms, imageOptions);
    ms.Position = 0;
    // Return ms as FileResult in ASP.NET Core
}
```

## 完全な動作例

以下は、ここまで説明したすべての手順を組み込んだ、コピー＆ペースト可能な完全プログラムです。

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a document
        Document doc = new Document();
        Paragraph para = new Paragraph(doc);
        Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
        para.AppendChild(run);
        doc.FirstSection.Body.AppendChild(para);

        // 2️⃣ Define rendering options (size and antialiasing)
        ImageRenderingOptions imageOptions = new ImageRenderingOptions
        {
            Width = 800,               // set image width
            Height = 600,              // set image height
            UseAntialiasing = true     // how to enable antialiasing
        };

        // 3️⃣ Export document to image (save document as PNG)
        doc.Save("output.png", imageOptions);

        Console.WriteLine("Image saved as output.png with antialiasing enabled.");
    }
}
```

このプログラムを実行すると、実行ファイルのフォルダーに `output.png` が生成されます。開いてみると、滑らかで 800 × 600 の PNG が確認でき、目指した通りの結果が得られます。

## よくある質問とトラブルシューティング

- **画像がぼやけている場合は？**  
  小さなソースページを拡大したときにぼやけが発生することがあります。ソースページのサイズを目標サイズに近づけるか、`imageOptions.Resolution`（例: `Resolution = 300`）で DPI を上げてください。

- **.NET Framework でも動作しますか？**  
  はい。従来のフレームワークでも同じ API が利用可能です。適切な DLL を参照すれば動作します。

- **背景色を制御できますか？**  
  もちろん可能です。保存前に `imageOptions.BackgroundColor = System.Drawing.Color.Transparent;` と設定してください。

- **アンチエイリアシングはハードウェアアクセラレートされていますか？**  
  多くのライブラリはソフトウェアでアンチエイリアシングを行います。GPU 加速が必要な場合は、ハードウェアアクセラレーションを明示的にサポートするレンダリングエンジンを探してください。

## 結論

**アンチエイリアシングを有効にしてドキュメントを画像としてエクスポート**する方法、**set image width** と **set image height** の設定手順、そして **save document as PNG** の具体的手順を網羅しました。上記スニペットは本番環境でもそのまま使用でき、JPEG やマルチページ PDF、あるいはストリームへの直接出力にも簡単に拡張できます。

次は透かしの追加や、印刷品質向けの DPI 調整、あるいはこのロジックを ASP.NET Core エンドポイントに組み込むことを検討してみてください。同じ原則が適用されますので、ファイルパスをレスポンスストリームに置き換えるだけです。

Happy coding, and enjoy those crisp, antialiased images!

![アンチエイリアシングが有効なレンダリングPNG](output.png "アンチエイリアシングが有効なレンダリングPNG")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}