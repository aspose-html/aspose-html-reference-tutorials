---
date: 2026-01-02
description: Aspose.HTML を使用して Java で EPUB を PDF に変換し、カスタム PDF ページサイズやその他の PDF 保存オプションを設定する方法を学びましょう。
linktitle: Specifying PDF Save Options for EPUB to PDF
second_title: Java HTML Processing with Aspose.HTML
title: カスタムPDFページサイズ：EPUBからPDFへの変換時のPDF保存オプションの指定
url: /ja/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# カスタム PDF ページサイズ: EPUB から PDF への変換時に PDF 保存オプションを指定する方法

## はじめに

Aspose.HTML for Java を使用すると、**EPUB を PDF に変換**することが簡単になり、**カスタム PDF ページサイズ**の設定を含む出力を完全にコントロールできます。このステップバイステップ ガイドでは、環境の準備から `PdfSaveOptions` の調整まで、生成された PDF が必要なページ寸法に正確に一致するようにする方法をすべて解説します。出版パイプラインや e‑ラーニング プラットフォームの構築、あるいは単にドキュメント変換を自動化したい場合にも、本ガイドのテクニックは役立ちます。

## クイック回答
- **このチュートリアルの主目的は何ですか？** カスタム PDF ページサイズを適用しながら EPUB ファイルを PDF に変換すること。  
- **使用するライブラリは？** Aspose.HTML for Java。  
- **ライセンスは必要ですか？** 無料トライアルは利用可能です。商用利用には製品ライセンスが必要です。  
- **背景色を変更できますか？** はい、`PdfSaveOptions` を使用します。  
- **Java 8+ はサポートされていますか？** もちろんです。最新の Java ランタイムで動作します。

## カスタム PDF ページサイズとは？

カスタム PDF ページサイズは、標準の A4 や Letter といったサイズに頼らず、出力 PDF の各ページの幅と高さを正確に指定できる機能です。電子書籍、チラシ、特定のデザインに合わせたレイアウトが必要なシーンで特に有用です。

## なぜ Aspose.HTML を EPUB から PDF への変換に使うのか？

- **高忠実度:** 複雑なレイアウト、フォント、画像をそのまま保持。  
- **細かな制御:** `PdfSaveOptions` でページサイズ、背景、余白などを調整可能。  
- **クロスプラットフォーム:** 同じ Java コードで Windows、Linux、macOS 上で動作。  
- **パフォーマンス:** 高速変換のために最適化されたレンダリングエンジン。

## 前提条件

開始する前に以下を用意してください。

- **Java 開発環境:** JDK 8 以降がインストールされ、設定済みであること。  
- **Aspose.HTML for Java:** 最新の JAR を [ウェブサイト](https://releases.aspose.com/html/java/) からダウンロード。  
- **EPUB ファイル:** 変換したい `.epub` ドキュメント。

すべて準備できたら、実際の変換手順に進みましょう。

## 手順 1: EPUB ファイルを開く

まず、`FileInputStream` を使って EPUB ファイルを開きます。このストリームは後でコンバータに渡します。

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

## 手順 2: PDF 保存オプションを定義する

ここで **カスタム PDF ページサイズ** と任意の背景色を設定します。ピクセル値を調整して、目的の寸法に合わせてください。

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

### プロのヒント:
- **ピクセル vs. ポイント:** `Length.fromPixels` は画面ピクセルを PDF のポイントに変換します (1 ポイント = 1/72 インチ)。最終的に印刷したいサイズに合わせた値を選びましょう。

## 手順 3: EPUB を PDF に変換する

入力ストリームとカスタムオプションが準備できたら、コンバータを呼び出します。出力 PDF は指定した場所に保存されます。

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

## 完全なソースコード

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
| **PDF ページが空白になる** | 変換前に入力ストリームが閉じられた | `try‑with‑resources` ブロックを `convertEPUB` の後まで保持する |
| **ページ寸法が正しくない** | 目的の印刷サイズに合わないピクセルを使用した | 必要なインチをポイントに変換 (`1 inch = 72 points`) し、`Length.fromPixels` でピクセルに変換する |
| **フォントが欠落している** | EPUB にフォントが埋め込まれていない | フォントが EPUB にパッケージ化されているか、ホストマシンにインストールされていることを確認する |

## FAQ（よくある質問）

### Aspose.HTML for Java は無料ライブラリですか？
Aspose.HTML for Java は商用ライブラリですが、[ウェブサイト](https://releases.aspose.com/) から無料トライアル版を入手できます。

### どの EPUB フォーマットが変換に対応していますか？
Aspose.HTML for Java はさまざまな EPUB フォーマットの変換をサポートしており、ほとんどの EPUB ドキュメントと互換性があります。

### PDF の出力をさらにカスタマイズできますか？
はい、`PdfSaveOptions` のページ設定、背景色、その他の設定を調整することで、PDF 出力を自由にカスタマイズできます。

### Aspose.HTML for Java のトライアル版には制限がありますか？
トライアル版にはいくつかの制限がある場合があります。詳細は公式ドキュメントをご確認ください。

### Aspose.HTML for Java のサポートはどこで受けられますか？
質問やサポートは [Aspose.HTML フォーラム](https://forum.aspose.com/) で受けられます。

---

**最終更新日:** 2026-01-02  
**テスト環境:** Aspose.HTML for Java 24.11（執筆時点での最新バージョン）  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}