---
title: EPUB から PDF への PDF 保存オプションの指定
linktitle: EPUB から PDF への PDF 保存オプションの指定
second_title: Aspose.HTML を使用した Java HTML 処理
description: 強力な HTML 操作ライブラリである Aspose.HTML を使用して、Java で EPUB を PDF に変換する方法を学びます。
type: docs
weight: 12
url: /ja/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
---

## 導入

Aspose.HTML for Java は、HTML および EPUB ドキュメントを操作するための強力なツールです。このステップ バイ ステップ ガイドでは、Aspose.HTML for Java を使用して EPUB ファイルを PDF に変換するプロセスについて説明します。熟練した開発者でも、初心者でも、このチュートリアルでは、このタスクを効率的に実行するために必要な知識とスキルを身に付けることができます。

## 前提条件

始める前に、次の前提条件が満たされていることを確認してください。

- Java 開発環境: システムに Java 開発環境が設定されている必要があります。

-  Aspose.HTML for Java: Aspose.HTML for Javaライブラリをダウンロードしてインストールします。ライブラリと関連ドキュメントは、[Webサイト](https://releases.aspose.com/html/java/).

- EPUB ファイル: PDF に変換する EPUB ファイルが必要です。

それでは、Aspose.HTML for Java を使用して EPUB を PDF に変換するためのステップバイステップ ガイドを見ていきましょう。

## ステップ1: EPUBファイルを開く

まず、既存のEPUBファイルを開いて読みます。`FileInputStream`これを実現するには、このステップのコードは次のとおりです。

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    //次のステップのコードはここに入力します。
}
```

## ステップ2: PDF保存オプションを定義する

インスタンスを作成する`PdfSaveOptions`ページ サイズと背景色をカスタマイズできます。ページ設定は必要に応じて構成できます。手順は次のとおりです。

```java
com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
anyPage.setSize(new com.aspose.html.drawing.Size(
    com.aspose.html.drawing.Length.fromPixels(3000),
    com.aspose.html.drawing.Length.fromPixels(1000))
);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
```

## ステップ3: EPUBをPDFに変換する

さて、`ConvertEPUB`EPUB ファイルを PDF に変換する方法。入力ストリーム、PDF 保存オプション、出力場所を指定します。手順は次のとおりです。

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

おめでとうございます! Aspose.HTML for Java を使用して EPUB ファイルを PDF に正常に変換しました。これで、指定した出力場所にある変換された PDF ファイルにアクセスできるようになりました。

## 完全なソースコード
```java
Specifying PDF Save Options for EPUB to PDF
        //既存の EPUB ファイルを開いて読み取ります。
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            //カスタム ページ サイズと背景色を使用して PdfSaveOptions のインスタンスを作成します。
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
            com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
            anyPage.setSize(new com.aspose.html.drawing.Size(
                    com.aspose.html.drawing.Length.fromPixels(3000),
                    com.aspose.html.drawing.Length.fromPixels(1000))
            );
            pageSetup.setAnyPage(anyPage);
            options.setPageSetup(pageSetup);
            options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
            // ConvertEPUB メソッドを呼び出して、EPUB を PDF に変換します。
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```


## 結論

このチュートリアルでは、Aspose.HTML for Java を使用して EPUB ファイルを PDF 形式に変換する方法を学習しました。この多目的ライブラリは、開発者にドキュメント操作のための強力なツールを提供します。このガイドで概説されている手順に従うことで、EPUB から PDF への変換を Java アプリケーションにシームレスに統合できます。

## よくある質問（FAQ）

### Aspose.HTML for Java は無料のライブラリですか?
 Aspose.HTML for Javaは商用ライブラリですが、無料試用版を入手できます。[Webサイト](https://releases.aspose.com/).

### 変換にサポートされている EPUB 形式は何ですか?
Aspose.HTML for Java はさまざまな EPUB 形式の変換をサポートしており、ほとんどの EPUB ドキュメントとの互換性が保証されます。

### PDF 出力をさらにカスタマイズできますか?
はい、ページ設定、背景色、その他の設定を調整することでPDF出力をカスタマイズできます。`PdfSaveOptions`.

### Aspose.HTML for Java の試用版には制限はありますか?
試用版にはいくつかの制限がある場合があるため、詳細についてはドキュメントを確認することをお勧めします。

### Aspose.HTML for Java のサポートはどこで受けられますか?
質問に対する回答やサポートは、[Aspose.HTML フォーラム](https://forum.aspose.com/).
