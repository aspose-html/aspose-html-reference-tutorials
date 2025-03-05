---
title: Aspose.HTML を使用して .NET で EPUB を画像に変換する
linktitle: .NET で EPUB を画像に変換する
second_title: Aspose.HTML .NET HTML 操作 API
description: Aspose.HTML for .NET を使用して EPUB を画像に変換する方法を学びます。コード例とカスタマイズ可能なオプションを含むステップバイステップのチュートリアルです。
type: docs
weight: 11
url: /ja/net/html-extensions-and-conversions/convert-epub-to-image/
---

今日のデジタル時代では、さまざまなドキュメント形式を操作および変換する能力は貴重なスキルです。Aspose.HTML for .NET は、開発者が HTML および EPUB ドキュメントを簡単に操作できるようにする強力なツールです。このチュートリアルでは、Aspose.HTML for .NET の世界を詳しく調べ、EPUB ドキュメントをさまざまな画像形式に変換するプロセスについて説明します。各例を複数のステップに分割し、そのすべてのステップを説明します。

## 前提条件

Aspose.HTML for .NET の世界に飛び込む前に、次の前提条件が満たされていることを確認する必要があります。

1. Visual Studio: システムに Visual Studio がインストールされていることを確認してください。Web サイトからダウンロードできます。

2.  Aspose.HTML for .NET: ライブラリはAsposeのWebサイトから入手できます。[ここ](https://releases.aspose.com/html/net/).

3. データ ディレクトリ: EPUB ファイルを保存し、出力画像を保存するディレクトリを準備します。

4. C# の基礎知識: このチュートリアルで提供されるコード例を理解して実装するには、C# プログラミングの知識が不可欠です。

## 必要な名前空間のインポート

Aspose.HTML for .NET の使用を開始する前に、必要な名前空間を C# コードにインポートする必要があります。これらの名前空間により、Aspose.HTML for .NET の機能にアクセスできるようになります。

```csharp
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using Aspose.Html.Rendering.Image;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
using System.IO;
using System.Drawing;
using System.Collections.Generic;
```

前提条件と名前空間が整ったので、ステップバイステップの例に進みましょう。

## EPUB を JPEG に変換する

```csharp
    string dataDir = "Your Data Directory";
    //既存の EPUB ファイルを開いて読み取ります。
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        //ConvertEPUB メソッドを呼び出して、EPUB ファイルを画像に変換します。
        Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), "output.jpg");
    }
```
### 手順

1. dataDir 変数に EPUB ファイルへのパスを指定します。
2. FileStream を使用して EPUB ファイルを読み取れるように開きます。
3. ConvertEPUB メソッドを呼び出し、EPUB ストリーム、出力形式 (JPEG) を指定する ImageSaveOptions、および出力ファイル名 ("output.jpg") を渡します。
5. EPUB ファイルは JPEG 画像に変換されます。

この例では、EPUB ファイルを開き、その内容を読み取り、JPEG 画像形式に変換します。出力画像は「output.jpg」として保存されます。

## EPUB を PNG に変換する

同様のコード構造を使用して、EPUB ファイルを PNG、BMP、GIF、TIFF などのさまざまな画像形式に簡単に変換できます。以下は PNG に変換する例です。

```csharp

    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Png);
        Converter.ConvertEPUB(stream, options, "output.png");
    }

```
### 手順
1. FileStream を使用して EPUB ファイルを読み取れるように開きます。
2. 目的の出力形式 (この場合は PNG) で ImageSaveOptions オブジェクトを初期化します。
3. EPUB ストリーム、画像保存オプション、および出力ファイル名を渡して、ConvertEPUB メソッドを呼び出します。
4. EPUB ファイルは指定された画像形式に変換されます。

## 画像保存オプションを指定する

ページ サイズや背景色などのオプションを指定して、画像出力をカスタマイズできます。次に例を示します。

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Jpeg)
        {
            PageSetup =
            {
                AnyPage = new Page()
                {
                    Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
                }
            },
            BackgroundColor = Color.AliceBlue,
        };
        Converter.ConvertEPUB(stream, options, "output.jpg");
    }
```
### 手順

1.  EPUBファイルへのパスを`dataDir`変数。
2. EPUBファイルを開いて、`FileStream`.
3. 作成する`ImageSaveOptions`オブジェクトを選択し、希望する出力形式 (JPEG) を指定します。
4. 必要に応じて、ページ サイズと背景色をカスタマイズします。
5. 電話する`ConvertEPUB`メソッドは、EPUB ストリーム、画像保存オプション、および出力ファイル名を渡します。
6. EPUB ファイルは指定されたオプションで画像に変換されます。

## カスタムストリームプロバイダーを指定する

出力ストリームを操作する必要がある場合は、カスタム ストリーム プロバイダーを使用できます。次に例を示します。

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        using (var streamProvider = new MemoryStreamProvider())
        {
            Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), streamProvider);
            
            for (int i = 0; i < streamProvider.Streams.Count; i++)
            {
                var memory = streamProvider.Streams[i];
                memory.Seek(0, SeekOrigin.Begin);
                
                using (FileStream fs = File.Create($"page_{i + 1}.jpg"))
                {
                    memory.CopyTo(fs);
                }
            }
        }
    }

```
MemoryStreamProvider クラスのソース コード。

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            //ドキュメントのレンダリング中に作成された MemoryStream オブジェクトのリスト
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                //このメソッドは、XPS、PDF、または TIFF 形式など、出力ストリームが 1 つだけ必要な場合に呼び出されます。
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                //このメソッドは、複数の出力ストリームの作成が必要な場合に呼び出されます。たとえば、HTML を画像ファイル (JPG、PNG など) のリストにレンダリングする場合などです。
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                //ここで、データで満たされたストリームを解放し、例えばハードドライブにフラッシュすることができます。
            }
            public void Dispose()
            {
                //リソースの解放
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```

### 手順
1.  EPUBファイルへのパスを`dataDir`変数。
2. EPUBファイルを開いて、`FileStream`.
3. 作成する`MemoryStreamProvider`カスタム出力ストリームを処理します。
4. 電話する`ConvertEPUB`メソッドは、EPUB ストリーム、画像保存オプション (JPEG)、およびカスタム ストリーム プロバイダーを渡します。
5. カスタム プロバイダー内のメモリ ストリームを反復処理し、個別のファイルに保存します。
6. この例では、必要に応じて複数の出力ストリームを操作および保存できます。

## 結論

Aspose.HTML for .NET は、EPUB および HTML ドキュメントの操作を簡素化する多目的ライブラリです。EPUB ドキュメントをさまざまな画像形式に変換する機能とカスタマイズ可能なオプションを備えており、開発者に幅広いアプリケーションを提供します。

---

## よくある質問

### 1. Aspose.HTML for .NET はどこからダウンロードできますか?

 Aspose.HTML for .NETはリリースページからダウンロードできます。[ここ](https://releases.aspose.com/html/net/).

### 2. Aspose.HTML for .NET の一時ライセンスを取得するにはどうすればよいですか?

一時ライセンスを取得するには、一時ライセンスページにアクセスしてください。[ここ](https://purchase.aspose.com/temporary-license/).

### 3. Aspose.HTML for .NET の追加サポートはどこで入手できますか?

ご質問や問題がある場合は、サポートフォーラムのAsposeコミュニティにご相談ください。[ここ](https://forum.aspose.com/).

### 4. EPUB ドキュメントを PDF や XPS などの他の形式に変換できますか?

はい、Aspose.HTML for .NET を使用して、EPUB ドキュメントを PDF や XPS などのさまざまな形式に変換できます。

### 5. Aspose.HTML for .NET は小規模プロジェクトと大規模プロジェクトの両方に適していますか?

もちろんです! Aspose.HTML for .NET はスケーラブルに設計されているため、あらゆる規模のプロジェクトに最適です。
