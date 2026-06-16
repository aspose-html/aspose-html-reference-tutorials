---
category: general
date: 2026-06-16
description: PythonでSVGを素早くリサイズする方法 – SVGファイルをPythonで読み込み、編集し、さらに小さなスクリプトでSVGファイルを一括リサイズ。
draft: false
keywords:
- how to resize svg
- batch resize svg files
- load svg file python
- edit svg file python
language: ja
og_description: PythonでSVGをリサイズする方法は？PythonでSVGファイルを読み込み、編集し、明確で実行可能な例を使ってSVGファイルを一括リサイズする方法を学びましょう。
og_title: PythonでSVGをリサイズする方法 – 完全チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to resize SVG in Python quickly – load SVG file Python, edit SVG
    file Python, and even batch resize SVG files with a tiny script.
  headline: How to Resize SVG in Python – Step‑by‑Step Guide
  type: TechArticle
- description: How to resize SVG in Python quickly – load SVG file Python, edit SVG
    file Python, and even batch resize SVG files with a tiny script.
  name: How to Resize SVG in Python – Step‑by‑Step Guide
  steps:
  - name: '**Collects** every `.svg` file in the source folder.'
    text: '**Collects** every `.svg` file in the source folder.'
  - name: '**Loads** each file using the same routine we used for a single SVG.'
    text: '**Loads** each file using the same routine we used for a single SVG.'
  - name: '**Resizes** to the desired width while keeping the aspect ratio.'
    text: '**Resizes** to the desired width while keeping the aspect ratio.'
  - name: '**Writes** the result to a new folder, leaving originals untouched.'
    text: '**Writes** the result to a new folder, leaving originals untouched.'
  type: HowTo
tags:
- Python
- SVG
- Automation
title: PythonでSVGをリサイズする方法 – ステップバイステップガイド
url: /ja/python/general/how-to-resize-svg-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでSVGのサイズを変更する方法 – 完全チュートリアル

グラフィックエディタを開かずに **SVGのサイズを変更する方法** を考えたことはありませんか？たとえば、ウェブバナー用に幅200 pxのロゴが必要だったり、モバイルアプリ用に何十個ものアイコンを用意したりすることがあるかもしれません。良いニュースは、すべてPythonで実行できることです—PhotoshopもInkscapeのUIも不要で、数行のコードだけです。

このガイドでは、PythonでSVGファイルを読み込み、サイズを編集し、さらにフォルダー全体のSVGを一括でスケーリングする方法を順を追って説明します。最後まで読むと、**load SVG file Python**、**edit SVG file Python**、**batch resize SVG files** を自信を持って実行できるようになります。

## 前提条件

- Python 3.8+ がインストールされていること（標準の `python` コマンドが動作すれば OK）
- `svgwrite` または `lxml` ライブラリ – ここでは直接DOMにアクセスできる `lxml` を使用します。
- リサイズしたいSVGが入ったフォルダー（例: `assets/icons/`）

GUIツールは不要です。すべてターミナル上で実行できます。

---

## 手順 1: 必要なライブラリをインストールする

まず、PyPI から `lxml` を取得します。サイズが小さく高速で、XML属性を直接操作できます。

```bash
pip install lxml
```

> **プロのコツ:** 仮想環境で作業している場合は、コマンドを実行する前に環境をアクティブにしてください。これによりプロジェクトの依存関係が整理されます。

## 手順 2: PythonでSVGファイルを読み込む

ここでは **load SVG file Python** のスタイルで、XMLを読み込み、ルートの `<svg>` 要素を取得し、現在のサイズを出力します。

```python
from lxml import etree

def load_svg(path: str) -> etree._ElementTree:
    """
    Load an SVG document and return the parsed XML tree.
    """
    parser = etree.XMLParser(remove_blank_text=True)
    tree = etree.parse(path, parser)
    return tree

# Example usage
svg_path = "assets/logo.svg"
svg_tree = load_svg(svg_path)
root = svg_tree.getroot()
print(f"Original width: {root.get('width')}, height: {root.get('height')}")
```

**なぜ重要か:** `lxml` は本格的なDOMを提供するため、任意の属性を照会・変更できます—**edit SVG file Python** のタスクに最適です。

## 手順 3: 幅（と高さ）を変更する – SVGのサイズ変更方法

SVGはベクター形式なので、幅、または高さ、あるいは両方を設定できます。幅だけを変更すると、viewBox がアスペクト比を保持しますが、多くのツールは対応する高さ属性も尊重します。以下は、元のアスペクト比を保ちつつリサイズするヘルパー関数です:

```python
def resize_svg(tree: etree._ElementTree, new_width: int) -> None:
    """
    Resize the root <svg> element to `new_width` while preserving aspect ratio.
    """
    root = tree.getroot()
    # Grab original dimensions (they may be in px, pt, or just numbers)
    orig_width = float(root.get("width").replace("px", ""))
    orig_height = float(root.get("height").replace("px", ""))

    # Compute scale factor and new height
    scale = new_width / orig_width
    new_height = round(orig_height * scale, 2)

    # Update attributes
    root.set("width", f"{new_width}px")
    root.set("height", f"{new_height}px")

    # Optional: ensure viewBox exists for better scaling in browsers
    if "viewBox" not in root.attrib:
        viewbox = f"0 0 {orig_width} {orig_height}"
        root.set("viewBox", viewbox)

# Resize to 200 px wide
resize_svg(svg_tree, 200)
```

上記の関数が **how to resize SVG** の核心です。現在のサイズを読み取り、比例した高さを計算し、新しい属性を書き戻します。

## 手順 4: 変更したSVGを保存する

編集後、変更をディスクに書き戻す必要があります。これで **edit SVG file Python** のサイクルが完了します。

```python
def save_svg(tree: etree._ElementTree, destination: str) -> None:
    """
    Write the modified SVG tree to `destination`.
    """
    tree.write(
        destination,
        pretty_print=True,
        xml_declaration=True,
        encoding="UTF-8"
    )
    print(f"Saved resized SVG to {destination}")

# Save as a new file so the original stays untouched
output_path = "assets/logo_resized.svg"
save_svg(svg_tree, output_path)
```

スクリプト全体を実行すると、幅が正確に200 px の新しい `logo_resized.svg` が生成されます。

## 手順 5: SVGファイルを一括リサイズ – フォルダー全体をスケールする

これで **load SVG file Python**、**edit SVG file Python**、そして保存ができたので、ディレクトリをループし、すべてのファイルに同じ変換を適用しましょう。これが **batch resize SVG files** の解決策です。

```python
import pathlib

def batch_resize(source_dir: str, target_dir: str, width: int) -> None:
    """
    Resize every .svg file in `source_dir` to `width` pixels and store
    the results in `target_dir`.
    """
    src = pathlib.Path(source_dir)
    tgt = pathlib.Path(target_dir)
    tgt.mkdir(parents=True, exist_ok=True)

    svg_files = list(src.glob("*.svg"))
    if not svg_files:
        print("No SVG files found.")
        return

    for svg_path in svg_files:
        try:
            tree = load_svg(str(svg_path))
            resize_svg(tree, width)
            out_path = tgt / svg_path.name
            save_svg(tree, str(out_path))
        except Exception as e:
            print(f"Failed on {svg_path.name}: {e}")

# Example: resize everything in 'assets/icons' to 64 px wide
batch_resize("assets/icons", "assets/icons_resized", 64)
```

### これが行うこと:

1. **Collects** ソースフォルダー内のすべての `.svg` ファイルを収集します。
2. **Loads** 各ファイルを、単一SVGで使用したのと同じ手順で読み込みます。
3. **Resizes** 目的の幅にリサイズし、アスペクト比を保持します。
4. **Writes** 結果を新しいフォルダーに書き込み、元のファイルはそのままにします。

これで **batch resize SVG files** 用のすぐに使えるパイプラインが完成しました。

## 手順 6: エッジケースと一般的な落とし穴

| 問題 | 発生理由 | 対策 |
|------|----------|------|
| `width`/`height` 属性が欠如している | 一部のSVGは `viewBox` のみで動作します。 | 属性がない場合は、viewBox の寸法 (`viewBox="0 0 w h"`) を代わりに使用します。 |
| `px` 以外の単位（例: `pt`、`%`） | スクリプトは `px` のみを除去します。 | `replace` 呼び出しを拡張するか、正規表現で任意の単位を取得できるようにします。 |
| 複雑な `<symbol>` または `<use>` 要素 | ルートのリサイズだけではネストされたシンボルに影響しないことがあります。 | 各 `<symbol>` タグにも同様の属性変更を適用するか、CSS の `transform: scale()` を使用します。 |
| ファイル名に Unicode や特殊文字が含まれる | `pathlib` はほとんどのケースを処理しますが、Windows は特定の文字で問題が起きることがあります。 | ファイル名が UTF‑8 安全であることを確認するか、処理前にリネームしてください。 |

事前にこれらに対処しておくことで、後で壊れたアイコンに驚かされることを防げます。

## 手順 7: 結果を検証する

簡単な妥当性チェックは、以下の小さなHTMLスニペットで行えます:

```html
<!DOCTYPE html>
<html>
<head><title>SVG Test</title></head>
<body>
  <h3>Original</h3>
  <img src="assets/logo.svg" alt="original logo">
  <h3>Resized</h3>
  <img src="assets/logo_resized.svg" alt="resized logo">
</body>
</html>
```

ブラウザでファイルを開きます—両方の画像は見た目が同じですが、リサイズされた方は開発者ツールで幅が **200 px** と表示されます。

---

## 結論

これで、単一ファイルからディレクトリ全体まで、純粋なPythonだけで **how to resize SVG** ができるようになりました。ワークフローは **load SVG file Python**、**edit SVG file Python**、そして **batch resize SVG files** をカバーし、ほんの数関数で実現できます。

試してみてください: 異なる幅を試したり、高さのみのリサイズを実験したり、`argparse` を使ってコマンドラインインターフェースを追加したり。可能性は無限で、スクリプトはビルドパイプライン、CIジョブ、デスクトップユーティリティに組み込むほど軽量です。

グラデーションや埋め込みフォントの扱い、Flaskアプリへの統合について質問がありますか？コメントを残してください。一緒にその課題を探ります。コーディングを楽しんでください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加のAPI機能を習得し、プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [Aspose.HTML を使用して .NET で SVG を画像に変換する](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [Aspose.HTML を使用して .NET で SVG を PDF に変換する](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-pdf/)
- [Aspose.HTML を使用して .NET で SVG ドキュメントを PNG としてレンダリングする](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}