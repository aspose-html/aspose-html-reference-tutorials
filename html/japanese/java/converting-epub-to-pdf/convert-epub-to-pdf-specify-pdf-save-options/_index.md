---
date: 2026-05-30
description: Java で Aspose.HTML を使用して EPUB を PDF に変換し、カスタム PDF ページサイズやその他の PDF 保存オプションを設定する方法を学びます。
keywords:
- custom pdf page size
- convert epub to pdf
- change pdf background color
- specify pdf page dimensions
- aspose.html java
linktitle: EPUB から PDF への変換時に PDF 保存オプションを指定する
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  headline: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  type: TechArticle
- description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  name: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  steps:
  - name: Open the EPUB File
    text: First, create a `FileInputStream` that points to your source `.epub`. Keeping
      the stream open until the conversion finishes prevents “blank page” errors.
  - name: Define PDF Save Options
    text: '`PdfSaveOptions` is Aspose.HTML''s configuration class that controls PDF
      output settings such as page size, background color, and margins. `Length.fromPixels`
      converts screen pixels to PDF points (1 point = 1/72 inch), allowing you to
      specify dimensions in familiar pixel units.'
  - name: Convert EPUB to PDF
    text: With the input stream and custom options ready, invoke the converter. The
      output PDF will be saved to the location you specify, preserving the exact page
      dimensions you defined. `PdfSaveOptions.setEnableParallelProcessing` is a method
      that enables parallel processing of pages during PDF conversion.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a commercial library, but you can obtain a free
      trial version from their [website](https://releases.aspose.com/).
    question: Is Aspose.HTML for Java a free library?
  - answer: Aspose.HTML for Java supports EPUB 2.0, EPUB 3.0, and EPUB 3.1, handling
      re‑flowable and fixed‑layout books with full CSS support.
    question: What EPUB formats are supported for conversion?
  - answer: Yes, you can customize the PDF output by adjusting the page setup, background
      color, compression level, and other settings in the `PdfSaveOptions`.
    question: Can I customize the PDF output further?
  - answer: The trial version may add a watermark to the first few pages and limits
      the maximum file size to 10 MB; purchase a license to remove these restrictions.
    question: Are there any limitations to the trial version of Aspose.HTML for Java?
  - answer: You can find answers to your questions and seek support on the [Aspose.HTML
      forum](https://forum.aspose.com/).
    question: Where can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: カスタム PDF ページサイズ - EPUB から PDF への変換時に PDF 保存オプションを指定する
url: /ja/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# カスタムPDFページサイズ：EPUBからPDFへのPDF保存オプションの指定

## はじめに

Aspose.HTML for Java は **EPUB を PDF に変換** することを簡単にし、**カスタムPDFページサイズ** の設定を含め、出力を完全に制御できます。このステップバイステップガイドでは、環境の準備から `PdfSaveOptions` の調整まで、生成された PDF が要求された正確なページ寸法に合致するようにすべてを解説します。出版パイプラインや e ラーニングプラットフォームの構築、あるいは単にドキュメント変換を自動化したい場合でも、ここで紹介する手法は役立ちます。

## クイック回答
- **このチュートリアルの主な目的は何ですか？** カスタムPDFページサイズを適用しながら EPUB ファイルを PDF に変換することです。  
- **使用されているライブラリは何ですか？** Aspose.HTML for Java。  
- **ライセンスは必要ですか？** 無料トライアルが利用可能ですが、商用利用には商用ライセンスが必要です。  
- **背景色を変更できますか？** はい、`PdfSaveOptions` を使用します。  
- **Java 8 以上はサポートされていますか？** もちろんです。最新の Java ランタイムであれば動作します。

## カスタムPDFページサイズとは何ですか？

カスタムPDFページサイズを使用すると、標準的な A4 や Letter といったサイズに頼ることなく、出力 PDF の各ページの幅と高さを正確に定義できます。寸法はポイント（1 ポイント = 1/72 インチ）で指定するか、ピクセルから変換して、最終レイアウトをピクセル単位で正確にコントロールできます。これは、事前に決められたフォーマットに合わせる必要がある電子書籍、チラシ、またはデザイン全般に最適です。

## なぜ Aspose.HTML を EPUB から PDF の変換に使用するのですか？

Aspose.HTML は 2 行のコードで EPUB を PDF に変換し、複雑なレイアウト、埋め込みフォント、高解像度画像を保持します。**50 以上の入力・出力フォーマット**をサポートし、**2,000 ページ**までの PDF をメモリ全体に読み込むことなくレンダリングでき、Windows、Linux、macOS で同一の結果を提供します。さらに、PDF 保存オプションが細かく設定可能で、ページサイズ、背景色、余白、圧縮設定などを Java だけで調整できます。

## 前提条件
- **Java 開発環境：** JDK 8 以降がインストールされ、設定されていること。  
- **Aspose.HTML for Java：** 最新の JAR を [ウェブサイト](https://releases.aspose.com/html/java/) からダウンロードしてください。  
- **EPUB ファイル：** 変換したい `.epub` ドキュメント。  

すべての準備が整ったので、実際の変換手順に進みましょう。

## カスタムページサイズで EPUB を PDF に変換する方法

`FileInputStream` はファイルからバイトを読み取る Java クラスです。  
`PdfSaveOptions` は Aspose.HTML のクラスで、ページサイズや背景色など PDF 出力設定を構成します。  
`FileInputStream` で EPUB を読み込み、`PdfSaveOptions` で正確なページ寸法を指定し、コンバータを呼び出します。以下の 3 ステップのワークフローは、典型的な電子書籍サイズで 1 分未満に変換を完了し、コードの変更を最小限に抑えて大規模コレクションにもスケールします。

### 手順 1: EPUB ファイルを開く

まず、ソースの `.epub` を指す `FileInputStream` を作成します。変換が完了するまでストリームを開いたままにしておくことで「空白ページ」エラーを防げます。

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

### 手順 2: PDF 保存オプションを定義する

`PdfSaveOptions` は PDF 出力設定（ページサイズ、背景色、余白など）を制御する Aspose.HTML の構成クラスです。  
`Length.fromPixels` は画面ピクセルを PDF ポイントに変換します（1 ポイント = 1/72 インチ）。ピクセル単位で寸法を指定でき、慣れ親しんだ単位でサイズ調整が可能です。

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

#### プロのコツ:
- **ピクセル vs ポイント：**`Length.fromPixels` は画面ピクセルを PDF ポイントに変換します（1 ポイント = 1/72 インチ）。必要な最終印刷サイズに合わせた値を選択してください。

### 手順 3: EPUB を PDF に変換する

入力ストリームとカスタムオプションが準備できたら、コンバータを呼び出します。出力 PDF は指定した場所に保存され、定義した正確なページ寸法が保持されます。

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

`PdfSaveOptions.setEnableParallelProcessing` は PDF 変換中にページの並列処理を有効にするメソッドです。

## 完全なソースコード

以下の完全な実行可能サンプルは上記 3 つの手順を 1 つの Java クラスに統合したものです。プレースホルダーのパスを実際のファイル位置に置き換えてください。

```java
Specifying PDF Save Options for EPUB to PDF
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of the PdfSaveOptions with a custom page-size and a background-color.
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
            // Call the ConvertEPUB method to convert the EPUB to PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```

## よくある問題と解決策

| 問題 | 原因 | 対策 |
|------|------|------|
| **PDFページが空白** | 変換前に入力ストリームが閉じられました | `try‑with‑resources` ブロックを `convertEPUB` の後まで開いたままにしてください。 |
| **ページ寸法が正しくない** | 希望する印刷サイズに対応しないピクセルを使用している | 希望するインチをポイント (`1 inch = 72 points`) に変換し、`Length.fromPixels` を使用してピクセルに変換してください。 |
| **フォントが欠落** | EPUB にフォントが埋め込まれていない | フォントが EPUB にパッケージされているか、ホストマシンにインストールされていることを確認してください。 |
| **大きな書籍でのパフォーマンス低下** | すべてのページを順次レンダリングしている | `PdfSaveOptions.setEnableParallelProcessing(true)` を使用してマルチスレッドレンダリングを有効にし、500 ページ以上の EPUB の処理を高速化してください。 |

## よくある質問 (FAQ)

**Q: Aspose.HTML for Java は無料のライブラリですか？**  
A: Aspose.HTML for Java は商用ライブラリですが、[ウェブサイト](https://releases.aspose.com/) から無料トライアル版を入手できます。

**Q: どの EPUB フォーマットが変換に対応していますか？**  
A: Aspose.HTML for Java は EPUB 2.0、EPUB 3.0、EPUB 3.1 をサポートし、リフロー可能および固定レイアウトの書籍をフル CSS 対応で処理します。

**Q: PDF の出力をさらにカスタマイズできますか？**  
A: はい、`PdfSaveOptions` のページ設定、背景色、圧縮レベル、その他の設定を調整することで PDF 出力をさらにカスタマイズできます。

**Q: Aspose.HTML for Java のトライアル版には制限がありますか？**  
A: トライアル版は最初の数ページに透かしを追加し、最大ファイルサイズを 10 MB に制限します。これらの制限を解除するにはライセンスを購入してください。

**Q: Aspose.HTML for Java のサポートはどこで受けられますか？**  
A: [Aspose.HTML フォーラム](https://forum.aspose.com/) で質問への回答やサポートを受けられます。

**最終更新日：** 2026-05-30  
**テスト環境：** Aspose.HTML for Java 24.11（執筆時点での最新）  
**作者：** Aspose

## 関連チュートリアル

- [Aspose.HTML for Java で PDF ページサイズを調整する](/html/java/advanced-usage/adjust-pdf-page-size/)
- [Java で EPUB を PDF に変換する方法 – Aspose.HTML を使用](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-pdf/)
- [Aspose.HTML for Java で EPUB を PDF と画像に変換する](/html/java/conversion-epub-to-image-and-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}