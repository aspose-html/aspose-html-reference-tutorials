---
date: 2025-12-10
description: Aspose を使用して壊れたリンクを処理する方法、HTML を PNG に変換する方法、そして Aspose.HTML for Java
  を使って Java で HTML ドキュメントを読み込む方法を学びましょう。
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: JavaでAspose.HTMLメッセージハンドラを使用する方法
url: /ja/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java で Aspose.HTML メッセージハンドラを使用する方法

## Introduction
このチュートリアルでは、HTML の欠落リソースを処理するための **aspose** の使用方法をステップバイステップで示します。欠落した画像を参照するシンプルな HTML ドキュメントを作成し、カスタムメッセージハンドラを添付し、**load html document java** を実行しながら壊れたリンクを優雅に処理する方法を示します。最後には、Aspose.HTML を使用して **convert html to png** を行う方法も紹介し、Java における HTML から画像への変換の全体像を把握できます。

## Quick Answers
- **メッセージハンドラの主な目的は何ですか？** ネットワーク操作をインターセプトし、欠落リソースなどのステータスコードに反応することです。  
- **Aspose.HTML は HTML を PNG に変換できますか？** はい、`Converter.convertHTML` を使用して HTML から画像への変換を実行できます。  
- **この例にライセンスは必要ですか？** 一時ライセンスは評価制限を解除します。製品環境では永続ライセンスが必要です。  
- **サポートされている Java バージョンはどれですか？** JDK 8 以上 (本チュートリアルは JDK 11 を使用)。  
- **複数の壊れたリンクを処理できますか？** もちろんです。シナリオに応じて複数のハンドラをチェーンできます。

## Prerequisites
ステップバイステップガイドに入る前に、必要なものがすべて揃っていることを確認しましょう：

1. Java Development Kit (JDK): システムに JDK がインストールされていることを確認してください。ダウンロードは [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html) から行えます。  
2. Aspose.HTML for Java: Aspose.HTML for Java をインストールする必要があります。ダウンロードは [Aspose releases page](https://releases.aspose.com/html/java/) から。  
3. IDE: IntelliJ IDEA、Eclipse、NetBeans などお好みの Java 統合開発環境 (IDE) を使用してください。  
4. Java の基本知識: Java プログラミングに慣れていることが、本チュートリアルを効果的に進めるために必須です。  
5. 一時ライセンス: Aspose.HTML のトライアル版を使用している場合は、開発中の制限を回避するために [temporary license](https://purchase.aspose.com/temporary-license/) の取得を検討してください。

## Import Packages
開始する前に、Java プロジェクトに必要なパッケージがインポートされていることを確認してください。以下は必要なインポートです：
```java
import java.io.IOException;
```
これらのインポートにより、ネットワーク操作の処理、HTML ドキュメントの作成、HTML‑to‑PNG 変換に必要なクラスとメソッドにアクセスできます。

## Step 1: Prepare the HTML Code
### ステップ 1: HTML コードの準備
最初に必要なのは、画像ファイルを参照するシンプルな HTML スニペットです。エラー処理メカニズムを発動させるため、意図的に存在しない画像を参照します。
```java
String code = "<img src='missing.jpg'>";
```
このコードは `missing.jpg` を指す `<img>` タグを作成します。画像が存在しないため、ネットワークサービスは 200 以外のステータスコードを返し、カスタムハンドラがそれを捕捉します。

## Step 2: Write the HTML Code to a File
### ステップ 2: HTML コードをファイルに書き込む
次に、Aspose.HTML がドキュメントとして読み込めるように HTML スニペットを永続化する必要があります。
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
`FileWriter` を使用して HTML を **document.html** に保存します。このファイルが後の **load html document java** 手順のソースとなります。

## Step 3: Create a Custom Message Handler
### ステップ 3: カスタムメッセージハンドラの作成
次に、画像が見つからないときに反応するカスタムメッセージハンドラを作成します。ハンドラは HTTP ステータスコードをチェックし、フレンドリーなメッセージを出力します。
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
`invoke` メソッドは `context.getResponse().getStatusCode()` を調べます。ステータスが **200** でない場合、ファイルが欠落していることを明確に警告します。最後の `invoke(context);` 呼び出しは、チェーン内の次のハンドラに制御を渡します。

## Step 4: Configure the Network Service
### ステップ 4: ネットワークサービスの構成
Aspose.HTML にハンドラを認識させるため、`Configuration` クラスを介してネットワークサービスに登録します。
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
ここでは `Configuration` インスタンスを作成し、`INetworkService` を取得して、カスタムハンドラをそのコレクションに追加します。これにより、画像の読み込みなど、あらゆるネットワーク要求時にハンドラが実行されます。

## Step 5: Load the HTML Document
### ステップ 5: HTML ドキュメントの読み込み
構成が整ったので、先に作成した HTML ファイルを読み込みます。この手順は、欠落画像がハンドラをトリガーする間に **load html document java** を実演します。
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
`HTMLDocument` コンストラクタはファイルパスとカスタム `configuration` の両方を受け取ります。ドキュメントが `<img>` タグを解析すると、ネットワークサービスは `missing.jpg` の取得を試み、404 を受け取り、ハンドラが警告を出力します。

## Step 6: Convert HTML to PNG
### ステップ 6: HTML を PNG に変換
Aspose.HTML の幅広い機能を示すため、読み込んだドキュメントを PNG 画像に変換します。これは典型的な **convert html to png** シナリオです。
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
`Converter.convertHTML` は `HTMLDocument` とオプションの `ImageSaveOptions`（DPI や品質などを設定可能）および出力ファイル名を受け取ります。結果はレンダリングされた HTML のラスタ画像です。

## Step 7: Clean Up Resources
### ステップ 7: リソースのクリーンアップ
適切なリソース管理はすべての Java アプリケーションで重要です。メモリリークを防ぐために `Configuration` と `HTMLDocument` の両方を破棄します。
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
クリーンアップを `finally` ブロックでラップすることで、例外が発生した場合でも確実に実行されます。

## Why Use Message Handlers?
### メッセージハンドラを使用する理由
メッセージハンドラは **handle broken links java** のようなネットワーク操作を細かく制御できます。ライブラリが黙って失敗するのを防ぎ、ログ記録、再試行、リソースの置換、フォールバックコンテンツの提供などが可能になり、HTML 処理を堅牢かつ本番環境向けにします。

## Common Issues and Solutions
### 一般的な問題と解決策
- **ハンドラの再帰** – 無限ループを防ぐため、`invoke(context);` は一度だけ呼び出すようにしてください。  
- **ライセンスがない** – 有効なライセンスがない場合、変換結果に透かしが入った画像が生成される可能性があります。  
- **ファイルパスエラー** – `document.html` を読み込む際は絶対パスを使用するか、作業ディレクトリを正しく設定してください。

## Frequently Asked Questions

**Q: 複数のメッセージハンドラをチェーンできますか？**  
A: はい、`network.getMessageHandlers()` コレクションに複数のハンドラを追加できます。追加された順序で実行されます。

**Q: ハンドラは CSS やスクリプトリソースにも適用されますか？**  
A: もちろんです。HTML エンジンが行うすべてのネットワーク要求（画像、CSS、JS、フォントなど）はハンドラを通過します。

**Q: 送信前に HTTP リクエストを変更するには？**  
A: `invoke(context)` を呼び出す前に `context.getRequest()` を変更するハンドラを実装します。

**Q: 特定の URL に対して警告を抑制する方法はありますか？**  
A: ハンドラ内で `context.getRequest().getRequestUri()` を確認し、条件に応じてログ出力をスキップします。

**Q: これらの API に必要な Aspose.HTML のバージョンは？**  
A: コードは Aspose.HTML for Java 22.10 以降で動作します。

## Conclusion
### 結論
以上で、Java における **how to use aspose** メッセージハンドラの包括的なガイドが完成です。HTML ファイルの作成、**handle broken links java** 用のカスタムハンドラの設定、ドキュメントの読み込み、そして **convert html to png** の実行までをカバーしました。このパターンを使えば、欠落リソースを確実に管理し、カスタムポリシーを適用し、任意の Java アプリケーションで Aspose.HTML のネットワーク機能を拡張できます。

---

**最終更新日:** 2025-12-10  
**テスト環境:** Aspose.HTML for Java 24.11  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}