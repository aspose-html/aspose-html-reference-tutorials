---
category: general
date: 2026-05-31
description: Python を使って HTML から SVG を抽出する方法を学びましょう。このステップバイステップのチュートリアルでは、HTML ドキュメントの読み取り、SVG
  ファイルの保存、インライン SVG の効率的な保存方法を示します。
draft: false
keywords:
- how to extract svg
- read html document
- save svg files
- save inline svg
- extract svg from html
language: ja
og_description: Python を使って HTML から SVG を抽出する方法。このチュートリアルに従って HTML ドキュメントを読み込み、SVG
  ファイルを保存し、インライン SVG を簡単に処理しましょう。
og_title: PythonでHTMLからSVGを抽出する方法 – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  headline: How to extract SVG from HTML with Python – Complete Guide
  type: TechArticle
- description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  name: How to extract SVG from HTML with Python – Complete Guide
  steps:
  - name: Reads an HTML file.
    text: Reads an HTML file.
  - name: Collects inline <svg> markup.
    text: Collects inline <svg> markup.
  - name: Finds external SVG references (<img> and <object> tags).
    text: Finds external SVG references (<img> and <object> tags).
  - name: Saves each SVG to a separate .svg file.
    text: Saves each SVG to a separate .svg file.
  type: HowTo
tags:
- Python
- SVG
- HTML parsing
- Aspose
title: PythonでHTMLからSVGを抽出する方法 – 完全ガイド
url: /ja/python/general/how-to-extract-svg-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML から SVG を抽出する方法 – 完全ガイド

乱雑な HTML ページから **SVG を抽出する方法** に悩んだことはありませんか？ あなたは一人ではありません。ウェブスクレイパーを作るときでも、デザインパイプラインを構築するときでも、アイコンを一括エクスポートしたいときでも、 **SVG を抽出する方法** を知っていれば、時間と手間を大幅に削減できます。

このチュートリアルでは、Aspose.HTML ライブラリ for Python を使って **SVG を抽出する方法** をステップバイステップで解説します。HTML ドキュメントを読み込み、インライン `<svg>` マークアップ **と** 外部 SVG 参照の両方を取得し、**SVG ファイルを保存** します。最後には、プロジェクトにすぐ適用できる再利用可能なスクリプトが手に入ります。

> **プロのコツ:** ページをざっと確認したいだけなら `BeautifulSoup` でも動きますが、Aspose.HTML はフル DOM を提供するため、インラインとリンクされた SVG の両方を簡単に抽出できます。

## 必要なもの

始める前に以下を用意してください。

* Python 3.8+（コードは f‑strings を使用しているので、最低でも 3.6 が必要です）
* `pip install aspose-html` – HTML パースを支える商用ライブラリ
* SVG を抽出したい `input.html` が入ったフォルダー
* 出力ディレクトリへの書き込み権限（ここでは `YOUR_DIRECTORY` と呼びます）

以上です—余計なバイナリやヘッドレスブラウザは不要です。シンプルですね。

## 手順 1: Aspose.HTML で HTML ドキュメントを読み込む

最初に **HTML ドキュメントを読み込む** 必要があります。Aspose.HTML はブラウザの `document` のように振る舞う `HTMLDocument` オブジェクトを提供します。

```python
from aspose.html import HTMLDocument

# Load the HTML file – replace YOUR_DIRECTORY with the actual path
doc = HTMLDocument("YOUR_DIRECTORY/input.html")
```

*重要ポイント:* HTML を正しい DOM にロードすることで、正規表現ベースのパースの落とし穴を回避でき、`get_elements_by_tag_name` や `query_selector_all` といった便利なメソッドがそのまま使えます。

## 手順 2: すべてのインライン <svg> 要素を取得

インライン SVG とは、HTML 内に直接埋め込まれた `<svg>…</svg>` ブロックのことです。**インライン SVG を保存** するには、外側の HTML（outerHTML）を取得すれば完了です。

```python
svg_contents = []  # We'll collect both markup and file paths here

# Find every <svg> element in the document
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)   # Store the raw markup
```

`svg_contents` に生のマークアップをそのまま追加していることに注目してください。後で各エントリがマークアップかファイルパスかを判定します。

## 手順 3: 外部 SVG 参照（img と object タグ）を検出

多くのページは `<img src="icon.svg">` や `<object data="logo.svg">` の形で外部 SVG ファイルを参照しています。**HTML から SVG を抽出する** には、これらの URL も取得する必要があります。

```python
# CSS selector: img or object whose src/data ends with .svg (case‑insensitive)
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    # For <img> we read the src attribute, for <object> the data attribute
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:                                   # Guard against missing attribute
        svg_contents.append(src)
```

*エッジケース注意:* SVG の URL が相対パスの場合、HTML ファイルのベースパスと結合する必要があります。ここでは簡潔にするため、HTML と SVG が同じディレクトリにあると仮定しています。

## 手順 4: 各 SVG を個別ファイルに書き出す

マークアップ文字列とファイルパスが混在したリストができたので、ループで **SVG ファイルを保存** します。スクリプトはインラインマークアップと既存ファイルへの参照を自動で判別します。

```python
import os
import shutil

for index, content in enumerate(svg_contents):
    output_path = f"YOUR_DIRECTORY/svg_{index}.svg"

    # Trim leading whitespace and check if it looks like markup
    if content.lstrip().startswith("<svg"):
        # Inline SVG – write the markup directly
        with open(output_path, "w", encoding="utf-8") as file:
            file.write(content)
        print(f"Saved inline SVG to {output_path}")
    else:
        # External reference – copy the source file's contents
        src_path = os.path.abspath(content)  # Resolve relative paths
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, output_path)
            print(f"Copied external SVG from {src_path} to {output_path}")
        else:
            print(f"⚠️  Warning: referenced SVG not found: {src_path}")
```

**実行結果:** スクリプト完了後、`YOUR_DIRECTORY` には `svg_0.svg`, `svg_1.svg`, … といった名前のファイルが作成され、各ファイルにはインラインマークアップまたは外部 SVG のコピーが格納されます。

### 期待される出力

```
Saved inline SVG to YOUR_DIRECTORY/svg_0.svg
Saved inline SVG to YOUR_DIRECTORY/svg_1.svg
Copied external SVG from /path/to/logo.svg to YOUR_DIRECTORY/svg_2.svg
...
```

参照されたファイルが見つからない場合は警告を出しますが、処理は続行されます。つまり、1 つのリンク切れが全体の抽出を止めることはありません。

## よくある落とし穴の対処法

| 問題 | 発生理由 | 簡単な対策 |
|------|----------|------------|
| **相対 URL が壊れる** | `src` 属性が `"../assets/icon.svg"` のようになっている | `os.path.join(os.path.dirname(html_path), src)` で解決 |
| **ファイル名が重複する** | 同名の SVG が複数あると上書きされる | ファイル名にコンテンツのハッシュを付与（`hashlib.md5(content.encode()).hexdigest()[:8]`） |
| **大きなインライン SVG がメモリを圧迫** | 書き出す前にすべてリストに保持している | バッファせずに要素ごとに直接ファイルへストリーム書き込み |
| **非 SVG 画像が混入する** | `<img>` タグが `.svg?version=1` のようなクエリ付き URL を持つ | 拡張子チェック前にクエリ文字列を除去（`src.split('?')[0]`） |

## コピー＆ペーストできる完全スクリプト

以下がそのまま実行可能なプログラムです。`extract_svg.py` として保存し、`YOUR_DIRECTORY` を適切に設定したうえで `python extract_svg.py` を実行してください。

```python
"""
extract_svg.py – How to extract SVG from HTML using Aspose.HTML for Python

This script:
1. Reads an HTML file.
2. Collects inline <svg> markup.
3. Finds external SVG references (<img> and <object> tags).
4. Saves each SVG to a separate .svg file.

Author: Your Name
Date: 2026-05-31
"""

import os
import shutil
from aspose.html import HTMLDocument

# ----------------------------------------------------------------------
# Configuration – change these paths to suit your environment
# ----------------------------------------------------------------------
HTML_PATH = "YOUR_DIRECTORY/input.html"          # Path to source HTML
OUTPUT_DIR = "YOUR_DIRECTORY"                    # Where SVGs will be written

# Ensure output directory exists
os.makedirs(OUTPUT_DIR, exist_ok=True)

# ----------------------------------------------------------------------
# Step 1: Load the HTML document (read html document)
# ----------------------------------------------------------------------
doc = HTMLDocument(HTML_PATH)

# ----------------------------------------------------------------------
# Step 2: Collect inline <svg> elements (save inline svg)
# ----------------------------------------------------------------------
svg_contents = []
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)

# ----------------------------------------------------------------------
# Step 3: Collect external SVG references (extract svg from html)
# ----------------------------------------------------------------------
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:
        # Resolve relative paths relative to the HTML file location
        src_path = os.path.join(os.path.dirname(HTML_PATH), src)
        svg_contents.append(src_path)

# ----------------------------------------------------------------------
# Step 4: Save each gathered SVG (save svg files)
# ----------------------------------------------------------------------
for idx, content in enumerate(svg_contents):
    out_path = os.path.join(OUTPUT_DIR, f"svg_{idx}.svg")

    # Detect inline markup vs file path
    if isinstance(content, str) and content.lstrip().startswith("<svg"):
        # Inline SVG – write directly
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(content)
        print(f"[✓] Inline SVG saved → {out_path}")
    else:
        # External file – copy its contents
        src_path = os.path.abspath(content)
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, out_path)
            print(f"[✓] External SVG copied → {out_path}")
        else:
            print(f"[⚠] Missing SVG file: {src_path}")

print("\n✅ Extraction complete. Check the", OUTPUT_DIR, "folder for your SVGs.")
```

## まとめ – SVG 抽出の全体像

* `HTMLDocument` で **HTML ドキュメントを読み込む**
* `get_elements_by_tag_name` で **インライン `<svg>`** を取得
* CSS セレクタで **外部 SVG** を検出（`.svg` で終わる属性を対象）
* 各要素を **保存** – マークアップはそのままファイルに書き込み、参照はコピー
* 相対パス、重複、欠損ファイルといった **エッジケース** に対応

これで **HTML から SVG を抽出する方法** がすべて網羅されました。シンプルでカスタマイズしやすいスクリプトを手に入れたので、ぜひ活用してください。

## 次にやるべきこと

**SVG の抽出** が安定したら、以下のような拡張を検討してみてください。

* **バッチ処理:** 複数の HTML ファイルをディレクトリ単位で走査し、アイコンライブラリを構築
* **最適化:** 保存した SVG を SVGO（Node.js 製オプティマイザ）で圧縮
* **変換:** `cairosvg` や `svglib` を使って SVG を PNG に変換し、レガシーブラウザ向けに出力
* **メタデータ抽出:** 各 SVG 内の `<title>` や `<desc>` を解析し、検索可能なラベルを生成

これらのトピックはすべて、**read HTML document**, **save svg files**, **save inline svg**, **extract svg from html** といったキーワードに関連しています。ぜひさらに深掘りしてみてください。

---

*ハッピーコーディング！問題があればコメントや GitHub で遠慮なく質問してください。SVG の世界は広大ですが、正しいツールさえあれば抽出は簡単です。*

## 次に学ぶべきこと

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [Rendre un document SVG au format PNG dans .NET avec Aspose.HTML](/html/french/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}