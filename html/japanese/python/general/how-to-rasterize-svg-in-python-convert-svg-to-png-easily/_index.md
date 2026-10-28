---
category: general
date: 2026-10-28
description: PythonでSVGをラスタライズし、CairoSVGを使用したシンプルなスクリプトでSVGをPNGに変換する方法を学びましょう。数秒でSVGをPNGとして保存できます。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to rasterize svg
- convert svg to png
- save svg as png
- svg to png python
- export svg as png
language: ja
lastmod: 2026-10-28
og_description: PythonでSVGをラスター化する方法：このガイドでは、CairoSVGを使用してSVGをPNGに変換する手順を、インストール、コード、トラブルシューティングを含めて解説します。
og_image_alt: Screenshot of Python code that rasterizes SVG to PNG
og_title: PythonでSVGをラスタライズする方法 – 簡単なSVGからPNGへのガイド
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to rasterize SVG in Python and convert SVG to PNG with a
    simple script using CairoSVG. Save SVG as PNG in seconds.
  headline: How to rasterize SVG in Python – convert SVG to PNG easily
  type: TechArticle
- description: Learn how to rasterize SVG in Python and convert SVG to PNG with a
    simple script using CairoSVG. Save SVG as PNG in seconds.
  name: How to rasterize SVG in Python – convert SVG to PNG easily
  steps:
  - name: Why CairoSVG?
    text: '- **Pure Python**: No need for external command‑line tools once the package
      is installed. - **SVG‑compliant**: Supports most SVG 1.1 features, including
      gradients, masks, and text. - **Flexible output**: Besides PNG, you can export
      to PDF, PS, or even raw bytes.'
  - name: Step‑by‑step breakdown
    text: 1. **Install the library** – `pip install cairosvg` pulls in the compiled
      Cairo bindings. 2. **Import the module** – `import cairosvg` gives you access
      to the `svg2png` helper. 3. **Call `svg2png`** – Pass the SVG file path (or
      a URL) and the destination PNG path. Optional `output_width`, `output_he
  - name: Edge cases you might encounter
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | **Large SVG (megapixel dimensions)** | Increase `dpi` or set explicit `output_width`/`output_height`
      to avoid memory spikes. | | **Missing fonts** | Install the required fonts on
      the system or em'
  type: HowTo
tags:
- svg
- python
- image processing
- cairosvg
title: PythonでSVGをラスタライズする方法 – SVGを簡単にPNGに変換
url: /ja/python/general/how-to-rasterize-svg-in-python-convert-svg-to-png-easily/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでSVGをラスタライズする方法 – SVGを簡単にPNGへ変換

If you need to **how to rasterize svg** for a web‑app, a report, or an automated build, this guide gives you a ready‑to‑run solution. You’ll see how to **convert svg to png** with just a few lines of Python, and the result is a crisp PNG that you can store or serve instantly.

このガイドでは、Webアプリやレポート、あるいは自動ビルドのために **how to rasterize svg** が必要な場合に、すぐに実行できるソリューションを提供します。数行のPythonだけで **convert svg to png** の方法が分かり、結果はすぐに保存または配信できる鮮明なPNGになります。

The tutorial covers everything from installing the required library to handling edge cases like large files or custom DPI settings. By the end, you’ll be able to **save svg as png**, **export svg as png**, and integrate the process into any Python workflow.

このチュートリアルでは、必要なライブラリのインストールから大きなファイルやカスタムDPI設定といったエッジケースの処理まで網羅しています。最後まで読むと、**save svg as png**、**export svg as png** ができ、任意のPythonワークフローにこのプロセスを組み込めるようになります。

## 必要なもの

- Python 3.8+（コードは3.9、3.10以降でも動作します）
- `pip`（パッケージをインストールするため）
- ラスタライズしたいローカルのSVGファイル（例: `logo.svg`）
- 任意: 依存関係をクリーンに管理するための仮想環境

> **Pro tip:** 仮想環境（`python -m venv .venv`）を使用すると、CairoSVG の依存関係がグローバルなPythonパッケージから分離されます。

## PythonでSVGをラスタライズする方法

**how to rasterize svg** を実現する最もシンプルな方法は **CairoSVG** ライブラリを使うことです。CairoSVG はSVG XMLを読み取り、Cairo グラフィックエンジンでレンダリングし、ラスタ画像をPNG、PDF、その他のビットマップ形式で書き出します。

```bash
# Install CairoSVG and its binary dependencies
pip install cairosvg
```

```python
# rasterize_svg.py
import sys
from pathlib import Path
import cairosvg

def rasterize_svg(input_path: str, output_path: str,
                  width: int | None = None,
                  height: int | None = None,
                  dpi: int = 96) -> None:
    """
    Convert an SVG file to a PNG image.

    Parameters
    ----------
    input_path : str
        Path to the source SVG file.
    output_path : str
        Destination path for the PNG file.
    width : int | None
        Desired output width in pixels (maintains aspect ratio if height is None).
    height : int | None
        Desired output height in pixels (maintains aspect ratio if width is None).
    dpi : int
        Dots per inch for the rasterization. Higher DPI yields larger files but more detail.
    """
    try:
        # CairoSVG can read from a file path directly
        cairosvg.svg2png(url=Path(input_path).as_uri(),
                         write_to=output_path,
                         output_width=width,
                         output_height=height,
                         dpi=dpi)
        print(f"✅ Successfully saved PNG to {output_path}")
    except Exception as e:
        print(f"❌ Failed to rasterize {input_path}: {e}", file=sys.stderr)
        raise

if __name__ == "__main__":
    # Example usage:
    # python rasterize_svg.py ./assets/logo.svg ./output/logo.png 300 300
    if len(sys.argv) < 3:
        print("Usage: python rasterize_svg.py <input_svg> <output_png> [width] [height] [dpi]")
        sys.exit(1)

    input_svg = sys.argv[1]
    output_png = sys.argv[2]
    w = int(sys.argv[3]) if len(sys.argv) > 3 else None
    h = int(sys.argv[4]) if len(sys.argv) > 4 else None
    d = int(sys.argv[5]) if len(sys.argv) > 5 else 96

    rasterize_svg(input_svg, output_png, width=w, height=h, dpi=d)
```

### なぜCairoSVGか？

- **Pure Python**: パッケージをインストールすれば外部コマンドラインツールは不要です。
- **SVG‑compliant**: グラデーション、マスク、テキストなど、ほとんどのSVG 1.1機能をサポートします。
- **Flexible output**: PNG以外にもPDF、PS、さらには生バイト列へエクスポート可能です。

### 手順ごとの解説

1. **Install the library** – `pip install cairosvg` でコンパイル済みのCairoバインディングがインストールされます。
2. **Import the module** – `import cairosvg` で `svg2png` ヘルパーが利用可能になります。
3. **Call `svg2png`** – SVGファイルのパス（またはURL）と出力先PNGパスを渡します。オプションの `output_width`、`output_height`、`dpi` でサイズと解像度を制御できます。
4. **Handle errors** – `try/except` ブロックは、SVGが不正な場合や出力ディレクトリが書き込み不可の場合に明確なメッセージを出力します。

## CairoSVGでSVGをPNGに変換

ワンライナーで簡単に変換したい場合、以下のスニペットはラッパー関数なしで実行できます。

```python
import cairosvg

cairosvg.svg2png(url="logo.svg", write_to="logo.png")
```

これは **convert svg to png** の最も簡潔な例です。現在のディレクトリから `logo.svg` を読み取り、同じ場所に `logo.png` として書き出します。

## SVGをPNGとして保存 – 結果を確認

スクリプトを実行すると、指定したパスにPNGファイルが作成されます。任意の画像ビューアで開き、正しく変換されたことを確認してください。

```bash
# Linux/macOS
xdg-open ./output/logo.png   # or open on macOS
# Windows
start ./output/logo.png
```

PNGがぼやけて見える場合は、`dpi` 引数を上げ（例: `dpi=300`）て、より高解像度のラスタを生成してください。

## SVGをPNG以外の形式でもエクスポート

CairoSVG は **PDF**、**PostScript**、または生の **PNG バイト列** も出力できます。メモリ上で画像が必要な場合（例: Flask のレスポンス）に `BytesIO` オブジェクトへエクスポートする例を以下に示します。

```python
import io
import cairosvg

svg_path = "logo.svg"
png_bytes = io.BytesIO()
cairosvg.svg2png(url=Path(svg_path).as_uri(), write_to=png_bytes)
png_bytes.seek(0)  # Ready for sending over HTTP
```

### 発生し得るエッジケース

| 状況 | 推奨される対処 |
|---|---|
| **大きなSVG（メガピクセルサイズ）** | `dpi` を上げるか、明示的に `output_width`/`output_height` を設定してメモリ使用量の急増を防ぎます。 |
| **フォントが見つからない** | システムに必要なフォントをインストールするか、`<style>` タグでSVGに埋め込んでください。 |
| **透過の問題** | PNGはデフォルトでアルファを保持します。背景を不透明にしたい場合は、`svg2png` に `background_color="#FFFFFF"` を渡してください。 |
| **バッチ処理** | SVGが入ったディレクトリをループし、各ファイルに対して `rasterize_svg` を呼び出します。 |

## 完全な動作例

以下は最小限の自己完結型スクリプトです。`svg_to_png.py` という名前のファイルにコピー＆ペーストしてすぐに実行できます。

```python
# svg_to_png.py
import cairosvg
from pathlib import Path

def main():
    src = Path("example.svg")
    dst = Path("example.png")
    if not src.is_file():
        raise FileNotFoundError(f"Source SVG not found: {src}")

    # Convert with default DPI (96) and keep original dimensions
    cairosvg.svg2png(url=src.as_uri(), write_to=dst)
    print(f"✅ {src.name} → {dst.name} created successfully.")

if __name__ == "__main__":
    main()
```

Running `python svg_to_png


## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加のAPI機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [PythonでSVGをラスタライズする方法 – 完全ガイド](/html/english/python/general/how-to-rasterize-svg-in-python-complete-guide/)
- [PythonでSVGをPNGに変換 – 高解像度エクスポートガイド](/html/english/python/general/convert-svg-to-png-in-python-high-resolution-export-guide/)
- [PythonでSVGドキュメントを作成 – SVGをPNGに変換ガイド](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}