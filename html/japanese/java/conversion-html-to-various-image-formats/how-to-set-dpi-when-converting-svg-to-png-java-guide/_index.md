---
category: general
date: 2026-05-06
description: Aspose.HTML を使用した Java での高解像度 SVG から PNG への変換における DPI 設定方法。SVG を PNG
  に変換し、SVG を PNG としてエクスポートし、ベクターをラスタ画像に変換する方法を学びます。
draft: false
keywords:
- how to set dpi
- convert svg to png
- how to convert svg
- export svg as png
- convert vector to raster
language: ja
og_description: Aspose.HTML を使用した Java での高解像度 SVG から PNG への変換における DPI 設定方法。ステップバイステップのコードと専門家のヒントを入手。
og_title: SVG を PNG に変換する際の DPI 設定方法 – Java ガイド
tags:
- Java
- Aspose.HTML
- Image Conversion
title: SVG を PNG に変換する際の DPI 設定方法 – Java ガイド
url: /ja/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SVG を PNG に変換する際の DPI 設定方法 – Java ガイド

SVG から PNG への変換で **DPI を設定** し、鮮明で印刷可能な画像を得たいと思ったことはありませんか？ あなたは一人ではありません。多くの開発者が、デフォルトの DPI（通常は 96）がプロフェッショナルな出力には十分でないため、エクスポートした PNG がぼやけてしまう壁にぶつかります。

このチュートリアルでは、Aspose.HTML for Java を使用して **DPI を設定** する完全な実行可能サンプルを順を追って解説します。最後まで読めば、**SVG を PNG に変換**、**SVG を PNG としてエクスポート**、さらには **ベクターをラスタに変換** できるようになります—謎はなく、コードは明快です。

## 学べること

- 変換前に DPI を設定する正確な手順
- **ベクターをラスタに変換** する際に DPI が重要な理由
- ワンラインで **SVG を PNG に変換** する方法
- 大きな SVG の取り扱いとバッチ処理のコツ
- 今すぐプロジェクトに組み込める、コンパイル可能な完全プログラム

## 前提条件

始める前に以下を用意してください。

- Java 17 以上（最新の LTS バージョンがベスト）
- Aspose.HTML ライブラリを取得できる Maven または Gradle
- ラスタライズしたいシンプルな SVG ファイル（例: `logo.svg`）
- IDE またはテキストエディタ – IntelliJ IDEA、VS Code、あるいは古典的なメモ帳でも可

他の外部ツールは不要です。ライブラリがすべての重い処理を担います。

## 手順 1: Aspose.HTML をプロジェクトに追加

まずは Aspose.HTML の JAR が必要です。Maven を使う場合は `pom.xml` に次のスニペットを追加してください。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

Gradle の場合は以下のようになります。

```groovy
implementation 'com.aspose:aspose-html:23.10'
```

> **プロのコツ:** 常に最新の安定版を使用しましょう。新しいリリースには高 DPI レンダリング向けのパフォーマンス改善が含まれています。

## 手順 2: 変換時に DPI を設定する方法

ここが本題です—**DPI の設定方法**。Aspose.HTML は `ImageConversionOptions` を公開しており、水平（`dpiX`）と垂直（`dpiY`）の解像度を指定できます。両方を `300` に設定すれば、印刷品質の密度が得られます。

```java
import com.aspose.html.converters.ImageConversionOptions;
import com.aspose.html.rendering.Converter;

public class SvgHighRes {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create conversion options
        ImageConversionOptions conversionOptions = new ImageConversionOptions();

        // 2️⃣ Set target DPI for high‑resolution output (300 dpi → crisp print quality)
        conversionOptions.setDpiX(300);
        conversionOptions.setDpiY(300);

        // 3️⃣ Convert the SVG file to a PNG using the configured options
        Converter.convertSvgToPng(
                "YOUR_DIRECTORY/logo.svg",        // source SVG
                "YOUR_DIRECTORY/logo_300dpi.png", // destination PNG
                conversionOptions);
    }
}
```

> **なぜ 300 dpi か？** これはプロフェッショナル印刷の事実上の標準です。ウェブ用画像であれば 72 dpi で十分ですが、チラシやパンフレットでは最低でも 300 dpi が求められます。

### 画像プレビュー

![SVG を PNG に変換する際の DPI 設定方法](https://example.com/placeholder.png "SVG を PNG に変換する際の DPI 設定方法")

*上の画像は、低 DPI PNG（左）と 300 dpi 出力（右）の違いを示しています。*

## 手順 3: SVG を PNG に変換 – ワンライナー

DPI を気にせずに **SVG を PNG に変換** したいだけなら、オプションオブジェクトを省略できます。

```java
Converter.convertSvgToPng("logo.svg", "logo_default.png", null);
```

`null` を渡すと Aspose.HTML はデフォルト DPI（通常は 96）を使用します。サムネイル作成や印刷品質が不要な場合に便利です。

## 手順 4: 結果を確認 – SVG を PNG としてエクスポート

変換が完了したら、生成された PNG を任意の画像ビューアで開きます。元のベクターと同じ寸法のラスタ画像が表示され、設定した DPI が反映されているはずです。Windows なら右クリック → プロパティ → 詳細で DPI を確認できます。

プログラムから DPI を検証したい場合は、Java の `ImageIO` で読み取れます。

```java
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;

BufferedImage img = ImageIO.read(new File("logo_300dpi.png"));
int dpi = (int) img.getProperty("dpi");
System.out.println("Exported PNG DPI: " + dpi);
```

> **注意:** すべての画像形式が DPI メタデータを保持しているわけではありません。PNG は保持しますが、JPEG は追加の処理が必要になることがあります。

## 境界ケースとバリエーション

### 1️⃣ 異なる DPI 値

「大判ポスター用に 600 dpi が必要だ」と思ったら、数値を変えるだけです。

```java
conversionOptions.setDpiX(600);
conversionOptions.setDpiY(600);
```

DPI が高くなるほどファイルサイズが大きくなるので、多数のファイルを処理する際はメモリ使用量に注意してください。

### 2️⃣ フォルダ単位でバッチ変換

数十個の SVG がある場合は、変換処理をシンプルなループで包みます。

```java
File dir = new File("YOUR_DIRECTORY");
for (File svg : dir.listFiles((d, name) -> name.endsWith(".svg"))) {
    String pngName = svg.getName().replace(".svg", "_300dpi.png");
    Converter.convertSvgToPng(svg.getAbsolutePath(),
                              new File(dir, pngName).getAbsolutePath(),
                              conversionOptions);
}
```

このパターンは **ベクターをラスタに変換** を一括で行い、手作業の時間を大幅に削減します。

### 3️⃣ 透明背景の扱い

SVG に透明が含まれ、白背景にしたい場合は、まず `BufferedImage` にレンダリングし、背景を塗りつぶします。

```java
// Render SVG to BufferedImage with DPI
BufferedImage raster = Converter.convertSvgToImage(
        "logo.svg", conversionOptions);

// Fill background (optional)
Graphics2D g = raster.createGraphics();
g.setComposite(AlphaComposite.SrcOver);
g.setColor(Color.WHITE);
g.fillRect(0, 0, raster.getWidth(), raster.getHeight());
g.dispose();

// Write out PNG
ImageIO.write(raster, "png", new File("logo_whitebg.png"));
```

## よくある質問

**Q: Linux でも動作しますか？**  
A: はい。Aspose.HTML はプラットフォームに依存せず、適切な Java ランタイムさえあれば動作します。

**Q: SVG が外部画像を参照している場合は？**  
A: 絶対パスまたは URL でリソースにアクセスできるようにしてください。そうしないとレンダラが画像をスキップします。

**Q: JPEG や BMP など他のラスタ形式に変換できますか？**  
A: できます。`Converter.convertSvgToJpeg` や `Converter.convertSvgToBmp` を同じ `ImageConversionOptions` と共に使用してください。

## 高品質ラスタライズのプロ Tips

- **最終出力サイズに DPI を合わせる。** 例: 2 インチのロゴを 300 dpi で印刷する場合、幅は 600 px（2 in × 300 dpi）必要です。特定のピクセル寸法が必要なら、変換前に SVG をスケールしてください。
- **カラープロファイルに注意。** PNG はデフォルトで ICC プロファイルを埋め込みません。色再現性が重要なら TIFF に変換するか、プロファイル埋め込みに対応したライブラリを使用しましょう。
- **`ImageConversionOptions` オブジェクトを再利用** すると、複数ファイルの変換時に余計なオブジェクト生成を防ぎ、パフォーマンスが向上します。

## 結論

これで Java における SVG‑to‑PNG 変換時の **DPI 設定方法** が分かり、**svg を png に変換**、**svg を png としてエクスポート**、さらに **ベクターをラスタに変換** する際に解像度を完全にコントロールできるようになりました。上記の完全例はそのまま実行可能で、追加のヒントは実務プロジェクトへのスケールアウト手順を示しています。

次は何をしますか？ 300 dpi を 600 dpi に変えてみる、バッチ処理を試す、あるいは他のラスタ形式を探索する。原則は同じです—出力方法を変えるだけで OK です。

難しい SVG やパフォーマンスに関する質問があればコメントで教えてください。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}