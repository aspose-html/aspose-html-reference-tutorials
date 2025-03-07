---
title: Aspose.HTML for Java で PDF ページ サイズを調整する
linktitle: PDF ページサイズの調整
second_title: Aspose.HTML を使用した Java HTML 処理
description: Aspose.HTML for Java を使用して PDF ページ サイズを調整する方法を学びます。HTML から高品質の PDF を簡単に作成します。ページ サイズを効果的に制御します。
weight: 15
url: /ja/java/advanced-usage/adjust-pdf-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML for Java で PDF ページ サイズを調整する


今日のデジタル時代では、HTML コンテンツから高品質の PDF を生成する必要性が高まっています。Aspose.HTML for Java は、HTML ドキュメントを PDF 形式に簡単に変換できる強力な Java ライブラリです。このチュートリアルでは、Aspose.HTML for Java を使用して HTML を PDF に変換する際のページ サイズの調整に焦点を当てます。

## 前提条件

始める前に、次の前提条件が満たされていることを確認してください。

- Java 開発環境: システムに Java 開発キット (JDK) がインストールされていることを確認します。
-  Aspose.HTML for Java: Aspose.HTML for JavaをWebサイトからダウンロードしてインストールする必要があります。[ここ](https://releases.aspose.com/html/java/).
- HTML ドキュメント: 変換用の HTML ドキュメントを用意しておく必要があります。用意していない場合は、作成するか、既存の HTML ファイルを使用します。

## パッケージのインポート

まず、Aspose.HTML for Java を使用するために必要なパッケージをインポートする必要があります。次のコード スニペットは、その方法を示しています。

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

前提条件が整い、必要なパッケージがインポートされたので、PDF ページ サイズを調整するプロセスを複数のステップに分解してみましょう。

## ステップ1: HTMLコンテンツの読み取り

まず、PDF に変換する HTML コンテンツを読み取る必要があります。この例では、「FirstFile.html」という名前のファイルから HTML を読み取ります。

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## ステップ2: HTMLコンテンツの作成

次に、HTML コンテンツを「FirstFileOut.html」という名前のファイルに書き込みます。

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    //ここにカスタム HTML スタイルまたはコンテンツを追加します
    String style = "<style>\n" +
                   ".st\n" +
                   "{\n" +
                   "color:\n" +
                   "green;\n" +
                   "}\n" +
                   "</style >\n" +
                   "<div id = id1 > Aspose.Html rendering Text in Black Color</div >\n" +
                   "<div id = id2 class='' st '' > Aspose.Html rendering Text in Green Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: blue;' > Aspose.Html rendering Text in Blue Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: red;' ><font face = 'Arial' > Aspose.Html rendering Text in Red\n" +
                   "Color</font ></div >\n";
    fileOutputStream.write(style.getBytes(java.nio.charset.StandardCharsets.UTF_8));
}
```

## ステップ3: HTMLをPDFにレンダリングする

ここで、HTML コンテンツを PDF ファイルにレンダリングします。ページ サイズがコンテンツの幅に合わせて調整されないシナリオと、調整されるシナリオの 2 つのシナリオについて説明します。

### ページサイズが調整されていません

このシナリオでは、ページ サイズは固定の幅と高さに設定されており、これらの寸法を超えるとコンテンツが切り取られる可能性があります。

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// HTMLファイルからHTMLDocumentインスタンスを作成する
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

//PDFレンダリングオプションを設定する
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//出力をレンダリングする
pdf_renderer.render(device, html_document);
```

### コンテンツの幅に合わせてページサイズを調整

このシナリオでは、ページ サイズはコンテンツの幅に応じて調整されます。

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//出力をレンダリングする
pdf_renderer.render(device, html_document);
```

## 結論

このチュートリアルでは、Aspose.HTML for Java を使用して HTML を PDF に変換するときに PDF ページ サイズを調整する方法について説明しました。前提条件を理解し、必要なパッケージをインポートし、このタスクを達成するためのステップ バイ ステップ ガイドに従いました。Aspose.HTML for Java を使用すると、生成された PDF のページ サイズを簡単に制御し、コンテンツが意図したとおりに表示されるようにすることができます。

さまざまなページサイズや設定を試して、特定の要件を満たしてください。問題が発生したり、さらに質問がある場合は、遠慮なくお問い合わせください。[Aspose.HTML for Java ドキュメント](https://reference.aspose.com/html/java/)または[Aspose サポート フォーラム](https://forum.aspose.com/).

## よくある質問

### Q1: Aspose.HTML for Java とは何ですか?

A1: Aspose.HTML for Java は、HTML ドキュメントを操作、変換し、PDF を含むさまざまな形式でレンダリングできる Java ライブラリです。

### Q2: Aspose.HTML for Java を使用して HTML を PDF に変換するときに、PDF ページ サイズを調整するにはどうすればよいですか?

 A2: PDFのページサイズは、`PageSetup`クラスと設定`AdjustToWidestPage`財産に`true`または、要件に応じて false になります。

### Q3: HTML コンテンツを PDF に変換する前にスタイルをカスタマイズできますか?

A3: はい、チュートリアルで説明されているように、PDF に変換する前に HTML コンテンツに CSS および HTML 要素を追加してスタイルをカスタマイズできます。

### Q4: Aspose.HTML for Java のドキュメントはどこにありますか?

 A4: ドキュメントを参照してください[ここ](https://reference.aspose.com/html/java/)包括的な情報と例については、こちらをご覧ください。

### Q5: Aspose.HTML for Java の無料試用版はありますか?

 A5: はい、Aspose.HTML for Javaの無料トライアルは以下からご利用いただけます。[このリンク](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
