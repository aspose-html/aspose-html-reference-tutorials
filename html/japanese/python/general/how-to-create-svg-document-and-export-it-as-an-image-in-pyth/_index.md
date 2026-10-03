---
category: general
date: 2026-10-02
description: PythonでSVGドキュメントを作成し、SVGをファイルに保存し、短くて完全なスクリプトでSVG画像をエクスポートする方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG to file
- how to generate SVG
- export SVG image
- SVG Python tutorial
language: ja
lastmod: 2026-10-02
og_description: PythonでSVGドキュメントを作成し、この実用的なチュートリアルでSVG画像をエクスポートします。スクリプトに従ってSVGをファイルに保存し、ベクターグラフィックをすぐに再利用できます。
og_image_alt: Screenshot of a Python script that creates an SVG document
og_title: PythonでSVGドキュメントを作成する – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Learn how to create SVG document in Python, save SVG to file, and export
    SVG image with a short, complete script.
  headline: How to create SVG document and export it as an image in Python
  type: TechArticle
tags:
- SVG
- Python
- graphics
title: PythonでSVGドキュメントを作成し、画像としてエクスポートする方法
url: /ja/python/general/how-to-create-svg-document-and-export-it-as-an-image-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでSVGドキュメントを作成し画像としてエクスポートする方法

プログラムで **SVGドキュメントを作成** したい場合、このチュートリアルで Python を使った具体的な手順を示します。シンプルな円を描画し、SVG をファイルに保存し、どこにでも埋め込めるエクスポート可能な SVG 画像を生成する完全なスクリプトをご覧いただけます。

コードからスケーラブルベクターグラフィックスを生成すれば、GUI エディタで手動で図形を描く手間が省けます。このガイドを終える頃には、SVG 作成をデータ可視化パイプラインや自動レポート生成ツール、あるいは高解像度でクリアなグラフィックが必要なあらゆるプロジェクトに組み込めるようになります。

## 前提条件

開始する前に、以下を確認してください。

- Python 3.8 以上がインストールされていること
- `svgwrite` ライブラリ（`pip install svgwrite` でインストール）
- SVG を保存するディレクトリへの書き込み権限

これらの要件により、サンプルは軽量でほとんどの環境に対応できます。

## 手順 1: SVG ライブラリをインストールしてインポートする

まず、SVG 作成用の便利な API を提供するサードパーティライブラリを追加します。

```python
# Install the library (run once in your terminal)
# pip install svgwrite

import svgwrite  # Provides the SVGDocument class and element helpers
```

`svgwrite` は SVG ファイルの XML 構造を抽象化し、マークアップの詳細ではなくジオメトリに集中できるようにします。

## 手順 2: SVG ドキュメントオブジェクトを作成する

`svgwrite.Drawing` をインスタンス化することで **SVGドキュメントを作成** できます。このオブジェクトはルート `<svg>` 要素を表し、以降のすべての形状を保持します。

```python
# Step 2: Initialize the SVG document
dwg = svgwrite.Drawing(
    filename="circle.svg",     # Desired output file name
    size=("100px", "100px"),   # Width and height of the canvas
    viewBox=("0 0 100 100")    # Coordinate system for drawing
)
```

`size` 引数はピクセル単位の描画サイズを定義し、`viewBox` は後で定義するジオメトリに合わせた座標系を設定します。

## 手順 3: 円要素を追加する

円は中心座標 (`cx`, `cy`) と半径 (`r`) で定義されます。`circle` ヘルパーを使ってこれらの属性を付与します。

```python
# Step 3: Create a <circle> element
circle = dwg.circle(
    center=("50", "50"),   # cx = 50, cy = 50
    r="40",                # radius = 40
    fill="lightcoral",     # Fill color for visual clarity
    stroke="black",        # Outline color
    stroke_width="2"
)

# Append the circle to the SVG root
dwg.add(circle)
```

円は 100 × 100 のキャンバスの中央に配置され、各辺に 10 ピクセルの余白が残ります。`fill` や `stroke` を調整してデザインに合わせましょう。

## 手順 4: SVG をファイルに保存する

グラフィックが完成したら、`save` メソッドを使って **SVGをファイルに保存** できます。これにより、ブラウザやベクターエディタが理解できる整形式の XML が書き出されます。

```python
# Step 4: Persist the SVG document
dwg.save()
print("SVG file saved as circle.svg")
```

`circle.svg` ファイルが現在の作業ディレクトリに作成されました。ウェブブラウザ、Inkscape、または SVG をサポートする任意のツールで開くことができます。

## 手順 5: エクスポートされた SVG 画像を確認する

保存したファイルをブラウザで開き、出力結果を確認してください。指定した色で中央に円が表示されるはずです。生の XML は次のようになります。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg width="100px" height="100px" viewBox="0 0 100 100"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40"
          fill="lightcoral" stroke="black" stroke-width="2"/>
</svg>
```

SVG はベクターベースなので、品質を損なうことなく画像を拡大縮小でき、レスポンシブウェブデザインや高解像度印刷に最適です。

## プロのコツ: SVG を PNG または JPEG にエクスポートする

ラスタ画像が必要な場合は、**CairoSVG** などの変換ツールと組み合わせます。

```python
# Optional: Convert SVG to PNG
# pip install cairosvg
import cairosvg

cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

この手順は **SVG画像をエクスポート** してビットマップ形式に変換する例で、下流システムが直接 SVG をレンダリングできない場合に便利です。

## よくあるバリエーションとエッジケース

| Variation | How to handle |
|-----------|---------------|
| Multiple shapes | `dwg.add()` を各新要素（rect、line、path）に対して呼び出す。 |
| Dynamic dimensions | `Drawing` 作成前にデータから `size` と `viewBox` を計算する。 |
| Text labels | `dwg.text("Label", insert=("10", "20"))` を使用し、`font_size` と `fill` でスタイル設定。 |
| Re‑using the document | `Drawing` オブジェクトをメモリ上に保持し、更新が必要なときに `save()` を呼び出す。 |
| Large files | `dwg.tostring()` で出力をストリームし、手動でファイルオブジェクトに書き込んでメモリスパイクを回避する。 |

これらのシナリオに対応すれば、**SVG生成方法** スクリプトはシンプルなアイコンから複雑な図までスケールします。

## 完全スクリプトのまとめ

以下に、すべての手順とオプションの変換を組み込んだ実行可能な完全例を示します。

```python
# Full SVG creation script – create SVG document, save SVG to file, export SVG image
import svgwrite
import cairosvg  # Optional, only needed for PNG conversion

# Initialize the drawing (SVG document)
dwg = svgwrite.Drawing(
    filename="circle.svg",
    size=("100px", "100px"),
    viewBox=("0 0 100 100")
)

# Define a circle element
circle = dwg.circle(
    center=("50", "50"),
    r="40",
    fill="lightcoral",
    stroke="black",
    stroke_width="2"
)

# Add the circle to the document
dwg.add(circle)

# Save the SVG file
dwg.save()
print("SVG file saved as circle.svg")

# Optional: convert SVG to PNG (export SVG image)
cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

このスクリプトを実行すると `circle.svg` が生成され、`cairosvg` がインストールされていれば `circle.png` も生成されます。どちらのファイルもウェブページ、レポート、あるいはさらなる処理にすぐに利用できます。

## 結論

Python で **SVGドキュメントを作成** し、**SVGをファイルに保存**、さらに **SVG画像をエクスポート** する方法が理解できたはずです。例は重要な API 呼び出しを網羅し、各ステップの意義を解説し、より高度なグラフィック向けの拡張方法も提示しています。

次は、パスの描画、グラデーションの適用、要素のアニメーションなど、追加の **SVG Python チュートリアル** トピックを探求してください。これらのテクニックを統合すれば、Python アプリケーションから動的でデータ駆動型のベクターグラフィックを直接生成できます。コーディングを楽しんでください！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法を基にした関連トピックをカバーしています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、API の追加機能を習得したり、独自プロジェクトで代替実装アプローチを試したりするのに役立ちます。

- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}