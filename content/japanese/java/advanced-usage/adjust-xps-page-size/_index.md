---
title: Aspose.HTML for Java を使用して XPS ページ サイズを調整する
linktitle: XPS ページ サイズの調整
second_title: Aspose.HTML を使用した Java HTML 処理
description: Aspose.HTML for Java を使用して XPS ページ サイズを調整する方法を学びます。 XPS ドキュメントの出力サイズを簡単に制御します。
type: docs
weight: 16
url: /ja/java/advanced-usage/adjust-xps-page-size/
---

このチュートリアルでは、Aspose.HTML for Java を使用して XPS ページ サイズを調整するプロセスを説明します。この強力なライブラリを使用すると、HTML ドキュメントを操作し、XPS などのさまざまな形式にレンダリングできます。 XPS ドキュメントの出力サイズを制御する必要がある場合、ページ サイズの調整は不可欠です。

## 前提条件

始める前に、次の前提条件が満たされていることを確認してください。

1. Java 開発環境: システムに Java Development Kit (JDK) がインストールされていることを確認します。

2.  Aspose.HTML for Java ライブラリ: Aspose.HTML for Java ライブラリをダウンロードして、Java プロジェクトに含める必要があります。図書館を見つけることができます[ここ](https://releases.aspose.com/html/java/).

3. 入力 HTML ファイル: レンダリングする HTML ファイルを準備し、XPS ページ サイズを調整します。このチュートリアルでは独自の HTML ファイルを使用できます。

## パッケージのインポート

まず、Aspose.HTML for Java を使用するために必要なパッケージをインポートする必要があります。 Java クラスの先頭に次のパッケージを含めます。

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## ステップ 1: 入力ファイル名を設定する

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    //...
}
```

このステップでは、`FileInputStream`.

## ステップ 2: HTML ドキュメントを作成し、スタイルを設定する

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n";

//...
```

このステップには、`HTMLDocument`それにスタイルを追加します。

## ステップ 3: XPS レンダリング オプションを作成する

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

ここでは、XPS レンダリング オプションを作成して、レンダリング プロセスを構成します。

## ステップ 4: ページ サイズを調整する

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

この手順では、ページ サイズを設定し、それを最大幅のページに調整するかどうかを指定します。

## ステップ 5: 出力をレンダリングする

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

最後のステップでは、構成されたオプションを使用して XPS 出力をレンダリングします。

## 結論

このチュートリアルでは、Aspose.HTML for Java を使用して XPS ページ サイズを調整する方法を説明しました。 XPS ドキュメントの出力サイズを制御して、特定の要件を確実に満たすことができます。提供されたコードと手順を使用すると、この機能を Java アプリケーションに簡単に実装できます。

ご質問がある場合、またはさらにサポートが必要な場合は、お気軽に次のサイトにアクセスしてください。[Aspose.HTML for Java ドキュメント](https://reference.aspose.com/html/java/)または、[アスペス フォーラム](https://forum.aspose.com/).

## よくある質問

### Q1: Aspose.HTML for Java とは何ですか?

A1: Aspose.HTML for Java は、開発者が HTML ドキュメントを操作し、XPS、PDF、画像などのさまざまな形式に変換できるようにする Java ライブラリです。

### Q2: Java 用の Aspose.HTML はどこでダウンロードできますか?

 A2: Aspose.HTML for Java ライブラリは、以下からダウンロードできます。[このリンク](https://releases.aspose.com/html/java/).

### Q3: Aspose.HTML for Java の無料トライアルはありますか?

 A3: はい、Aspose.HTML for Java の無料トライアルを次のサイトから入手できます。[ここ](https://releases.aspose.com/).

### Q4: Aspose.HTML for Java の一時ライセンスを取得するにはどうすればよいですか?

 A4: Aspose.HTML for Java の一時ライセンスを取得するには、次のサイトにアクセスしてください。[このページ](https://purchase.aspose.com/temporary-license/).

### Q5: Aspose.HTML for Java のサポートを受けることはできますか?

 A5: はい、Aspose コミュニティからヘルプやサポートを求めることができます。[アスペス フォーラム](https://forum.aspose.com/).