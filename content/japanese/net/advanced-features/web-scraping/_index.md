---
title: Aspose.HTML を使用した .NET での Web スクレイピング
linktitle: .NETでのWebスクレイピング
second_title: Aspose.HTML .NET HTML 操作 API
description: Aspose.HTML を使用して .NET で HTML ドキュメントを操作する方法を学びます。要素を効果的に移動、フィルター、クエリ、選択して、Web 開発を強化します。
type: docs
weight: 13
url: /ja/net/advanced-features/web-scraping/
---

今日のデジタル時代では、HTML ドキュメントから情報を操作して抽出することは、開発者にとって一般的なタスクです。 Aspose.HTML for .NET は、.NET アプリケーションでの HTML の処理と操作を簡素化する強力なツールです。このチュートリアルでは、前提条件、名前空間、その可能性を最大限に活用するためのステップバイステップの例など、Aspose.HTML for .NET のさまざまな側面を検討します。

## 前提条件

Aspose.HTML for .NET の世界に飛び込む前に、いくつかの前提条件が必要です。

1. 開発環境: Visual Studio またはその他の .NET 開発用の互換性のある IDE を使用して、作業可能な開発環境がセットアップされていることを確認します。

2.  Aspose.HTML for .NET: Aspose.HTML for .NET ライブラリを次の場所からダウンロードしてインストールします。[ダウンロードリンク](https://releases.aspose.com/html/net/)。ニーズに応じて、無料試用版とライセンス版のどちらかを選択できます。

3. HTML の基本知識: Aspose.HTML for .NET を効果的に使用するには、HTML の構造と要素を理解することが不可欠です。

## 名前空間のインポート

まず、必要な名前空間を C# プロジェクトにインポートする必要があります。これらの名前空間は、Aspose.HTML for .NET クラスおよび機能へのアクセスを提供します。

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.XPath;
using Aspose.Html.Css;
```

前提条件が整い、名前空間がインポートされたので、いくつかの主要な例を段階的に説明して、Aspose.HTML for .NET を効果的に使用する方法を説明します。

## HTML 内を移動する

この例では、HTML ドキュメント内を移動し、その要素に段階的にアクセスします。

```csharp
public static void NavigateThroughHTML()
{
    // HTMLコードを用意する
    var html_code = "<span>Hello</span> <span>World!</span>";
    
    //準備されたコードからドキュメントを初期化する
    using (var document = new HTMLDocument(html_code, "."))
    {
        //BODY の最初の子 (最初の SPAN) への参照を取得します。
        var element = document.Body.FirstChild;
        Console.WriteLine(element.TextContent); //出力: こんにちは

        //HTML要素間の空白への参照を取得します。
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); //出力: ' '

        // 2 番目の SPAN 要素への参照を取得します
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); //出力: 世界!
    }
}
```

この例では、HTML ドキュメントを作成し、その最初の子 (`SPAN`要素)、要素間の空白、および 2 番目の`SPAN`要素。基本的なナビゲーションを示します。

## ノードフィルターの使用

ノード フィルターを使用すると、HTML ドキュメント内の特定の要素を選択的に処理できます。

```csharp
public static void NodeFilterUsageExample()
{
    // HTMLコードを用意する
    var code = @"
        <p>Hello</p>
        <img src='image1.png'>
        <img src='image2.png'>
        <p>World!</p>";
    
    //準備されたコードに基づいてドキュメントを初期化します
    using (var document = new HTMLDocument(code, "."))
    {
        //画像要素のカスタム フィルターを使用して TreeWalker を作成する
        using (var iterator = document.CreateTreeWalker(document, NodeFilter.SHOW_ALL, new OnlyImageFilter()))
        {
            while (iterator.NextNode() != null)
            {
                var image = (HTMLImageElement)iterator.CurrentNode;
                Console.WriteLine(image.Src);
                //出力: image1.png
                //出力: image2.png
            }
        }
    }
}
```

この例では、カスタム ノード フィルターを使用して特定の要素を抽出する方法を示します (この場合、`IMG`要素)を HTML ドキュメントから取得します。

## XPath クエリ

XPath クエリを使用すると、特定の基準に基づいて HTML ドキュメント内の要素を検索できます。

```csharp
public static void XPathQueryUsageExample()
{
    // HTMLコードを用意する
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello!</span>
            </div>
        </div>
        <p class='happy'>
            <span>World</span>
        </p>
    ";
    
    //準備されたコードに基づいてドキュメントを初期化します
    using (var document = new HTMLDocument(code, "."))
    {
        // XPath 式を評価して特定の要素を選択する
        var result = document.Evaluate("//*[@class='happy']//スパン",
                                        document,
                                        null,
                                        XPathResultType.Any,
                                        null);
        
        //結果のノードを反復処理する
        for (Node node; (node = result.IterateNext()) != null;)
        {
            Console.WriteLine(node.TextContent);
            //出力: こんにちは
            //出力: 世界!
        }
    }
}
```

この例では、XPath クエリを使用して、属性と構造に基づいて HTML ドキュメント内の要素を検索する方法を示します。

## CSSセレクター

CSS セレクターは、CSS スタイルシートが要素をターゲットとする方法と同様に、HTML ドキュメント内の要素を選択するための代替方法を提供します。

```csharp
public static void CSSSelectorUsageExample()
{
    // HTMLコードを用意する
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello</span>
            </div>
        </div>
        <p class='happy'>
            <span>World!</span>
        </p>
    ";
    
    //準備されたコードに基づいてドキュメントを初期化します
    using (var document = new HTMLDocument(code, "."))
    {
        //CSS セレクターを使用して、クラスと階層に基づいて要素を抽出します
        var elements = document.QuerySelectorAll(".happy span");
        
        //結果として得られる要素のリストを反復処理します。
        foreach (HTMLElement element in elements)
        {
            Console.WriteLine(element.InnerHTML);
            //出力: こんにちは
            //出力: 世界!
        }
    }
}
```

ここでは、CSS セレクターを使用して HTML ドキュメント内の特定の要素をターゲットにする方法を示します。

これらの例により、Aspose.HTML for .NET を使用して HTML ドキュメント内の要素を移動、フィルター、クエリ、および選択する方法の基礎を理解できました。

## 結論

 Aspose.HTML for .NET は、.NET 開発者が HTML ドキュメントを効率的に操作できるようにする多用途ライブラリです。ナビゲーション、フィルタリング、クエリ、要素の選択などの強力な機能を備えているため、さまざまな HTML 処理タスクをシームレスに処理できます。このチュートリアルに従い、次のドキュメントを参照してください。[Aspose.HTML for .NET ドキュメント](https://reference.aspose.com/html/net/)を使用すると、.NET アプリケーションに対してこのツールの可能性を最大限に引き出すことができます。

## よくある質問

### Q1. Aspose.HTML for .NET は無料で使用できますか?

A1: Aspose.HTML for .NET は無料の試用版を提供していますが、運用環境で使用するにはライセンスを購入する必要があります。ライセンスの詳細とオプションについては、次のサイトで確認できます。[Aspose.HTML の購入](https://purchase.aspose.com/buy).

### Q2. Aspose.HTML for .NET の一時ライセンスを取得するにはどうすればよいですか?

 A2: テスト目的の一時ライセンスは、以下から取得できます。[Aspose.HTML 一時ライセンス](https://purchase.aspose.com/temporary-license/).

### Q3. Aspose.HTML for .NET のヘルプやサポートはどこに問い合わせればよいですか?

 A3: 問題が発生したり質問がある場合は、次のサイトにアクセスしてください。[Aspose.HTML フォーラム](https://forum.aspose.com/)援助とコミュニティサポートのために。

### Q4. Aspose.HTML for .NET を学習するための追加リソースはありますか?

 A4: このチュートリアルに加えて、さらに多くのチュートリアルやドキュメントを参照できます。[Aspose.HTML for .NET ドキュメント ページ](https://reference.aspose.com/html/net/).

### Q5. Aspose.HTML for .NET は最新の .NET バージョンと互換性がありますか?

A5: Aspose.HTML for .NET は、最新の .NET バージョンおよびテクノロジとの互換性を確保するために定期的に更新されます。