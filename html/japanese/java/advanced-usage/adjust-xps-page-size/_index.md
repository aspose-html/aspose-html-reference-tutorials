---
date: 2025-11-29
description: Aspose.HTML for Java を使用して HTML を XPS に変換し、XPS のページサイズを調整する方法を学びましょう。出力サイズを簡単に制御できます。
language: ja
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Aspose.HTML for Java を使用して HTML を XPS に変換し、XPS のページサイズを調整する
url: /java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML を XPS に変換し、Aspose.HTML for Java で XPS ページサイズを調整する

このチュートリアルでは、**HTML を XPS に変換する方法** と、Aspose.HTML for Java を使用して生成されたページサイズを微調整する方法を紹介します。印刷可能なレポート、請求書、アーカイブ文書を生成する場合でも、XPS の寸法を制御することで、出力が期待通りの外観になることが保証されます。環境設定から最終的な XPS ファイルのレンダリングまで、すべての手順を順に解説するので、すぐに Java アプリケーションにこの機能を組み込むことができます。

## クイック回答

- **“convert HTML to XPS” とは何ですか？** HTML ドキュメントを XPS ファイルにレンダリングし、レイアウトとスタイルを保持します。  
- **ライセンスは必要ですか？** 開発には無料トライアルで利用可能ですが、本番環境では商用ライセンスが必要です。  
- **サポートされている Java バージョンはどれですか？** Java 8 以上 (JDK 11+ 推奨)。  
- **ページサイズを変更できますか？** はい – Aspose.HTML を使用すると、レンダリング前にカスタム寸法を指定できます。  
- **変換にかかる時間はどれくらいですか？** 標準的なページであれば通常 1 秒未満で完了しますがサイズの大きい文書はそれ以上かかる場合があります。

## HTML を XPS に変換するとは何ですか？

HTML を XPS に変換するとは、Web 向けのマークアップファイルを取得し、XPS（XML Paper Specification）ドキュメント—PDF に似た固定レイアウトの印刷準備済みット—を生成することを意味します。Java アプリケーションからのアーカイブや印刷用に、高忠実度でデバイスに依存しない文書が必要な場合に便利です。

## なぜ XPS ページサイズを調整するのですか？

ページサイズを調整することで、最終文書の物理的な寸法（例: A4、Letter、カスタムラベル）を制御できます。不要な拡大縮小を防ぎ、コンテンツがきちんと収まるようにし、余分な余白を除去することでファイルサイズの削減にもつながります。

## 前提条件

開始する前に、以下の前提条件が整っていることを確認してください。

1. **Java Development Environment** – システムにインストールされた Java Development Kit (JDK)。  
2. **Aspose.HTML for Java Library** – Aspose.HTML for Java ライブラリをダウンロードし、プロジェクトに組み込んでください。ライブラリは [here](https://releases.aspose.com/html/java/) で入手できます。  
3. **Input HTML File** – XPS ページサイズを調整してレンダリングしたい HTML ファイルを用意してください。このチュートリアルではご自身の HTML ファイルを使用できます。

## パッケージのインポート

まず、必要なクラスをインポートします。これらのパッケージにより、ドキュメント処理、レンダリング、ページ設定機能にアクセスできます。

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## 手順 1: 入力ファイル名の設定

`FileInputStream` を使用してソース HTML ファイルを読み取ります。このストリームは生の HTML を Aspose.HTML エンジンに供給します。

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

## 手順 2: HTML ドキュメントの作成とスタイルの設定

レンダリングするコンテンツを表す `HTMLDocument` インスタンスを作成します。この例では、スタイリングを示すために小さな CSS ブロックも挿入しています—ご自身のマークアップに置き換えて構いません。

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

## 手順 3: XPS レンダリング オプションの作成

`XpsRenderingOptions` をインスタンス化し、HTML から XPS への変換に影響するすべての設定を保持します。

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

## 手順 4: ページサイズの調整

カスタムページサイズ（幅 × 高さ、単位はポイント）を定義し、レンダラに最も幅の広いページへ自動的に拡張させるかどうかを指示します。`adjustToWidestPage` を `false` に設定すると、指定した正確な寸法が保持されます。

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

## 手順 5: 出力のレンダリング

最後に、設定したオプションで `XpsDevice` を作成し、HTML ドキュメントをレンダリングします。結果として、指定したカスタムページ寸法を持つ完全な XPS ファイルが生成されます。

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## よくある問題と解決策

| 問題 | 発生原因 | 対策 |
|------|----------|------|
| **Blank XPS output** | 入力ストリームが閉じられていない、または HTMLDocument が誤ったファイルを指している。 | `FileInputStream` が try‑with‑resources ブロックで正しくラップされ、ファイルパスが正確であることを確認してください。 |
| **Page size not applied** | `adjustToWidestPage` が `true` のままになっている。 | Step 4 の例のように `pageSetup.setAdjustToWidestPage(false);` を設定してください。 |
| **Unsupported CSS** | Aspose.HTML は CSS のサブセットしかサポートしていない。 | 基本的なレイアウト、フォント、カラーに限定し、高度なセレクタや CSS Grid は避けてください。 |
| **LicenseException** | 本番環境で有効なライセンスなしで実行している。 | レンダリング前に一時または購入したライセンスを適用してください（`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`）。 |

## よくある質問

**Q: Aspose.HTML for Java とは何ですか？**  
A: Aspose.HTML for Java は、開発者が HTML ドキュメントを操作し、XPS、PDF、画像などのさまざまな形式に変換できる Java ライブラリです。

**Q: Aspose.HTML for Java はどこからダウンロードできますか？**  
A: Aspose.HTML for Java ライブラリは [this link](https://releases.aspose.com/html/java/) からダウンロードできます。

**Q: Aspose.HTML for Java の無料トライアルはありますか？**  
A: はい、[here](https://releases.aspose.com/) から Aspose.HTML for Java の無料トライアルを取得できます。

**Q: Aspose.HTML for Java の一時ライセンスはどのように取得できますか？**  
A: Aspose.HTML for Java の一時ライセンスを取得するには、[this page](https://purchase.aspose.com/temporary-license/) をご覧ください。

**Q: Aspose.HTML for Java のサポートは受けられますか？**  
A: はい、[Aspose Forum](https://forum.aspose.com/) の Aspose コミュニティで支援やサポートを受けられます。

**Q: ヘッドレスサーバーで HTML を XPS に変換できますか？**  
A: もちろんです。Aspose.HTML は GUI のない環境でも動作しますので、Java ランタイムが適切に設定されていれば問題ありません。

**Q: ライブラリはカスタムページ余白に対応していますか？**  
A: はい。`PageSetup.setMarginTop()`、`setMarginBottom()` などを使用し、`PageSetup` をレンダリング オプションに割り当てる前に設定してください。

## 結論

**HTML を XPS に変換** し、Aspose.HTML for Java でページサイズを調整する完全な手順を解説しました。これらの手順に従うことで、正確なレイアウト要件に合致した印刷準備済みの XPS 文書を生成できます。プロジェクトのニーズに合わせて、さまざまなページ寸法やスタイルを試したり、ヘッダーやフッターを追加したりしてみてください。

ご質問やさらにサポートが必要な場合は、[Aspose.HTML for Java ドキュメント](https://reference.aspose.com/html/java/) をご覧いただくか、[Aspose Forum](https://forum.aspose.com/) でディスカッションに参加してください。

---

**最終更新日:** 2025-11-29  
**テスト環境:** Aspose.HTML for Java 24.11（執筆時点での最新バージョン）  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}