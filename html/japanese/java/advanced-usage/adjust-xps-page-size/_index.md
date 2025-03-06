---
title: Aspose.HTML for Java で XPS ページ サイズを調整する
linktitle: XPS ページ サイズの調整
second_title: Aspose.HTML を使用した Java HTML 処理
description: Aspose.HTML for Java を使用して XPS ページ サイズを調整する方法を学びます。XPS ドキュメントの出力サイズを簡単に制御します。
weight: 16
url: /ja/java/advanced-usage/adjust-xps-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML for Java で XPS ページ サイズを調整する


このチュートリアルでは、Aspose.HTML for Java を使用して XPS ページ サイズを調整する手順を説明します。この強力なライブラリを使用すると、HTML ドキュメントを操作し、XPS を含むさまざまな形式にレンダリングできます。XPS ドキュメントの出力寸法を制御する必要がある場合は、ページ サイズの調整が不可欠です。

## 前提条件

始める前に、次の前提条件が満たされていることを確認してください。

1. Java 開発環境: システムに Java 開発キット (JDK) がインストールされていることを確認します。

2.  Aspose.HTML for Javaライブラリ: Aspose.HTML for JavaライブラリをダウンロードしてJavaプロジェクトに含める必要があります。ライブラリは次の場所にあります。[ここ](https://releases.aspose.com/html/java/).

3. 入力 HTML ファイル: レンダリングして XPS ページ サイズを調整する HTML ファイルを準備します。このチュートリアルでは独自の HTML ファイルを使用できます。

## パッケージのインポート

まず、Aspose.HTML for Java を使用するために必要なパッケージをインポートする必要があります。Java クラスの先頭に次のパッケージを含めます。

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## ステップ1: 入力ファイル名を設定する

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    //...
}
```

このステップでは、HTML入力ファイルを読み取ります。`FileInputStream`.

## ステップ2: HTMLドキュメントを作成し、スタイルを設定する

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

このステップでは、`HTMLDocument`それにスタイルを追加します。

## ステップ3: XPSレンダリングオプションを作成する

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

ここでは、レンダリング プロセスを構成するための XPS レンダリング オプションを作成します。

## ステップ4: ページサイズを調整する

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

この手順では、ページ サイズを設定し、最も幅の広いページに合わせて調整するかどうかを指定します。

## ステップ5: 出力をレンダリングする

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

最後のステップでは、構成されたオプションを使用して XPS 出力をレンダリングします。

## 結論

このチュートリアルでは、Aspose.HTML for Java を使用して XPS ページ サイズを調整する方法を説明しました。XPS ドキュメントの出力サイズを制御して、特定の要件を満たすようにすることができます。提供されているコードと手順を使用すると、この機能を Java アプリケーションに簡単に実装できます。

ご質問やご不明な点がございましたら、お気軽に[Aspose.HTML for Java ドキュメント](https://reference.aspose.com/html/java/)または、[Aspose フォーラム](https://forum.aspose.com/).

## よくある質問

### Q1: Aspose.HTML for Java とは何ですか?

A1: Aspose.HTML for Java は、開発者が HTML ドキュメントを操作し、XPS、PDF、画像などのさまざまな形式に変換できるようにする Java ライブラリです。

### Q2: Aspose.HTML for Java はどこからダウンロードできますか?

 A2: Aspose.HTML for Javaライブラリは以下からダウンロードできます。[このリンク](https://releases.aspose.com/html/java/).

### Q3: Aspose.HTML for Java の無料試用版はありますか?

 A3: はい、Aspose.HTML for Javaの無料トライアルは以下から入手できます。[ここ](https://releases.aspose.com/).

### Q4: Aspose.HTML for Java の一時ライセンスを取得するにはどうすればよいですか?

 A4: Aspose.HTML for Javaの一時ライセンスを取得するには、[このページ](https://purchase.aspose.com/temporary-license/).

### Q5: Aspose.HTML for Java のサポートを受けることはできますか?

 A5: はい、Asposeコミュニティからヘルプやサポートを受けることができます。[Aspose フォーラム](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
