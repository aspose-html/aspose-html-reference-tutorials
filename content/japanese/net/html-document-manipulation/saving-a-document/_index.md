---
title: Aspose.HTML を使用して .NET にドキュメントを保存する
linktitle: .NET でのドキュメントの保存
second_title: Aspose.HTML .NET HTML 操作 API
description: ステップバイステップのガイドを使用して、Aspose.HTML for .NET の機能を最大限に活用してください。 HTML および SVG ドキュメントの作成、操作、変換方法を学びます
type: docs
weight: 16
url: /ja/net/html-document-manipulation/saving-a-document/
---

今日のデジタル時代では、HTML および SVG ドキュメントの作成と操作は、多くのソフトウェア開発者や企業にとって不可欠です。 Aspose.HTML for .NET は、これらのタスクを簡素化する強力なライブラリであり、HTML、SVG などを操作するためのさまざまな機能を提供します。この包括的なガイドでは、Aspose.HTML for .NET の要点を詳しく説明し、各例をわかりやすい手順に分けて説明します。経験豊富な開発者であっても、初心者であっても、このガイドは Aspose.HTML の機能を活用する上で非常に有益であることがわかります。

## 前提条件

この旅に着手する前に、必要なものがすべて揃っていることを確認してください。

- 開発環境: Visual Studio またはその他の .NET 開発環境がコンピュータにインストールされていることを確認してください。

- Aspose.HTML for .NET: Aspose.HTML for .NET ライブラリを取得する必要があります。からダウンロードできます[ここ](https://releases.aspose.com/html/net/).

- C# の知識: C# プログラミング言語に精通していると有益ですが、必須ではありません。このガイドは初心者向けに作成されています。

## 名前空間のインポート

Aspose.HTML for .NET の使用を開始するには、必要な名前空間をプロジェクトにインポートする必要があります。 C# コードに次の名前空間を含めます。

### ステップ 1: Aspose.HTML 名前空間をインポートする
```csharp
using Aspose.Html;
```

この名前空間により、さまざまな HTML および SVG 操作機能へのアクセスが許可されます。

## HTMLからファイルへ

### ステップ 1: 空の HTML ドキュメントを初期化する
```csharp
//空の HTML ドキュメントを初期化します。
using (var document = new Aspose.Html.HTMLDocument())
{
    //テキスト要素を作成してドキュメントに追加する
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    //HTML をディスク上のファイルに保存します。
    document.Save("document.html");
}
```

この例では、HTML ドキュメントを作成し、単純な「Hello World!」を追加します。それにテキストを送信します。次に、HTML をディスク上のファイルに保存します。

## リンクされたファイルのない HTML

### ステップ 1: 単純な HTML ファイルを準備する
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

ここでは、別のファイルへのアンカー リンクを含む基本的な HTML ファイルを作成します。

### ステップ 2: 「document.html」をメモリにロードする
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    //保存オプションのインスタンスを作成する
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    //リンクされた HTML ファイルを切り離すには、最大処理深度を 0 に設定します。
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    //文書を保存する
    document.Save(@".\html-to-file-example\document.html", options);
}
```

この例では、HTML ドキュメントをメモリにロードし、リンクされたファイルを切り離すための最大処理深度を設定し、ドキュメントを保存します。 

## HTMLからMHTMLへ

### ステップ 1: 単純な HTML ファイルを準備する
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

例 2 と同様に、別のファイルへのアンカー リンクを含む基本的な HTML ファイルを作成します。

### ステップ 2: 「document.html」をメモリにロードし、MHTML として保存する
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    //ドキュメントを MHTML として保存する
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

ここでは、HTML ドキュメントをメモリにロードし、MHTML 形式で保存します。

## HTMLからマークダウンへ

### ステップ 1: HTML コードを準備する
```csharp
var html_code = "<H2>Hello World!</H2>";
```

このステップでは、次の内容を含む HTML コード スニペットを定義します。`<H2>`要素。

### ステップ 2: HTML コードからドキュメントを初期化し、マークダウンとして保存する
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    //ドキュメントを Markdown ファイルとして保存します。
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

コード スニペットから HTML ドキュメントを作成し、Markdown ファイルとして保存します。

## SVGをファイルへ

### ステップ 1: SVG コードを準備する
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
    //SVG ファイルをディスクに保存します
    document.Save("document.svg");
}
```

このステップでは、コードから SVG ドキュメントを作成し、SVG ファイルとして保存します。

## 結論

Aspose.HTML for .NET は、.NET アプリケーションでの HTML および SVG ドキュメントの処理を簡素化する多用途ライブラリです。このガイドでは、5 つの重要な例を取り上げ、それぞれを段階的な手順に分けて説明しました。ドキュメントの作成、操作、変換のいずれを行う場合でも、Aspose.HTML が対応します。これらの手順に従うことで、この強力なツールをマスターできるようになります。

## よくある質問

### Q1: Aspose.HTML for .NET とは何ですか?

A1: Aspose.HTML for .NET は、作成、操作、変換など、HTML および SVG ドキュメントを操作するための幅広い機能を提供する .NET ライブラリです。

### Q2: .NET 用の Aspose.HTML はどこでダウンロードできますか?

 A2: Aspose.HTML for .NET は、次のサイトからダウンロードできます。[ここ](https://releases.aspose.com/html/net/).

### Q3: Aspose.HTML for .NET は初心者に適していますか?

A3: はい、Aspose.HTML for .NET は初心者と経験豊富な開発者の両方が使用できます。このガイドの例は初心者向けに設計されています。

### Q4: Aspose.HTML for .NET を使用して HTML を他の形式に変換できますか?

A4: はい、Aspose.HTML for .NET は、例に示すように、MHTML や Markdown などのさまざまな形式への変換をサポートしています。

### Q5: Aspose.HTML for .NET のサポートはどこで入手できますか?

 A5: Aspose.HTML コミュニティ フォーラムでサポートと質問への回答を見つけることができます。[ここ](https://forum.aspose.com/).