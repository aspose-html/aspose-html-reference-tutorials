---
category: general
date: 2026-11-27
description: Python を使用して SVG ドキュメントを作成し、SVG ファイルを保存します。ベクターを SVG としてエクスポートし、SVG 画像を素早く生成する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG file
- export vector as SVG
- save SVG image
- how to create SVG
language: ja
lastmod: 2026-11-27
og_description: PythonでSVGドキュメントを作成し、SVGファイルを保存します。このガイドでは、ベクターをSVGとしてエクスポートし、数分でSVG画像を作成する方法を示します。
og_image_alt: Screenshot of a red circle saved as an SVG document
og_title: Pythonを使用してSVGドキュメントを作成し、SVGファイルを保存する
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  headline: Create SVG document and save SVG file with Python
  type: TechArticle
- description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  name: Create SVG document and save SVG file with Python
  steps:
  - name: Expected output
    text: 'The resulting `circle.svg` contains:'
  - name: Exporting more complex vectors
    text: 'If you need to **export vector as SVG** for multi‑shape illustrations,
      simply repeat the `dwg.add()` pattern with other primitives (`rect`, `line`,
      `path`, etc.). For example:'
  - name: Handling Unicode and text
    text: "SVG supports text elements with full Unicode support. Use `dwg.text(\"Hello,
      \U0001F30D\", insert=(5, 95), fill=\"black\")` to embed multilingual labels."
  - name: Saving to a different location
    text: 'When **save SVG image** to a user‑specified folder, validate the path to
      avoid permission errors:'
  - name: Minifying the output
    text: 'For production pipelines, you might want a smaller file size. Pass `pretty=False`
      to `dwg.tostring()` and write the result manually:'
  type: HowTo
tags:
- SVG
- Python
- Vector graphics
title: PythonでSVGドキュメントを作成し、SVGファイルを保存する
url: /ja/python/general/create-svg-document-and-save-svg-file-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでSVGドキュメントを作成し、SVGファイルを保存する

スクラッチから**SVGドキュメントを作成**したい場合、このガイドが全工程を案内します。**SVGファイルを保存**する方法、ベクターをSVGとしてエクスポートする手順、数行のコードで使えるSVG画像を手に入れるまでを解説します。

プログラムでスケーラブルなグラフィックを生成することは、レポートや UI アイコン、解像度に依存しない画像が必要なあらゆるシーンで役立ちます。このチュートリアルの最後には、シンプルな形状に対して「**SVGの作り方**」に答えられるようになり、複雑なベクターアートワークへと応用できるようになります。

## 必要な環境

- Python 3.8 以上  
- `svgwrite` パッケージ（`pip` でインストール可能）  
- 出力ファイルを書き込めるディレクトリ  

外部のグラフィックエディタは不要です。すべてコマンドライン上で完結します。

## Step 1: `svgwrite` ライブラリをインストール

`svgwrite` は SVG マークアップを構築するためのクリーンで Pythonic な API を提供します。以下のコマンドで一度だけインストールしてください。

```bash
pip install svgwrite
```

> **Pro tip:** 依存関係を分離するために仮想環境（`python -m venv .venv`）を使用しましょう。

## Step 2: SVGドキュメントを作成

ここで実際に**SVGドキュメント**オブジェクトを作ります。`Drawing` クラスはルート `<svg>` 要素を表し、名前空間を自動で処理します。

```python
import pathlib
import svgwrite

# Define where the file will be saved
output_path = pathlib.Path("output/circle.svg")
output_path.parent.mkdir(parents=True, exist_ok=True)

# Initialize a new SVG document with a 100×100 viewport
dwg = svgwrite.Drawing(
    filename=str(output_path),
    size=("100px", "100px"),
    profile="tiny"  # tiny profile keeps the file lightweight
)
```

`Drawing` インスタンスが以降のすべての SVG 操作のエントリーポイントになります。`size` を指定することでキャンバスサイズを決め、ブラウザでの描画サイズに影響を与えます。

## Step 3: 赤い円要素を追加

形状の追加はとてもシンプルです。`circle` メソッドで `<circle>` 要素を作成し、ルートに追加します。

```python
# Create a red circle with radius 40 centered at (50, 50)
circle = dwg.circle(
    center=(50, 50),
    r=40,
    fill="red"
)

# Append the circle to the SVG root
dwg.add(circle)
```

円を選んだ理由: 円はベクタープリミティブで、品質を失うことなくスケーラビリティを示す代表例です。これにより **export vector as SVG** ワークフローのテストに最適です。

## Step 4: SVGファイルを保存

最後にマークアップをディスクに書き出します。このステップで **save SVG file** の要件を満たし、任意のブラウザやベクターエディタで開けるファイルが生成されます。

```python
# Persist the SVG document to the filesystem
dwg.save()
print(f"SVG saved to {output_path.resolve()}")
```

スクリプトを実行すると、生成されたファイルの場所を示すコンソールメッセージが表示されます。

### 期待される出力

生成された `circle.svg` の内容は以下の通りです。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg height="100px" version="1.1" width="100px" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" fill="red"/>
</svg>
```

ブラウザで開くと鮮明な赤い円が表示され、ベクター形式なのでピクセル化せずに無限にズームできます。

## Step 5: よくあるバリエーションとエッジケース

### より複雑なベクターのエクスポート

複数形状のイラスト向けに **export vector as SVG** が必要な場合は、`dwg.add()` パターンを他のプリミティブ（`rect`、`line`、`path` など）でも繰り返すだけです。例:

```python
dwg.add(dwg.rect(insert=(10, 10), size=(30, 30), fill="blue"))
dwg.add(dwg.line(start=(0, 0), end=(100, 100), stroke="black", stroke_width=2))
```

### Unicode とテキストの取り扱い

SVG はフル Unicode 対応のテキスト要素をサポートします。`dwg.text("Hello, 🌍", insert=(5, 95), fill="black")` のように記述すれば多言語ラベルを埋め込めます。

### 別の場所へ保存

**save SVG image** をユーザー指定のフォルダに保存する際は、パスの検証を行い権限エラーを防ぎます。

```python
if not output_path.parent.exists():
    raise PermissionError(f"Cannot write to {output_path.parent}")
dwg.save()
```

### 出力の縮小（ミニファイ）

本番パイプラインではファイルサイズを小さくしたいことがあります。`dwg.tostring()` に `pretty=False` を渡し、結果を手動で書き込むと圧縮できます。

```python
minified = dwg.tostring(pretty=False)
output_path.write_text(minified)
```

## 代替ライブラリでSVGを作成する方法（任意）

`svgwrite` は軽量で純粋な Python 実装ですが、他にも選択肢があります:

- **cairosvg** – PNG、PDF、HTML から SVG へ変換  
- **lxml** – XML API を使って手動で SVG マークアップを構築  

プロジェクトの規模や既存の依存関係に応じてライブラリを選択してください。

## 結論

これで **SVGドキュメントを作成**し、ベクター形状を追加し、Python で **SVGファイルを保存**する方法が分かりました。全体の流れは **export vector as SVG**、**SVG image** の生成、そしてプログラムで **how to create SVG** と問われたときの回答例を示しています。

ここからは次のように応用できます:

- ループを組み込んでチャートやアイコンを自動生成  
- SVG 出力を Web アプリやメールテンプレートに組み込む  
- `svgwrite` の `<animate>` 要素でアニメーションを追加  

さまざまな形状、色、グラデーションを試して、Python プロジェクトでスケーラブルベクターグラフィックスの力を最大限に活用してください。Happy coding!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを基にした関連トピックを扱っています。各リソースは完全なコード例とステップバイステップの解説を含み、API の追加機能習得や別実装アプローチの探求に役立ちます。

- [Create SVG Document – Add a Circle and Save as SVG](/html/english/python/general/create-svg-document-add-a-circle-and-save-as-svg/)
- [Create SVG Document in Python – Convert SVG to PNG Guide](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)
- [Load SVG File Python – Complete Guide to Export, Embed & Convert](/html/english/python/general/load-svg-file-python-complete-guide-to-export-embed-convert/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}