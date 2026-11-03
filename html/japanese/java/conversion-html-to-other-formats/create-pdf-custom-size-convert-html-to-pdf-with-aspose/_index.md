---
category: general
date: 2026-03-26
description: Aspose.HTML for Java を使用して HTML からカスタムサイズの PDF を作成します。HTML を PDF に変換し、PDF
  のページサイズを数ステップで設定する方法をご紹介します。
draft: false
keywords:
- create pdf custom size
- convert html to pdf
- change pdf page size
- generate pdf from html
- set pdf page size
language: ja
og_description: AsposeでHTMLからカスタムサイズのPDFを作成。このガイドでは、HTMLをPDFに変換し、PDFのページサイズを変更・設定する方法を簡単に紹介します。
og_title: PDFカスタムサイズの作成 – HTMLをPDFに変換するクイックガイド
tags:
- aspose
- java
- pdf
- html
title: PDF カスタムサイズを作成 – AsposeでHTMLをPDFに変換
url: /ja/java/conversion-html-to-other-formats/create-pdf-custom-size-convert-html-to-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF カスタムサイズの作成 – Aspose を使用した HTML から PDF への変換

HTML ファイルから **PDF カスタムサイズを作成** したことはありますか？このチュートリアルでは、**HTML を PDF に変換**し、Aspose.HTML for Java を使用して PDF のページサイズを設定する方法を紹介します。

請求書、レポート、電子書籍などを作成する場合、正確なページ寸法が重要です。そうでなければレイアウトがずれたり、切り取られたりしてしまいます。

ソース HTML の読み込みから余白の調整まで、すべての手順を順に解説し、すぐに使用できる PDF を完成させます。曖昧な説明はなく、今日からコピー＆ペーストできる完全な実行可能サンプルをご提供します。

## 必要なもの

- **Java 17**（または最近の JDK）。  
- **Aspose.HTML for Java** の JAR – 最新バージョンは Maven リポジトリまたは Aspose のウェブサイトから取得できます。  
- 任意のフォルダーに配置したシンプルな `input.html` ファイル。  
- お好みの IDE またはテキストエディタ；私は主に IntelliJ IDEA を使用しますが、Eclipse でも問題なく動作します。

これらの前提条件が揃っていれば、途中で “class not found” エラーに遭遇することはありません。  

それでは、始めましょう。

![PDF カスタムサイズ作成例](/images/create-pdf-custom-size.png "カスタムページサイズと余白で生成された PDF を示すスクリーンショット – PDF カスタムサイズ作成")

## PDF カスタムサイズの作成 – 基本手順

以下は完成形の Java プログラムです。`ConvertHtmlToPdfCustomPage.java` というファイル名でコピーし、プロジェクトに Aspose の依存関係を追加した後に実行してください。

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.PdfConversionOptions;
import com.aspose.html.saving.PageSize;
import com.aspose.html.saving.Margin;

public class ConvertHtmlToPdfCustomPage {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the source HTML document
        HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/input.html");

        // Step 2: Set up PDF conversion options
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setPageSize(PageSize.A4); // Choose page size (A4, Letter, etc.)
        pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Portrait); // Portrait or Landscape
        pdfOptions.setMargins(new Margin(20, 20, 20, 20)); // Margins: left, top, right, bottom (points)

        // Step 3: Convert the HTML document to a PDF file with the custom settings
        Converter.convertHTML(htmlDoc, "YOUR_DIRECTORY/custom_page.pdf", pdfOptions);

        // Step 4: Inform the user that the PDF has been created
        System.out.println("PDF generated with custom page size and margins.");
    }
}
```

### 手順 1 – HTML を PDF に変換: ドキュメントの読み込み

最初に行うのは、PDF に変換したい **HTML の読み込み** です。`HTMLDocument` はファイルを読み込み、相対リンクを解決し、Aspose がレンダリングできる DOM を構築します。

> **なぜ重要か:** HTML が CSS や画像を参照している場合、Aspose はファイルパスを基準にそれらを取得します。絶対パス（`YOUR_DIRECTORY/input.html`）を使用すれば “file not found” の問題を回避できます。

### 手順 2 – PDF ページサイズの変更: オプションの設定

ここで `PdfConversionOptions` オブジェクトを作成します。  
- `setPageSize(PageSize.A4)` は Aspose に標準的な A4 サイズ（210 × 297 mm）を使用させます。  
- `setPageOrientation(...)` は横向きが必要な場合にページを回転させます。  
- `setMargins(new Margin(20, 20, 20, 20))` は各辺に 20 ポイントの余白を設定します。

`PageSize.A4` を `PageSize.LETTER` に置き換えることもできますし、`SizeF` オブジェクトを渡すことで **カスタムサイズ** を指定することも可能です。例:

```java
pdfOptions.setPageSize(new SizeF(500, 800)); // width, height in points
```

> **プロのコツ:** 1 ポイントは 1/72 インチです。ミリメートルで考える場合は、2.83465 を掛けてポイントに変換します。

### 手順 3 – HTML から PDF を生成: 変換の実行

`Converter.convertHTML` が実際の変換処理を行います。読み込んだ `HTMLDocument`、出力パス、そして先ほど設定したオプションを受け取ります。

コンテンツに応じて **PDF ページサイズを動的に設定**したい場合は、この手順の前に必要な寸法を計算し、`pdfOptions` を調整すれば実現できます。

### 手順 4 – 結果の確認

`System.out.println` 行は任意ですが、コンソールからプログラムを実行した際にすぐにフィードバックが得られます。実行後に `custom_page.pdf` を開くと、指定通りの 20 ポイント均一余白の A4 縦向き PDF が表示されるはずです。

## HTML を PDF に変換 – よくあるバリエーション

### ファイルパスの代わりにストリームを使用する

物理的なファイルがない場合もあります。HTML がデータベースや API から取得されることもあるでしょう。その場合は文字列を `ByteArrayInputStream` でラップします。

```java
String htmlContent = "<html><body><h1>Hello, PDF!</h1></body></html>";
HTMLDocument htmlDoc = new HTMLDocument(
        new ByteArrayInputStream(htmlContent.getBytes(StandardCharsets.UTF_8)),
        "http://example.com/");
```

第2引数は相対リソースを解決するためのベース URL です。

### ページ向きの変更

レポートが横長の場合は、横向きに切り替えます。

```java
pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Landscape);
```

### 余白の微調整

余白は浮動小数点値を受け付けるため、0.5 pt のような極細のボーダーも設定できます。

```java
pdfOptions.setMargins(new Margin(5.5, 10.2, 5.5, 10.2));
```

### 大容量 HTML ファイルの処理

非常に大きなドキュメントの場合は、**メモリ効率の良いストリーミング** を有効にすることを検討してください。

```java
pdfOptions.setUseMemoryCache(true);
```

これにより、Aspose は中間データを RAM に保持せず、一時ファイルに書き出すようになります。

## PDF ページサイズの設定 – エッジケースと落とし穴

- **フォントが見つからない:** HTML がサーバーにインストールされていないカスタムフォントを使用している場合、PDF はデフォルトフォントにフォールバックします。`pdfOptions.getFontEmbeddingMode().setEmbeddingMode(EmbeddingMode.Always);` でフォントを埋め込みましょう。  
- **画像のスケーリング:** 高解像度画像は PDF を肥大化させます。`pdfOptions.setImageResolution(150);` を使用して品質を保ちつつダウンサンプリングしてください。  
- **CSS の互換性:** すべての CSS プロパティが完全にサポートされているわけではありません。標準的なレイアウト手法を使用してください（flexbox は動作しますが、grid は問題がある場合があります）。  
- **パスの権限:** プロセスが `YOUR_DIRECTORY` に書き込み権限を持っていることを確認してください。権限がないと `IOException` がスローされます。

## 期待される出力

プログラムを実行すると、以下のような PDF が生成されます（概念図）。

```
+---------------------------------------------------+
|                     Header                        |
|                                                   |
|   (HTML rendered content goes here)               |
|                                                   |
|                     Footer                        |
+---------------------------------------------------+
```

- ページサイズ: **A4**（210 × 297 mm）。  
- 向き: **縦向き**。  
- 余白: 各側 **20 pt**。

任意の PDF ビューア（Adobe Reader、Chrome など）でファイルを開き、確認してください。

## まとめ

これで、Aspose.HTML for Java を使用して HTML ソースから **PDF カスタムサイズを作成**する方法が分かりました。このチュートリアルでは、**HTML を PDF に変換**、**PDF ページサイズの変更**、**PDF ページサイズの設定**、そしてカスタム余白付きで **HTML から PDF を生成**するという一連の流れを網羅しました。

自由に試してみてください。`PageSize.LETTER` を Legal サイズに変更したり、余白を調整したり、独自のフォントを埋め込んだりできます。次のステップとしては、**透かしの追加**、**PDF の暗号化**、または **複数 HTML ファイルのバッチ処理** などに挑戦できるでしょう。これらのトピックはすべて、今回学んだ基本概念に基づいています。

特定のエッジケースについて質問がありますか？下にコメントを残してください。問題解決をお手伝いします。コーディングを楽しんでください！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}