---
title: Aspose.HTML を使用して .NET で EPUB を PDF に変換する
linktitle: .NET で EPUB を PDF に変換する
second_title: Aspose.HTML .NET HTML 操作 API
description: Aspose.HTML for .NET を使用して EPUB を PDF に変換する方法を学びます。このステップ バイ ステップ ガイドでは、シームレスなドキュメント変換のためのカスタマイズ オプション、FAQ などについて説明します。
weight: 12
url: /ja/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML を使用して .NET で EPUB を PDF に変換する


このチュートリアルでは、Aspose.HTML for .NET を使用して EPUB ファイルを PDF に変換する方法について説明します。Aspose.HTML は、HTML および EPUB ドキュメントを操作するためのさまざまな機能を提供する強力な .NET ライブラリです。前提条件を説明し、必要な名前空間をインポートし、複数の例を分解して、各手順を詳しく説明します。

## 前提条件

始める前に、次の前提条件が満たされていることを確認してください。

1. Aspose.HTML for .NET: .NETプロジェクトにAspose.HTML for .NETがインストールされていることを確認してください。ダウンロードはここから行えます。[ここ](https://releases.aspose.com/html/net/).

2. データ ディレクトリ: EPUB ファイルが保存されるデータ ディレクトリが必要になります。

それでは、Aspose.HTML for .NET を使用して EPUB を PDF に変換する手順を詳しく説明します。

## EPUBをPDFに変換する

### ステップ1: プロジェクトを初期化する

.NET プロジェクトがセットアップされ、Aspose.HTML for .NET がインストールされていることを確認してください。

### ステップ2: 必要な名前空間をインポートする

C# コード ファイルで、必要な名前空間をインポートします。

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### ステップ3: EPUBファイルを開く

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    //次のステップに進みます...
}
```

- 交換する`"Your Data Directory"` EPUB ファイルが配置されている実際のディレクトリに置き換えます。
- このコードは EPUB ファイルを開いて読み取ります。

### ステップ4: PDFオプションを設定して変換を実行する

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

- インスタンスを作成する`PdfSaveOptions`PDF 変換設定を指定します。
- 使用`Converter.ConvertEPUB`指定されたオプションを使用して EPUB を PDF に変換する方法。
- 結果の PDF を「output.pdf」として保存します。

## PDF保存オプションを指定する

### ステップ1: プロジェクトを初期化する

.NET プロジェクトがセットアップされ、Aspose.HTML for .NET がインストールされていることを確認します。

### ステップ2: 必要な名前空間をインポートする

C# コードに必要な名前空間をインポートします。

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
```

### ステップ3: EPUBファイルを開く

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    //次のステップに進みます...
}
```

- 交換する`"Your Data Directory"` EPUB ファイルの実際のディレクトリに置き換えます。
- EPUB ファイルを開いて読み取ります。

### ステップ4: PDFオプションをカスタマイズする

```csharp
var options = new PdfSaveOptions()
{
    PageSetup = { AnyPage = new Page() { Size = Size.FromPixels(3000, 1000) } },
    BackgroundColor = System.Drawing.Color.AliceBlue
};
```

- インスタンスを作成する`PdfSaveOptions`要件に応じてカスタマイズします。
- この例では、ページ サイズを幅 3000 ピクセル、高さ 1000 ピクセルに設定し、背景色をアリス ブルーに設定します。

### ステップ5: 変換を実行する

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

- 使用`Converter.ConvertEPUB`カスタム オプションを使用して EPUB を PDF に変換する方法。
- 結果の PDF を「output.pdf」として保存します。

## カスタムストリームプロバイダーを使用する

### ステップ1: プロジェクトを初期化する

.NET プロジェクトをセットアップし、Aspose.HTML for .NET をインストールします。

### ステップ2: 必要な名前空間をインポートする

C# コードで、必要な名前空間をインポートします。

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
```

### ステップ3: EPUBファイルを開く

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    //次のステップに進みます...
}
```

- 交換する`"Your Data Directory"` EPUB ファイルの実際のディレクトリに置き換えます。
- EPUB ファイルを開いて読み取ります。

### ステップ4: カスタムストリームプロバイダーを使用する

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    //次のステップに進みます...
}
```

- 作成する`MemoryStreamProvider`変換結果をメモリ ストリームとして管理します。
- 使用`Converter.ConvertEPUB`カスタム ストリーム プロバイダーを使用したメソッド。

### ステップ5: 結果を保存する

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.pdf"))
{
    memory.CopyTo(fs);
}
```

- 変換されたデータを含むメモリ ストリームにアクセスします。
- ストリームの位置を先頭に設定します。
- 出力 PDF ファイルを作成し、メモリ ストリームからそのファイルにコンテンツをコピーします。

### クラス MemoryStreamProvider のソース コード。 

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
これで、さまざまなオプションとカスタマイズ機能を備えた Aspose.HTML for .NET を使用して EPUB ファイルを PDF に変換する方法を学習しました。Aspose.HTML はプロセスを簡素化し、ドキュメント変換の柔軟性と制御性を高めます。

## 結論

Aspose.HTML for .NET は、EPUB ファイルを PDF に変換するための多目的ツールで、結果の PDF ドキュメントをニーズに合わせて調整するためのカスタマイズ オプションを提供します。単純な変換でも高度なカスタマイズでも、Aspose.HTML が対応します。

まだお持ちでない場合は、Aspose.HTML for .NETを以下のサイトからダウンロードできます。[Webサイト](https://releases.aspose.com/html/net/)今すぐ .NET アプリケーションで使い始めましょう。

---

## よくある質問

### Aspose.HTML for .NET は無料で使用できますか?
    Aspose.HTML for .NETは商用製品ですが、無料試用版もご利用いただけます。[ここ](https://releases.aspose.com/).

### 変換された PDF の外観をカスタマイズできますか?
   はい、例 2 に示すように、ページ サイズや背景色などのオプションを調整して PDF の外観をカスタマイズできます。

### Aspose.HTML for .NET のサポートを受けるにはどうすればよいですか?
   サポートとリソースについては、[Aspose.HTML フォーラム](https://forum.aspose.com/).

### Aspose.HTML for .NET で変換できる他の形式はありますか?
   はい、Aspose.HTML for .NET は HTML、EPUB など、さまざまなドキュメント形式をサポートしています。

### Aspose.HTML for ..NET は大規模なドキュメント変換に適していますか?
   Aspose.HTML for .NET は、大規模なドキュメント変換を効率的に処理するように設計されており、幅広いアプリケーションに適しています。


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
