---
title: Aspose.HTML を使用して HTML ページの余白をカスタマイズする
linktitle: CSS 拡張機能 - タイトルとページ番号の追加
second_title: Aspose.HTML を使用した Java HTML 処理
description: Aspose.HTML for Java を使用して、ページ余白をカスタマイズし、ページ番号とタイトルを HTML ドキュメントに追加する方法を学びます。
type: docs
weight: 10
url: /ja/java/advanced-usage/css-extensions-adding-title-page-number/
---
Aspose.HTML for Java は、Java アプリケーションで HTML ドキュメントを処理するための強力なライブラリです。このチュートリアルでは、Aspose.HTML for Java を使用してカスタム ページ余白を作成し、HTML ドキュメントにページ番号とタイトルを追加する方法を説明します。このステップバイステップのガイドでは、これらの機能を HTML ドキュメントに簡単に統合できるように、プロセスを管理しやすいステップに分割して説明します。

## 前提条件

始める前に、次の前提条件が満たされていることを確認してください。

1. Java 開発環境: コンピュータに Java 開発環境がセットアップされていることを確認します。

2.  Aspose.HTML for Java: Aspose.HTML for Java ライブラリをダウンロードしてインストールします。[ここ](https://releases.aspose.com/html/java/).

## パッケージのインポート

開始するには、Aspose.HTML for Java から必要なパッケージをインポートする必要があります。次のインポート ステートメントを Java コードに追加します。

```java
// Aspose.HTML パッケージをインポートする
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

ここで、カスタムのページ余白、ページ番号、タイトルを追加するプロセスを管理しやすい手順に分割してみましょう。

## ステップ 1: 構成とページ余白を初期化する

```java
//構成オブジェクトを初期化し、ドキュメントのページマージンを設定します
Configuration configuration = new Configuration();
try {
    //ユーザー エージェント サービスを取得する
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    //カスタム余白のスタイルを設定し、その上にマークを作成します
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

このステップでは、構成オブジェクトを初期化し、ページカウンターとページタイトルの位置を含むカスタムページマージンを設定します。

## ステップ 2: HTML ドキュメントを初期化する

```java
//HTMLドキュメントを初期化する
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

ここでは、サンプル コンテンツ (この場合は「Hello World」メッセージ) を含む HTML ドキュメントを作成し、ステップ 1 の構成を適用します。

## ステップ 3: 出力デバイスを初期化してドキュメントをレンダリングする

```java
//出力デバイスを初期化する
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    //ドキュメントを出力デバイスに送信します
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

このステップでは、出力デバイスをセットアップし、HTML ドキュメントをレンダリングします。ドキュメントは処理され、指定されたページ余白、ページ番号、タイトルを持つ XPS ファイルとして保存されます。

## 結論

おめでとう！ Aspose.HTML for Java を使用してカスタム ページ余白を作成し、HTML ドキュメントにページ番号とタイトルを追加する方法を学習しました。このカスタマイズにより、よりプロフェッショナルで視覚的に魅力的なドキュメントを作成できます。

ご質問や問題がございましたら、お気軽にアクセスしてください。[Aspose.HTML for Java ドキュメント](https://reference.aspose.com/html/java/)または、[Aspose サポート フォーラム](https://forum.aspose.com/).

## よくある質問

### Q1: Aspose.HTML for Java とは何ですか?

A1: Aspose.HTML for Java は、Java アプリケーションで HTML ドキュメントを操作するための強力なツールを提供する Java ライブラリです。

### Q2: ページの余白をさらにカスタマイズできますか?

A2: はい、ステップ 1 で CSS スタイルを変更して、要件に応じてページの余白をカスタマイズできます。

### Q3: HTML ドキュメントにさらにコンテンツを追加するにはどうすればよいですか?

A3: サンプル コンテンツを独自のコンテンツに置き換えることで、ステップ 2 の HTML コンテンツを変更できます。

### Q4: Aspose.HTML for Java は他のドキュメント形式と互換性がありますか?

A4: はい、Aspose.HTML for Java を使用して、HTML ドキュメントを PDF、XPS、画像などのさまざまな形式に変換できます。

### Q5: Aspose.HTML for Java を使用するにはライセンスが必要ですか?

 A5: はい、次のサイトからライセンスまたは無料トライアルを取得できます。[ここ](https://purchase.aspose.com/buy)または[ここ](https://releases.aspose.com/).