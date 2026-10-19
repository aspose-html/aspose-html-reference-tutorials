---
category: general
date: 2026-06-19
description: PythonでSVGをPNGに素早く簡単に変換しましょう。SVGをPNGとして保存する方法、SVGからPNGへの変換処理、シンプルなスクリプトでSVGをPNGにエクスポートする方法を学びます。
draft: false
keywords:
- convert svg to png
- save svg as png
- svg to png conversion
- svg to png python
- export svg to png
language: ja
og_description: この実践的なチュートリアルで、Pythonを使ってSVGをPNGに変換しましょう。SVGからPNGへの変換プロセス全体と、効率的なエクスポート方法を学べます。
og_title: PythonでSVGをPNGに変換する完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Convert SVG to PNG in Python quickly and easily. Learn how to save
    SVG as PNG, handle svg to png conversion, and export SVG to PNG with a simple
    script.
  headline: Convert SVG to PNG in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Convert SVG to PNG in Python quickly and easily. Learn how to save
    SVG as PNG, handle svg to png conversion, and export SVG to PNG with a simple
    script.
  name: Convert SVG to PNG in Python – Complete Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - Basic familiarity with pip and
      virtual environments. - An SVG file you want to transform (we’ll use `logo.svg`
      as an example).'
  - name: Why This Approach Works
    text: '- **Explicit I/O handling:** By reading the SVG as bytes, we avoid issues
      with Unicode encodings that sometimes crop up on Windows. - **Custom DPI:**
      Scaling is often required when the target PNG must match a specific pixel density
      (think print vs. screen). - **Optional background:** Some SVGs have '
  - name: Expected Result
    text: '- `output/logo.png` – a 1:1 raster of the original SVG, preserving any
      transparency. - `output/logo_highres.png` – a 300 DPI version with a white background,
      perfect for print.'
  - name: 1. **What if the SVG uses external fonts?**
    text: '`cairosvg` tries to embed referenced fonts, but it only sees files on the
      local filesystem. Copy the font files next to the SVG or embed them directly
      in the SVG with `<style>` tags. Otherwise you’ll get fallback fonts in the PNG.'
  - name: 2. **How do I keep the original aspect ratio when scaling?**
    text: Pass only `dpi` and let Cairo compute the pixel dimensions from the SVG’s
      viewBox. If you need a fixed width/height, calculate the appropriate DPI yourself
      or use the `output_width`/`output_height` arguments provided by `svg2png`.
  - name: 3. **Can I convert large SVGs without exhausting memory?**
    text: Yes. `cairosvg` streams the rasterization, but you should avoid loading
      massive SVGs into memory all at once. Process them one by one, as shown in the
      batch example.
  - name: 4. **Is the conversion thread‑safe?**
    text: The underlying Cairo library is not fully thread‑safe on all platforms.
      If you plan to run conversions in parallel, wrap calls in a multiprocessing
      pool rather than threading.
  - name: What’s Next?
    text: '- Explore **svg to png conversion** with alternative libraries like `svglib`
      + `reportlab` for PDF‑first workflows. - Combine this script with image‑optimization
      tools (e.g., `pngquant`) to shrink file size for the web. - Add a CLI wrapper
      using `argparse` or `click` so you can run `python -m conver'
  type: HowTo
tags:
- Python
- Image Processing
- SVG
title: PythonでSVGをPNGに変換する – 完全ステップバイステップガイド
url: /ja/python/general/convert-svg-to-png-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでSVGをPNGに変換する – 完全ステップバイステップガイド

**SVGをPNGに変換**したいけど、どのライブラリを選べばいいか分からないことはありませんか？同じ悩みを抱える開発者は多く、ベクター画像をウェブ資産に埋め込んだり、サムネイルをリアルタイムで生成したりする際に壁にぶつかります。朗報です！数行のPythonコードで **SVGをPNGとして保存** でき、ビルドパイプラインもスムーズに保てます。

このチュートリアルでは、人気ライブラリを使った実用的な **svg to png conversion** の手順を追い、 **svg to png python** コードのポイントを解説し、適切なエラーハンドリングを備えた **export SVG to PNG** の方法を示します。最後まで読めば、CLIツールでもサーバーサイドの画像サービスでも使える再利用可能な関数が手に入ります。

## 学べること

- Pythonで **convert svg to png** に必要な最小限の依存関係  
- SVGファイルを読み込み、PNGエクスポートオプションを設定し、出力画像を書き出す方法  
- よくある落とし穴（透明背景や大きすぎるサイズ）と回避策  
- バッチ処理や Flask/Django エンドポイントへの組み込みにすぐ使えるスクリプト

### 前提条件

- Python 3.8+ がインストールされていること  
- pip と仮想環境の基本的な使い方が分かっていること  
- 変換したい SVG ファイル（例として `logo.svg` を使用）

これらが揃っていれば、さっそく始めましょう。

## Step 1: 必要なライブラリをインストール

Pythonで **convert SVG to PNG** を行う最もシンプルな方法は `cairosvg` パッケージを使うことです。Cairo グラフィックスライブラリをラップし、内部でベクターのラスタライズを処理してくれます。

```bash
pip install cairosvg
```

> **プロのコツ:** `requirements.txt` でバージョンを固定（例: `cairosvg==2.7.0`）しておくと、メジャーリリースが出たときの予期せぬ破壊を防げます。

## Step 2: シンプルな変換関数を作成

ライブラリが準備できたので、重い処理を担う小さなヘルパー関数を作ります。この関数は **svg to png python** ロジックをカプセル化し、再利用が簡単になります。

```python
# convert_svg_to_png.py
import os
from cairosvg import svg2png

def convert_svg_to_png(
    input_path: str,
    output_path: str,
    dpi: int = 96,
    background_color: str = None,
) -> None:
    """
    Convert an SVG file to a PNG image.

    Parameters
    ----------
    input_path : str
        Path to the source SVG file.
    output_path : str
        Destination path for the generated PNG.
    dpi : int, optional
        Dots per inch for the rasterized image (default: 96).
    background_color : str, optional
        Hex color (e.g., "#FFFFFF") to use as background.
        If None, the SVG's own transparency is preserved.

    Raises
    ------
    FileNotFoundError
        If the input SVG does not exist.
    ValueError
        If the output directory cannot be created.
    """
    # Validate input file
    if not os.path.isfile(input_path):
        raise FileNotFoundError(f"SVG file not found: {input_path}")

    # Ensure output directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Read the SVG content
    with open(input_path, "rb") as svg_file:
        svg_bytes = svg_file.read()

    # Perform the conversion
    svg2png(
        bytestring=svg_bytes,
        write_to=output_path,
        dpi=dpi,
        background_color=background_color,
    )
    print(f"✅ Successfully saved PNG to {output_path}")
```

### このアプローチが有効な理由

- **明示的な I/O 処理:** SVG をバイト列として読み込むことで、Windows で時折発生する Unicode エンコーディング問題を回避  
- **カスタム DPI:** 印刷用と画面用でピクセル密度が異なる場合にスケーリングが必要になることが多いです  
- **オプションの背景色:** 透明領域を持つ SVG でも、16 進カラーを指定すれば **export SVG to PNG** 時に固定の背景色を付与でき、UI サムネイル作成に便利です

## Step 3: 変換スクリプトを実行

関数ができたら、実際のファイルを変換してみましょう。`logo.svg` を `assets/` フォルダに置き、プロジェクトのルートからスクリプトを実行します。

```python
# demo_conversion.py
from convert_svg_to_png import convert_svg_to_png

if __name__ == "__main__":
    INPUT_SVG = "assets/logo.svg"
    OUTPUT_PNG = "output/logo.png"

    # Simple call – defaults keep transparency and 96 DPI
    convert_svg_to_png(INPUT_SVG, OUTPUT_PNG)

    # Example with a white background and higher DPI for sharper output
    convert_svg_to_png(
        INPUT_SVG,
        "output/logo_highres.png",
        dpi=300,
        background_color="#FFFFFF",
    )
```

実行例:

```bash
python demo_conversion.py
```

コンソールに以下のように出力され、ファイルが正常に書き込まれたことが確認できます:

```
✅ Successfully saved PNG to output/logo.png
✅ Successfully saved PNG to output/logo_highres.png
```

### 期待される結果

- `output/logo.png` – 元の SVG と 1:1 のラスタ画像で、透明情報を保持  
- `output/logo_highres.png` – 300 DPI のバージョンで白背景、印刷に最適

![convert svg to png example output](example.png){alt="SVG を PNG に変換した例の出力"}

*(スクリーンショットは画像ビューアで開いた PNG ファイルを示し、変換が成功したことを確認できます。)*

## Step 4: 複数の SVG をバッチ処理 (任意)

ディレクトリ全体の **save SVG as PNG** が必要な場合は、短いループで実現できます。このスニペットはエラーハンドリングも備えており、壊れた SVG が混在していても安心です。

```python
import glob
from pathlib import Path

def batch_convert(source_dir: str, dest_dir: str, **options):
    svg_paths = glob.glob(os.path.join(source_dir, "*.svg"))
    for svg_path in svg_paths:
        try:
            filename = Path(svg_path).stem + ".png"
            output_path = os.path.join(dest_dir, filename)
            convert_svg_to_png(svg_path, output_path, **options)
        except Exception as e:
            print(f"⚠️  Failed to convert {svg_path}: {e}")

if __name__ == "__main__":
    batch_convert(
        source_dir="assets/",
        dest_dir="output/batch/",
        dpi=150,
        background_color="#F0F0F0",
    )
```

実行すると `output/batch/` に `assets/` 内のすべての SVG に対応した PNG が生成されます。エラーが出たファイルはログに記録され、処理は続行されるため、ジョブ全体を止める必要はありません。

## よくある質問とエッジケース

### 1. **SVG が外部フォントを使用している場合は？**  
`cairosvg` は参照されたフォントを埋め込もうとしますが、ローカルファイルシステム上にあるものしか認識できません。フォントファイルを SVG と同じディレクトリに置くか、`<style>` タグで SVG に直接埋め込んでください。そうしないと PNG では代替フォントが使用されます。

### 2. **スケーリング時に元のアスペクト比を保つには？**  
`dpi` のみを指定し、Cairo に SVG の viewBox からピクセルサイズを計算させます。固定の幅・高さが必要な場合は、適切な DPI を自分で算出するか、`svg2png` が提供する `output_width`/`output_height` 引数を利用してください。

### 3. **大きな SVG をメモリ不足なく変換できるか？**  
可能です。`cairosvg` はラスタライズをストリーミングしますが、巨大な SVG を一度にメモリに読み込むのは避けましょう。バッチ例のように 1 ファイルずつ処理すれば問題ありません。

### 4. **変換はスレッドセーフか？**  
基盤となる Cairo ライブラリはプラットフォームによっては完全にスレッドセーフではありません。並列実行したい場合は、スレッドではなく `multiprocessing` プールで呼び出すことを推奨します。

## パフォーマンス向上のヒント

- **PNG をキャッシュ** しておくと、SVG が頻繁に変わらない限り再計算を防げます  
- **同一 DPI を再利用** すれば、スケーリング計算のオーバーヘッドを削減  
- Web サービスの場合は、ディスクに書き出す代わりに `BytesIO` ストリームとして PNG を返すと I/O レイテンシが減ります

```python
from io import BytesIO
def convert_svg_to_png_bytes(svg_path: str, dpi: int = 96) -> BytesIO:
    with open(svg_path, "rb") as f:
        svg_bytes = f.read()
    png_bytes = BytesIO()
    svg2png(bytestring=svg_bytes, write_to=png_bytes, dpi=dpi)
    png_bytes.seek(0)
    return png_bytes
```

## まとめ

Python で **convert SVG to PNG** を行うために必要なことはすべて網羅しました:

1. `cairosvg` をインストール  
2. DPI、背景色、エラーチェックを備えた再利用可能な `convert_svg_to_png` 関数を作成  
3. 単一ファイルまたはフォルダ全体をバッチ処理  
4. 外部フォント、アスペクト比保持、スレッド安全性といった一般的な課題に対処  

この知識があれば、任意の自動化パイプラインで **save SVG as PNG** が可能になり、Web API に組み込んだり、デザインシステム向けの資産を生成したりできます。

### 次にやること

- `svglib` + `reportlab` など別ライブラリを使った **svg to png conversion** を試してみる（PDF ファーストのワークフロー向け）  
- `pngquant` などの画像最適化ツールと組み合わせて、ウェブ向けにファイルサイズを削減  
- `argparse` や `click` を使って CLI ラッパーを作成し、`python -m convert_svg_to_png INPUT.svg OUTPUT.png` のように端末から実行できるようにする

質問があればコメントで教えてください。またはリポジトリをフォークして、さまざまなエクスポート設定を試してみてください。Happy coding!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで学んだテクニックを応用できる関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、API の追加機能をマスターしたり、別実装アプローチを自分のプロジェクトに取り入れたりするのに役立ちます。

- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Render SVG Doc as PNG in .NET with Aspose.HTML](/html/english/net/rendering-html-documents/render-svg-doc-as-png/)
- [svg a png java – Convertir SVG a imagen con Aspose.HTML para Java](/html/spanish/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}