---
title: Aspose.HTML を使用した .NET での環境構成
linktitle: .NETでの環境構成
second_title: Aspose.HTML .NET HTML 操作 API
description: スクリプト管理、カスタム スタイル、JavaScript 実行制御などのタスクに Aspose.HTML を使用して .NET で HTML ドキュメントを操作する方法を学びます。この包括的なチュートリアルでは、開始するための段階的な例と FAQ を提供します。
type: docs
weight: 10
url: /ja/net/advanced-features/environment-configuration/
---

今日のデジタル世界では、HTML ドキュメントの作成と操作は、多くの開発者にとって基本的なタスクです。 Web アプリケーションを構築している場合でも、HTML を PDF や画像などの他の形式に変換する必要がある場合でも、Aspose.HTML for .NET はツールキットに含めるべき強力なツールです。このチュートリアルでは、前提条件、名前空間のインポート、詳細な説明を含むステップバイステップの例など、Aspose.HTML for .NET のさまざまな側面を検討します。

## 前提条件

Aspose.HTML for .NET の使用に入る前に、次の前提条件が満たされていることを確認する必要があります。

1. Visual Studio: 開発マシンに Visual Studio がインストールされていることを確認してください。 Aspose.HTML for .NET は、Visual Studio とシームレスに連携するように設計されています。

2.  Aspose.HTML for .NET: Aspose.HTML for .NET ライブラリは Web サイトからダウンロードできます。次のリンクを使用してダウンロード ページにアクセスします。[.NET 用の Aspose.HTML をダウンロード](https://releases.aspose.com/html/net/).

3. インストールとライセンス: ライブラリをダウンロードした後、ドキュメントに記載されているインストール手順に従ってください。一部の高度な機能を使用するには、有効なライセンスが必要な場合もあります。ライセンスは、Aspose Web サイトから取得できます。[Aspose.HTML ライセンスを購入する](https://purchase.aspose.com/buy).

4. 無料トライアル: ライセンスを購入する前に Aspose.HTML を試してみたい場合は、次のリンクから無料トライアル バージョンを入手できます。[Aspose.HTML 無料トライアル](https://releases.aspose.com/).

必要な前提条件が揃ったので、次のセクションに進み、必要な名前空間をインポートします。

## 名前空間のインポート

Aspose.HTML for .NET を効果的に操作するには、適切な名前空間をプロジェクトにインポートする必要があります。以下に、これから説明する例に必要な名前空間をリストします。

```csharp
using Aspose.Html;
using Aspose.Html.Configuration;
using Aspose.Html.Sandbox;
using Aspose.Html.Services;
using Aspose.Html.Saving;
using System;
using System.IO;
```

これらの名前空間をインポートすると、Aspose.HTML for .NET が提供する機能にアクセスできます。

## スクリプトの実行を無効にする

HTML ドキュメント内でのスクリプトの実行を無効にして、それを PDF に変換する基本的な例から始めましょう。次の手順を実行します：

1. HTML コード スニペットを作成し、「document.html」という名前のファイルに保存します。

```csharp
var code = "<span>Hello World!!</span> " +
           "<script>document.write('Have a nice day!');</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. Aspose.HTML 構成を初期化し、「scripts」を信頼できないリソースとしてマークします。

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    configuration.Security |= Aspose.Html.Sandbox.Scripts;
    
    //指定された構成で HTML ドキュメントを初期化します。
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // HTML を PDF に変換する
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

この例では、HTML ドキュメント内のスクリプトの実行を防止し、PDF への変換時のセキュリティを確保しています。さて、次の例に進みましょう。

## ユーザースタイルシートの指定

場合によっては、HTML ドキュメント内の要素にカスタム スタイルを適用したい場合があります。 Aspose.HTML for .NET を使用してこれを行う方法は次のとおりです。

1. HTML コード スニペットを作成し、「document.html」という名前のファイルに保存します。

```csharp
var code = @"<span>Hello World!!!</span>";
System.IO.File.WriteAllText("document.html", code);
```

2. のカスタムカラーを設定します。`<span>`ユーザースタイルシートを使用した要素。

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var userAgent = configuration.GetService<Aspose.Html.Services.IUserAgentService>();
    userAgent.UserStyleSheet = "span { color: green; }";
    
    //指定された構成で HTML ドキュメントを初期化します。
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // HTML を PDF に変換する
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

この例では、カスタム スタイルを`<span>`要素のテキストの色を緑色に設定します。 Aspose.HTML for .NET を使用すると、スタイルを簡単に操作できます。

## JavaScriptの実行タイムアウト

時間がかかる可能性のある JavaScript コードを扱う場合、無期限の実行を防ぐためにタイムアウトを設定することが不可欠です。その方法は次のとおりです。

1. 無限ループを含む HTML コード スニペットを作成し、「document.html」という名前のファイルに保存します。

```csharp
var code = @"<script>while(true){}</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. JavaScript の実行タイムアウトを 10 秒に設定します。

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var runtime = configuration.GetService<Aspose.Html.Services.IRuntimeService>();
    runtime.JavaScriptTimeout = TimeSpan.FromSeconds(10);
    
    //指定された構成で HTML ドキュメントを初期化します。
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        //すべてのスクリプトが完了/キャンセルされるまで待って、HTML を PNG に変換します
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

この例では、JavaScript の実行時間を 10 秒に制限して、スクリプトが無期限に実行されないようにしています。これによりパフォーマンスの問題が発生する可能性があります。

## カスタムメッセージハンドラー

場合によっては、HTML ドキュメントをロードするときに、エラー メッセージや不足しているリソースの処理が必要になることがあります。カスタム メッセージ ハンドラーを作成する方法の例を次に示します。

1. 画像ファイル参照が欠落している HTML コード スニペットを作成し、「document.html」という名前のファイルに保存します。

```csharp
var code = @"<img src='missing.jpg'>";
System.IO.File.WriteAllText("document.html", code);
```

2. エラー メッセージ ハンドラーをネットワーク サービスに追加して、失敗した要求をログに記録します。

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var network = configuration.GetService<Aspose.Html.Services.INetworkService>();
    network.MessageHandlers.Add(new LogMessageHandler());
    
    //指定された構成で HTML ドキュメントを初期化します。
    //ドキュメントの読み込み中、アプリケーションは画像の読み込みを試行し、この操作の結果がコンソールに表示されます。
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // HTML を PNG に変換する
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

この例では、カスタム メッセージ ハンドラー (`LogMessageHandler`) 失敗したリクエストに関する情報をログに記録します。これは、不足しているリソースをデバッグしたり適切に処理したりする場合に特に役立ちます。

## 結論

Aspose.HTML for .NET は、開発者が HTML ドキュメントを効率的に操作できるようにする多用途ライブラリです。このチュートリアルでは、重要な概念を説明し、スクリプト管理、スタイルシートのカスタマイズ、JavaScript 実行制御、カスタム メッセージ処理などの一般的なタスクのステップバイステップの例を示しました。

このチュートリアルで概説されている手順に従うことで、Aspose.HTML for .NET の機能を活用して、.NET アプリケーションで HTML ドキュメントを自信を持って作成、操作、変換できます。

## よくある質問

### Q1: ライセンスを購入せずに Aspose.HTML for .NET を使用できますか?

A1: はい、無料試用版で Aspose.HTML for .NET を試すことができますが、一部の高度な機能には有効なライセンスが必要な場合があります。

### Q2: Aspose.HTML for .NET のライセンスを取得するにはどうすればよいですか?

 A2: Aspose Web サイトからライセンスを購入できます。[Aspose.HTML ライセンスを購入する](https://purchase.aspose.com/buy).

### Q3: Aspose.HTML for .NET を使用して HTML ドキュメントをどの形式に変換できますか?

A3: Aspose.HTML for .NET は、PDF、画像などを含むさまざまな形式への変換をサポートしています。

### Q4: Aspose.HTML for .NET のコミュニティまたはサポート フォーラムはありますか?

 A4: はい、Aspose フォーラムでヘルプとサポートを見つけることができます。[Aspose.HTML サポート フォーラム](https://forum.aspose.com/).

### Q5: Aspose.HTML for .NET にはドキュメントとチュートリアルが提供されていますか?

 A5: はい、ここからドキュメントにアクセスできます。[Aspose.HTML for .NET ドキュメント](https://reference.aspose.com/html/net/).