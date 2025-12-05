---
date: 2025-12-05
description: Aspose.HTML を使用して Java で HTML ページの余白を設定し、ドキュメントにページ番号とタイトルを追加する方法を学びましょう。
language: ja
linktitle: CSS Extensions - Adding Title and Page Number
second_title: Java HTML Processing with Aspose.HTML
title: Aspose.HTML を使用した Java で HTML ページの余白を設定する方法
url: /java/advanced-usage/css-extensions-adding-title-page-number/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML を使用した Java での HTML ページ余白の設定方法

このチュートリアルでは、Aspose.HTML for Java を使用して **Java スタイルで HTML ページの余白を設定する方法** を学びます。カスタム余白の作成、ページ番号の挿入、文書タイトルの追加を順を追って解説し、プロジェクトにそのままコピーできるコードをステップバイステップで示します。

## クイック回答
- **必要なライブラリは？** Aspose.HTML for Java  
- **余白をプログラムで制御できますか？** はい、ユーザースタイルシートの CSS `@page` ルールで可能です  
- **どの出力フォーマットが余白に対応していますか？** XPS、PDF、その他のラスターフォーマット  
- **本番環境でライセンスは必要ですか？** トライアル以外の使用には有効な Aspose.HTML ライセンスが必要です  
- **Java 11+ と互換性がありますか？** 完全に対応しています – ライブラリは最新の Java バージョンで動作します  

## 「HTMLページ余白の設定（Java）」とは？
Java で HTML ページの余白を設定するとは、Aspose.HTML が提供するレンダリングエンジンを構成し、文書が XPS や PDF といった印刷可能な形式に変換される前に CSS のページボックスプロパティを適用することを意味します。カスタム `@page` ルールを定義することで、印刷領域やページ番号、ヘッダー/フッターの内容を制御できます。

## 余白制御に Aspose.HTML を使用する理由
- **正確なレイアウト** – CSS `@page` により、余白、ヘッダー、フッターをピクセル単位で正確に制御できます。  
- **フォーマット横断の一貫性** – 同じ余白定義が XPS、PDF、画像出力でも機能します。  
- **ブラウザ不要** – レンダリングはサーバー側で行われるため、ヘッドレスブラウザは不要です。  

## 前提条件

始める前に、以下の前提条件が整っていることをご確認ください。

1. **Java 開発環境** – JDK 11 以上がインストールされていること。  
2. **Aspose.HTML for Java** – ライブラリを [here](https://releases.aspose.com/html/java/) からダウンロードしてインストールしてください。  

## パッケージのインポート

まず、必要な Aspose.HTML クラスをインポートします。

```java
// Import Aspose.HTML packages
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

## HTML ページ余白の設定（Java） – ステップバイステップガイド

### 手順 1: Configuration の初期化とカスタムページ余白の定義

```java
// Initialize configuration object and set up the page-margins for the document
Configuration configuration = new Configuration();
try {
    // Get the User Agent service
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Set the style of custom margins and create marks on it
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

このブロックでは `Configuration` オブジェクトを作成し、`IUserAgentService` を取得して、余白、右下のページカウンタ、上部中央の文書タイトルを定義する CSS `@page` ルールを注入しています。

### 手順 2: HTML ドキュメントの作成

```java
// Initialize an HTML document
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

ここではシンプルな “Hello World” スニペットで `HTMLDocument` をインスタンス化します。手順 1 で作成した同じ構成が適用されるため、ドキュメントのレンダリング時にカスタム余白が反映されます。

### 手順 3: XPS ファイル（または任意のサポート出力）へレンダリング

```java
// Initialize an output device
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    // Send the document to the output device
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

この手順では、レンダリングされたページを `output.xps` に書き込む `XpsDevice` を作成します。先ほど定義した余白、ページ番号、タイトルが最終ファイルに反映されます。

## よくある問題とヒント
- **余白が変わらない** – `@page` ルールが他のスタイルシートで上書きされていないか確認してください。`setUserStyleSheet` 呼び出しにより最優先になります。  
- **ページ番号が “NaN” と表示される** – Aspose.HTML バージョン 23.10 以降を使用しているか確認してください。古いバージョンには `currentPageNumber()` 関数がありません。  
- **出力ファイルが空** – `Resources.output` パスが正しく解決され、書き込み権限があることを確認してください。  

## よくある質問

### Q1: Aspose.HTML for Java とは？

**A:** Aspose.HTML for Java は、Java アプリケーションで HTML ドキュメントを扱うための強力なツールを提供する Java ライブラリで、変換、レンダリング、操作などが可能です。

### Q2: ページ余白をさらにカスタマイズできますか？

**A:** はい、`setUserStyleSheet` 内の CSS を編集するだけです。`margin-*` の値を変更したり、追加の `@top-*` / `@bottom-*` ボックスを追加したりできます。

### Q3: HTML ドキュメントにさらにコンテンツを追加するには？

**A:** `new HTMLDocument("<div>Hello World!!!</div>", …)` の文字列を独自の HTML マークアップに置き換えるか、`HTMLDocument(String url, …)` コンストラクタを使用して外部ファイルをロードしてください。

### Q4: Aspose.HTML for Java は他のドキュメント形式と互換性がありますか？

**A:** もちろんです。同じ `HTMLDocument` を出力デバイス（例: `PdfDevice`、`PngDevice`）を切り替えることで、PDF、XPS、画像、さらには EPUB にもレンダリングできます。

### Q5: Aspose.HTML for Java の使用にライセンスは必要ですか？

**A:** はい、本番環境で使用するにはライセンスが必要です。トライアル版を取得するか、[here](https://purchase.aspose.com/buy) または [here](https://releases.aspose.com/) からライセンスを購入してください。

### Q6: 奇数ページと偶数ページで異なる余白を設定するには？

**A:** スタイルシート内で `@page :left` と `@page :right` 疑似クラスを使用し、左側（偶数）ページと右側（奇数）ページで異なる余白を定義してください。

### Q7: レンダリングされたドキュメントにカスタムフォントを埋め込めますか？

**A:** はい。ユーザースタイルシートに `@font-face` ルールを追加し、HTML コンテンツでそのフォントを参照してください。

## 結論

これで Aspose.HTML を使用した **Java での HTML ページ余白の設定** を習得し、ページ番号やタイトルを追加して文書をプロフェッショナルに仕上げる方法が分かりました。プロジェクトの要件に合わせて、追加の `@page` ボックスやカスタムフォント、さまざまな出力形式を自由に試してみてください。

問題が発生した場合は、公式の [Aspose.HTML for Java ドキュメント](https://reference.aspose.com/html/java/) と [Aspose サポートフォーラム](https://forum.aspose.com/) が有用です。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2025-12-05  
**Tested With:** Aspose.HTML for Java 23.12  
**Author:** Aspose