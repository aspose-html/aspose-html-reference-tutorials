---
category: general
date: 2026-02-14
description: Java を使用した SVG から PNG への変換で DPI を設定する方法。高解像度 PNG をエクスポートし、SVG を PNG に変換する方法と
  Java の画像変換ライブラリの使い方を学びましょう。
draft: false
keywords:
- how to set dpi
- convert svg to png
- export high resolution png
- how to convert svg
- java image conversion library
language: ja
og_description: Java を使用した SVG から PNG への変換で DPI を設定する方法。このガイドでは、高解像度 PNG のエクスポート方法と
  Java の画像変換ライブラリの使用方法を紹介します。
og_title: JavaでSVGをPNGに変換するときのDPI設定方法
tags:
- java
- image-conversion
- svg
- png
title: JavaでSVGをPNGに変換する際のDPI設定方法
url: /ja/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaでSVGをPNGに変換するときのDPI設定方法

印刷用ポスターで鮮明に見えるように **DPIの設定方法** を知りたくなったことはありませんか？ あなただけではありません。マーケティング用チラシ、UIモックアップ、技術図など、多くのプロジェクトで SVG から高解像度 PNG を取得することは必須です。  

このチュートリアルでは、**SVG を PNG に変換**し、**高解像度 PNG をエクスポート**し、最も重要なこととして Aspose.HTML for Java ライブラリを使って DPI を制御する手順を詳しく解説します。最後まで読めば、デスクトップツールでもバックエンドサービスでも使える再利用可能なスニペットが手に入ります。

## 必要なもの

- **Java 8+**（任意の最新 JDK でコンパイル可能）
- **Aspose.HTML for Java** JAR（Maven Central または Aspose のウェブサイトから入手可能）
- ラスタライズしたい SVG ファイル  
- 少しの好奇心—それだけです。

Maven に慣れている方は次のセクションの依存関係を追加してください。そうでない場合は JAR を手動でダウンロードし、クラスパスに追加します。

## 手順 1: Java 画像変換ライブラリを追加

まず最初に、**java image conversion library**、つまり SVG を読み込み PNG を書き出すことができるライブラリがプロジェクトに必要です。Aspose.HTML は CSS、フォント、複雑なベクタ機能を標準でサポートしているので堅実な選択肢です。

**Maven ユーザー**は `pom.xml` に以下を貼り付けてください：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- use the latest stable version -->
</dependency>
```

**Gradle ユーザー**は以下を追加してください：

```gradle
implementation 'com.aspose:aspose-html:23.12'
```

手動で行う場合は、Aspose のダウンロードページから JAR を取得し `libs/` に配置し、IDE のビルドパスに追加します。

> **プロのコツ:** バージョン番号に注意してください。新しいリリースは DPI 処理の改善やエッジケースのバグ修正が含まれることが多いです。

## 手順 2: 変換オプションを作成し目的の DPI を設定

ライブラリが導入できたら、出力 PNG の見た目を指示する必要があります。ここでキーワードである **DPIの設定方法** が登場します。`ImageConversionOptions` クラスを使うと、水平 (`dpiX`) と垂直 (`dpiY`) の解像度を細かく制御できます。

```java
import com.aspose.html.converters.ImageConversionOptions;

// Step 2: Build the options object and set DPI
ImageConversionOptions conversionOptions = new ImageConversionOptions();
conversionOptions.setDpiX(300); // 300 DPI horizontally
conversionOptions.setDpiY(300); // 300 DPI vertically
```

なぜ 300 DPI なのか？ 多くの印刷ワークフローでは 300 dots‑per‑inch が「印刷品質」と見なされています。Web 用の資産だけなら 72 または 96 DPI に下げてファイルサイズを小さくすることも可能です。

> **幅と高さで異なる DPI が必要な場合は？**  
> `setDpiX` と `setDpiY` を個別に変更すれば OK です。ライブラリは非均一な値をサポートしているので、アナモルフィック画像にも便利です。

## 手順 3: SVG‑to‑PNG 変換を実行

オプションが整ったら、実際の変換は静的メソッドの一呼び出しです。`java.nio.file.Paths` を使ってプラットフォーム非依存に保ちます。

```java
import com.aspose.html.converters.Converter;
import java.nio.file.Paths;

public class SvgToPng {
    public static void main(String[] args) throws Exception {
        // Paths to input SVG and output PNG
        var inputSvg  = Paths.get("YOUR_DIRECTORY/input.svg").toUri();
        var outputPng = Paths.get("YOUR_DIRECTORY/output.png").toUri();

        // Convert using the DPI settings we defined earlier
        Converter.convert(inputSvg, outputPng, conversionOptions);
    }
}
```

以上です。`main` メソッドを実行すれば、`YOUR_DIRECTORY` に 300 DPI の鮮明な PNG が生成されます。ライブラリは指定した DPI に合わせてベクタ画像を自動的にスケーリングし、アスペクト比とテキストの鮮明さを保持します。

## 手順 4: 結果を確認（任意だが推奨）

簡単なチェックを行うだけで後々のトラブルを防げます。DPI メタデータを表示できる画像ビューア（例: Photoshop、GIMP、または Windows Explorer の「詳細」タブ）で生成された PNG を開き、水平・垂直解像度が **300 DPI** と表示されていることを確認してください。

画像がぼやけている場合は、次を再確認してください：

1. 元の SVG が低解像度でないか（ベクタファイルは解像度に依存しませんが、埋め込みラスタ画像が品質を制限することがあります）。  
2. DPI を設定した後にファイルを正しく保存したか—IDE が古いビルドをキャッシュしていることがあります。  
3. 変換オプションがコードの別箇所で上書きされていないか。

## なぜ DPI が高解像度 PNG のエクスポートに重要なのか

「PNG はピクセルだけなのに、DPI を設定する意味は？」と思うかもしれません。実際、DPI は *メタデータ* タグで、下流のアプリケーション（特に印刷向け）に「1 インチあたり何ピクセルか」を伝えます。DPI メタデータが正しくない PNG を印刷機に渡すと、デフォルト（多くの場合 72 DPI）とみなされ、画像が拡大されてぼやけた出力になることがあります。

正しい DPI 設定はパフォーマンス面でも有利です。後からラスタ画像を拡大する必要がなくなるため、計算コストが削減され、品質劣化も防げます。

## エッジケースとよくある落とし穴

| 状況 | 注意点 | 対処法 |
|-----------|-------------------|------------|
| **SVG に埋め込みビットマップ画像が含まれる** | 埋め込みビットマップが低解像度だと、高 DPI に設定しても最終 PNG がピクセル化します。 | 高解像度版に差し替えるか、外部画像を参照するよう SVG を編集します。 |
| **非常に大きな DPI 値（例: 1200 DPI）** | メモリ消費が急増し、`OutOfMemoryError` が発生する可能性があります。 | JVM ヒープサイズを増やす（例: `-Xmx2g`）か、用途に合わせて DPI を適切な上限に抑えます。 |
| **非正方形ピクセル** | 一部のディスプレイは DPI を異なる方法で解釈し、画像が伸びて見えることがあります。 | 特別な理由がない限り `setDpiX` と `setDpiY` を同じ値にします。 |
| **フォントが欠落している** | SVG 内のテキストがデフォルトフォントにフォールバックし、レイアウトが変わります。 | フォントを SVG に埋め込むか、実行環境に必要なフォントをインストールします。 |

## ワンセンテンスでのまとめ

SVG‑to‑PNG 変換で **DPI の設定方法** は、`ImageConversionOptions` オブジェクトを作成し `dpiX`/`dpiY` を設定した上で、Aspose.HTML Java ライブラリの `Converter.convert` を呼び出すことです。

## 次のステップと関連トピック

- **バッチ処理:** ディレクトリ内の SVG をループし、同じ DPI 設定を適用。  
- **動的 DPI:** 設定ファイルやコマンドライン引数から実行時に DPI を取得。  
- **代替ライブラリ:** Aspose が使えない場合は **Batik**（Apache）や **SVG Salamander** を検討。ただし DPI 対応には追加コードが必要になることがあります。  
- **Android 用高解像度 PNG のエクスポート:** この手法と Android の `drawable‑hdpi`、`xhdpi` などのフォルダを組み合わせる。

ぜひ試してみてください—Web サムネイル用に 72 DPI、ラージフォーマット印刷用に 600 DPI、あるいは中間の 150 DPI など、用途に合わせて数値を変えるだけで同じコードが使えます。

---

![DPI設定方法](placeholder-image.png "Java変換ワークフローにおけるDPI設定のイラスト")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}