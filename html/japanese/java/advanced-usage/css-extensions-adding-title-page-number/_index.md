---
title: Aspose.HTML で HTML ページの余白をカスタマイズする
linktitle: CSS 拡張機能 - タイトルとページ番号の追加
second_title: Aspose.HTML を使用した Java HTML 処理
description: Aspose.HTML for Java を使用して、ページ余白をカスタマイズし、ページ番号とタイトルを HTML ドキュメントに追加する方法を学びます。
type: docs
weight: 10
url: /ja/java/advanced-usage/css-extensions-adding-title-page-number/
---
Aspose.HTML for Java は、Java アプリケーションで HTML ドキュメントを処理するための強力なライブラリです。このチュートリアルでは、Aspose.HTML for Java を使用して、カスタム ページ マージンを作成し、HTML ドキュメントにページ番号とタイトルを追加する方法について説明します。このステップ バイ ステップ ガイドでは、プロセスを管理しやすいステップに分解して、これらの機能を HTML ドキュメントに簡単に統合できるようにします。

## 前提条件

始める前に、次の前提条件が満たされていることを確認してください。

1. Java 開発環境: コンピューターに Java 開発環境が設定されていることを確認します。

2.  Aspose.HTML for Java: Aspose.HTML for Javaライブラリをここからダウンロードしてインストールします。[ここ](https://releases.aspose.com/html/java/).

## パッケージのインポート

開始するには、Aspose.HTML for Java から必要なパッケージをインポートする必要があります。次のインポート ステートメントを Java コードに追加します。

```java
// Aspose.HTML パッケージをインポートする
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

ここで、カスタム ページ余白、ページ番号、タイトルを追加するプロセスを管理しやすい手順に分解してみましょう。

## ステップ1: 構成とページ余白を初期化する

```java
//構成オブジェクトを初期化し、ドキュメントのページ余白を設定します。
Configuration configuration = new Configuration();
try {
    //ユーザーエージェントサービスを取得する
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

このステップでは、構成オブジェクトを初期化し、ページ カウンターとページ タイトルの位置を含むカスタム ページ マージンを設定します。

## ステップ2: HTMLドキュメントを初期化する

```java
//HTMLドキュメントを初期化する
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

ここでは、サンプル コンテンツ (この場合は「Hello World」メッセージ) を含む HTML ドキュメントを作成し、手順 1 の構成を適用します。

## ステップ3: 出力デバイスを初期化してドキュメントをレンダリングする

```java
//出力デバイスを初期化する
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    //文書を出力デバイスに送信する
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

この手順では、出力デバイスを設定し、HTML ドキュメントをレンダリングします。ドキュメントは処理され、指定されたページ余白、ページ番号、およびタイトルを含む XPS ファイルとして保存されます。

## 結論

おめでとうございます! Aspose.HTML for Java を使用して、カスタム ページ マージンを作成し、HTML ドキュメントにページ番号とタイトルを追加する方法を学習しました。このカスタマイズにより、よりプロフェッショナルで視覚的に魅力的なドキュメントを作成できます。

ご質問や問題がある場合は、お気軽に[Aspose.HTML for Java ドキュメント](https://reference.aspose.com/html/java/)または、[Aspose サポート フォーラム](https://forum.aspose.com/).

## よくある質問

### Q1: Aspose.HTML for Java とは何ですか?

A1: Aspose.HTML for Java は、Java アプリケーションで HTML ドキュメントを操作するための強力なツールを提供する Java ライブラリです。

### Q2: ページの余白をさらにカスタマイズできますか?

A2: はい、ステップ 1 で CSS スタイルを変更して、要件に応じてページ余白をカスタマイズできます。

### Q3: HTML ドキュメントにコンテンツを追加するにはどうすればよいですか?

A3: サンプル コンテンツを独自のコンテンツに置き換えることで、手順 2 の HTML コンテンツを変更できます。

### Q4: Aspose.HTML for Java は他のドキュメント形式と互換性がありますか?

A4: はい、Aspose.HTML for Java を使用すると、HTML ドキュメントを PDF、XPS、画像などのさまざまな形式に変換できます。

### Q5: Aspose.HTML for Java を使用するにはライセンスが必要ですか?

 A5: はい、ライセンスまたは無料トライアルは以下から入手できます。[ここ](https://purchase.aspose.com/buy)または[ここ](https://releases.aspose.com/).