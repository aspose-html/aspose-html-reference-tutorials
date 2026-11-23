---
date: 2026-05-04
description: Aspose.HTML for Java を使用して、HTML を PNG に変換する方法、Java でネットワーク要求をインターセプトする方法、そして
  Java で壊れたリンクを処理する方法を学びましょう。
keywords:
- html to png conversion
- intercept network requests java
- html to image conversion
- load html document java
- handle broken links java
linktitle: Aspose.HTMLでメッセージハンドラを使用する
second_title: Java HTML Processing with Aspose.HTML
title: JavaでAspose.HTMLメッセージハンドラを使用したHTMLからPNGへの変換
url: /ja/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java における Aspose.HTML メッセージハンドラを使用した HTML から PNG への変換

## HTML から PNG への変換の概要
このチュートリアルでは、Aspose.HTML for Java を使用して **HTML を PNG に変換する方法** を学びながら、欠損リソースを優雅に処理する方法を紹介します。存在しない画像を指す小さな HTML ページを作成し、**カスタムメッセージハンドラ** を **ネットワークリクエストのインターセプト** に接続し、**ネットワークサービス** を構成し、ドキュメントを読み込み、最後に **html から画像への変換** を実行します。最後まで読むと、**handle broken links java** と高品質な PNG 出力の両方に対応できる堅牢なパターンが手に入ります—レポート、サムネイル、メールプレビューに最適です。

## クイック回答
- **メッセージハンドラは何をするのですか？** 画像リクエストなどのネットワーク操作をインターセプトし、404 などのステータスコードに対してリアクションできます。  
- **Aspose.HTML は HTML を PNG に変換できますか？** はい—`Converter.convertHTML` が単一呼び出しで変換を実行します。  
- **このサンプルにライセンスは必要ですか？** 一時ライセンスで評価制限が解除されますが、本番利用には永続ライセンスが必要です。  
- **どの Java バージョンが動作しますか？** JDK 8 以上 (サンプルは JDK 11 で動作)  
- **ネットワークサービスは設定できますか？** もちろんです—`configuration.getService(INetworkService.class)` を使用してハンドラを追加します。

## HTML から PNG への変換とは？
HTML から PNG への変換は、ウェブページ（または HTML の一部）をラスタ画像にレンダリングします。動的コンテンツの静的プレビューが必要なときや、メールニュースレター用のサムネイル生成、ウェブページの画像アーカイブなどに便利です。

## Java においてネットワークリクエストをインターセプトするためにメッセージハンドラを使用する理由
メッセージハンドラは、画像、CSS、JavaScript、フォントファイルなど、すべてのネットワークリクエストに対して **細かな制御** を提供します。これらのリクエストをインターセプトすることで、**欠損アセットのログ記録**、フォールバックコンテンツの提供、失敗したダウンロードの再試行などが可能になり、HTML 処理パイプラインを **堅牢** かつ **本番環境対応** にします。

## 前提条件
1. **Java Development Kit (JDK)** – [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html) からダウンロードしてください。  
2. **Aspose.HTML for Java** – [Aspose releases page](https://releases.aspose.com/html/java/) からライブラリを取得してください。  
3. **IDE** – IntelliJ IDEA、Eclipse、または NetBeans が使用可能です。  
4. **Basic Java knowledge** – クラス、try‑with‑resources、例外処理に慣れている必要があります。  
5. **Temporary License** – トライアル中の場合は、ウォーターマークを回避するために [temporary license](https://purchase.aspose.com/temporary-license/) を取得してください。

## パッケージのインポート
まず、ファイル操作に必要な Java I/O クラスをインポートします。残りの Aspose クラスは後で完全修飾名で参照するため、インポートリストはすっきりします。

```java
import java.io.IOException;
```

## ステップ 1: HTML コードの準備
欠損画像を意図的に参照する最小限の HTML スニペットを作成します。これにより、エンジンがリソース取得を試みたときにハンドラがトリガーされます。

```java
String code = "<img src='missing.jpg'>";
```

## ステップ 2: HTML コードをファイルに書き込む
次に、スニペットを *document.html* に保存します。try‑with‑resources ブロックを使用することで `FileWriter` が適切にクローズされます。

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## ステップ 3: カスタムメッセージハンドラの作成
**カスタムメッセージハンドラ** を構築し、すべてのネットワークリクエストの HTTP ステータスをチェックします。レスポンスが `200` でない場合はフレンドリーな警告をログに記録します。最後の `invoke(context);` 呼び出しは、リクエストをチェーン内の次のハンドラに転送し、再帰を防ぎます。

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

## ステップ 4: ネットワークサービスの構成
Aspose.HTML にハンドラを認識させるため、`Configuration` インスタンスから **ネットワークサービス** を取得し、ハンドラをコレクションに追加します。これがカスタム動作のために **ネットワークサービスを構成** するステップです。

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## ステップ 5: HTML ドキュメントの読み込み
構成が整ったら *document.html* を読み込みます。エンジンは今回設定したネットワークサービスを使用するため、欠損画像リクエストは先ほど追加したハンドラでインターセプトされます。

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

## ステップ 6: HTML を PNG に変換
**html to image conversion** の核心です。`Converter.convertHTML` メソッドは、読み込んだ `HTMLDocument`、任意の `ImageSaveOptions`（DPI や品質の調整が可能）、および出力ファイル名を受け取ります。

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## ステップ 7: リソースのクリーンアップ
Java のベストプラクティスとして、すべてのネイティブリソースを解放します。`finally` ブロックは例外がスローされても `Configuration` が確実に破棄されるようにします。

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## 一般的な問題と解決策
- **ハンドラの再帰** – 無限ループを防ぐために `invoke(context);` は一度だけ呼び出してください。  
- **ライセンスがない** – 有効なライセンスがないと、出力 PNG にウォーターマークが入ります。  
- **ファイルパスが間違っている** – `document.html` を読み込む際は絶対パスを使用するか、作業ディレクトリを正しく設定してください。  
- **サポートされていないリソースタイプ** – インターセプトしたいリソース（画像、CSS など）が実際に HTML エンジンからリクエストされていることを確認してください。

## よくある質問

**Q: 複数のメッセージハンドラをチェーンできますか？**  
A: はい、`network.getMessageHandlers()` コレクションに複数のハンドラを追加できます。追加された順序で実行されます。

**Q: ハンドラは CSS やスクリプトリソースにも対応していますか？**  
A: 対応しています—HTML エンジンが行うすべてのネットワークリクエスト（画像、CSS、JS、フォントなど）はハンドラを通過します。

**Q: 送信前に HTTP リクエストを変更するにはどうすればよいですか？**  
A: `invoke(context)` を呼び出す前に `context.getRequest()` を変更するハンドラを実装してください。

**Q: 特定の URL に対して警告を抑制する方法はありますか？**  
A: ハンドラ内で `context.getRequest().getRequestUri()` をチェックし、条件に応じてログ出力をスキップできます。

**Q: これらの API を使用するために必要な Aspose.HTML のバージョンは？**  
A: コードは Aspose.HTML for Java 22.10 以降で動作します。

---

**Last Updated:** 2026-05-04  
**Tested With:** Aspose.HTML for Java 24.11  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}