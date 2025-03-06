---
title: Aspose.HTML を使用して .NET で EPUB を XPS に変換する
linktitle: .NET で EPUB を XPS に変換する
second_title: Aspose.HTML .NET HTML 操作 API
description: Aspose.HTML for .NET を使用して .NET で EPUB を XPS に変換する方法を学びます。ステップ バイ ステップ ガイドに従って、簡単に変換してください。
weight: 13
url: /ja/net/html-extensions-and-conversions/convert-epub-to-xps/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML を使用して .NET で EPUB を XPS に変換する


.NET アプリケーションで EPUB ファイルを XPS 形式にシームレスに変換する方法をお探しですか? Aspose.HTML for .NET は、これを簡単に実現する強力なソリューションを提供します。このステップ バイ ステップ ガイドでは、Aspose.HTML を使用して EPUB を XPS に変換するプロセスについて説明します。さあ、始めましょう!

## 前提条件

EPUB から XPS への変換プロセスに進む前に、次の前提条件が満たされていることを確認する必要があります。

### 1. Aspose.HTML for .NET ライブラリ

プロジェクトにAspose.HTML for .NETライブラリがインストールされていることを確認してください。まだインストールしていない場合は、[Aspose.HTML for .NET ダウンロード ページ](https://releases.aspose.com/html/net/).

### 2. EPUBファイルを入力する

XPS に変換するには、EPUB ファイルが必要です。変換可能な EPUB ファイルがあることを確認してください。

### 3. .NET開発環境

このガイドでは、マシンに動作する .NET 開発環境がセットアップされていることを前提としています。

## 名前空間のインポート

まず、Aspose.HTML に必要な名前空間をインポートする必要があります。

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## EPUBをXPSに変換する

EPUB ファイルを XPS 形式に変換するプロセスを複数のステップに分解してみましょう。

### ステップ1.1: EPUBファイルを開く

まず、FileStream を使用して既存の EPUB ファイルを開いて読み取ります。

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    //変換プロセスを続行する
}
```

### ステップ 1.2: XpsSaveOptions を作成する

XpsSaveOptions のインスタンスを作成します。この手順は、XPS 出力を構成するために重要です。

```csharp
var options = new XpsSaveOptions();
```

### ステップ 1.3: EPUB を XPS に変換する

ここで、ConvertEPUB メソッドを呼び出して EPUB を XPS に変換します。

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## カスタム XPS オプションを指定する

ページ サイズや背景色などのカスタム オプションを指定して、XPS 出力をさらにカスタマイズできます。

### ステップ 2.1: ページ サイズと背景色のカスタマイズ

カスタム ページ サイズと背景色を使用して XpsSaveOptions のインスタンスを作成します。

```csharp
var options = new XpsSaveOptions()
{
    PageSetup =
    {
        AnyPage = new Page()
        {
            Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
        }
    },
    BackgroundColor = System.Drawing.Color.AliceBlue,
};
```

### ステップ 2.2: カスタム オプションを使用して EPUB を XPS に変換する

次に、ConvertEPUB メソッドを呼び出して、カスタム オプションを使用して EPUB を XPS に変換します。

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## カスタムストリームプロバイダーを使用する

この手順では、カスタム ストリーム プロバイダーを使用して EPUB を XPS に変換し、結果のデータを操作できるようにします。

### ステップ 3.1: MemoryStreamProvider を作成する

MemoryStreamProvider のインスタンスを作成します。

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    //変換プロセスを続行する
}
```

### ステップ 3.2: ストリーム プロバイダーを使用して EPUB を XPS に変換する

MemoryStreamProvider を使用して EPUB を XPS に変換します。

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### ステップ 3.3: 結果にアクセスして保存する

変換されたデータを含むメモリ ストリームを取得し、出力ファイルに保存します。

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### クラス MemoryStreamProvider ソース コード

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
おめでとうございます! Aspose.HTML for .NET を使用して EPUB ファイルを XPS 形式に正常に変換しました。

## 結論

この包括的なチュートリアルでは、Aspose.HTML for .NET を活用して、さまざまなカスタマイズ オプションを使用して EPUB ファイルを XPS 形式に変換する方法について説明しました。熟練した開発者でも、初心者でも、Aspose.HTML によってプロセスが簡素化され、EPUB から XPS への変換を簡単に処理できるようになります。

ご質問や問題がありましたら、[Aspose.HTML ドキュメント](https://reference.aspose.com/html/net/)さらに詳しい情報やサポートが必要な場合は、[Aspose.HTML コミュニティ フォーラム](https://forum.aspose.com/).

## よくある質問

### Aspose.HTML for .NET とは何ですか?
Aspose.HTML for .NET は、開発者が .NET アプリケーションで HTML、EPUB、XPS ドキュメントを操作できるようにする強力なライブラリです。

### Aspose.HTML for .NET はどこからダウンロードできますか?
 Aspose.HTML for .NETは以下からダウンロードできます。[ダウンロードページ](https://releases.aspose.com/html/net/).

### Aspose.HTML for .NET の無料試用版はありますか?
はい、無料トライアルをご利用いただけます[ここ](https://releases.aspose.com/).

### Aspose.HTML for .NET の一時ライセンスを取得するにはどうすればよいですか?
一時ライセンスを取得するには、[一時ライセンスページ](https://purchase.aspose.com/temporary-license/).

### Aspose.HTML for .NET のその他のチュートリアルやドキュメントはどこで入手できますか?
幅広いチュートリアルと詳細なドキュメントをご覧ください[Aspose.HTML ドキュメント](https://reference.aspose.com/html/net/)ページ。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
