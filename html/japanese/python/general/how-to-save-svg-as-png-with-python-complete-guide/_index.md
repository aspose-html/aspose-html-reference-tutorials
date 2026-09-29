---
category: general
date: 2026-09-29
description: PythonでSVGを保存し、SVGをPNGにエクスポートする方法。数分で細かく調整したオプションを使ってSVGをPNGに変換する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save svg
- convert svg to png
- save svg as png
- export svg to png
- vector svg to png
language: ja
lastmod: 2026-09-29
og_description: PythonでSVGを保存し、SVGをPNGにエクスポートする方法。このガイドに従って、オプションを完全に制御しながらSVGをPNGに変換しましょう。
og_image_alt: Screenshot of Python code converting a vector SVG file to a PNG image
og_title: PythonでSVGをPNGとして保存する方法 – ステップバイステップ
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: How to save SVG using Python and export SVG to PNG. Learn to convert
    SVG to PNG with fine‑tuned options in minutes.
  headline: How to save SVG as PNG with Python – complete guide
  type: TechArticle
- description: How to save SVG using Python and export SVG to PNG. Learn to convert
    SVG to PNG with fine‑tuned options in minutes.
  name: How to save SVG as PNG with Python – complete guide
  steps:
  - name: Load the SVG document
    text: '```python from aspose.svg import SVGDocument'
  - name: (Optional) Create image‑save options
    text: '```python from aspose.svg import ImageSaveOptions'
  - name: Save the SVG as PNG
    text: '```python # Export the SVG to a PNG file using the options defined above
      svg_doc.save("YOUR_DIRECTORY/vector.png", options) ```'
  - name: Full script
    text: 'Putting the pieces together yields a complete, runnable program:'
  - name: Missing file or invalid path
    text: 'If `src_path` does not exist, `SVGDocument` raises a `FileNotFoundError`.
      Wrap the call in a `try/except` block to provide a friendly error message:'
  - name: Preserving aspect ratio
    text: When only one dimension (width **or** height) is set, the library automatically
      scales the other dimension to maintain the original aspect ratio. If you set
      both dimensions, the image may stretch. Choose the approach that matches your
      UI requirements.
  - name: Transparent backgrounds
    text: 'If the original SVG relies on transparency (e.g., icons), you can keep
      the PNG transparent by omitting `background_color`:'
  type: HowTo
tags:
- Python
- SVG
- Image conversion
title: PythonでSVGをPNGに保存する完全ガイド
url: /ja/python/general/how-to-save-svg-as-png-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでSVGをPNGとして保存する方法 – 完全ガイド

ラスタ画像として **SVGを保存する方法** が必要な場合、このチュートリアルではすぐに実行できるソリューションを示します。ベクタSVGファイルの読み込み方法、必要に応じて画像保存設定を調整する方法、そしてたった3行のコードでPNGにエクスポートする方法を学びます。

SVGファイルをPNGとして保存することは、ウェブページにグラフィックを埋め込んだり、サムネイルを生成したり、機械学習パイプラインにラスタ画像を供給したりする際に一般的です。ここで紹介するアプローチは、Windows、macOS、Linux すべてで追加のネイティブ依存関係なしに動作します。

## 前提条件

開始する前に、以下がインストールされていることを確認してください。

* Python 3.9 以上がインストールされていること
* `aspose.svg` パッケージ（公式 Aspose SVG for Python via .NET）。以下でインストールします：

```bash
pip install aspose-svg
```

* ディスク上に有効な SVG ファイルがあること（例: `vector.svg`）

これらの要件により、サンプルは外部ツール（例: CairoSVG）に依存せず、自己完結型となります。

## PythonでSVGを保存する方法

このプロセスのコアは 3 つのステップです：読み込み、設定、保存。以下のセクションで各ステップを詳しく解説します。

### 手順 1: SVGドキュメントの読み込み

```python
from aspose.svg import SVGDocument

# Load the SVG file from the local filesystem
svg_doc = SVGDocument("YOUR_DIRECTORY/vector.svg")
```

`SVGDocument` は SVG の XML を解析し、メモリ内表現を構築します。ファイルを最初に読み込むことは必須で、これがないと保存操作にソースデータがありません。

### 手順 2: （オプション）画像保存オプションの作成

```python
from aspose.svg import ImageSaveOptions

# Create default options; you can tweak width, height, and background
options = ImageSaveOptions()
options.width = 800          # Desired output width in pixels
options.height = 600         # Desired output height in pixels
options.background_color = "#FFFFFF"  # Force a white background for transparent SVGs
```

`ImageSaveOptions` を使うと PNG の出力を細かく調整できます。幅と高さを個別に設定しない限り、アスペクト比は自動的に保持されます。元の SVG が透過を含んでいるが不透明な PNG が必要な場合は、背景色を設定すると便利です。

### 手順 3: SVGをPNGとして保存

```python
# Export the SVG to a PNG file using the options defined above
svg_doc.save("YOUR_DIRECTORY/vector.png", options)
```

`save` メソッドは PNG ファイルを指定したパスに書き込みます。`options` 引数を省略すると、ライブラリは SVG の viewBox から導出されたデフォルト寸法を使用します。

### 完全なスクリプト

各部品を組み合わせると、以下のような完全で実行可能なプログラムになります：

```python
# -*- coding: utf-8 -*-
"""
How to save SVG as PNG with Python.
This script loads an SVG file, applies optional image‑save settings,
and exports the result to PNG.
"""

from aspose.svg import SVGDocument, ImageSaveOptions

def convert_svg_to_png(
    src_path: str,
    dst_path: str,
    width: int = 800,
    height: int = 600,
    background: str = "#FFFFFF"
) -> None:
    """Convert an SVG file to PNG with custom dimensions and background."""
    # Load the SVG document
    svg_doc = SVGDocument(src_path)

    # Prepare save options
    options = ImageSaveOptions()
    options.width = width
    options.height = height
    options.background_color = background

    # Save as PNG
    svg_doc.save(dst_path, options)


if __name__ == "__main__":
    # Example usage
    convert_svg_to_png(
        src_path="YOUR_DIRECTORY/vector.svg",
        dst_path="YOUR_DIRECTORY/vector.png",
        width=1024,
        height=768,
        background="#FFFFFF"
    )
    print("SVG successfully saved as PNG.")
```

スクリプトを実行すると **“SVG successfully saved as PNG.”** と表示され、同じフォルダーに `vector.png` が作成されます。

## SVGをPNGに変換する – よくある落とし穴の対処

### ファイルが見つからない、またはパスが無効

`src_path` が存在しない場合、`SVGDocument` は `FileNotFoundError` をスローします。以下のように `try/except` ブロックでラップして、ユーザーフレンドリーなエラーメッセージを提供しましょう：

```python
try:
    svg_doc = SVGDocument(src_path)
except FileNotFoundError:
    raise SystemExit(f"File not found: {src_path}")
```

### アスペクト比の保持

幅 **または** 高さのいずれか一方だけを設定すると、ライブラリは自動的にもう一方の寸法をスケーリングして元のアスペクト比を維持します。両方の寸法を設定すると画像が伸びる可能性があります。UI の要件に合わせてアプローチを選択してください。

### 透明な背景

元の SVG が透過（例: アイコン）に依存している場合、`background_color` を省略することで PNG を透過のまま保持できます：

```python
options.background_color = None   # PNG will retain transparency
```

このバリエーションは、PNG を他のグラフィックの上に重ねて表示する場合に便利です。

## SVGをPNGにエクスポートする – パフォーマンスのヒント

* **`ImageSaveOptions` を再利用** すると、バッチで多数のファイルを変換する際にオーバーヘッドを削減できます。各ファイルごとに新しいオプションオブジェクトを作成してもほぼ無視できる負荷ですが、再利用することでメモリ割り当てを減らせます。
* **バッチ処理**: SVG ファイルが格納されたディレクトリをループし、各ファイルに対して `convert_svg_to_png` を呼び出します。ライブラリは各ファイルを独立して処理するため、`concurrent.futures.ThreadPoolExecutor` を使ってループを並列化すれば、マルチコアマシンでの変換速度を向上させられます。

```python
import os
from concurrent.futures import ThreadPoolExecutor

svg_folder = "YOUR_DIRECTORY"
png_folder = "YOUR_DIRECTORY/pngs"
os.makedirs(png_folder, exist_ok=True)

def batch_convert(file_name):
    src = os.path.join(svg_folder, file_name)
    dst = os.path.join(png_folder, file_name.replace('.svg', '.png'))
    convert_svg_to_png(src, dst)

with ThreadPoolExecutor(max_workers=8) as executor:
    executor.map(batch_convert, [f for f in os.listdir(svg_folder) if f.endswith('.svg')])
```

## SVGをPNGとして保存 – 検証

変換後は、プログラムから出力を検証できます：

```python
from PIL import Image

with Image.open("YOUR_DIRECTORY/vector.png") as img:
    print(f"PNG size: {img.size}, mode: {img.mode}")
```

典型的な出力例：

```
PNG size: (1024, 768), mode: RGBA
```

`mode` が `RGBA` であれば、画像にアルファチャンネル（透過）が含まれていることを示します。背景色を設定した場合は `RGB` になります。

## 結論

これで、Python を使って **SVGを保存する方法** として PNG に変換する方法、そしてカスタム寸法や背景処理を伴う **SVGをPNGにエクスポートする方法** が分かりました。完全なスクリプトは、ベクタ SVG ファイルの読み込みからラスタ PNG 画像の生成までの全ワークフローを示しています。

次は、バッチモードで **SVGをPNGとして保存** する方法や、代替ライブラリ **CairoSVG** の利用、SVG ソースからのマルチページ PDF 生成などの関連トピックを探求してください。さまざまな `ImageSaveOptions` 設定を試して、品質、DPI、圧縮を自分のユースケースに合わせて微調整しましょう。

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、完全に動作するコード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、プロジェクトで代替実装アプローチを検討したりするのに役立ちます。

- [svg to png java – Aspose.HTML for JavaでSVGを画像に変換](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Aspose.HTML を使用して .NET で SVG ドキュメントを PNG としてレンダリング](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)
- [JavaでSVGをPNGに変換する際の DPI 設定方法](/html/english/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-with-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}