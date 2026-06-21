---
category: general
date: 2026-04-23
description: Aspose を使用した Java での超高品質 SVG から PNG への変換において DPI を設定する方法を学びましょう。ステップバイステップのコード、ヒント、エッジケースの処理を含みます。
draft: false
keywords:
- how to set dpi
- convert svg to png
- svg to png java
- how to convert svg
- aspose svg to png
language: ja
og_description: JavaでAspose HTMLを使用したSVGからPNGへの変換におけるDPI設定をマスターしよう。完全なコード、解説、ベストプラクティスのヒント付き。
og_title: SVG を PNG に変換する際の DPI 設定方法 – Java チュートリアル
tags:
- Aspose
- Java
- SVG
- PNG
- Image Conversion
title: Aspose を使用した SVG から PNG への変換時に DPI を設定する方法 – Java ガイド
url: /ja/java/advanced-usage/how-to-set-dpi-when-converting-svg-to-png-with-aspose-java-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose を使用して SVG を PNG に変換する際の DPI 設定方法 – Java ガイド

SVG から生成されたクリスタルクリアな PNG の **DPI を設定する方法** が気になったことはありませんか？ブランドパイプラインを構築していて、印刷用にロゴを 600 dpi にしたい場合や、高解像度ディスプレイでラスタ画像をシャープに見せたい場合などに役立ちます。良いニュースは、推測で行う必要はなく、Aspose HTML for Java が簡単に実現してくれることです。

このチュートリアルでは、Aspose ライブラリを使用して **SVG を PNG に変換** しながら **DPI を設定する方法** を順を追って解説します。実行可能なコードサンプル、各設定オプションの説明、実務で役立つヒントを多数掲載しています。外部参照は不要です—必要な情報はすべてここにあります。

## 前提条件

始める前に、以下が揃っていることを確認してください。

- Java 17（または最近の JDK）がインストール済み。
- 依存関係管理に Maven または Gradle が使用できる（Maven のスニペットを示します）。
- ラスタライズしたい SVG ファイル（例: `logo.svg`）。
- 基本的な Java 文法の理解—特別な知識は不要で、通常の `public static void main` が書ければ OK です。

これらが不足している場合は先に入手してください。以降のガイドはすでに環境が整っていることを前提としています。

## Maven 依存関係

`pom.xml` に Aspose HTML for Java の依存関係を追加します。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Gradle を使用する場合は、同等の `implementation "com.aspose:aspose-html:23.12"` 行に置き換えてください。

## 手順 1: 変換オプションオブジェクトの作成

最初に行うべきことは `SvgConversionOptions` のインスタンス化です。このオブジェクトは DPI、背景色、スケーリングなど、必要なすべての調整項目を保持します。

```java
// Step 1: Build conversion options for SVG → PNG
SvgConversionOptions conversionOptions = new SvgConversionOptions();
```

**ポイント:** DPI を明示的に設定しない場合、Aspose はデフォルトで 96 dpi を使用します。これはウェブ向きですが、印刷には遠く及びません。オプションオブジェクトを作成することで、ラスタライズプロセスを完全にコントロールできます。

## 手順 2: 目的の DPI を設定

ここが核心です: **DPI の設定方法**。`setDpi(int)` メソッドは整数を受け取ります。一般的な範囲は 72 dpi（低解像度）から 1200 dpi（超高解像度）です。多くの印刷物では 300 dpi が最適で、スケールが必要なロゴでは 600 dpi が安全な選択です。

```java
// Step 2: Define the resolution (DPI) – 600 DPI for ultra‑high‑quality output
conversionOptions.setDpi(600);
```

> **プロのコツ:** 72 の倍数でない DPI を指定すると、ピクセル寸法が整数でなくなることがあります。正確なピクセルサイズが必要な場合は、`pixel = inches * DPI` を事前に計算し、SVG の viewBox を調整してください。

## 手順 3: 背景色で透明性を処理

SVG には透明領域が含まれることが多いです。PNG は透明をサポートしますが、印刷ワークフローで不透明な背景が求められる場合は置き換える必要があります。`setBackgroundColor(String)` メソッドは CSS 互換のカラー文字列を受け取ります。

```java
// Step 3: Replace transparent areas with white (or any color you prefer)
conversionOptions.setBackgroundColor("white");
```

`#FFFFFF`、`rgb(255,255,255)`、あるいは透明度を保持したい場合は `transparent` も使用できます。

## 手順 4: 変換を実行

オプションが設定できたら、実際の変換は `Converter.convert` の静的呼び出し一つです。入力 SVG のパス、出力 PNG のパス、そしてオプションオブジェクトを渡します。

```java
// Step 4: Convert the SVG file to a PNG using the configured options
Converter.convert(
        "YOUR_DIRECTORY/logo.svg",   // Input SVG
        "YOUR_DIRECTORY/logo.png",   // Output PNG
        conversionOptions);          // Options we just set
```

これだけです—Aspose が SVG の解析、DPI スケーリング、背景塗りつぶし、PNG ファイルの書き出しをすべて行います。

## 完全な実行可能サンプル

以下は `SvgToPngHighRes.java` というファイル名でコピー＆ペーストできる完全な Java クラスです。`YOUR_DIRECTORY` を実際のフォルダパスに置き換えてください。

```java
import com.aspose.html.converters.SvgConversionOptions;
import com.aspose.html.converters.Converter;

/**
 * Demonstrates how to set DPI when converting an SVG file to a high‑resolution PNG
 * using Aspose.HTML for Java.
 *
 * Prerequisites:
 *   - Aspose.HTML for Java library (Maven dependency shown earlier)
 *   - Java 17+ runtime
 *
 * Expected result:
 *   - logo.png created at 600 DPI with a white background.
 */
public class SvgToPngHighRes {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create conversion options for SVG → PNG
        SvgConversionOptions conversionOptions = new SvgConversionOptions();

        // 2️⃣ Set the desired resolution (DPI) – 600 DPI yields ultra‑high‑quality output
        conversionOptions.setDpi(600);

        // 3️⃣ Define a background color to replace any transparency (white works for most prints)
        conversionOptions.setBackgroundColor("white");

        // 4️⃣ Convert the SVG file to a PNG using the configured options
        Converter.convert(
                "YOUR_DIRECTORY/logo.svg",   // <-- change this to your source file
                "YOUR_DIRECTORY/logo.png",   // <-- change this to your target file
                conversionOptions);

        System.out.println("Conversion complete! Check YOUR_DIRECTORY/logo.png");
    }
}
```

### 期待される出力

プログラムを実行すると、同じフォルダに `logo.png` が生成されます。画像ビューアで **画像プロパティ** を確認すると、次のようになっているはずです。

- **解像度:** 600 dpi（設定した値）
- **寸法:** 元の SVG の viewBox に DPI 倍率を掛けたサイズ
- **背景:** 透明ピクセルがない純白

Photoshop などのツールで PNG を開くと、*Image → Image Size* の下に DPI メタデータが表示されます。

## よくあるエッジケースと対処法

| 状況 | 注意点 | 推奨される対策 |
|-----------|-------------------|-----------------|
| **SVG ファイルが見つからない** | `Converter.convert` が `FileNotFoundException` をスロー | 変換前に `Files.exists(Paths.get(...))` でパスを検証 |
| **未対応の SVG 機能**（例: フィルタが未実装） | Aspose が機能を黙って除去する可能性あり | フィルタが必要な場合は `SvgConversionOptions.setEnableSvgFilters(true)` を使用（新しいバージョンで利用可） |
| **非常に高い DPI（≥1200）** | 出力ファイルが数百 MB になることがある | 結果をストリーミングするか、画像が大きすぎる場合は DPI を下げる |
| **透明性の保持** | 背景色を設定したが実際にはアルファが必要 | `setBackgroundColor` を省略するか、`"transparent"` を渡して元のアルファチャンネルを保持 |
| **バッチ変換** | 各ファイルごとに `SvgConversionOptions` を再生成すると無駄 | ループ内で同一インスタンスを再利用 |

## FAQ（よくある質問）

**Q: JPEG や BMP など他のラスタ形式でも同様に動作しますか？**  
A: はい。出力ファイルの拡張子を `.png` から `.jpg` または `.bmp` に変更すれば、Aspose が自動的に適切なエンコーダを選択します。JPEG の品質は `JpegConversionOptions` で細かく調整可能です。

**Q: ファイルではなくバイト配列から SVG を変換できますか？**  
A: もちろん可能です。`Converter.convert(InputStream, OutputStream, conversionOptions)` のオーバーロードを使用すれば、ストリームベースで処理でき、Web サービスに最適です。

**Q: DPI 設定は画像のスケーリングと同じですか？**  
A: DPI はプリンタが「1 インチあたり何ピクセルか」を示すメタデータです。内部的には Aspose が DPI に合わせてラスタ画像をスケーリングするため、DPI を尊重するビューアで 100 % 表示すると実際の物理サイズが変わります。

## 本番向けコードのプロ・ティップ

1. **オプションのキャッシュ** – 同一 DPI と背景色で多数のロゴを変換する場合、`SvgConversionOptions` を一度だけ生成して再利用するとオブジェクト生成コストが削減できます。
2. **入力サイズの検証** – 非常に大きな SVG では、期待ピクセルサイズ（`width * DPI/96`）を計算し、20 000 px 以上になる場合は中止して `OutOfMemoryError` を防止してください。
3. **変換メタデータのログ出力** – DPI、ソースファイル名、タイムスタンプをログに残すと、後々のデバッグが楽になります。
4. **スレッド安全性** – `Converter.convert` はスレッドセーフなので、`ExecutorService` を使ってバッチジョブを並列化できます。

## ビジュアルサマリー

![how to set dpi example](image.png){: .align-center alt="how to set dpi example"}

上図はフローを示しています: **SVG → DPI と背景設定 → PNG**。

## 結論

これで Aspose HTML for Java を使用して **SVG を PNG に変換** する際の **DPI 設定方法** が分かりました。`SvgConversionOptions` を設定すれば、解像度や背景処理などを自在にコントロールでき、数行のコードで印刷対応のラスタ画像に変換できます。

次のステップとして以下を試してみてください。

- フォルダ内の SVG を一括でバッチ変換するループを実装
- ウェブ向け資産として JPEG に出力形式を切り替える
- `setScaleX/Y` など他の Aspose 変換オプションを使い、DPI 以外のカスタムスケーリングを適用

コーディングを楽しんで、PNG が常に必要なだけ鮮明になるようにしましょう！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}