---
title: Aspose.HTML を使用して .NET でドキュメントを作成する
linktitle: .NET でドキュメントを作成する
second_title: Aspose.HTML .NET HTML 操作 API
description: Aspose.HTML for .NET のパワーを解き放ちましょう。HTML および SVG ドキュメントを簡単に作成、操作、最適化する方法を学びます。ステップバイステップの例と FAQ を調べます。
type: docs
weight: 14
url: /ja/net/html-document-manipulation/creating-a-document/
---

進化し続ける Web 開発の世界では、常に先を行くことが重要です。Aspose.HTML for .NET は、開発者に HTML ドキュメントを操作するための強力なツールキットを提供します。ゼロから始める場合、ファイルから読み込む場合、URL から取得する場合、または SVG ドキュメントを処理する場合など、このライブラリは必要な汎用性を提供します。

このステップバイステップ ガイドでは、Aspose.HTML for .NET の使用の基礎を詳しく説明し、Web 開発プロジェクトでこの強力なツールを活用できるように準備します。詳細に入る前に、旅を始めるための前提条件と必要な名前空間を確認しましょう。

## 前提条件

このチュートリアルを正しく実行し、Aspose.HTML for .NET のパワーを活用するには、次の前提条件が必要です。

- .NET Framework または .NET Core がインストールされた Windows マシン。
- Visual Studio のようなコード エディター。
- C# プログラミングの基礎知識。

前提条件が整いましたので、始めましょう。

## 名前空間のインポート

Aspose.HTML for .NET の使用を開始する前に、必要な名前空間をインポートする必要があります。これらの名前空間には、HTML ドキュメントの操作に不可欠なクラスとメソッドが含まれています。インポートする必要がある名前空間の一覧を以下に示します。

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

これらの名前空間をインポートしたら、ステップバイステップの例に進む準備が整いました。

## HTML ドキュメントをゼロから作成する

### ステップ1: 空のHTMLドキュメントを初期化する

```csharp
//空の HTML ドキュメントを初期化します。
using (var document = new Aspose.Html.HTMLDocument())
{
    //テキスト要素を作成し、ドキュメントに追加する
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    //ドキュメントをディスクに保存します。
    document.Save("document.html");
}
```

この例では、まず空の HTML ドキュメントを作成し、それに「Hello World!」というテキストを追加します。次に、ドキュメントをファイルに保存します。

## ファイルから HTML ドキュメントを作成する

### ステップ1: 「document.html」ファイルを準備する

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### ステップ2: 「document.html」ファイルから読み込む

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    //ドキュメントの内容を出力ストリームに書き込みます。
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

ここでは、「Hello World!」コンテンツを含むファイルを準備し、それを HTML ドキュメントとして読み込みます。ドキュメントのコンテンツをコンソールに出力します。

## URL から HTML ドキュメントを作成する

### ステップ1: Webページからドキュメントを読み込む

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    //ドキュメントの内容を出力ストリームに書き込みます。
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

この例では、Web ページから HTML ドキュメントを直接読み込み、そのコンテンツを表示します。

## 文字列から HTML ドキュメントを作成する

### ステップ1: HTMLコードを準備する

```csharp
var html_code = "<p>Hello World!</p>";
```

### ステップ2: 文字列変数からドキュメントを初期化する

```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    //ドキュメントをディスクに保存します。
    document.Save("document.html");
}
```

ここでは、文字列変数から HTML ドキュメントを作成し、ファイルに保存します。

## MemoryStream から HTML ドキュメントを作成する

### ステップ1: メモリストリームオブジェクトを作成する

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    //HTMLコードをメモリオブジェクトに書き込む
    sw.Write("<p>Hello World!</p>");
    //位置を先頭に設定する
    sw.Flush();
    mem.Seek(0, System.IO.SeekOrigin.Begin);
    //メモリストリームからドキュメントを初期化する
    using (var document = new Aspose.Html.HTMLDocument(mem, "."))
    {
        //ドキュメントをディスクに保存します。
        document.Save("document.html");
    }
}
```

この例では、メモリ ストリームから HTML ドキュメントを作成し、それをファイルに保存します。

## SVG ドキュメントの操作

### ステップ1: 文字列からSVGドキュメントを初期化する

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    //ドキュメントの内容を出力ストリームに書き込みます。
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

ここでは、文字列から SVG ドキュメントを作成して表示します。

## HTML ドキュメントを非同期に読み込む

### ステップ1: HTMLドキュメントのインスタンスを作成する

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### ステップ2: 「ReadyStateChange」イベントをサブスクライブする

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    //「ReadyState」プロパティの値を確認します。
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### ステップ3: 指定されたURIで非同期に移動する

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

この例では、HTML ドキュメントを非同期的に読み込み、読み込みが完了したらコンテンツを表示するために「ReadyStateChange」イベントを処理します。

## 「OnLoad」イベントの処理

### ステップ1: HTMLドキュメントのインスタンスを作成する

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### ステップ2: 「OnLoad」イベントをサブスクライブする

```csharp
document.OnLoad += (sender, @event) =>
{
    Console.WriteLine(document.DocumentElement.OuterHTML);
    Console.WriteLine("Loading is completed. Press any key to continue...");
};
```

### ステップ3: 指定されたURIで非同期に移動する

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

この例では、HTML ドキュメントを非同期的に読み込み、完了時にコンテンツを表示するために 'OnLoad' イベントを処理する方法を示します。

## 結論は

動的な Web 開発の世界では、適切なツールを自由に使えることが非常に重要です。Aspose.HTML for .NET は、HTML および SVG ドキュメントを効率的に作成、操作、処理する手段を提供します。この包括的なガイドでは、基本的な事項を順を追って説明し、プロジェクトで Aspose.HTML for .NET のパワーを活用できるようにします。

## よくある質問

### Q1: Aspose.HTML for .NET とは何ですか?

A1: Aspose.HTML for .NET は、開発者が HTML および SVG ドキュメントを操作できるようにする強力な .NET ライブラリです。ドキュメントを最初から作成することから、既存の HTML および SVG ファイルの解析と操作まで、幅広い機能を提供します。

### Q2: Aspose.HTML for .NET を .NET Core で使用できますか?

A2: はい、Aspose.HTML for .NET は .NET Framework と .NET Core の両方と互換性があるため、最新の .NET アプリケーションに最適な選択肢となります。

### Q3: Aspose.HTML for .NET は Web スクレイピングや解析に適していますか?

A3: もちろんです! Aspose.HTML for .NET は、URL や文字列から HTML ドキュメントを読み込む機能を備えているため、Web スクレイピングや解析タスクに最適です。データの抽出、分析の実行などが可能です。

### Q4: Aspose.HTML for .NET のサポートにアクセスするにはどうすればいいですか?

 A4: Aspose.HTML for .NETの使用中に問題が発生した場合や質問がある場合は、[Aspose フォーラム](https://forum.aspose.com/)コミュニティと Aspose の専門家からのサポートと支援を受けられます。

### A5: 詳細なドキュメントとダウンロード オプションはどこにありますか?

A5: 包括的なドキュメントとダウンロード オプションへのアクセスについては、次のリンクを参照してください。

- [ドキュメント](https://reference.aspose.com/html/net/)
- [ダウンロード](https://releases.aspose.com/html/net/)
- [買う](https://purchase.aspose.com/buy)
- [無料トライアル](https://releases.aspose.com/)
- [一時ライセンス](https://purchase.aspose.com/temporary-license/)