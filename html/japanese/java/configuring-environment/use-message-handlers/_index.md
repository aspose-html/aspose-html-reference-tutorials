---
date: 2026-02-10
description: Aspose を使用して壊れたリンクを処理する方法、HTML を PNG に変換する方法、そして Aspose.HTML for Java
  を使って Java で HTML ドキュメントを読み込む方法を学びましょう。
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: JavaのAspose.HTMLメッセージハンドラでHTMLをPNGに変換
url: /ja/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML メッセージハンドラを使用した Java での HTML から PNG への変換

## はじめに
このチュートリアルでは、Aspose.HTML for Java を使用して、欠落したリソースを優雅に処理しながら **HTML を PNG に変換する方法** を学びます。存在しない画像を指す小さな HTML ページを作成し、**custom message handler** を **ネットワーク要求のインターセプト** に接続し、**ネットワークサービス** を構成し、ドキュメントをロードし、最後に **HTML から画像への変換** を実行する手順を順に説明します。最後まで読むと、**handle broken links java** と高品質な PNG 出力の両方に対応できる堅牢なパターンが手に入ります—レポート、サムネイル、メールプレビューに最適です。

## クイック回答
- **メッセージハンドラは何をしますか？** ネットワーク操作（画像リクエストなど）をインターセプトし、404 などのステータスコードに応じて処理できます。  
- **Aspose.HTML は HTML を PNG に変換できますか？** はい—`Converter.convertHTML` は単一の呼び出しで変換を実行します。  
- **この例にライセンスは必要ですか？** 一時ライセンスは評価制限を解除します。製品環境で使用するには永続ライセンスが必要です。  
- **どの Java バージョンが使用できますか？** JDK 8 以上であればどれでも使用できます（サンプルは JDK 11 で動作します）。  
- **ネットワークサービスを構成できますか？** もちろんです—`configuration.getService(INetworkService.class)` を使用してハンドラを追加します。

## 前提条件
1. **Java Development Kit (JDK)** – [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html) からダウンロードしてください。  
2. **Aspose.HTML for Java** – ライブラリは [Aspose releases page](https://releases.aspose.com/html/java/) から取得してください。  
3. **IDE** – IntelliJ IDEA、Eclipse、または NetBeans が使用できます。  
4. **Basic Java knowledge** – クラス、try‑with‑resources、例外処理に慣れている必要があります。  
5. **Temporary License** – トライアル中の場合は、透かしを回避するために [temporary license](https://purchase.aspose.com/temporary-license/) を取得してください。

## パッケージのインポート
まず、ファイル操作に必要な Java I/O クラスをインポートします。残りの Aspose クラスは後で完全修飾名で参照するため、インポートリストはすっきりと保たれます。

```java
import java.io.IOException;
```

## ステップ 1: HTML コードの準備
意図的に存在しない画像を参照する最小限の HTML スニペットを作成します。エンジンがリソースの取得を試みたときにハンドラがトリガーされます。

```java
String code = "<img src='missing.jpg'>";
```

## ステップ 2: HTML コードをファイルに書き込む
次に、スニペットを *document.html* に保存します。try‑with‑resources ブロックを使用することで `FileWriter` が適切にクローズされることが保証されます。

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## ステップ 3: カスタムメッセージハンドラの作成
ここで、すべてのネットワーク要求の HTTP ステータスをチェックする **custom message handler** を作成します。レスポンスが `200` でない場合は、フレンドリーな警告をログに記録します。最後の `invoke(context);` の呼び出しに注目してください—これにより要求がチェーン内の次のハンドラに転送され、再帰が防止されます。

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
Aspose.HTML にハンドラを認識させるため、`Configuration` インスタンスから **network service** を取得し、ハンドラをそのコレクションに追加します。ここがカスタム動作のために **configure network service** を行うステップです。

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## ステップ 5: HTML ドキュメントのロード
構成が完了したら、*document.html* をロードします。エンジンは現在、当社のネットワークサービスを使用するため、先ほど追加したハンドラが欠落画像のリクエストをインターセプトします。

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
これが **html to image conversion** プロセスの核心です。`Converter.convertHTML` メソッドは、ロードされた `HTMLDocument`、オプションの `ImageSaveOptions`（DPI や品質を調整できる）および出力ファイル名を受け取ります。

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## ステップ 7: リソースのクリーンアップ
適切な Java の慣習として、すべてのネイティブリソースを解放する必要があります。`finally` ブロックは、例外がスローされても `Configuration` が確実に破棄されることを保証します。

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## なぜメッセージハンドラを使用するのか？
メッセージハンドラは、画像、CSS、JavaScript、フォントファイルなど、すべてのネットワーク要求に対して **fine‑grained control** を提供します。ライブラリが黙って失敗するのを防ぎ、欠落したアセットをログに記録したり、フォールバックコンテンツを提供したり、リクエストを再試行したりできます。これにより、HTML 処理パイプラインは **robust**、**production‑ready** となり、デバッグも容易になります。

## 一般的な問題と解決策
- **Handler recursion** – 無限ループを防ぐために `invoke(context);` は一度だけ呼び出してください。  
- **Missing license** – 有効なライセンスがない場合、出力 PNG に透かしが入ります。  
- **Incorrect file paths** – `document.html` をロードする際は絶対パスを使用するか、作業ディレクトリを正しく設定してください。  
- **Unsupported resource types** – インターセプトしたいリソース（画像、CSS など）が HTML エンジンによって実際にリクエストされていることを確認してください。

## よくある質問

**Q: 複数のメッセージハンドラをチェーンできますか？**  
A: はい、`network.getMessageHandlers()` コレクションに複数のハンドラを追加できます。追加された順序で実行されます。

**Q: ハンドラは CSS やスクリプトリソースでも機能しますか？**  
A: もちろんです—HTML エンジンが行うすべてのネットワークリクエスト（画像、CSS、JS、フォント）はハンドラを通過します。

**Q: 送信前に HTTP リクエストを変更するにはどうすればよいですか？**  
A: `invoke(context)` を呼び出す前に `context.getRequest()` を変更するハンドラを実装してください。

**Q: 特定の URL に対する警告を抑制する方法はありますか？**  
A: ハンドラ内で `context.getRequest().getRequestUri()` を確認し、条件に応じてログ出力をスキップしてください。

**Q: これらの API に必要な Aspose.HTML のバージョンは何ですか？**  
A: このコードは Aspose.HTML for Java 22.10 以降で動作します。

## 結論
これで、**HTML を PNG に変換する方法** の完全なエンドツーエンド例が完成し、**custom message handler** を使用して **ネットワークリクエストをインターセプト** し、**handle broken links java** を処理できます。ネットワークサービスを構成し、ドキュメントをロードし、コンバータを呼び出すことで、任意の Java アプリケーションで PNG サムネイルやフルページのスクリーンショットを確実に生成できます。

---

**最終更新日:** 2026-02-10  
**テスト環境:** Aspose.HTML for Java 24.11  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}