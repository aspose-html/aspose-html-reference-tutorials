---
date: 2025-12-08
description: Aspose.HTML for Java を使用して、壊れたリンクを処理し、カスタム メッセージ ハンドラで欠落したリソースを検出しながら、HTML
  を PNG に変換する方法を学びましょう。
language: ja
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Aspose.HTML for JavaでHTMLをPNGに変換し、メッセージハンドラを使用する方法
url: /java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML for Java を使用した HTML から PNG への変換 – メッセージハンドラの利用

## はじめに  
このチュートリアルでは、Aspose.HTML for Java を使用して **HTML を PNG に変換する方法** と、同時にカスタムメッセージハンドラを使って **壊れたリンク** や欠落したリソースを処理する方法を学びます。シンプルな HTML ファイルの作成、ディスクへの書き込み、ロード、そしてネットワークエラーの捕捉までを順に解説します。プロダクションレベルの Java アプリケーションで信頼できる **html to image conversion** が必要な開発者に最適です。

## クイック回答
- **このチュートリアルでカバーする内容は？** HTML を PNG に変換し、メッセージハンドラで欠落リソースを処理します。  
- **使用しているライブラリは？** Aspose.HTML for Java。  
- **ライセンスは必要ですか？** 試用ビルドには一時ライセンスの使用が推奨されます。  
- **Java から HTML ファイルを書き込めますか？** はい – “write html file java” の手順をご覧ください。  
- **ハンドラは壊れたリンクを捕捉しますか？** もちろんです。200 以外のレスポンスをすべてログに記録します。

## Aspose.HTML のメッセージハンドラとは？  
メッセージハンドラはネットワークスタックへのフックで、例外が発生する前に **欠落リソース**（壊れた画像 URL など）を **捕捉** できます。レスポンスのステータスコードを検査することで、ログ記録、置換、再試行などが可能となり、ネットワーク操作を完全に制御できます。

## なぜ HTML を PNG に変換するのか？  
HTML を画像に変換することは、サムネイルやメールプレビュー、PDF のようなスナップショットを生成する際に、フル PDF 変換が不要な場合に便利です。Aspose.HTML はブラウザを使用せずに動作する高速なサーバーサイド **html to image conversion** エンジンを提供します。

## 前提条件
1. **Java Development Kit (JDK)** – [Oracle のウェブサイト](https://www.oracle.com/java/technologies/javase-downloads.html) からダウンロードしてください。  
2. **Aspose.HTML for Java** – 最新の JAR は [Aspose のリリースページ](https://releases.aspose.com/html/java/) から取得してください。  
3. **IDE** – IntelliJ IDEA、Eclipse、または NetBeans。  
4. **基本的な Java の知識** – try‑with‑resources やオブジェクトの破棄に慣れていることが望ましいです。  
5. **一時ライセンス**（オプション） – 試用版の制限を回避するために [temporary license](https://purchase.aspose.com/temporary-license/) を使用してください。

## パッケージのインポート
開始する前に、必要な Java クラスをインポートします：

```java
import java.io.IOException;
```

これらのインポートにより、ファイル I/O と Aspose.HTML のネットワーク API にアクセスできるようになります。

## ステップ 1: HTML ファイルを書き込む (write html file java)  
まず、**存在しない** 画像を参照する小さな HTML スニペットを作成します。これによりハンドラのテストが可能になります。

```java
String code = "<img src='missing.jpg'>";
```

## ステップ 2: HTML をディスクに保存  
`document.html` という名前のファイルにスニペットを保存します。このファイルは後で Aspose.HTML エンジンで読み込まれます。

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## ステップ 3: カスタムメッセージハンドラの作成 (catch missing resource)  
ここで、HTTP ステータスコードをチェックするハンドラを定義します。ステータスが `200` でない場合、フレンドリーなメッセージをログに記録します。

```java
com.aspose.html.net.MessageHandler handler = new com.aspose.html.net.MessageHandler() {
    @Override
    public void invoke(com.aspose.html.net.INetworkOperationContext context) {
        if (context.getResponse().getStatusCode() != 200) {
            System.out.println(String.format("File '%s' Not Found", context.getRequest().getRequestUri().toString()));
        }
        invoke(context);
    }
};
```

## ステップ 4: ハンドラをネットワークサービスに登録  
カスタムハンドラを Aspose.HTML のネットワークサービスに追加し、すべてのリクエストに参加させます。

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## ステップ 5: HTML ドキュメントのロード (load html document java)  
設定が完了したら、HTML ファイルをロードします。欠落した画像がハンドラをトリガーします。

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Additional operations will go here
} finally {
    if (document != null) {
        document.dispose();
    }
}
```

## ステップ 6: HTML を PNG に変換 (convert html to png)  
最後に、ロードしたドキュメントを PNG 画像に変換します。これにより、完全な **html to image conversion** ワークフローが実演されます。

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## ステップ 7: リソースのクリーンアップ  
`Configuration` オブジェクトは常に破棄し、ネイティブリソースを解放してメモリリークを防止してください。

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## よくある落とし穴とヒント
- **再帰的な invoke 呼び出し:** カスタムハンドラはロジックの *後* に `invoke(context);` を呼び出す必要があります。これを忘れると他のハンドラが実行されなくなります。  
- **ライセンス未取得の警告:** 有効なライセンスがない場合、変換に透かしが付加されたり、出力サイズが制限されたりします。  
- **パスの問題:** `document.html` が作業ディレクトリに書き込まれていること、または絶対パスを指定していることを確認してください。  

## よくある質問

**Q: Aspose.HTML for Java とは何ですか？**  
A: ブラウザを使用せずに、Java 開発者が HTML ドキュメントを作成、操作、変換できる堅牢なライブラリです。

**Q: Aspose.HTML for Java でメッセージハンドラを使用する理由は？**  
A: **壊れたリンク** を処理したり、欠落リソースをログに記録したり、リクエスト/レスポンスをリアルタイムで変更したりできます。

**Q: 複数のメッセージハンドラをチェーンできますか？**  
A: はい。各ハンドラを `network.getMessageHandlers()` リストに追加すれば、追加した順に実行されます。

**Q: Configuration と HTMLDocument オブジェクトの破棄は必須ですか？**  
A: 絶対に必要です。破棄することでネイティブメモリが解放され、長時間稼働するアプリケーションでのリークを防げます。

**Q: 欠落画像以外に、ハンドラで管理できるエラーは何ですか？**  
A: 200 以外のすべての HTTP レスポンス（タイムアウト、404 ページ、認証失敗など）を捕捉して処理できます。

## 結論  
これで、Aspose.HTML for Java を使用して **HTML を PNG に変換** しながら **壊れたリンク** を処理し、**欠落リソース** を捕捉する完全なプロダクション向けサンプルが完成しました。このパターンを大規模プロジェクトに組み込むことで、ネットワーク操作を細かく制御し、HTML コンテンツの信頼性の高い画像スナップショットを生成できます。

---

**最終更新日:** 2025-12-08  
**テスト環境:** Aspose.HTML for Java 24.12（最新）  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}