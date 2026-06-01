---
category: general
date: 2026-05-31
description: Aspose HTML を使用して Java でウェブページを PNG にレンダリングする際に外部画像を無効にします。サンドボックス内で安全にウェブページを読み込み、HTML
  ドキュメントを PNG として保存する方法を学びましょう。
draft: false
keywords:
- disable external images
- render webpage to png
- load webpage in sandbox
- how to render html to image java
- save html document as png
language: ja
og_description: JavaでウェブページをPNGにレンダリングする際に外部画像を無効にする。このステップバイステップガイドでは、サンドボックス内でウェブページを読み込み、HTMLドキュメントをPNGとして保存する方法を示します。
og_title: JavaでWebページをPNGにレンダリングする際に外部画像を無効化する
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Disable external images when you render webpage to PNG in Java using
    Aspose HTML. Learn to load webpage in sandbox safely and save HTML document as
    PNG.
  headline: Disable External Images While Rendering Webpage to PNG in Java
  type: TechArticle
- questions:
  - answer: Yes. Inline `data:` URIs or base64‑encoded images are treated as part
      of the document and will appear in the PNG.
    question: Can I still display images that are bundled inside the HTML?
  - answer: The sandbox works as an all‑or‑nothing switch. For fine‑grained control,
      download the allowed images yourself, embed them as data URIs, and then render.
    question: What if I need to keep some external images but block others?
  - answer: Absolutely. Aspose.HTML is a pure‑Java library; it does not require a
      display server or browser engine.
    question: Does this approach work on headless servers?
  - answer: 'Selenium drives a real browser, which is heavyweight and harder to sandbox.
      Aspose.HTML renders HTML directly in memory, giving you deterministic performance
      and easier security controls like **disable external images**. --- ## Conclusion
      You now have a solid, end‑to‑end recipe for **disabling exter'
    question: How does this differ from using Selenium or Puppeteer?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- Image Rendering
title: JavaでウェブページをPNGにレンダリングする際に外部画像を無効化する
url: /ja/java/conversion-html-to-various-image-formats/disable-external-images-while-rendering-webpage-to-png-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaでウェブページをPNGにレンダリングする際に外部画像を無効化する方法

ウェブページをPNGにレンダリングする際に **外部画像を無効化** したいことはありませんか？たとえば、インターネットから隔離されたサムネイルサービスを構築したい場合や、変換中にサードパーティの画像が漏れないようにしたい場合などです。どちらの場合でも、ここが正しい場所です。

このチュートリアルでは、サンドボックス内でウェブページを読み込み、外部画像取得をオフにし、最終的に HTML ドキュメントを PNG ファイルとして保存する手順を Aspose.HTML for Java を使って解説します。最後まで読むと、すぐに実行できるサンプルと、一般的な落とし穴を回避するための実用的なヒントが手に入ります。

## 学べること

- Aspose.HTML の `Converter` を使った **HTML から画像への変換** 方法
- カスタムビューポートと DPI を設定した **サンドボックスでのウェブページ読み込み** 手順
- **外部画像を無効化** しながらページをレンダリングするための設定方法
- HTML ドキュメントを PNG（または他のサポート形式）としてディスクに **保存** する方法
- エッジケースの対処法、パフォーマンスのヒント、トラブルシューティングのアドバイス

### 前提条件

- Java 8 以上がインストールされていること（コードは JDK 11+ でも動作します）
- Aspose.HTML for Java ライブラリを取得できる Maven または Gradle が使用できること
- Java の構文と例外処理に関する基本的な知識
- 初回のページ読み込みのためにインターネット接続が必要（ローカルで HTML を提供する場合は不要）

> **プロのコツ:** 企業プロキシ環境下で作業している場合は、サンプルを実行する前に JVM の `http.proxyHost` と `http.proxyPort` プロパティを設定してください。

---

## 手順 1: プロジェクトをセットアップし Aspose.HTML を追加

まずは Aspose.HTML の依存関係を追加します。Maven を使用している場合は、`pom.xml` に以下を追加してください。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Gradle を使用する場合は、同等の記述は次の通りです。

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

ライブラリがクラスパスに追加されたら、コーディングを開始できます。

---

## 手順 2: サンドボックス環境で **外部画像を無効化**

解決策の核心は `DocumentSandbox` にあります。`allowExternalImages` フラグに `false` を渡すことで、サンドボックス外の URL を指す `<img>` タグをすべて無視するよう Aspose.HTML に指示します。これが **外部画像を無効化** する正確なメカニズムです。

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox that blocks external scripts and images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport size (width x height)
                96,                     // DPI – 96 is the screen default
                "MyApp/1.0",            // custom user‑agent string
                false,                  // allowExternalScripts = false
                false);                 // allowExternalImages = false  <-- disables external images
```

> **なぜ重要か:** サンドボックスを使用しない場合、レンダラはページが参照するすべての画像をダウンロードしようとします。これにより処理が遅くなったり、信頼性が低下したり、セキュリティリスクが生じる可能性があります。フラグを `false` に設定することで、クリーンで自己完結型のレンダリングが保証されます。

---

## 手順 3: **サンドボックスでウェブページを読み込む**  

次に、Aspose.HTML に取得したい URL を渡します。`HTMLDocument` コンストラクタはサンドボックスインスタンスを受け取り、先ほど定義した制限を自動的に適用します。

```java
        // 2️⃣ Load the target page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // replace with your target URL
                sandbox);
```

ページがレイアウトに外部スクリプトに大きく依存している場合、スクリプトも無効化しているためコンテンツが欠落することがあります。その場合は `allowExternalScripts` フラグを `true` に切り替え、`allowExternalImages` は引き続き `false` のままにしてください。

---

## 手順 4: **ウェブページを PNG にレンダリング**  

ドキュメントが読み込まれたら、`Converter.convert` を使ったワンライナーで画像に変換できます。`ImageSaveOptions` オブジェクトで出力形式を指定し、ここでは PNG を選択しています。

```java
        // 3️⃣ Render the document to a PNG image.
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png"; // ensure the folder exists

        Converter.convert(htmlDoc, saveOptions, outputPath);
        System.out.println("Image saved to: " + outputPath);
    }
}
```

生成されたファイル `sandboxed.png` には、**外部画像が一切含まれない** ページのスナップショットが保存されます。インライン SVG や base64 エンコードされた画像があればそれらは残ります。

---

## 手順 5: 出力を確認し、一般的な問題をデバッグ

プログラム実行後、任意の画像ビューアで `sandboxed.png` を開きます。ページのレイアウト、テキスト、CSS スタイルは表示されますが、`<img src="http://…">` 要素は空白（白い矩形になるか、完全に省略される）になっているはずです。

### 典型的な障害と対処法

| 症状 | 考えられる原因 | 対策 |
|---|---|---|
| ページが真っ白になる | ターゲット URL がリクエストをブロック（例: Cloudflare） | サンドボックスのユーザーエージェントに適切なヘッダーを付与するか、プロキシを使用する |
| フォントが欠けている | フォントファイルが外部にホストされている | フォントをローカルにインストールするか、`@font-face` に data URI を埋め込む |
| レイアウトが崩れる | CSS が外部スタイルシートを参照してブロックされた | CSS 読み込みだけを許可するために `allowExternalScripts` を `true` に設定し、再実行 |
| `java.lang.OutOfMemoryError` が発生 | 高 DPI で非常に大きなページをレンダリングしている | ビューポートサイズや DPI を下げる、または JVM ヒープを増やす（`-Xmx2g` など） |

---

## 手順 6: サンプルを拡張 – 他形式で保存

同じコードで JPEG、BMP、さらには PDF も出力できます。`SaveFormat` 列挙型を変更するだけです。

```java
// Example: Save as JPEG with quality 80%
ImageSaveOptions jpegOptions = new ImageSaveOptions(SaveFormat.JPEG);
jpegOptions.setQuality(80);
Converter.convert(htmlDoc, jpegOptions, "output/sandboxed.jpg");
```

PDF が必要な場合は、`ImageSaveOptions` を `PdfSaveOptions` に置き換え、拡張子も適切に変更してください。

---

## 完全動作サンプル（コピペで実行可能）

以下は **完全な実行可能プログラム** です。新しい Java クラスを作成し、コードを貼り付け、`output` ディレクトリが存在することを確認してから実行してください。

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1 – Create a sandbox that disables external images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport width & height
                96,                     // DPI
                "MyApp/1.0",            // custom user‑agent
                false,                  // external scripts disabled
                false);                 // external images disabled (primary goal)

        // Step 2 – Load the page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // change to your URL
                sandbox);

        // Step 3 – Render to PNG.
        ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png";

        Converter.convert(htmlDoc, pngOptions, outputPath);
        System.out.println("PNG image saved to: " + outputPath);
    }
}
```

**期待されるコンソール出力**:

```
PNG image saved to: output/sandboxed.png
```

`sandboxed.png` を開くと、**外部画像が一切含まれない** ページがレンダリングされていることが確認できます。

---

## よくある質問

**Q: HTML に埋め込まれた画像は表示されますか？**  
A: はい。インラインの `data:` URI や base64 エンコード画像はドキュメントの一部として扱われ、PNG に描画されます。

**Q: 特定の外部画像だけは許可したい場合は？**  
A: サンドボックスはオンオフのスイッチです。細かい制御が必要な場合は、許可したい画像を自分でダウンロードし、data URI に変換して HTML に埋め込んでからレンダリングしてください。

**Q: ヘッドレスサーバーでも動作しますか？**  
A: 完全に動作します。Aspose.HTML は純粋な Java ライブラリで、ディスプレイサーバやブラウザエンジンは不要です。

**Q: Selenium や Puppeteer と比べて何が違うのですか？**  
A: Selenium は実際のブラウザを操作するため重量が大きく、サンドボックス化が難しいです。Aspose.HTML はメモリ上で直接 HTML をレンダリングするため、パフォーマンスが決定的で、**外部画像の無効化** などのセキュリティ制御も簡単に行えます。

---

## 結論

これで **Java でウェブページを PNG にレンダリングする際に外部画像を無効化する** 完全なレシピが手に入りました。`DocumentSandbox` を活用すれば、許可する外部リソースを厳密に管理でき、セキュリティと再現性の両方が確保できます。ここからはビューポートサイズや DPI、出力形式を自由に変えて、サムネイル作成、プレビュー生成、アーカイブスナップショットなど、さまざまな用途に応用できます。

次のチャレンジはどうですか？複数の URL を並列で処理したり、Spring Boot マイクロサービスに組み込んでオンデマンドで PNG を返す API を作ったり。Aspose.HTML の柔軟性と Java の並行処理ツールを組み合わせれば、可能性は無限です。

Happy coding, and don’t forget to share your success stories in the comments!

## 次に学ぶべきこと

- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [How to Render HTML to PNG with Aspose – Complete Guide](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)
- [How to Edit CSS - Advanced External CSS Editing with Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}