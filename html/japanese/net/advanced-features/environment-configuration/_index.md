---
title: Aspose.HTML を使用した .NET の環境構成
linktitle: .NET での環境構成
second_title: Aspose.HTML .NET HTML 操作 API
description: スクリプト管理、カスタム スタイル、JavaScript 実行制御などのタスクに Aspose.HTML を使用して .NET で HTML ドキュメントを操作する方法を学習します。この包括的なチュートリアルでは、開始するためのステップバイステップの例と FAQ を提供します。
weight: 10
url: /ja/net/advanced-features/environment-configuration/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML を使用した .NET の環境構成


今日のデジタル世界では、HTML ドキュメントの作成と操作は多くの開発者にとって基本的なタスクです。Web アプリケーションを構築する場合でも、HTML を PDF や画像などの他の形式に変換する必要がある場合でも、Aspose.HTML for .NET はツールキットに備えておきたい強力なツールです。このチュートリアルでは、前提条件、名前空間のインポート、詳細な説明付きのステップバイステップの例など、Aspose.HTML for .NET のさまざまな側面について説明します。

## 前提条件

Aspose.HTML for .NET の使用を開始する前に、次の前提条件が満たされていることを確認する必要があります。

1. Visual Studio: 開発マシンに Visual Studio がインストールされていることを確認してください。Aspose.HTML for .NET は Visual Studio とシームレスに連携するように設計されています。

2.  Aspose.HTML for .NET: Aspose.HTML for .NET ライブラリは Web サイトからダウンロードできます。ダウンロード ページにアクセスするには、次のリンクを使用します。[Aspose.HTML for .NET をダウンロード](https://releases.aspose.com/html/net/).

3. インストールとライセンス: ライブラリをダウンロードしたら、ドキュメントに記載されているインストール手順に従ってください。一部の高度な機能を使用するには、有効なライセンスが必要になる場合もあります。ライセンスは Aspose Web サイトから取得できます。[Aspose.HTML ライセンスを購入する](https://purchase.aspose.com/buy).

4. 無料トライアル: ライセンスを購入する前に Aspose.HTML を試してみたい場合は、次のリンクから無料トライアル版を入手できます。[Aspose.HTML 無料トライアル](https://releases.aspose.com/).

必要な前提条件が揃ったので、次のセクションに進み、必要な名前空間をインポートしましょう。

## 名前空間のインポート

Aspose.HTML for .NET を効果的に使用するには、適切な名前空間をプロジェクトにインポートする必要があります。以下に、ここで説明する例に必要な名前空間を示します。

```csharp
using Aspose.Html;
using Aspose.Html.Configuration;
using Aspose.Html.Sandbox;
using Aspose.Html.Services;
using Aspose.Html.Saving;
using System;
using System.IO;
```

これらの名前空間をインポートすると、Aspose.HTML for .NET によって提供される機能にアクセスできるようになります。

## スクリプトの実行を無効にする

まず、HTML ドキュメント内でのスクリプト実行を無効にして PDF に変換する基本的な例から始めましょう。次の手順に従います。

1. HTML コード スニペットを作成し、「document.html」という名前のファイルに保存します。

```csharp
var code = "<span>Hello World!!</span> " +
           "<script>document.write('Have a nice day!');</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. Aspose.HTML 構成を初期化し、「スクリプト」を信頼できないリソースとしてマークします。

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    configuration.Security |= Aspose.Html.Sandbox.Scripts;
    
    //指定された構成でHTMLドキュメントを初期化する
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // HTMLをPDFに変換する
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

この例では、HTML ドキュメント内でのスクリプトの実行を防止し、PDF への変換中にセキュリティを確保しています。それでは、次の例に進みましょう。

## ユーザースタイルシートを指定する

場合によっては、HTML ドキュメント内の要素にカスタム スタイルを適用したいことがあります。Aspose.HTML for .NET を使用してこれを行う方法は次のとおりです。

1. HTML コード スニペットを作成し、「document.html」という名前のファイルに保存します。

```csharp
var code = @"<span>Hello World!!!</span>";
System.IO.File.WriteAllText("document.html", code);
```

2. カスタムカラーを設定する`<span>`ユーザー スタイルシートを使用する要素。

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var userAgent = configuration.GetService<Aspose.Html.Services.IUserAgentService>();
    userAgent.UserStyleSheet = "span { color: green; }";
    
    //指定された構成でHTMLドキュメントを初期化する
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // HTMLをPDFに変換する
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

この例では、カスタムスタイルを`<span>`要素のテキストの色を緑に設定します。Aspose.HTML for .NET を使用すると、スタイルを簡単に操作できます。

## JavaScript 実行タイムアウト

時間のかかる可能性のある JavaScript コードを扱う場合、無期限の実行を防ぐためにタイムアウトを設定することが重要です。その方法は次のとおりです。

1. 無限ループを含む HTML コード スニペットを作成し、「document.html」という名前のファイルに保存します。

```csharp
var code = @"<script>while(true){}</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. JavaScript 実行タイムアウトを 10 秒に設定します。

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var runtime = configuration.GetService<Aspose.Html.Services.IRuntimeService>();
    runtime.JavaScriptTimeout = TimeSpan.FromSeconds(10);
    
    //指定された構成でHTMLドキュメントを初期化する
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        //すべてのスクリプトが終了/キャンセルされるまで待ってから、HTMLをPNGに変換します。
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

この例では、JavaScript の実行時間を 10 秒に制限して、スクリプトが無期限に実行されないようにし、パフォーマンスの問題が発生する可能性を回避しています。

## カスタムメッセージハンドラー

HTML ドキュメントを読み込むときに、エラー メッセージや不足しているリソースを処理する必要がある場合があります。カスタム メッセージ ハンドラーを作成する方法の例を次に示します。

1. 画像ファイル参照が欠落している HTML コード スニペットを作成し、「document.html」という名前のファイルに保存します。

```csharp
var code = @"<img src='missing.jpg'>";
System.IO.File.WriteAllText("document.html", code);
```

2. 失敗した要求をログに記録するには、ネットワーク サービスにエラー メッセージ ハンドラーを追加します。

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var network = configuration.GetService<Aspose.Html.Services.INetworkService>();
    network.MessageHandlers.Add(new LogMessageHandler());
    
    //指定された構成でHTMLドキュメントを初期化する
    //ドキュメントの読み込み中に、アプリケーションはイメージの読み込みを試み、この操作の結果がコンソールに表示されます。
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // HTML を PNG に変換する
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

この例では、カスタムメッセージハンドラー（`LogMessageHandler`) を使用して、失敗したリクエストに関する情報をログに記録します。これは、不足しているリソースを適切にデバッグおよび処理する場合に特に便利です。

## 結論

Aspose.HTML for .NET は、開発者が HTML ドキュメントを効率的に操作できるようにする多目的ライブラリです。このチュートリアルでは、スクリプト管理、スタイルシートのカスタマイズ、JavaScript 実行制御、カスタム メッセージ処理などの一般的なタスクの基本的な概念と手順ごとの例を説明しました。

このチュートリアルで説明されている手順に従うことで、Aspose.HTML for .NET の機能を活用して、.NET アプリケーションで HTML ドキュメントを自信を持って作成、操作、変換できるようになります。

## よくある質問

### Q1: ライセンスを購入せずに Aspose.HTML for .NET を使用できますか?

A1: はい、Aspose.HTML for .NET を無料試用版で試すことができます。ただし、一部の高度な機能には有効なライセンスが必要になる場合があります。

### Q2: Aspose.HTML for .NET のライセンスを取得するにはどうすればよいですか?

 A2: ライセンスは Aspose の Web サイトから購入できます。[Aspose.HTML ライセンスを購入する](https://purchase.aspose.com/buy).

### Q3: Aspose.HTML for .NET を使用して HTML ドキュメントをどのような形式に変換できますか?

A3: Aspose.HTML for .NET は、PDF、画像など、さまざまな形式への変換をサポートしています。

### Q4: Aspose.HTML for .NET のコミュニティまたはサポート フォーラムはありますか?

 A4: はい、Aspose フォーラムでヘルプとサポートを見つけることができます。[Aspose.HTML サポート フォーラム](https://forum.aspose.com/).

### Q5: Aspose.HTML for .NET にはドキュメントやチュートリアルが用意されていますか?

 A5: はい、こちらからドキュメントにアクセスできます:[Aspose.HTML for .NET ドキュメント](https://reference.aspose.com/html/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
