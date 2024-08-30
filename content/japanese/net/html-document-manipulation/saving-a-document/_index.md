---
title: Aspose.HTML を使用して .NET でドキュメントを保存する
linktitle: .NET でドキュメントを保存する
second_title: Aspose.HTML .NET HTML 操作 API
description: ステップバイステップガイドで Aspose.HTML for .NET のパワーを解き放ちましょう。HTML および SVG ドキュメントの作成、操作、変換方法を学びます。
type: docs
weight: 16
url: /ja/net/html-document-manipulation/saving-a-document/
---

今日のデジタル時代では、HTML および SVG ドキュメントの作成と操作は、多くのソフトウェア開発者や企業にとって不可欠です。Aspose.HTML for .NET は、これらのタスクを簡素化し、HTML、SVG などを操作するさまざまな機能を提供する強力なライブラリです。この包括的なガイドでは、Aspose.HTML for .NET の基本を詳しく説明し、各例をわかりやすい手順に分解します。熟練した開発者でも、始めたばかりの開発者でも、このガイドは Aspose.HTML の機能を活用する上で非常に役立ちます。

## 前提条件

この旅に出発する前に、必要なものがすべて揃っていることを確認しましょう。

- 開発環境: コンピューターに Visual Studio またはその他の .NET 開発環境がインストールされていることを確認します。

- Aspose.HTML for .NET: Aspose.HTML for .NETライブラリを入手する必要があります。ダウンロードはこちらからできます。[ここ](https://releases.aspose.com/html/net/).

- C# の知識: C# プログラミング言語の知識があると有利ですが、必須ではありません。このガイドは初心者向けに設計されています。

## 名前空間のインポート

Aspose.HTML for .NET の使用を開始するには、必要な名前空間をプロジェクトにインポートする必要があります。C# コードに次の名前空間を含めます。

### ステップ 1: Aspose.HTML 名前空間をインポートする
```csharp
using Aspose.Html;
```

この名前空間により、さまざまな HTML および SVG 操作機能にアクセスできるようになります。

## HTML からファイルへ

### ステップ1: 空のHTMLドキュメントを初期化する
```csharp
//空の HTML ドキュメントを初期化します。
using (var document = new Aspose.Html.HTMLDocument())
{
    //テキスト要素を作成し、ドキュメントに追加する
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    //HTML をディスク上のファイルに保存します。
    document.Save("document.html");
}
```

この例では、HTML ドキュメントを作成し、それに単純な「Hello World!」テキストを追加します。次に、HTML をディスク上のファイルに保存します。

## リンクファイルなしの HTML

### ステップ1: シンプルなHTMLファイルを準備する
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

ここでは、別のファイルへのアンカー リンクを含む基本的な HTML ファイルを作成します。

### ステップ2: 'document.html'をメモリにロードする
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    //保存オプションインスタンスを作成する
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    //リンクされた HTML ファイルを切断するには、最大処理深度を 0 に設定します。
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    //文書を保存する
    document.Save(@".\html-to-file-example\document.html", options);
}
```

この例では、HTML ドキュメントをメモリに読み込み、リンクされたファイルを切り取るための最大処理深度を設定して、ドキュメントを保存します。 

## HTML から MHTML へ

### ステップ1: シンプルなHTMLファイルを準備する
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

例 2 と同様に、別のファイルへのアンカー リンクを含む基本的な HTML ファイルを作成します。

### ステップ2: 「document.html」をメモリに読み込み、MHTMLとして保存する
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    //ドキュメントをMHTMLとして保存する
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

ここでは、HTML ドキュメントをメモリに読み込み、MHTML 形式で保存します。

## HTML から Markdown へ

### ステップ1: HTMLコードを準備する
```csharp
var html_code = "<H2>Hello World!</H2>";
```

このステップでは、HTMLコードスニペットを定義します。`<H2>`要素。

### ステップ2: HTMLコードからドキュメントを初期化し、Markdownとして保存する
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    //ドキュメントを Markdown ファイルとして保存します。
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

コード スニペットから HTML ドキュメントを作成し、それを Markdown ファイルとして保存します。

## SVG からファイルへ

### ステップ1: SVGコードを準備する
```csharp
var code = @"
    <svg xmlns='http://www.w3.org/2000/svg' 高さ='80' 幅='300'>
        <g fill='none'>
            <path stroke='red' d='M5 20 l215 0' />
            <path stroke='black' d='M5 40 l215 0' />
            <path stroke='blue' d='M5 60 l215 0' />
        </g>
    </svg>";
```

ここでは、シンプルでカラフルなグラフィックを描画する SVG コードを作成します。

### ステップ 2: コードから SVG ドキュメントを初期化し、ディスクに保存する
```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument(code, "."))
{
    //SVGファイルをディスクに保存する
    document.Save("document.svg");
}
```

このステップでは、コードから SVG ドキュメントを作成し、SVG ファイルとして保存します。

## 結論

Aspose.HTML for .NET は、.NET アプリケーションでの HTML および SVG ドキュメントの処理を簡素化する多目的ライブラリです。このガイドでは、5 つの重要な例を取り上げ、それぞれをステップ バイ ステップの手順に分解して説明しています。ドキュメントの作成、操作、または変換のいずれを行う場合でも、Aspose.HTML が役立ちます。これらの手順に従うことで、この強力なツールを習得する準備が整います。

## よくある質問

### Q1: Aspose.HTML for .NET とは何ですか?

A1: Aspose.HTML for .NET は、HTML および SVG ドキュメントの作成、操作、変換など、さまざまな機能を提供する .NET ライブラリです。

### Q2: Aspose.HTML for .NET はどこからダウンロードできますか?

 A2: Aspose.HTML for .NETは以下からダウンロードできます。[ここ](https://releases.aspose.com/html/net/).

### Q3: Aspose.HTML for .NET は初心者に適していますか?

A3: はい、Aspose.HTML for .NET は初心者と経験豊富な開発者の両方が使用できます。このガイドの例は初心者向けに設計されています。

### Q4: Aspose.HTML for .NET を使用して HTML を他の形式に変換できますか?

A4: はい、Aspose.HTML for .NET は、例に示すように、MHTML や Markdown を含むさまざまな形式への変換をサポートしています。

### Q5: Aspose.HTML for .NET のサポートはどこで受けられますか?

 A5: Aspose.HTMLコミュニティフォーラムでサポートや質問への回答を見つけることができます。[ここ](https://forum.aspose.com/).