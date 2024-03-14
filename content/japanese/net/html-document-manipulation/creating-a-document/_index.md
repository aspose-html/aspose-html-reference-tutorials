---
title: Aspose.HTML を使用して .NET でドキュメントを作成する
linktitle: .NETでのドキュメントの作成
second_title: Aspose.HTML .NET HTML 操作 API
description: Aspose.HTML for .NET のパワーを解き放ちます。 HTML および SVG ドキュメントを簡単に作成、操作、最適化する方法を学びます。ステップバイステップの例とよくある質問をご覧ください。
type: docs
weight: 14
url: /ja/net/html-document-manipulation/creating-a-document/
---

進化し続ける Web 開発の世界では、時代の先を行くことが不可欠です。 Aspose.HTML for .NET は、HTML ドキュメントを操作するための堅牢なツールキットを開発者に提供します。最初から始める場合でも、ファイルからロードする場合でも、URL から取得する場合でも、SVG ドキュメントを処理する場合でも、このライブラリは必要な多用途性を提供します。

このステップバイステップ ガイドでは、Aspose.HTML for .NET の使用の基礎を詳しく説明し、Web 開発プロジェクトでこの強力なツールを活用するための十分な準備が整っていることを確認します。詳細に入る前に、作業を開始するための前提条件と必要な名前空間について確認しましょう。

## 前提条件

このチュートリアルを正しく実行し、Aspose.HTML for .NET の機能を活用するには、次の前提条件が必要です。

- .NET Framework または .NET Core がインストールされた Windows マシン。
- Visual Studio のようなコード エディター。
- C# プログラミングの基本的な知識。

前提条件が整ったので、始めましょう。

## 名前空間のインポート

Aspose.HTML for .NET の使用を開始する前に、必要な名前空間をインポートする必要があります。これらの名前空間には、HTML ドキュメントを操作するために不可欠なクラスとメソッドが含まれています。以下は、インポートする必要がある名前空間のリストです。

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

これらの名前空間をインポートしたら、段階的な例に進む準備が整いました。

## HTML ドキュメントを最初から作成する

### ステップ 1: 空の HTML ドキュメントを初期化する

```csharp
//空の HTML ドキュメントを初期化します。
using (var document = new Aspose.Html.HTMLDocument())
{
    //テキスト要素を作成してドキュメントに追加する
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    //ドキュメントをディスクに保存します。
    document.Save("document.html");
}
```

この例では、まず空の HTML ドキュメントを作成し、「Hello World!」を追加します。それにテキストを送信します。次に、ドキュメントをファイルに保存します。

## ファイルから HTML ドキュメントを作成する

### ステップ 1: 「document.html」ファイルを準備する

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### ステップ 2: 「document.html」ファイルからロードする

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    //ドキュメントのコンテンツを出力ストリームに書き込みます。
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

ここでは「Hello World!」と書かれたファイルを用意します。コンテンツを抽出し、HTML ドキュメントとしてロードします。ドキュメントのコンテンツをコンソールに出力します。

## URL から HTML ドキュメントを作成する

### ステップ 1: Web ページからドキュメントをロードする

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    //ドキュメントのコンテンツを出力ストリームに書き込みます。
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

この例では、Web ページから HTML ドキュメントを直接ロードし、そのコンテンツを表示します。

## 文字列から HTML ドキュメントを作成する

### ステップ 1: HTML コードを準備する

```csharp
var html_code = "<p>Hello World!</p>";
```

### ステップ 2: 文字列変数からドキュメントを初期化する

```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    //ドキュメントをディスクに保存します。
    document.Save("document.html");
}
```

ここでは、文字列変数から HTML ドキュメントを作成し、ファイルに保存します。

## MemoryStream から HTML ドキュメントを作成する

### ステップ 1: メモリ ストリーム オブジェクトを作成する

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    //HTMLコードをメモリオブジェクトに書き込みます。
    sw.Write("<p>Hello World!</p>");
    //位置を先頭に設定します
    sw.Flush();
    mem.Seek(0, System.IO.SeekOrigin.Begin);
    //メモリストリームからドキュメントを初期化します
    using (var document = new Aspose.Html.HTMLDocument(mem, "."))
    {
        //ドキュメントをディスクに保存します。
        document.Save("document.html");
    }
}
```

この例では、メモリ ストリームから HTML ドキュメントを作成し、ファイルに保存します。

## SVG ドキュメントの操作

### ステップ 1: 文字列から SVG ドキュメントを初期化する

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    //ドキュメントのコンテンツを出力ストリームに書き込みます。
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

ここでは、文字列から SVG ドキュメントを作成して表示します。

## HTML ドキュメントの非同期ロード

### ステップ 1: HTML ドキュメントのインスタンスを作成する

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### ステップ 2: 「ReadyStateChange」イベントをサブスクライブする

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    //「ReadyState」プロパティの値を確認してください。
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### ステップ 3: 指定された Uri で非同期に移動する

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

この例では、HTML ドキュメントを非同期的にロードし、「ReadyStateChange」イベントを処理して、ロードの完了時にコンテンツを表示します。

## 「OnLoad」イベントの処理

### ステップ 1: HTML ドキュメントのインスタンスを作成する

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### ステップ 2: 「OnLoad」イベントをサブスクライブする

```csharp
document.OnLoad += (sender, @event) =>
{
    Console.WriteLine(document.DocumentElement.OuterHTML);
    Console.WriteLine("Loading is completed. Press any key to continue...");
};
```

### ステップ 3: 指定された Uri で非同期に移動する

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

この例では、HTML ドキュメントを非同期でロードし、「OnLoad」イベントを処理して完了時にコンテンツを表示する方法を示します。

## 結論は

Web 開発のダイナミックな世界では、適切なツールを自由に使えることが非常に重要です。 Aspose.HTML for .NET は、HTML および SVG ドキュメントを効率的に作成、操作、処理する手段を提供します。この包括的なガイドでは、プロジェクトで Aspose.HTML for .NET の機能を確実に活用できるように、要点を説明しています。

## よくある質問

### Q1: Aspose.HTML for .NET とは何ですか?

A1: Aspose.HTML for .NET は、開発者が HTML および SVG ドキュメントを操作できるようにする強力な .NET ライブラリです。ドキュメントを最初から作成することから、既存の HTML および SVG ファイルの解析と操作まで、幅広い機能を提供します。

### Q2: Aspose.HTML for .NET を .NET Core で使用できますか?

A2: はい、Aspose.HTML for .NET は .NET Framework と .NET Core の両方と互換性があるため、最新の .NET アプリケーションにとって多用途の選択肢となります。

### Q3: Aspose.HTML for .NET は Web スクレイピングと解析に適していますか?

A3：もちろんです！ Aspose.HTML for .NET は、URL や文字列から HTML ドキュメントを読み込む機能があるため、Web スクレイピングおよび解析タスクに最適です。データの抽出、分析などを実行できます。

### Q4: Aspose.HTML for .NET のサポートにアクセスするにはどうすればよいですか?

 A4: Aspose.HTML for .NET の使用中に問題が発生したり質問がある場合は、次のサイトにアクセスしてください。[アスペス フォーラム](https://forum.aspose.com/)コミュニティおよび Aspose の専門家からのサポートと援助が必要です。

### A5: 詳細なドキュメントとダウンロード オプションはどこで見つけられますか?

A5: 包括的なドキュメントとダウンロード オプションへのアクセスについては、次のリンクを参照してください。

- [ドキュメンテーション](https://reference.aspose.com/html/net/)
- [ダウンロード](https://releases.aspose.com/html/net/)
- [買う](https://purchase.aspose.com/buy)
- [無料トライアル](https://releases.aspose.com/)
- [仮免許](https://purchase.aspose.com/temporary-license/)