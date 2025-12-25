---
date: 2025-12-25
description: Aspose.HTML for Java を使用して EPUB ファイルを画像に変換し、カスタムページサイズを設定する方法を学びます。このステップバイステップガイドでは、前提条件、パッケージのインポート、および変換プロセスについて説明します。
linktitle: Specifying Image Save Options for EPUB to Image Conversion
second_title: Java HTML Processing with Aspose.HTML
title: Aspose.HTML for Java を使用して EPUB を画像に変換 – カスタムページサイズの設定
url: /ja/java/converting-between-epub-and-image-formats/convert-epub-to-image-specify-image-save-options/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML for Java を使用して EPUB を画像に変換 – カスタムページサイズの設定

## クイック回答
- **「set custom page size」とは何ですか？** 各出力画像ページの幅と高さを定義できます。  
- **画像の背景色を変更できますか？** はい、`ImageSaveOptions` を使用して任意の色を指定できます。  
- **サポートされているフォーマットは何ですか？** `ImageFormat` を介して JPEG、PNG、GIF などが利用可能です。  
- **ライセンスは必要ですか？** テストには無料トライアルが使用できますが、本番環境では商用ライセンスが必要です。  
- **必要な Java バージョンは何ですか？** Java 1.7 以降が完全にサポートされています。

## EPUB から画像への変換で「set custom page size」とは何ですか？
カスタムページサイズを設定するということは、レンダリングされた画像の寸法（例：3000 × 1000 ピクセル）を制御することを意味します。これは、電子書籍の高解像度スクリーンショットが必要な場合や、出力を特定のレイアウトに合わせたい場合に便利です。

## なぜカスタムページサイズを設定し、画像の背景色を変更するのですか？
カスタムページサイズは、モバイル画面、印刷用 PDF、ウェブサムネイルなど、さまざまな表示対象に対する柔軟性を提供します。色を変更することで、ブランドに合わせたり、透明要素を含む画像の可読性を向上させたりできます。

## 前提条件

**EPUB を画像に変換**する前に、以下が揃っていることを確認してください。

1. **Java 環境** – マシンにインストールされた Java 開発キットです。まだ Java がない場合は、[here](https://www.java.com) からダウンロードできます。

2. **Aspose.HTML for Java** – Aspose.HTML for Java ライブラリです。最新リリースは [Aspose.HTML for Java page](https://releases.aspose.com/html/java/) から取得してください。

## パッケージのインポート

Aspose.HTML for Java を使用するには、必要な名前空間をインポートします。

```java
// Import the required Aspose.HTML for Java packages
import com.aspose.html.saving.ImageSaveOptions;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.drawing.Page;
import com.aspose.html.drawing.Size;
import com.aspose.html.drawing.Length;
import com.aspose.html.drawing.Color;
import com.aspose.html.converters.Converter;
import java.io.FileInputStream;
```

## ステップバイステップ ガイド

### ステップ 1: 既存の EPUB ファイルを読み取り用に開く

ここでソースの EPUB を開きます。`"input.epub"` を電子書籍ファイルへのパスに置き換えてください。

```java
try (FileInputStream fileInputStream = new FileInputStream("input.epub")) {
```

### ステップ 2: カスタム設定で ImageSaveOptions を初期化（カスタムページサイズの設定と画像背景色の変更）

このブロックでは、**カスタムページサイズ**を 3000 × 1000 ピクセルに設定し、背景色を AliceBlue に変更しています。プロジェクトに合わせて `size` や `Color` を自由に調整してください（例: 白い背景の場合は `Color.getWhite()`）。

```java
ImageSaveOptions options = new ImageSaveOptions(ImageFormat.Jpeg);
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
Size size = new Size(
    Length.fromPixels(3000),
    Length.fromPixels(1000)
);
anyPage.setSize(size);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

### ステップ 3: EPUB を画像に変換

この行が実際の変換を実行します。出力ファイル（`"output.jpg"`）には、指定した寸法と背景色でレンダリングされた画像が含まれます。**java convert epub png** が必要な場合は、拡張子を `.png` に変更することもできます。

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    "output.jpg"
);
```

### ステップ 4: リソースのクローズ（自動的に処理）

`try‑with‑resources` 文は `FileInputStream` を自動的にクローズし、ファイルハンドルが開いたままになることを防ぎます。

## 一般的な使用例

- **電子書籍ライブラリ用のサムネイル生成**。  
- **ドキュメントやマーケティング用の高解像度スクリーンショット作成**。  
- **大量の EPUB を PNG/JPEG アセットにバッチ処理し、ウェブギャラリー用に変換**。

## ヒントとベストプラクティス

- **プロのコツ:** ピクセルではなく実寸単位を使用したい場合は `Length.fromInches()` または `Length.fromCentimeters()` を使用してください。  
- **パフォーマンスのコツ:** 大きな EPUB の場合、メモリ不足を防ぐために JVM ヒープサイズ（`-Xmx2g`）を増やすことを検討してください。  
- **エラーハンドリング:** 変換呼び出しを `try‑catch` ブロックでラップし、`IOException` や `AsposeException` を捕捉してください。

## よくある質問

**Q: EPUB ファイルを他の画像フォーマットに変換できますか？**  
A: はい、`ImageFormat.Jpeg` を `ImageFormat.Png` や `ImageFormat.Gif` に変更することで、PNG や GIF などのフォーマットを指定できます。

**Q: Aspose.HTML for Java は EPUB3 をサポートしていますか？**  
A: もちろんです。ライブラリは EPUB3 を完全にサポートしており、最新の電子書籍規格で作業できます。

**Q: 変換プロセス中のエラーはどのように処理できますか？**  
A: 変換コードを `try‑catch` ブロックで囲み、例外を捕捉してログに記録することで、アプリケーションの堅牢性を保てます。

**Q: 画像のサイズや品質をカスタマイズできますか？**  
A: はい、`Size` オブジェクトで寸法を調整し、`options.setQuality(int)` で JPEG の圧縮品質を制御できます。

**Q: Aspose.HTML for Java はすべての Java バージョンと互換性がありますか？**  
A: ライブラリは Java 1.7 以降で動作し、幅広い開発環境をカバーしています。

---

**最終更新日:** 2025-12-25  
**テスト環境:** Aspose.HTML for Java 24.10  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}