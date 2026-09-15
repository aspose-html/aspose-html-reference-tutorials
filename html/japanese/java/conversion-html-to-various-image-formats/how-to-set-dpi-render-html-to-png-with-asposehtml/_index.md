---
category: general
date: 2026-01-14
description: URL を PNG に変換するときに DPI を設定する方法。Aspose.HTML を使用して Java で HTML を PNG にレンダリングし、ビューポートサイズを設定し、HTML
  を PNG として保存する方法を学びます。
draft: false
keywords:
- how to set dpi
- render html to png
- convert url to png
- set viewport size
- save html as png
language: ja
og_description: URL を PNG に変換するときに DPI を設定する方法。HTML を PNG にレンダリングし、ビューポートサイズを制御し、Aspose.HTML
  を使用して HTML を PNG として保存するステップバイステップガイド。
og_title: DPIの設定方法 – AsposeHTMLでHTMLをPNGにレンダリング
tags:
- AsposeHTML
- Java
- image rendering
title: dpi の設定方法 – AsposeHTML で HTML を PNG にレンダリング
url: /ja/java/conversion-html-to-various-image-formats/how-to-set-dpi-render-html-to-png-with-asposehtml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# DPI の設定方法 – Aspose.HTML を使用した HTML の PNG へのレンダリング

Web ページから生成されたスクリーンショットのような画像の **DPI の設定方法** を考えたことはありますか？印刷用に 300 DPI の PNG が必要な場合や、モバイルアプリ用の低解像度サムネイルが必要な場合があります。どちらの場合でも、レンダリングエンジンに論理 DPI を指定し、残りの処理を任せるのがコツです。

このチュートリアルでは、実際の URL を取得し、PNG ファイルにレンダリングし、**ビューポートサイズを設定**し、DPI を調整し、最後に **HTML を PNG として保存** します—すべて Aspose.HTML for Java を使用します。外部ブラウザや面倒なコマンドラインツールは不要で、Maven や Gradle プロジェクトにそのまま組み込めるシンプルな Java コードだけです。

> **プロのコツ:** 手軽なサムネイルだけが必要な場合は、DPI を 96 DPI（ほとんどの画面のデフォルト）に保って構いません。印刷用のアセットの場合は、300 DPI 以上に上げてください。

![DPI 設定例](https://example.com/images/how-to-set-dpi.png "DPI 設定例")

## 必要なもの

- **Java 17**（または最近の JDK）。  
- **Aspose.HTML for Java** 24.10 以上。Maven Central から取得できます:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.10</version>
</dependency>
```

- ターゲットページを取得するためのインターネット接続（例では `https://example.com/sample.html` を使用）。  
- 出力フォルダーへの書き込み権限。

以上です—Selenium もヘッドレス Chrome も不要。Aspose.HTML はプロセス内でレンダリングを行うため、JVM 内に留まり、ブラウザ起動のオーバーヘッドを回避できます。

## ステップ 1 – URL から HTML ドキュメントをロード

まず、取得したいページを指す `HTMLDocument` インスタンスを作成します。コンストラクタは自動的に HTML をダウンロードし、解析し、DOM を準備します。

```java
import com.aspose.html.HTMLDocument;
import java.nio.file.Paths;

// Load the remote page
HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");
```

*この重要性:* ドキュメントを直接ロードすることで、別途 HTTP クライアントを使用する必要がなくなります。Aspose.HTML はリダイレクト、クッキー、URL に埋め込んだ基本認証もサポートします。

## ステップ 2 – 任意の DPI とビューポートでサンドボックスを構築

**サンドボックス** は Aspose.HTML がブラウザ環境を模倣する仕組みです。ここでは、1280 × 720 の画面として振る舞うよう指示し、重要な **デバイス DPI** を設定します。DPI を変更すると、論理サイズは変わらずにレンダリング画像のピクセル密度が変わります。

```java
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;

// Create a sandbox that simulates a 1280×720 screen at 96 DPI
SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
        .setViewportSize(1280, 720)          // width, height in pixels
        .setDeviceDpi(96)                    // logical DPI (change to 300 for print)
        .setUserAgent("AsposeHTML/24.10")    // optional custom user‑agent
        .build();

// Apply the sandbox to the document
htmlDoc.setSandbox(sandbox);
```

*これらの値を調整する理由:*  
- **ビューポートサイズ** は CSS メディアクエリ（`@media (max-width: …)`）の挙動を制御します。  
- **デバイス DPI** は印刷時の画像の実際のサイズに影響します。96 DPI の画像は画面上で問題ありませんが、300 DPI の画像は紙上で鮮明さを保ちます。  

正方形のサムネイルが必要な場合は、`setViewportSize(500, 500)` に変更し、DPI は低めに保ちます。

## ステップ 3 – 出力形式として PNG を選択

Aspose.HTML は複数のラスタ形式（PNG、JPEG、BMP、GIF）をサポートしています。PNG はロスレスで、すべてのピクセルを保持したいスクリーンショットに最適です。

```java
import com.aspose.html.rendering.ImageSaveOptions;

// Prepare PNG save options
ImageSaveOptions pngOptions = new ImageSaveOptions();
pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);
```

ファイルサイズが気になる場合は、圧縮レベル（`pngOptions.setCompressionLevel(9)`）を調整することもできます。

## ステップ 4 – 画像をレンダリングして保存

ここで、ドキュメントに画像として **保存** させます。`save` メソッドはファイルパスと先ほど設定したオプションを受け取ります。

```java
// Define the output path (replace with your own directory)
String outputPath = "YOUR_DIRECTORY/sandboxed.png";

// Render the document to a PNG file
htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

System.out.println("Rendering completed.");
```

プログラムが終了すると、`YOUR_DIRECTORY/sandboxed.png` に PNG ファイルが生成されます。開いてみてください—DPI を 300 に設定していれば、ピクセルサイズは 1280 × 720 のままメタデータにその DPI が記録されています。

## ステップ 5 – DPI を確認する（任意だが便利）

DPI が正しく適用されたか二重チェックしたい場合は、軽量ライブラリ **metadata‑extractor** で PNG のメタデータを読み取れます。

```java
import com.drew.imaging.ImageMetadataReader;
import com.drew.metadata.png.PngDirectory;

File pngFile = new File(outputPath);
var metadata = ImageMetadataReader.readMetadata(pngFile);
var pngDir = metadata.getFirstDirectoryOfType(PngDirectory.class);
int dpi = pngDir.getInt(PngDirectory.TAG_PIXELS_PER_UNIT_X);
System.out.println("DPI stored in PNG: " + dpi);
```

コンソールに `300`（設定した値）が表示されるはずです。この手順はレンダリングに必須ではありませんが、特に印刷ワークフロー向けのアセットを生成する際の簡易的な確認として便利です。

## よくある質問とエッジケース

### 「ページが JavaScript でコンテンツをロードする場合は？」

Aspose.HTML は **限定的なサブセット** の JavaScript を実行します。ほとんどの静的サイトではそのまま機能します。ページがクライアント側フレームワーク（React、Angular、Vue）に大きく依存している場合は、ページを事前にレンダリングするか、ヘッドレスブラウザを使用する必要があります。ただし、DOM が準備できれば DPI の設定は同様に機能します。

### 「PNG の代わりに PDF をレンダリングできますか？」

もちろんです。`ImageSaveOptions` を `PdfSaveOptions` に置き換え、出力拡張子を `.pdf` に変更します。DPI 設定は埋め込まれた画像のラスタ化された外観にも影響します。

### 「Retina ディスプレイ向けの高解像度スクリーンショットはどうすれば？」

ビューポートのサイズを 2 倍にしつつ DPI を 96 DPI のままにするか、ビューポートはそのままで DPI を 192 に上げます。生成される PNG はピクセル数が 2 倍になり、Retina ディスプレイ向けの鮮明さが得られます。

### 「リソースのクリーンアップは必要ですか？」

`HTMLDocument` は `AutoCloseable` を実装しています。本番アプリでは、try‑with‑resources ブロックでラップしてください:

```java
try (HTMLDocument doc = new HTMLDocument(url)) {
    // configure sandbox, render, etc.
}
```

これにより、ネイティブリソースが速やかに解放されます。

## 完全動作サンプル（コピー＆ペースト可能）

以下に、完全な実行可能プログラムを示します。`YOUR_DIRECTORY` を実際のフォルダーに置き換えてください。

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.ImageSaveOptions;
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;
import java.nio.file.Paths;

public class RenderHtmlToPng {
    public static void main(String[] args) {
        // 1️⃣ Load the HTML document from a URL
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");

        // 2️⃣ Create a sandbox – set viewport size and DPI
        SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
                .setViewportSize(1280, 720)   // width × height in pixels
                .setDeviceDpi(96)             // change to 300 for print‑ready PNG
                .setUserAgent("AsposeHTML/24.10")
                .build();

        htmlDoc.setSandbox(sandbox); // apply sandbox to the document

        // 3️⃣ Prepare PNG save options
        ImageSaveOptions pngOptions = new ImageSaveOptions();
        pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);

        // 4️⃣ Render and save
        String outputPath = "YOUR_DIRECTORY/sandboxed.png";
        htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

        System.out.println("Rendering completed. Check: " + outputPath);
    }
}
```

クラスを実行すると、指定した **DPI の設定** を反映した PNG が生成されます。

## 結論

本稿では、**HTML を PNG にレンダリングする際の DPI の設定方法** を解説し、**ビューポートサイズの設定** 手順を取り上げ、Aspose.HTML for Java を使用した **HTML の PNG 保存** 方法を示しました。主なポイントは以下の通りです。

- **サンドボックス** を使用して DPI とビューポートを制御する。  
- ロスレス出力には適切な **ImageSaveOptions** を選択する。  
- 印刷品質を保証する必要がある場合は DPI メタデータを確認する。  

ここからは、さまざまな DPI 値や大きなビューポート、さらには URL のリストをバッチ処理することも試せます。ウェブサイト全体を PNG サムネイルに変換したい場合は、URL 配列をループし、同じサンドボックス設定を再利用すれば完了です。

レンダリングを楽しんで、スクリーンショットが常にピクセルパーフェクトでありますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}