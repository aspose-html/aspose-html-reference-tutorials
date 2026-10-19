---
date: 2026-03-18
description: Aspose.HTML for Java を使用して HTML を XPS に変換し、XPS のページサイズを調整する方法を学びましょう。出力サイズを簡単に制御できます。
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Aspose.HTML for Java を使用して HTML を XPS に変換し、XPS のページサイズを調整する
url: /ja/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML を XPS に変換し、Aspose.HTML for Java で XPS ページサイズを調整する

このチュートリアルでは、**HTML を XPS に変換する方法**と、変換後のページサイズを微調整する方法を Aspose.HTML for Java を使って解説します。印刷可能なレポート、請求書、アーカイブ文書を生成する際に、XPS の寸法を制御することで、期待通りの出力が得られます。環境設定から最終 XPS ファイルのレンダリングまで、すべての手順を順を追って説明するので、すぐに Java アプリケーションに組み込むことができます。

## Quick Answers
- **「HTML を XPS に変換する」とは何ですか？** HTML ドキュメントを XPS ファイルにレンダリングし、レイアウトとスタイルを保持します。  
- **ライセンスは必要ですか？** 開発段階では無料トライアルで動作しますが、本番環境では商用ライセンスが必要です。  
- **対応している Java バージョンは？** Java 8 以降（JDK 11+ 推奨）。  
- **ページサイズは変更できますか？** はい – Aspose.HTML ではレンダリング前にカスタム寸法を指定できます。  
- **変換にかかる時間は？** 標準的なページであれば通常 1 秒未満です。大きな文書はそれ以上かかる場合があります。

## HTML を XPS に変換するとは？
HTML を XPS に変換するとは、Web 向けのマークアップファイルを XPS（XML Paper Specification）ドキュメント、すなわち PDF に似た固定レイアウト・印刷対応フォーマットに変換することです。Java アプリケーションから高忠実度でデバイスに依存しない文書をアーカイブや印刷用に生成したい場合に有用です。

## XPS ページサイズを調整する理由
ページサイズを調整すると、最終文書の物理的寸法（例：A4、Letter、カスタムラベル）を自由に設定できます。不要なスケーリングを防ぎ、コンテンツがぴったり収まるようにし、余分な余白を削除することでファイルサイズの削減にもつながります。

## 前提条件

開始する前に、以下の前提条件が整っていることを確認してください。

1. **Java 開発環境** – システムに Java Development Kit (JDK) がインストールされていること。  
2. **Aspose.HTML for Java ライブラリ** – Aspose.HTML for Java ライブラリをダウンロードし、プロジェクトに組み込んでください。ライブラリは [こちら](https://releases.aspose.com/html/java/) から入手できます。  
3. **入力 HTML ファイル** – XPS ページサイズを調整したい HTML ファイルを用意します。このチュートリアルではご自身の HTML ファイルを使用してください。

## パッケージのインポート

まず、必要なクラスをインポートします。これらのパッケージにより、ドキュメント操作、レンダリング、ページ設定機能が利用可能になります。

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## 手順別ガイド

以下は元の手順を簡潔にまとめ、追加の解説を加えた番号付きガイドです。

### 手順 1: 入力ファイル名の設定

`FileInputStream` を使用してソース HTML ファイルを読み込みます。このストリームが生の HTML を Aspose.HTML エンジンに供給します。

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

### 手順 2: HTML ドキュメントの作成とスタイル設定

レンダリング対象となる `HTMLDocument` インスタンスを作成します。この例では、簡単な CSS ブロックを注入してスタイリングをデモしています。必要に応じてご自身のマークアップに置き換えてください。

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
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n" +
               "\n";

// ...
```

### 手順 3: XPS レンダリングオプションの作成

`XpsRenderingOptions` をインスタンス化し、HTML から XPS への変換に影響するすべての設定を保持します。

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

### 手順 4: ページサイズの調整  

**XPS ページサイズの設定方法** – カスタムページサイズ（幅 × 高さ、単位はポイント）を定義し、最も幅の広いページに自動的に拡張するかどうかを指定します。`adjustToWidestPage` を `false` に設定すると、指定した正確な寸法が保持されます。

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

### 手順 5: 出力のレンダリング

最後に、設定済みオプションを使用して `XpsDevice` を作成し、HTML ドキュメントをレンダリングします。結果として、カスタムページ寸法が適用された完全な XPS ファイルが生成されます。

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## よくある問題と解決策

| 問題 | 発生理由 | 解決策 |
|------|----------|--------|
| **XPS が空白になる** | 入力ストリームが閉じられていない、または `HTMLDocument` が誤ったファイルを指している | `FileInputStream` を try‑with‑resources で正しくラップし、ファイルパスが正しいことを確認してください。 |
| **ページサイズが適用されない** | `adjustToWidestPage` が `true` のまま | 手順 4 のように `pageSetup.setAdjustToWidestPage(false);` を設定してください。 |
| **CSS がサポート外** | Aspose.HTML がサポートする CSS のサブセットしか認識しない | 基本的なレイアウト、フォント、カラーに留め、Advanced セレクタや CSS Grid は使用しないでください。 |
| **LicenseException** | 本番環境で有効なライセンスがない状態で実行している | レンダリング前に一時または購入済みのライセンスを適用します（例: `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`）。 |

## FAQ（よくある質問）

**Q: Aspose.HTML for Java とは何ですか？**  
A: Aspose.HTML for Java は、開発者が HTML ドキュメントを操作・変換し、XPS、PDF、画像などさまざまな形式に出力できる Java ライブラリです。

**Q: Aspose.HTML for Java はどこからダウンロードできますか？**  
A: ライブラリは [このリンク](https://releases.aspose.com/html/java/) からダウンロードできます。

**Q: Aspose.HTML for Java の無料トライアルはありますか？**  
A: はい、[こちら](https://releases.aspose.com/) から無料トライアルを取得できます。

**Q: Aspose.HTML for Java の一時ライセンスはどこで取得できますか？**  
A: 一時ライセンスは [このページ](https://purchase.aspose.com/temporary-license/) から入手できます。

**Q: Aspose.HTML for Java のサポートは受けられますか？**  
A: はい、[Aspose Forum](https://forum.aspose.com/) でコミュニティからサポートを受けられます。

**Q: ヘッドレスサーバー上で HTML を XPS に変換できますか？**  
A: 完全に可能です。Aspose.HTML は GUI が無くても動作しますので、Java ランタイムが正しく設定されていれば問題ありません。

**Q: カスタムページ余白はサポートされていますか？**  
A: はい。`PageSetup.setMarginTop()`、`setMarginBottom()` などを使用して、レンダリングオプションに設定する前に余白を指定できます。

## 結論

**HTML を XPS に変換し、Aspose.HTML for Java でページサイズを調整**する手順をすべて解説しました。これらの手順に従うことで、レイアウト要件に完全に合致した印刷対応 XPS 文書を生成できます。さまざまなページ寸法やスタイル、ヘッダー・フッターの追加などを試して、プロジェクトに最適な出力を実現してください。

ご質問や追加のサポートが必要な場合は、[Aspose.HTML for Java のドキュメント](https://reference.aspose.com/html/java/) を参照するか、[Aspose Forum](https://forum.aspose.com/) でディスカッションに参加してください。

---

**最終更新日:** 2026-03-18  
**テスト環境:** Aspose.HTML for Java 24.11（執筆時点の最新バージョン）  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}