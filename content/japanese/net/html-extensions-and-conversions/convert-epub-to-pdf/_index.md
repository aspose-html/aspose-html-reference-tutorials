---
title: Aspose.HTML を使用して .NET で EPUB を PDF に変換する
linktitle: .NET で EPUB を PDF に変換する
second_title: Aspose.HTML .NET HTML 操作 API
description: Aspose.HTML for .NET を使用して EPUB を PDF に変換する方法を学びます。このステップバイステップのガイドでは、シームレスなドキュメント変換のためのカスタマイズ オプション、FAQ などについて説明します。
type: docs
weight: 12
url: /ja/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

このチュートリアルでは、Aspose.HTML for .NET を使用して EPUB ファイルを PDF に変換する方法を検討します。 Aspose.HTML は、HTML および EPUB ドキュメントを操作するためのさまざまな機能を提供する強力な .NET ライブラリです。前提条件を説明し、必要な名前空間をインポートし、複数の例に分けて各ステップを詳しく説明します。

## 前提条件

始める前に、次の前提条件が満たされていることを確認してください。

1. Aspose.HTML for .NET: Aspose.HTML for .NET が .NET プロジェクトにインストールされていることを確認します。からダウンロードできます[ここ](https://releases.aspose.com/html/net/).

2. データ ディレクトリ: EPUB ファイルを保存するデータ ディレクトリが必要です。

ここで、Aspose.HTML for .NET を使用して EPUB を PDF に変換する段階的なプロセスを見てみましょう。

## EPUBをPDFに変換

### ステップ 1: プロジェクトを初期化する

.NET プロジェクトが設定されていること、および Aspose.HTML for .NET がインストールされていることを確認してください。

### ステップ 2: 必要な名前空間をインポートする

C# コード ファイルで、必要な名前空間をインポートします。

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### ステップ 3: EPUB ファイルを開く

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    //次のステップに進みます...
}
```

- 交換する`"Your Data Directory"` EPUB ファイルが置かれている実際のディレクトリに置き換えます。
- このコードは、EPUB ファイルを読み取り用に開きます。

### ステップ 4: PDF オプションを設定し、変換を実行する

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

- のインスタンスを作成します`PdfSaveOptions`PDF 変換設定を指定します。
- 使用`Converter.ConvertEPUB`指定されたオプションを使用して EPUB を PDF に変換するメソッド。
- 結果の PDF を「output.pdf」として保存します。

## PDF 保存オプションの指定

### ステップ 1: プロジェクトを初期化する

.NET プロジェクトが設定されており、Aspose.HTML for .NET がインストールされていることを確認してください。

### ステップ 2: 必要な名前空間をインポートする

必要な名前空間を C# コードにインポートします。

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
```

### ステップ 3: EPUB ファイルを開く

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    //次のステップに進みます...
}
```

- 交換する`"Your Data Directory"` EPUB ファイルの実際のディレクトリに置き換えます。
- EPUB ファイルを開いて読み取ります。

### ステップ 4: PDF オプションをカスタマイズする

```csharp
var options = new PdfSaveOptions()
{
    PageSetup = { AnyPage = new Page() { Size = Size.FromPixels(3000, 1000) } },
    BackgroundColor = System.Drawing.Color.AliceBlue
};
```

- のインスタンスを作成します`PdfSaveOptions`要件に応じてカスタマイズします。
- この例では、ページ サイズを幅 3000 ピクセル、高さ 1000 ピクセルに設定し、背景色をアリス ブルーに設定します。

### ステップ 5: 変換を実行する

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

- 使用`Converter.ConvertEPUB`カスタム オプションを使用して EPUB を PDF に変換するメソッド。
- 結果の PDF を「output.pdf」として保存します。

## カスタム ストリーム プロバイダーを使用する

### ステップ 1: プロジェクトを初期化する

.NET プロジェクトをセットアップし、Aspose.HTML for .NET をインストールします。

### ステップ 2: 必要な名前空間をインポートする

C# コードで、必要な名前空間をインポートします。

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
```

### ステップ 3: EPUB ファイルを開く

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    //次のステップに進みます...
}
```

- 交換する`"Your Data Directory"` EPUB ファイルの実際のディレクトリに置き換えます。
- EPUB ファイルを開いて読み取ります。

### ステップ 4: カスタム ストリーム プロバイダーを使用する

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    //次のステップに進みます...
}
```

- を作成します`MemoryStreamProvider`変換結果をメモリストリームとして管理します。
- 使用`Converter.ConvertEPUB`カスタム ストリーム プロバイダーを使用したメソッド。

### ステップ 5: 結果を保存する

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.pdf"))
{
    memory.CopyTo(fs);
}
```

- 変換されたデータを含むメモリ ストリームにアクセスします。
- ストリーム位置を先頭に設定します。
- 出力 PDF ファイルを作成し、メモリ ストリームからそのファイルにコンテンツをコピーします。

### クラス MemoryStreamProvider のソース コード。 

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            //ドキュメントのレンダリング中に作成される MemoryStream オブジェクトのリスト
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
                //このメソッドは、複数の出力ストリームの作成が必要な場合に呼び出されます。たとえば、HTML をレンダリング中に画像ファイル (JPG、PNG など) のリストを表示します。
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                //ここで、データで満たされたストリームを解放し、たとえばハードドライブにフラッシュできます。
            }
            public void Dispose()
            {
                //リソースの解放
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
これで、さまざまなオプションとカスタマイズの可能性を備えた Aspose.HTML for .NET を使用して、EPUB ファイルを PDF に変換する方法を学習しました。 Aspose.HTML はプロセスを簡素化し、ドキュメント変換に対する柔軟性と制御を提供します。

## 結論

Aspose.HTML for .NET は、EPUB ファイルを PDF に変換するための多用途ツールであり、結果として得られる PDF ドキュメントをニーズに合わせて調整するためのカスタマイズ オプションを提供します。単純な変換が必要な場合でも、高度なカスタマイズが必要な場合でも、Aspose.HTML が対応します。

まだダウンロードしていない場合は、.NET 用の Aspose.HTML をダウンロードできます。[Webサイト](https://releases.aspose.com/html/net/)今すぐ .NET アプリケーションで使用を開始してください。

---

## よくある質問

### Aspose.HTML for .NET は無料で使用できますか?
    Aspose.HTML for .NET は商用製品ですが、無料試用版が利用可能です[ここ](https://releases.aspose.com/).

### 変換された PDF の外観をカスタマイズできますか?
   はい、例 2 に示すように、ページ サイズや背景色などのオプションを調整して PDF の外観をカスタマイズできます。

### Aspose.HTML for .NET のサポートを取得するにはどうすればよいですか?
   サポートとリソースは次の場所にあります。[Aspose.HTML フォーラム](https://forum.aspose.com/).

### Aspose.HTML for .NET で変換できる他の形式はありますか?
   はい、Aspose.HTML for .NET は、HTML、EPUB などを含むさまざまなドキュメント形式をサポートしています。

### Aspose.HTML for ..NET は大規模なドキュメント変換に適していますか?
   Aspose.HTML for .NET は、大規模なドキュメント変換を効率的に処理できるように設計されており、幅広いアプリケーションに適しています。

