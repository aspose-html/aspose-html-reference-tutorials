---
date: 2025-12-01
description: Aspose.HTML for Java を使用して、PDF のページサイズを調整し、HTML を PDF にレンダリングし、HTML から
  PDF を生成する方法を学びましょう。ページ寸法を簡単に制御できます。
linktitle: Adjusting PDF Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Aspose.HTML for JavaでPDFページサイズを調整する
url: /ja/java/advanced-usage/adjust-pdf-page-size/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML for Java を使用した PDF ページサイズの調整

HTML から PDF を生成することは、レポート、請求書、電子書籍などで一般的な要件です。**PDF ページサイズを調整**することで、最終ドキュメントが HTML で設計したレイアウトと一致することを保証できます。このチュートリアルでは、HTML を PDF にレンダリングし、カスタム寸法を設定し、ページが最も幅の広いコンテンツに自動的に拡張するかどうかを制御する方法を学びます。Aspose.HTML for Java を使用した完全なハンズオン例を順に解説します。

## クイック回答
- **“adjust PDF page size” とは何ですか？** 各 PDF ページの幅と高さを定義するか、レンダラに最も幅の広い要素に自動的に合わせさせることができます。  
- **使用されているライブラリはどれですか？** Aspose.HTML for Java（最新バージョン）。  
- **ライセンスは必要ですか？** 開発目的であれば無料トライアルで動作しますが、本番環境では商用ライセンスが必要です。  
- **プログラムで寸法を変更できますか？** はい – `PageSetup` と `AdjustToWidestPage` プロパティを使用します。  
- **Java 8 以降に対応していますか？** はい、API は JDK 8 以降のすべてのバージョンで動作します。  

## “adjust PDF page size” とは？
PDF ページサイズの調整とは、HTML レンダラが作成する各ページの寸法を設定することを指します。固定サイズ（例：A4、Letter）を指定することも、コンテンツに基づいて最適な幅をレンダラに計算させることもできます。これにより、レイアウト、ページ分割、視覚的忠実度を正確にコントロールできます。

## HTML を PDF に変換する際に PDF ページサイズを調整する理由
- **デザイン意図の保持:** コンテンツが切れたり伸びたりするのを防ぎます。  
- **印刷向けの最適化:** 後続プロセスで必要とされる用紙サイズに合わせます。  
- **可読性の向上:** 過度な余白や文字の詰まりを防ぎます。  
- **動的ドキュメント:** 手動計算なしで幅の広いテーブルや画像に自動的に合わせます。  

## 前提条件
- **Java Development Kit (JDK) 8 以上** がマシンにインストールされていること。  
- **Aspose.HTML for Java** – 最新の JAR は[公式リリースページ](https://releases.aspose.com/html/java/)からダウンロードしてください。  
- **変換したい HTML ファイル**（例では `FirstFile.html` を使用します）。  

## パッケージのインポート
まず、必要なクラスをインポートします。以下のコードブロックは元のチュートリアルと同じです。

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

## ステップ 1: HTML コンテンツの読み取り
`FileInputStream` を使用してソース HTML ファイルを読み取ります。このステップで、後で操作するための生のマークアップを準備します。

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## ステップ 2: HTML の書き込み（および任意の拡張）
ここでは、元の HTML を新しいファイルにコピーし、インラインスタイルをいくつか注入して、スタイリングが PDF 出力に与える影響を示します。サンプル CSS は自由に自分のものに置き換えて構いません。

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Add custom HTML styles or content here
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

## ステップ 3: HTML を PDF にレンダリング – 2 つのシナリオ
次に、**HTML から PDF を生成**する際の、2 つの異なるページサイズ戦略を見ていきます。

### 3.1 ページサイズをコンテンツ幅に合わせない場合
このケースではページ寸法を固定します（100 × 100 ポイント）。要素がこの制限を超えると、切り取られます。

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Create an HTMLDocument instance from the HTML file
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Set PDF rendering options
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

### 3.2 ページサイズをコンテンツ幅に合わせる場合
ここでは `AdjustToWidestPage` を有効にし、レンダラが最も幅の広い要素に合わせてページ幅を自動的に拡張し、高さは固定したままにします。

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

## コードで PDF の寸法を設定する方法（PDF ページサイズの変更方法）
`PageSetup` オブジェクトが鍵です：

- `setAnyPage(Page page)`: 基本となる幅 × 高さを定義します。  
- `setAdjustToWidestPage(boolean)`: 自動幅拡張のオン/オフを切り替えます。  

これら 2 つのプロパティを調整することで、**PDF の寸法設定方法**を任意のシナリオに適用できます。静的な A4 ページが必要な場合でも、HTML レイアウトに合わせた動的幅が必要な場合でも対応可能です。

## よくある問題とヒント
| 問題 | 発生理由 | 対処法 |
|------|----------|--------|
| コンテンツが切り取られる | 固定サイズが小さすぎる | `Size` の値を増やすか、`AdjustToWidestPage` を有効にしてください。 |
| テキストがぼやけて見える | デフォルトのレンダリング DPI が低い | `PdfRenderingOptions.setResolution(int dpi)` を使用して品質を向上させます。 |
| スタイルが欠如している | 外部 CSS が読み込まれていない | CSS をインラインで埋め込むか、`HTMLDocument.setBaseUrl()` を使用してスタイルシートフォルダを指すようにしてください。 |
| 大きな HTML ファイルで OutOfMemoryError が発生する | レンダラがドキュメント全体をメモリに読み込む | ドキュメントを分割して処理するか、JVM ヒープ (`-Xmx`) を増やしてください。 |

## よくある質問

**Q: Aspose.HTML for Java とは何ですか？**  
A: HTML ドキュメントの作成、編集、レンダリングを可能にする Java ライブラリで、PDF、PNG などへの変換もサポートします。

**Q: Aspose.HTML for Java で HTML を PDF に変換する際に PDF ページサイズを調整するにはどうすればよいですか？**  
A: `PageSetup` クラスを使用し、`AdjustToWidestPage` を `true`（自動サイズ）または `false`（固定サイズ）に設定します。その後、`new Page(new Size(width, height))` で希望の `Size` を指定します。

**Q: PDF に変換する前に HTML コンテンツのスタイルをカスタマイズできますか？**  
A: はい。CSS を注入したり、DOM を変更したり、外部スタイルシートを使用したりできます。このチュートリアルではインライン CSS の注入例を示しています。

**Q: Aspose.HTML for Java のドキュメントはどこで見つけられますか？**  
A: 詳細なドキュメントは[こちら](https://reference.aspose.com/html/java/)で入手できます。

**Q: Aspose.HTML for Java の無料トライアルは利用できますか？**  
A: もちろんです。[リリースページ](https://releases.aspose.com/html/java/)からトライアルをダウンロードしてください。

## 結論
これで、Aspose.HTML for Java を使用して **PDF ページサイズを調整**し、**HTML を PDF にレンダリング**し、**カスタム PDF 寸法を設定**する方法が分かりました。さまざまなページサイズ、DPI 設定、CSS の調整を試して、特定のユースケースに最適な出力を実現してください。問題が発生した場合は、公式ドキュメントや Aspose のサポートフォーラムを参照してください。

---

**最終更新日:** 2025-12-01  
**テスト環境:** Aspose.HTML for Java 24.12（最新）  
**作者:** Aspose  
**関連リソース:** [API リファレンス](https://reference.aspose.com/html/java/) | [無料トライアルをダウンロード](https://releases.aspose.com/html/java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}