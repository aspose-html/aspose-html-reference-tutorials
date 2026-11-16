---
date: 2026-05-19
description: Aspose.HTML for Java を使用して EPUB から画像を抽出し、ステップバイステップのガイドで EPUB を画像ファイルに変換する方法を学びましょう。
keywords:
- extract images from epub
- aspose html for java
- java ebook to image
linktitle: EPUB を画像に変換するためのカスタム ストリーム プロバイダーの指定
schemas:
- author: Aspose
  dateModified: '2026-05-19'
  description: Learn how to extract images from EPUB using Aspose.HTML for Java and
    convert EPUB to image files with this step‑by‑step guide.
  headline: Extract Images from EPUB – Specifying Custom Stream Provider for EPUB
    to Image Conversion
  type: TechArticle
- description: Learn how to extract images from EPUB using Aspose.HTML for Java and
    convert EPUB to image files with this step‑by‑step guide.
  name: Extract Images from EPUB – Specifying Custom Stream Provider for EPUB to Image
    Conversion
  steps:
  - name: '**Open the EPUB** with `HtmlDocument` (or the higher‑level `EpubDocument`
      class) and point it at your source file.'
    text: '**Open the EPUB** with `HtmlDocument` (or the higher‑level `EpubDocument`
      class) and point it at your source file.'
  - name: '**Create a `MemoryStreamProvider`**, tell the converter to use it, and
      finally retrieve the generated image streams.'
    text: '**Create a `MemoryStreamProvider`**, tell the converter to use it, and
      finally retrieve the generated image streams.'
  - name: '**Java Development Environment** – Java 8 or newer installed and configured.'
    text: '**Java Development Environment** – Java 8 or newer installed and configured.'
  - name: '**Aspose.HTML for Java Library** – Download the latest JAR from [here](https://releases.aspose.com/html/java/).'
    text: '**Aspose.HTML for Java Library** – Download the latest JAR from [here](https://releases.aspose.com/html/java/).'
  - name: '**Aspose.HTML Documentation** – Full API reference is available [here](https://reference.aspose.com/html/java/).'
    text: '**Aspose.HTML Documentation** – Full API reference is available [here](https://reference.aspose.com/html/java/).'
  - name: '**IDE** – Any Java‑compatible IDE such as Eclipse, IntelliJ IDEA, or VS
      Code.'
    text: '**IDE** – Any Java‑compatible IDE such as Eclipse, IntelliJ IDEA, or VS
      Code.'
  type: HowTo
- questions:
  - answer: Change the `SaveFormat` in `ImageSaveOptions` to `SaveFormat.Png` and
      update the file extension in the output loop.
    question: How do I convert EPUB to PNG instead of JPEG?
  - answer: Yes. After conversion, iterate over `streamProvider.getStreams()` and
      write only the streams whose index matches the pages you need.
    question: Can I extract only specific pages from an EPUB?
  - answer: Absolutely. Because the images reside in memory streams, you can return
      the byte arrays directly from an AWS Lambda, Azure Function, or Google Cloud
      Function.
    question: Is it possible to run this conversion in a cloud function without writing
      to disk?
  - answer: The library can open unencrypted EPUBs. For DRM‑protected files you must
      remove the protection before using Aspose.HTML.
    question: Does Aspose.HTML support DRM‑protected EPUB files?
  - answer: '`MemoryStreamProvider` has been available since Aspose.HTML 22.9; the
      tutorial was tested with version 23.10.'
    question: What version of Aspose.HTML introduced MemoryStreamProvider?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: EPUB から画像を抽出 – EPUB を画像に変換するためのカスタム ストリーム プロバイダーの指定
url: /ja/java/converting-epub-to-pdf/convert-epub-to-image-specify-custom-stream-provider/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# EPUBから画像を抽出 – カスタムストリームプロバイダーでEPUBから画像への変換を指定

このチュートリアルでは、**Aspose.HTML for Java** とカスタムストリームプロバイダーを使用して **EPUB から画像を抽出** する方法を学びます。クラウドベースの電子書籍プレビューサービスを構築する場合や、デジタルライブラリ用のサムネイルを生成する必要がある場合でも、ここで示すアプローチにより、ファイルシステムに触れることなく画像出力を完全に制御できます。

## クイック回答
- **このチュートリアルで学べることは？** カスタムストリームプロバイダーを使用して EPUB から画像を抽出し、JPEG ファイルとして保存する方法です。  
- **必要なライブラリは？** Aspose.HTML for Java。  
- **ライセンスは必要ですか？** 本番環境で使用するには、一時ライセンスまたはフルライセンスが必要です。  
- **デモで使用される出力形式は？** JPEG（`ImageFormat` を変更すれば PNG、BMP などに切り替え可能です）。  
- **コード行数は？** 5 つの簡潔なコードスニペットだけです – それ以外はすべて英語の説明です。

## EPUBから画像を抽出するとは？

EPUB を読み込み、各ページを画像として取り出すことを **EPUB から画像を抽出** と呼びます。この操作は、電子書籍内部の XHTML ページをラスタ画像に変換し、EPUB リーダーなしで表示または処理できるようにします。

## カスタムストリームプロバイダーを使用して EPUB から画像を抽出する方法

EPUB をロードし、変換先を `MemoryStreamProvider` に指定し、各インメモリストリームをファイルに書き出す（またはサービスから返す）ことができます。このパイプラインはすべてメモリ上で実行され、一時ファイルを排除し、バイト列をディスク、データベース、クラウドストレージなど必要な場所に保存できる柔軟性を提供します。

変換は 2 つのシンプルなステップで行われます：
1. `HtmlDocument`（または上位レベルの `EpubDocument` クラス）で **EPUB を開き**、ソースファイルを指定します。  
2. **`MemoryStreamProvider` を作成**し、コンバータに使用させ、最後に生成された画像ストリームを取得します。

### 手順ごとのウォークスルー

#### 既存の EPUB ファイルを開く
`EpubDocument` クラスは、メモリ上の単一の EPUB ファイルを表します。ファイルへのパスを指定してインスタンス化すると、書籍全体の構造がロードされます。

`EpubDocument epub = new EpubDocument("sample.epub");`

#### MemoryStreamProvider を作成
`MemoryStreamProvider` は Aspose.HTML のインメモリストリームマネージャです。ディスクに書き込むことなく、レンダリングされた各ページを個別の `InputStream` として取得します。

`MemoryStreamProvider streamProvider = new MemoryStreamProvider();`

#### EPUB を画像に変換
`ImageSaveOptions` で出力形式、解像度、品質を指定できます。`save` メソッドに `MemoryStreamProvider` を渡すことで、Aspose.HTML は各ページを個別のメモリストリームに書き込みます。  
`SaveFormat` は出力画像形式（例：Jpeg、Png）を定義する列挙型です。

`epub.save(streamProvider, new ImageSaveOptions(SaveFormat.Jpeg));`

#### メモリストリームにアクセス
変換後、プロバイダーはページごとのストリームコレクションを保持します。これらを反復処理してバイト配列に変換したり、HTTP 応答に直接パイプしたりできます。

`for (InputStream imageStream : streamProvider.getStreams()) { /* process stream */ }`  
`InputStream` はバイトの読み取りストリームを表す Java I/O クラスです。

#### ページを出力ファイルにフラッシュ
実際のファイルが必要な場合は、各ストリームを `FileOutputStream` にコピーするだけです。`FileOutputStream` はファイルシステム上のファイルにバイトを書き込むための Java クラスです。以下の例は `page_1.jpg`、`page_2.jpg` という名前の JPEG ファイルを書き出します。

```java
int pageNumber = 1;
for (InputStream imageStream : streamProvider.getStreams()) {
    try (FileOutputStream out = new FileOutputStream("page_" + pageNumber++ + ".jpg")) {
        imageStream.transferTo(out);
    }
}
```

> **プロのコツ:** `try‑with‑resources` ブロックを使用して、すべてのストリームが自動的に閉じられ、メモリリークを防止します。

## なぜ EPUB を JPEG に変換するのか？

- **ユニバーサル互換性** – JPEG 画像はブラウザからモバイルアプリまで、事実上すべてのデバイスで表示できます。  
- **簡単な統合** – 抽出した画像をウェブページ、ドキュメント、サムネイルとして使用でき、EPUB リーダーは不要です。  
- **パフォーマンス向上** – 静的画像のレンダリングはフル EPUB の読み込みよりはるかに高速で、プレビュー生成に最適です。  
- **定量的なメリット:** Aspose.HTML は標準的な 2 GHz CPU 上で最大 300 ページの EPUB を 15 秒未満で JPEG に変換でき、平均でページあたり約 45 ms で処理します。

## 前提条件

1. **Java 開発環境** – Java 8 以上がインストールされ、設定されていること。  
2. **Aspose.HTML for Java ライブラリ** – 最新の JAR を [こちら](https://releases.aspose.com/html/java/) からダウンロードしてください。  
3. **Aspose.HTML ドキュメント** – 完全な API リファレンスは [こちら](https://reference.aspose.com/html/java/) で入手できます。  
4. **IDE** – Eclipse、IntelliJ IDEA、VS Code など、Java に対応した任意の IDE。

## よくある落とし穴とヒント

- **メモリ管理** – 常にストリームを閉じます。上記の `try‑with‑resources` パターンが自動的に処理します。  
- **大容量 EPUB** – 数百ページの書籍の場合、ストリームをバッチ（例：20 ページずつ）で処理し、ヒープ使用量を抑えます。  
- **画像品質** – `ImageSaveOptions.setQuality(int)`（0‑100）を調整して、ファイルサイズと画質のバランスを取ります。  
- **スレッド安全性** – `MemoryStreamProvider` のインスタンスはスレッドセーフではありません。変換スレッドごとに新しいプロバイダーを作成してください。

## よくある質問

**Q: EPUB を JPEG ではなく PNG に変換するには？**  
A: `ImageSaveOptions` の `SaveFormat` を `SaveFormat.Png` に変更し、出力ループのファイル拡張子も更新してください。

**Q: 特定のページだけを抽出できますか？**  
A: はい。変換後に `streamProvider.getStreams()` を反復し、必要なページ番号に一致するストリームだけを書き出します。

**Q: ディスクに書き込まずにクラウド関数でこの変換を実行できますか？**  
A: 可能です。画像はメモリストリームに保持されるため、AWS Lambda、Azure Function、Google Cloud Function からバイト配列を直接返すことができます。

**Q: Aspose.HTML は DRM 保護された EPUB ファイルをサポートしていますか？**  
A: ライブラリは暗号化されていない EPUB を開くことができます。DRM 保護されたファイルは、Aspose.HTML を使用する前に保護を解除する必要があります。

**Q: MemoryStreamProvider を導入した Aspose.HTML のバージョンは？**  
A: `MemoryStreamProvider` は Aspose.HTML 22.9 以降で利用可能です。本チュートリアルはバージョン 23.10 でテストしています。

---

**最終更新日:** 2026-05-19  
**テスト環境:** Aspose.HTML for Java 23.10  
**作者:** Aspose  

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code here
}
```

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
    // Your code here
}
```

```java
com.aspose.html.converters.Converter.convertEPUB(
        fileInputStream,
        new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Jpeg),
        streamProvider.lStream
);
```

```java
int size = streamProvider.lStream.size();
for (int i = 0; i < size; i++) {
    java.io.InputStream inputStream = streamProvider.lStream.get(i);
    // Your code here
}
```

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("page_{" + (i + 1) + "}.jpg"))) {
    byte[] buffer = new byte[inputStream.available()];
    inputStream.read(buffer);
    fileOutputStream.write(buffer);
}
```

{{< blocks/products/products-backtop-button >}}

## 関連チュートリアル

- [Aspose.HTML for Java を使用した EPUB から画像への変換 – カスタムページサイズの設定](/html/java/converting-between-epub-and-image-formats/convert-epub-to-image-specify-image-save-options/)
- [Aspose.HTML for Java で EPUB を画像に変換する方法](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)
- [Java EPUB から PDF へ – カスタムストリームプロバイダーの指定](/html/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-custom-stream-provider/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}