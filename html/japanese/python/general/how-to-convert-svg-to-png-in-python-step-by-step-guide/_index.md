---
category: general
date: 2026-11-17
description: Pythonで数行のコードでSVGをPNGに変換。オプションの変換設定を使用してSVGをPNGとして保存する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert svg to png
- save svg as png
- export svg as png
- svg to raster image
- how to convert svg to png
language: ja
lastmod: 2026-11-17
og_description: PythonでSVGをPNGに変換する簡潔な例。手順に従ってSVGを効率的にPNGへエクスポートしてください。
og_image_alt: Diagram illustrating convert svg to png workflow in Python
og_title: PythonでSVGをPNGに変換する – クイックガイド
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: convert svg to png using Python in a few lines. Learn to save SVG as
    PNG with optional conversion settings.
  headline: How to convert SVG to PNG in Python – step‑by‑step guide
  type: TechArticle
tags:
- svg
- png
- python
- image conversion
title: PythonでSVGをPNGに変換する方法 – ステップバイステップガイド
url: /ja/python/general/how-to-convert-svg-to-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでSVGをPNGに変換する方法 – ステップバイステップガイド

**svg を png に変換**する必要がある場合、このガイドでは今日実行できる完全なソリューションを示します。また、サイズや背景色のオプション設定を使用して **svg を png として保存**する方法も紹介します。

ベクター SVG ファイルからラスタ画像を生成することは、ブラウザにグラフィックを配信したり、サムネイルを作成したり、PDF に画像を埋め込んだりする際に一般的です。このチュートリアルでは、必要なライブラリのインストールから、ファイルが見つからない場合や非常に大きな SVG の処理といったエッジケースまで、すべてをカバーします。

## Prerequisites

開始する前に、以下が揃っていることを確認してください。

* Python 3.8 以上がインストールされていること。
* ターミナルまたはコマンドプロンプトにアクセスできること。
* **svg to raster image** 変換を実行する `cairosvg` パッケージがインストールされていること。

以下の pip コマンドでパッケージをインストールできます。

```bash
pip install cairosvg
```

> **Pro tip:** 仮想環境を使用して、依存関係を他のプロジェクトから分離しておくと便利です。

## How to convert SVG to PNG in Python

このプロセスの核心は、3 つのアクションで構成されています：SVG を読み込み、必要に応じて変換パラメータを調整し、PNG ファイルを書き出す。以下のコードは、これら 3 つのステップを再利用可能な関数として実装しています。

```python
import cairosvg
from pathlib import Path

def convert_svg_to_png(svg_path: str, png_path: str) -> None:
    """
    Convert an SVG file to a PNG raster image.

    Parameters
    ----------
    svg_path : str
        Path to the source SVG file.
    png_path : str
        Destination path for the generated PNG file.
    """
    # Verify that the SVG file exists
    if not Path(svg_path).is_file():
        raise FileNotFoundError(f"SVG file not found: {svg_path}")

    # Perform the conversion using default settings
    cairosvg.svg2png(url=svg_path, write_to=png_path)

# Example usage
if __name__ == "__main__":
    svg_file = "YOUR_DIRECTORY/image.svg"
    png_file = "YOUR_DIRECTORY/image.png"
    convert_svg_to_png(svg_file, png_file)
    print(f"Converted {svg_file} to {png_file}")
```

### Why this works

* `cairosvg.svg2png` は SVG ファイル（`url=svg_path`）を読み取り、PNG ファイル（`write_to=png_path`）を書き出します。  
* ソース SVG が見つからない場合は明確なエラーを発生させるため、ファイルパスの問題を早期にデバッグできます。  
* 変換ロジックを関数内に収めることで、複数のスクリプトで再利用したり、より大規模なアプリケーションに統合したりするのが容易になります。

## Optional: fine‑tune the conversion

特定の出力サイズや別の背景色が必要な場合、`cairosvg.svg2png` は追加の引数を受け取ります。以下は幅 300 px、背景色を白に設定したバリエーションです。

```python
def convert_svg_to_png_custom(svg_path: str, png_path: str,
                              width: int = 300,
                              background_color: str = "white") -> None:
    """
    Convert an SVG to PNG with custom dimensions and background.

    Parameters
    ----------
    width : int
        Desired width of the PNG in pixels; height scales proportionally.
    background_color : str
        Hex or named color for the PNG background.
    """
    if not Path(svg_path).is_file():
        raise FileNotFoundError(f"SVG file not found: {svg_path}")

    cairosvg.svg2png(
        url=svg_path,
        write_to=png_path,
        output_width=width,
        background_color=background_color
    )
```

基本バージョンと同様にこの関数を呼び出し、希望する幅や色を渡すだけで利用できます。

## Common questions and edge cases

**What if the SVG contains external fonts?**  
`cairosvg` は参照されたフォントを自動的に埋め込みますが、フォントファイルは SVG の位置からアクセス可能である必要があります。フォントファイルを SVG と同じディレクトリに置くか、絶対 URL を使用してください。

**How do I handle very large SVGs?**  
大きなファイルはかなりのメモリを消費します。ディスクから直接読み込む代わりに、SVG コンテンツをストリームすることができます。

```python
with open(svg_path, "rb") as svg_stream:
    cairosvg.svg2png(file_obj=svg_stream, write_to=png_path)
```

**Can I convert multiple files in a batch?**  
変換呼び出しをループでラップし、`Path.glob("*.svg")` を使ってディレクトリ内のすべての SVG を検出すれば、一括変換が可能です。

## Expected output

サンプルスクリプトを実行すると、変換が完了したことを示す一行が出力されます。

```
Converted YOUR_DIRECTORY/image.svg to YOUR_DIRECTORY/image.png
```

生成された `image.png` ファイルは同じディレクトリに保存され、任意の画像ビューアで開くことができます。

## Conclusion

これで Python で **svg を png に変換**する方法、**svg を png として保存**する方法、そしてカスタム寸法で **svg を png にエクスポート**する方法が分かりました。同じアプローチは任意の SVG ファイルに適用でき、ベクターグラフィックをウェブページ、レポート、サムネイル向けの **svg to raster image** 形式に変換できます。

次のステップとしては:

* DPI 制御のために `export svg as png` パラメータを調査する。  
* Flask や Django のエンドポイントに変換関数を組み込み、オンザフライで画像生成を提供する。  
* 二次キーワード **how to convert svg to png** を使用して、バッチ処理や CI/CD パイプラインなどの高度なユースケースを検索する。

さまざまな設定を試してみて、結果をコミュニティと共有してください！

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示したテクニックを基にした、密接に関連するトピックをカバーしています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [Convert SVG to PNG in Python – High‑Resolution Export Guide](/html/english/python/general/convert-svg-to-png-in-python-high-resolution-export-guide/)
- [Convert SVG to PNG in Python using Aspose.HTML](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)
- [Convert SVG to PNG in Python – Complete Step‑by‑Step Guide](/html/english/python/general/convert-svg-to-png-in-python-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}