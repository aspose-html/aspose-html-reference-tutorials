---
category: general
date: 2026-04-03
description: Aspose.HTML Java のサンドボックスを使用して、ユーザーエージェントを設定し、サイズを指定し、ビューポートサイズを即座に取得する方法を学びましょう。完全なコード、解説、ヒントが含まれています。
draft: false
keywords:
- how to use sandbox
- set user agent
- get viewport size
- how to set size
- how to get viewport
language: ja
og_description: Aspose.HTML Java のサンドボックスを使用して、ユーザーエージェントの設定、サイズの指定、ビューポートサイズの即時取得方法を学びましょう。コードとベストプラクティスを含む完全ガイド。
og_title: サンドボックスの使い方 – ユーザーエージェントの設定とビューポートサイズの取得
tags:
- AsposeHTML
- Java
- Sandbox
title: サンドボックスの使い方 – ユーザーエージェントの設定とビューポートサイズの取得
url: /ja/java/configuring-environment/how-to-use-sandbox-set-user-agent-get-viewport-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# サンドボックスの使い方 – ユーザーエージェントの設定とビューポートサイズの取得

HTML を Aspose.HTML for Java でレンダリングするときに **サンドボックスの使い方** を疑問に思ったことはありませんか？特定の画面サイズをシミュレートしたり、ユーザーエージェント文字列を偽装してページをモバイルブラウザから閲覧しているかのように振る舞わせたいことはありませんか。

良いニュースは、サンドボックス API を使えばまさにそれが可能で、ページの読み込み後に計算されたビューポートサイズを取得することもできます。このチュートリアルでは、サンドボックスの作成、サイズ設定、カスタムユーザーエージェントの設定、リモートページの読み込み、そしてビューポート寸法の取得までを順に解説します。最後まで読めば **サイズの設定方法**、**ビューポートの取得方法**、そしてこれらの手順がヘッドレスレンダリングの信頼性にどのように寄与するかが分かります。

> **クイックウィン:** 数秒で `Viewport: 1280×800` のような出力を行う実行可能な Java クラスが手に入ります。

---

## 必要なもの

- **Aspose.HTML for Java** バージョン 24.6 以上（使用する API は 24.5 で導入）。  
- Java 17+ 開発キット（最近の JDK ならどれでも可）。  
- IDE またはシンプルなテキストエディタ – 特別なプラグインは不要。  
- `https://example.com` のような外部 URL を読み込みたい場合はインターネット接続。

以上です。Maven/Gradle の設定は必須ではなく、JAR を手動でクラスパスに置くだけでも構いません。  

---

## サンドボックスの使い方 – 概要

サンドボックスはレンダリングエンジンをホスト OS から分離し、仮想スクリーン（幅、高さ、DPI）とカスタム **ユーザーエージェント** 文字列を定義できるようにします。メモリ上だけに存在する小さなブラウザウィンドウと考えてください。後で `HTMLDocument` のデフォルトビューを取得すると、エンジンはサンドボックス設定に基づいて計算した **ビューポートサイズ** を返します。

大まかな流れは次の通りです：

1. `DocumentSandbox` を **作成**し、幅・高さ・DPI・ユーザーエージェントを設定。  
2. そのサンドボックス内で `HTMLDocument` を **ロード**。  
3. ドキュメントのデフォルトビューを **問い合わせ**てビューポートサイズを取得。  

それぞれのステップを詳しく見ていきましょう。

---

## 手順 1: サンドボックスを作成しサイズを設定

まずサンドボックスを起動し、仮想スクリーンのサイズを指定します。ここで **ヘッドレスレンダリングのサイズ設定方法** が決まります。

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.drawing.Size2D;

/* Step 1 – instantiate the sandbox */
DocumentSandbox sandbox = new DocumentSandbox();

/* Set the virtual screen width & height (in pixels) */
sandbox.setScreenWidth(1280);   // width in pixels
sandbox.setScreenHeight(800);   // height in pixels

/* DPI influences CSS pixel calculations – 96 is the CSS default */
sandbox.setDeviceDpi(96);

/* Optional: give the sandbox a friendly name for debugging */
sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");
```

> **プロチップ:** レスポンシブレイアウトをテストする場合、`360` のような狭い幅でスマートフォンをエミュレートしたり、`1920` のような広い幅でデスクトップをシミュレートしたりすると便利です。サンドボックスは設定した DPI を尊重するため、`144 DPI` の高密度スクリーンは `device-pixel-ratio` を使用したメディアクエリに影響します。

---

## 手順 2: サンドボックスのユーザーエージェントを設定

カスタム **ユーザーエージェント** が必要なのはなぜでしょうか？サイトによっては、報告されたブラウザに応じて異なるマークアップやスクリプトを配信します。`setUserAgent` を呼び出すことで、ページに Chrome、Firefox、またはモバイルデバイスからアクセスしていると偽装できます。

```java
/* Step 2 – customize the user‑agent string */
sandbox.setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                     "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                     "Version/15.0 Mobile/15E148 Safari/604.1");
```

これでページは iPhone で表示されていると認識します。デフォルトの **ユーザーエージェント** に戻したい場合は、以前の “AsposeHTML/24.6 …” 文字列を再利用してください。

---

## 手順 3: サンドボックス内で HTML ドキュメントをロード

サンドボックスの準備ができたら、任意の URL またはローカル HTML ファイルをロードできます。`HTMLDocument` コンストラクタは第2引数にサンドボックスを受け取り、両者を結び付けます。

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – load the page using the configured sandbox */
try (HTMLDocument doc = new HTMLDocument("https://example.com", sandbox)) {
    // The document is now rendered inside the sandbox environment.
    // Any JavaScript or CSS will see the size and user‑agent we defined.
```

`try‑with‑resources` ブロックは、ドキュメントを適切に破棄し、Aspose.HTML が内部で確保するネイティブリソースを解放します。

---

## 手順 4: ドキュメントからビューポートサイズを取得

いよいよ待ちに待った **ビューポートサイズ** の取得です。これにより **ページレイアウト後のビューポート取得方法** が分かります。

```java
    /* Step 4 – fetch the viewport dimensions */
    Size2D viewport = doc.getDefaultView().getScreenSize();
    System.out.println("Viewport: " + viewport.getWidth() + "×" + viewport.getHeight());
}
```

プログラムを実行すると、次のような出力が得られるはずです：

```
Viewport: 1280×800
```

手順 1でサンドボックスの寸法を変更した場合、出力される数値はその新しい値を反映します。レスポンシブブレークポイントを検証する自動テストに最適です。

---

## 完全動作サンプル

以下は、すべての要素を組み合わせた完成形のクラスです。`SandboxExample.java` という名前で保存し、Aspose.HTML の JAR をクラスパスに追加して `java SandboxExample` を実行してください。

```java
import com.aspose.html.*;
import com.aspose.html.drawing.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox with a custom screen size and DPI
        DocumentSandbox sandbox = new DocumentSandbox();
        sandbox.setScreenWidth(1280);          // width in pixels
        sandbox.setScreenHeight(800);          // height in pixels
        sandbox.setDeviceDpi(96);              // screen DPI
        sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");

        // Step 2: (Optional) Override the user agent if you need a mobile profile
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
            "Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 3: Load the HTML document inside the configured sandbox
        try (HTMLDocument htmlDocument = new HTMLDocument("https://example.com", sandbox)) {

            // Step 4: Retrieve and display the computed viewport size
            Size2D viewportSize = htmlDocument.getDefaultView().getScreenSize();
            System.out.println("Viewport: " + viewportSize.getWidth() + "×" + viewportSize.getHeight());
        }
    }
}
```

**期待される出力**（上記のサンドボックス設定の場合）：

```
Viewport: 1280×800
```

サンドボックスで幅・高さを変更すれば、出力もそれに応じて変化します。レスポンシブデザインのテストにまさに必要な動作です。

---

## エッジケースとよくある質問

### ページが CSS メディアクエリではなく `window.innerWidth` を使用している場合は？

サンドボックスの仮想スクリーンサイズは CSS レイアウトだけでなく、JavaScript の `window.innerWidth/innerHeight` にも影響します。したがって **JavaScript でのビューポート取得方法** は、Java コンソールに表示される数値と同じになります。

### 複数のサンドボックスを並列で実行できる？

はい。各 `DocumentSandbox` インスタンスは独立しているため、スレッドプールを作成し、各スレッドに異なる寸法のサンドボックスを割り当てて多数のページを同時にレンダリングできます。JAR がスレッドセーフであること（実際にスレッドセーフです）を忘れずに。

### DPI 設定は画像のスケーリングに影響しますか？

もちろんです。DPI が高いほど、1 CSS ピクセルがより多くのデバイスピクセルにマッピングされ、高解像度画像がより鮮明に表示されます。Retina 風のアセットをテストする場合は `sandbox.setDeviceDpi(144)` を試してください。

### 自己署名証明書を使用した HTTPS の取り扱いは？

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}