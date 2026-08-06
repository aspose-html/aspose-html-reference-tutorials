---
category: general
date: 2026-08-06
description: PythonでHTMLをPDFに変換する完全な例。HTMLからPDFを生成し、HTMLをPDFとして保存し、一般的なエッジケースを処理する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to pdf
- generate pdf from html
- save html as pdf
- create pdf from html file
- how to convert html to pdf
language: ja
lastmod: 2026-08-06
og_description: PythonでHTMLをPDFに変換し、ドキュメント作成を自動化します。このガイドに従ってHTMLからPDFを生成し、HTMLをPDFとして保存し、出力をカスタマイズしてください。
og_image_alt: Example of convert html to pdf script in Python
og_title: PythonでHTMLをPDFに変換する – 包括的チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-08-06'
  description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  headline: Convert HTML to PDF in Python – step‑by‑step guide
  type: TechArticle
- description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  name: Convert HTML to PDF in Python – step‑by‑step guide
  steps:
  - name: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
    text: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
  - name: '**Input handling** – read the HTML file or build the markup programmatically.'
    text: '**Input handling** – read the HTML file or build the markup programmatically.'
  - name: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
    text: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
  type: HowTo
tags:
- HTML to PDF
- Python
- Document conversion
title: PythonでHTMLをPDFに変換する – ステップバイステップガイド
url: /ja/python/general/convert-html-to-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでHTMLをPDFに変換 – ステップバイステップガイド

HTML を **PDF に変換** したい場合、このチュートリアルでは Python での完全なソリューションを示します。HTML から PDF を生成し、HTML を PDF として保存し、コードから離れることなく変換プロセスを制御する方法が分かります。

本ガイドでは、信頼できるライブラリのインストール、HTML ドキュメントの読み込み、変換の実行、結果の検証までを順に解説します。最終的には、静的ページでも動的に生成されたマークアップでも、任意の Python プロジェクトで HTML ファイルから PDF を作成できるようになります。

## 学べること

* HTML‑to‑PDF 変換に必要な `pdfkit` と `wkhtmltopdf` の依存関係をインストールする方法。  
* ディスク上または文字列から HTML ドキュメントを読み込む方法。  
* カスタムページサイズ、余白、エンコーディングオプションを指定して HTML から PDF を生成する方法。  
* ワンライナーで HTML を PDF として保存する方法。  
* アセットの欠如、Unicode 文字、大容量ファイルなど、典型的なエッジケースへの対処方法。  

**前提条件** – Python 3.8 以上と基本的なファイル I/O の知識。外部サービスは不要です。

## HTML を PDF に変換する全体フロー

変換プロセスは次の 3 つの論理フェーズで構成されます。

1. **準備** – コンバータをインストールし、`wkhtmltopdf` バイナリが参照可能であることを確認する。  
2. **入力処理** – HTML ファイルを読み込むか、プログラムでマークアップを構築する。  
3. **出力生成** – コンバータを呼び出し、PDF ファイルを書き出し、結果を確認する。

各フェーズは以下のステップで詳しく解説します。

## ステップ 1: 必要なライブラリをインストール

`pdfkit` は広く使われている `wkhtmltopdf` エンジンの薄い Python ラッパーです。`pip` で両方をインストールし、バイナリのパスを確認します。

```bash
# Install the Python wrapper
pip install pdfkit

# On Ubuntu/Debian install wkhtmltopdf package
sudo apt-get install wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf
```

ポータブルバイナリを使用したい場合は、[wkhtmltopdf GitHub ページ](https://github.com/wkhtmltopdf/wkhtmltopdf/releases)から適切なリリースをダウンロードし、`PATH` に追加したディレクトリに配置してください。スクリプトは後で自動的にパスをチェックします。

## ステップ 2: HTML ドキュメントを読み込む

静的ファイルを読む、リモートコンテンツを取得する、またはその場で HTML を構築することができます。以下の例は、任意のディレクトリにある `sample.html` というローカルファイルを読み込む方法を示しています。

```python
import pathlib
import pdfkit

# Define the directory that holds the HTML source
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")

# Resolve the full path to the HTML file
html_path = BASE_DIR / "sample.html"

# Read the file content as a UTF‑8 string
with html_path.open(encoding="utf-8") as f:
    html_content = f.read()
```

ファイルを Unicode 文字列として読み込むことで、 “é”、 “ß”、 またはアジア系文字などが変換中に保持されます。国際化テキストを含む **HTML から PDF を生成** する際に必須のステップです。

## ステップ 3: HTML から PDF を生成

`pdfkit.from_string` は HTML マークアップを含む文字列を PDF ファイルに変換します。ページサイズ、余白、ヘッダー/フッターの動作を制御するオプション辞書を渡すことができます。

```python
# Define the output PDF path
pdf_path = BASE_DIR / "sample.pdf"

# Conversion options – adjust as needed
options = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left": "0.75in",
    "encoding": "UTF-8",
    "enable-local-file-access": None,  # Allows loading local images/CSS
}

# Perform the conversion
pdfkit.from_string(html_content, str(pdf_path), options=options)
```

上記の呼び出しは `sample.pdf` に **HTML ファイルから PDF を作成** します。ソース HTML がローカルの CSS や画像を参照している場合、`enable‑local‑file‑access` フラグにより `wkhtmltopdf` がそれらのリソースを解決できるようになります。

### このアプローチが有効な理由

* `pdfkit` は重い処理を `wkhtmltopdf` に委譲し、WebKit エンジンで HTML をレンダリングするため、元のレイアウトと高い忠実度が保証されます。  
* オプション辞書を提供することで、HTML 自体を変更せずに出力を細かく調整できます。  
* `from_string` を使用するとメモリ上で完結でき、HTML がその場で生成される場合に便利です。

## ステップ 4: HTML を PDF として保存し、出力を検証

変換後、PDF が存在し読み取り可能か確認したいことがあります。以下のスニペットはファイルサイズをチェックし、デフォルトのシステムビューアで PDF を開きます（プラットフォーム固有）。

```python
import os
import subprocess
import sys

# Verify that the PDF file was created
if pdf_path.is_file() and pdf_path.stat().st_size > 0:
    print(f"✅ PDF generated successfully: {pdf_path}")

    # Open the PDF for visual verification (optional)
    if sys.platform.startswith("darwin"):      # macOS
        subprocess.run(["open", str(pdf_path)])
    elif os.name == "nt":                      # Windows
        os.startfile(str(pdf_path))
    else:                                      # Linux and others
        subprocess.run(["xdg-open", str(pdf_path)])
else:
    raise FileNotFoundError("PDF generation failed – file not found or empty.")
```

スクリプトを実行すると成功メッセージが表示され、PDF ビューアが起動してレイアウトが元の HTML と一致しているか即座に確認できます。このステップで **HTML を PDF として保存** のサイクルが完了します。

## ステップ 5: 高度なオプション – カスタム設定で HTML ファイルから PDF を作成

ディスク上に実体のある HTML ファイルがあり、内容を自前で読み込む代わりに `pdfkit.from_file` を使いたい場合があります。このメソッドは、HTML がすでに複雑な相対パスを含んでいるときに便利です。

```python
# Directly convert a file path to PDF
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

`options` 辞書を拡張することで、表紙ページ、目次、JavaScript 実行フラグなども埋め込めます。例として表紙ページを追加する方法を示します。

```python
options.update({
    "cover": str(BASE_DIR / "cover.html"),
    "toc": None,  # Generates a table of contents
})
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

これらの調整は、より高度な出版パイプライン向けに **HTML を PDF に変換** する方法を示しています。

## よくある落とし穴と回避策

| 問題 | 原因 | 対策 |
|------|------|------|
| 画像や CSS が表示されない | `wkhtmltopdf` がデフォルトでローカルファイルアクセスをブロックする | `options` 辞書に `"enable-local-file-access": None` を追加 |
| Unicode 文字が文字化けする | `encoding` オプションが欠如、または誤った文字コードでファイルを読み込んでいる | 常に `"encoding": "UTF-8"` を設定し、UTF‑8 で HTML を読み込む |
| PDF が空白になる | `wkhtmltopdf` バイナリへのパスが誤っている | パスを明示的に指定: `pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")` |
| 大容量 HTML がタイムアウトする | デフォルトのタイムアウトが短すぎる | `"javascript-delay": "2000"` を設定するか、`"timeout": "60"` でタイムアウトを延長 |

これらの対策を行うことで、さまざまな環境でも **HTML から PDF を生成** するプロセスが安定します。

## フルスクリプト – エンドツーエンド例

以下を `html_to_pdf.py` として保存し、`python html_to_pdf.py` で実行してください。`YOUR_DIRECTORY` をプロジェクトフォルダに合わせて変更します。

```python
#!/usr/bin/env python3
"""
Convert HTML to PDF in Python – complete, runnable example.
"""

import pathlib
import pdfkit
import os
import subprocess
import sys

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")          # <-- change this
HTML_FILE = BASE_DIR / "sample.html"
PDF_FILE = BASE_DIR / "sample.pdf"

# wkhtmltopdf configuration (optional – only needed if binary is not on PATH)
# config = pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")

# Conversion options – customize as required
OPTIONS = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left":


## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示したテクニックを基にした、密接に関連するトピックをカバーしています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [How to Convert HTML to PDF Java - Set Page Margins with Aspose.HTML](/html/english/java/advanced-usage/css-extensions-adding-title-page-number/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}