---
title: Aspose.HTML を使用して .NET で HTML ドキュメントを作成する
linktitle: .NET で HTML ドキュメントを作成する
second_title: Aspose.HTML .NET HTML 操作 API
description: Aspose.HTML を使用して、ゼロからまたは URL から .NET で HTML ドキュメントを作成する方法を学びます。Web 開発者向けの包括的なチュートリアルです。
weight: 10
url: /ja/net/working-with-html-documents/creating-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML を使用して .NET で HTML ドキュメントを作成する


Web 開発とデータ操作の分野では、HTML ドキュメントを作成、変更、操作するための強力なツールが不可欠です。Aspose.HTML for .NET は、HTML 関連のタスクを簡素化できるツールの 1 つです。この包括的なチュートリアルでは、Aspose.HTML for .NET を使用して HTML ドキュメントを作成する方法を段階的に説明します。例に進む前に、いくつかの前提条件について説明します。

## 前提条件

この旅を始める前に、次の前提条件が満たされていることを確認してください。

1. Visual Studio: システムに Visual Studio がインストールされていることを確認します。

2. Aspose.HTML for .NET: Aspose.HTML for .NETライブラリをダウンロードしてインストールします。ダウンロードリンクは[ここ](https://releases.aspose.com/html/net/).

3. C# の基礎知識: C# プログラミング言語の基礎を理解します。

前提条件が満たされたので、HTML ドキュメントの作成を始めましょう。

## 名前空間のインポート

まず、C# プロジェクトで Aspose.HTML を使用するために必要な名前空間をインポートする必要があります。コード ファイルに次の using ディレクティブを追加します。

```csharp
using Aspose.Html.Dom.Svg;
using Aspose.Html;
```

## SVGドキュメントの作成

```csharp
static void CreateSVG()
{
    using (var document = new SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "about:blank"))
    {
        //ここで SVG ドキュメントに対してアクションを実行します...
    }
}
```

この例では、SVGコンテンツとベースURLを指定してSVGドキュメントを作成します。`SVGDocument` Aspose.HTML for .NET のクラスを使用すると、SVG ドキュメントを簡単に操作できます。

## HTML ドキュメントをゼロから作成する

```csharp
static void FromScratch()
{
    using (var document = new HTMLDocument())
    {
        //ここで HTML ドキュメントに対してアクションを実行します...
    }
}
```

この例では、HTML文書を最初から作成する方法を示します。`HTMLDocument`クラスは、HTML コンテンツ用の空白のキャンバスを提供します。

## ローカルファイルから HTML ドキュメントを作成する

```csharp
static void FromLocalFile()
{
    string dataDir = "Your Data Directory";
    using (var document = new HTMLDocument(dataDir + "input.html"))
    {
        //ここで HTML ドキュメントに対してアクションを実行します...
    }
}
```

ローカルシステムに既存のHTMLファイルがある場合は、`HTMLDocument`この例に示すように、クラスです。

## リモート URL から HTML ドキュメントを作成する

```csharp
static void FromRemoteURL()
{
    using (var document = new HTMLDocument("http://your.site.com/))
    {
        //ここで HTML ドキュメントに対してアクションを実行します...
    }
}
```

場合によっては、リモート サーバーでホストされている HTML コンテンツを操作する必要があることがあります。この例では、リモート URL から HTML ドキュメントを作成する方法を示します。

## リモート URL から HTML ドキュメントを作成する (代替)

```csharp
static void FromRemoteURL1()
{
    using (var document = new HTMLDocument(new Url("http://your.site.com/")))
    {
        //ここで HTML ドキュメントに対してアクションを実行します...
    }
}
```

この代替アプローチでは、別のコンストラクターを使用してリモート URL から HTML ドキュメントを作成する方法も示します。

## HTML コンテンツから HTML ドキュメントを作成する

```csharp
static void FromHTML()
{
    using (var document = new HTMLDocument("<p>my first paragraph</p>", "."))
    {
        //ここで HTML ドキュメントに対してアクションを実行します...
    }
}
```

文字列形式の HTML コンテンツがある場合は、この例に示すように、それを使用して HTML ドキュメントを作成できます。

## ストリームから HTML ドキュメントを作成する

```csharp
static void FromStream()
{
    using (MemoryStream mem = new MemoryStream())
    using (StreamWriter sw = new StreamWriter(mem))
    {
        sw.Write("<p>my first paragraph</p>");
        sw.Flush();
        mem.Seek(0, SeekOrigin.Begin);
        using (var document = new HTMLDocument(mem, "about:blank"))
        {
            //ここで HTML ドキュメントに対してアクションを実行します...
        }
    }
}
```

この例では、メモリ ストリーム内のデータから HTML ドキュメントを作成する方法を示します。これは、ストリーム内に HTML コンテンツがあり、それを操作したい場合に便利です。

## 結論

Aspose.HTML for .NET は、.NET アプリケーションで HTML ドキュメントを作成および操作するための強力なツール セットを提供します。このチュートリアルで提供される例を使用すると、最初から、ローカル ファイル、リモート URL、または既存の HTML コンテンツから、HTML ドキュメントを簡単に作成できます。

ご質問やサポートが必要な場合は、Aspose.HTMLコミュニティフォーラムにアクセスしてサポートを受けてください。[フォーラム](https://forum.aspose.com/).

## よくある質問

### Q1: Aspose.HTML for .NET は無料で使用できますか?
 A1: Aspose.HTML for .NET は無料トライアルを提供していますが、フル機能を使用するにはライセンスを購入する必要があります。詳細については、[https://purchase.aspose.com/buy](https://purchase.aspose.com/buy).

### Q2: Aspose.HTML for .NET の一時ライセンスを取得するにはどうすればよいですか?
 A2: 臨時免許証が必要な場合は、[https://purchase.aspose.com/temporary-license/](https://purchase.aspose.com/temporary-license/).

### Q3: Aspose.HTML for .NET のドキュメントはどこにありますか?
A3: ドキュメントは次の場所にあります。[https://reference.aspose.com/html/net/](https://reference.aspose.com/html/net/).

### Q4: .NET 開発用の他の Aspose ライブラリはありますか?
 A4: はい、Aspose はさまざまなファイル形式やドキュメント操作タスク用のライブラリを提供しています。提供内容については、次の Web サイトをご覧ください。[https://products.aspose.com/](https://products.aspose.com/).

### Q5: Web アプリケーションで Aspose.HTML for .NET を使用できますか?
A5: はい、Aspose.HTML for .NET は Web アプリケーションと互換性があるため、デスクトップと Web ベースの両方のプロジェクトに幅広く使用できます。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
