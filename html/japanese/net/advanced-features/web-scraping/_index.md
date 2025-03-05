---
title: Aspose.HTML を使用した .NET での Web スクレイピング
linktitle: .NET での Web スクレイピング
second_title: Aspose.HTML .NET HTML 操作 API
description: Aspose.HTML を使用して .NET で HTML ドキュメントを操作する方法を学びます。要素を効果的にナビゲート、フィルター処理、クエリ、選択して、Web 開発を強化します。
type: docs
weight: 13
url: /ja/net/advanced-features/web-scraping/
---

今日のデジタル時代では、HTML ドキュメントから情報を操作したり抽出したりすることは、開発者にとって一般的なタスクです。Aspose.HTML for .NET は、.NET アプリケーションでの HTML の処理と操作を簡素化する強力なツールです。このチュートリアルでは、前提条件、名前空間、ステップバイステップの例など、Aspose.HTML for .NET のさまざまな側面を取り上げ、その可能性を最大限に活用できるようにします。

## 前提条件

Aspose.HTML for .NET の世界に飛び込む前に、いくつかの前提条件を満たす必要があります。

1. 開発環境: Visual Studio または .NET 開発用のその他の互換性のある IDE を使用して、機能する開発環境が設定されていることを確認します。

2.  Aspose.HTML for .NET: Aspose.HTML for .NETライブラリを以下のサイトからダウンロードしてインストールします。[ダウンロードリンク](https://releases.aspose.com/html/net/)ニーズに応じて、無料試用版またはライセンス版を選択できます。

3. HTML の基礎知識: Aspose.HTML for .NET を効果的に使用するには、HTML の構造と要素を理解していることが不可欠です。

## 名前空間のインポート

まず、C# プロジェクトに必要な名前空間をインポートする必要があります。これらの名前空間は、Aspose.HTML for .NET のクラスと機能へのアクセスを提供します。

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.XPath;
using Aspose.Html.Css;
```

前提条件が整い、名前空間がインポートされたので、Aspose.HTML for .NET を効果的に使用する方法を説明するために、いくつかの重要な例を段階的に説明しましょう。

## HTML でのナビゲーション

この例では、HTML ドキュメント内を移動し、その要素に段階的にアクセスします。

```csharp
public static void NavigateThroughHTML()
{
    // HTMLコードを準備する
    var html_code = "<span>Hello</span> <span>World!</span>";
    
    //準備したコードからドキュメントを初期化する
    using (var document = new HTMLDocument(html_code, "."))
    {
        //BODYの最初の子（最初のSPAN）への参照を取得します。
        var element = document.Body.FirstChild;
        Console.WriteLine(element.TextContent); //出力: こんにちは

        //HTML要素間の空白への参照を取得する
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); //出力: ' '

        // 2番目のSPAN要素への参照を取得する
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); //出力: World!
    }
}
```

この例では、HTML文書を作成し、その最初の子（`SPAN`要素）、要素間の空白、および2番目の`SPAN`基本的なナビゲーションを示す要素。

## ノードフィルターの使用

ノード フィルターを使用すると、HTML ドキュメント内の特定の要素を選択的に処理できます。

```csharp
public static void NodeFilterUsageExample()
{
    // HTMLコードを準備する
    var code = @"
        <p>Hello</p>
        <img src='image1.png'>
        <img src='image2.png'>
        <p>World!</p>";
    
    //準備したコードに基づいてドキュメントを初期化する
    using (var document = new HTMLDocument(code, "."))
    {
        //画像要素用のカスタムフィルターを備えた TreeWalker を作成する
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

この例では、カスタムノードフィルターを使用して特定の要素（この場合は`IMG`HTML ドキュメントから要素を削除します。

## XPath クエリ

XPath クエリを使用すると、特定の条件に基づいて HTML ドキュメント内の要素を検索できます。

```csharp
public static void XPathQueryUsageExample()
{
    // HTMLコードを準備する
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
    
    //準備したコードに基づいてドキュメントを初期化する
    using (var document = new HTMLDocument(code, "."))
    {
        // XPath式を評価して特定の要素を選択する
        var result = document.Evaluate("//*[@class='happy']//span",
                                        document,
                                        null,
                                        XPathResultType.Any,
                                        null);
        
        //結果のノードを反復処理する
        for (Node node; (node = result.IterateNext()) != null;)
        {
            Console.WriteLine(node.TextContent);
            //出力: こんにちは
            //出力: World!
        }
    }
}
```

この例では、XPath クエリを使用して、属性と構造に基づいて HTML ドキュメント内の要素を特定する方法を示します。

## CSS セレクター

CSS セレクターは、CSS スタイルシートが要素をターゲットにする方法と同様に、HTML ドキュメント内の要素を選択する別の方法を提供します。

```csharp
public static void CSSSelectorUsageExample()
{
    // HTMLコードを準備する
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
    
    //準備したコードに基づいてドキュメントを初期化する
    using (var document = new HTMLDocument(code, "."))
    {
        //CSSセレクタを使用してクラスと階層に基づいて要素を抽出する
        var elements = document.QuerySelectorAll(".happy span");
        
        //結果の要素リストを反復処理する
        foreach (HTMLElement element in elements)
        {
            Console.WriteLine(element.InnerHTML);
            //出力: こんにちは
            //出力: World!
        }
    }
}
```

ここでは、CSS セレクターを使用して HTML ドキュメント内の特定の要素をターゲットにする方法を示します。

これらの例により、Aspose.HTML for .NET を使用して HTML ドキュメント内の要素を移動、フィルター処理、クエリ、および選択する方法の基礎を理解できました。

## 結論

 Aspose.HTML for .NET は、.NET 開発者が HTML ドキュメントを効率的に操作できるようにする多機能ライブラリです。ナビゲーション、フィルタリング、クエリ、要素の選択などの強力な機能により、さまざまな HTML 処理タスクをシームレスに処理できます。このチュートリアルに従い、次のドキュメントを参照してください。[Aspose.HTML for .NET ドキュメント](https://reference.aspose.com/html/net/)、.NET アプリケーションでこのツールの潜在能力を最大限に引き出すことができます。

## よくある質問

### Q1. Aspose.HTML for .NET は無料で使用できますか?

A1: Aspose.HTML for .NET には無料試用版がありますが、実稼働で使用する場合はライセンスを購入する必要があります。ライセンスの詳細とオプションについては、[Aspose.HTML 購入](https://purchase.aspose.com/buy).

### Q2. Aspose.HTML for .NET の一時ライセンスを取得するにはどうすればいいですか?

 A2: テスト目的の臨時ライセンスは、[Aspose.HTML 一時ライセンス](https://purchase.aspose.com/temporary-license/).

### Q3. Aspose.HTML for .NET に関するヘルプやサポートはどこで受けられますか?

 A3: 問題が発生した場合やご質問がある場合は、[Aspose.HTML フォーラム](https://forum.aspose.com/)援助とコミュニティのサポートのため。

### Q4. Aspose.HTML for .NET を学習するための追加リソースはありますか?

 A4: このチュートリアルに加えて、[Aspose.HTML for .NET ドキュメント ページ](https://reference.aspose.com/html/net/).

### Q5. Aspose.HTML for .NET は最新の .NET バージョンと互換性がありますか?

A5: Aspose.HTML for .NET は、最新の .NET バージョンおよびテクノロジとの互換性を確保するために定期的に更新されます。