---
category: general
date: 2026-10-28
description: PythonでHTMLをMarkdownに変換：HTMLからリンクを抽出し、GitLab 風のMarkdownとして保存する方法をたった3ステップで学ぶ。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- how to convert html document
language: ja
lastmod: 2026-10-28
og_description: PythonでHTMLをMarkdownに素早く変換。この記事では、HTMLからリンクを抽出し、GitLab 風のMarkdownを3つの簡単な手順で作成する方法を紹介します。
og_image_alt: Screenshot of Python script converting HTML to GitLab‑flavored Markdown
  with extracted links
og_title: HTMLをMarkdownに変換し、Pythonでリンクを抽出する
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: 'convert html to markdown using Python: learn to extract links from
    HTML and save as GitLab‑flavored Markdown in just three steps.'
  headline: How to convert HTML to Markdown and extract links in Python
  type: TechArticle
- description: 'convert html to markdown using Python: learn to extract links from
    HTML and save as GitLab‑flavored Markdown in just three steps.'
  name: How to convert HTML to Markdown and extract links in Python
  steps:
  - name: Multiple input sources
    text: 'If you need to batch‑process a folder of HTML files, wrap the conversion
      in a loop:'
  - name: Missing links
    text: When an HTML document contains no `<a>` elements, the converter still creates
      a valid Markdown file containing only the permitted paragraphs. No additional
      error handling is required, but you can check `save_options.features` if you
      need to enforce the presence of links.
  - name: Custom output encoding
    text: 'If your target system expects UTF‑8 with a BOM, set the encoding on the
      `MarkdownSaveOptions`:'
  type: HowTo
tags:
- HTML
- Markdown
- Python
- Conversion
title: PythonでHTMLをMarkdownに変換し、リンクを抽出する方法
url: /ja/python/general/how-to-convert-html-to-markdown-and-extract-links-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML を Markdown に変換し、Python でリンクを抽出する方法

HTML を **Markdown に変換** する必要がある場合、このチュートリアルは完全な、すぐに実行できるソリューションを提供します。HTML からリンクを抽出し、GitLab 風の Markdown フォーマッタを選択し、数行のコードだけで結果を保存する方法が分かります。

このガイドでは、必要なパッケージ、さまざまなソースからの HTML の読み込み、`MarkdownSaveOptions` の設定、リンクが欠如している場合やカスタム出力ディレクトリなどのエッジケースの処理と、必要なすべてを網羅しています。最後まで読むと、*HTML ドキュメントをどのようにクリーンでリンクが豊富な Markdown に変換するか* という質問に答えられるようになります。

## 前提条件

- Python 3.8 以上
- `aspose-html` パッケージ（Python 用公式 Aspose.HTML ライブラリ）
- Python スクリプトとファイル I/O の基本的な知識

以下のコマンドでライブラリをインストールできます:

```bash
pip install aspose-html
```

> **プロのコツ:** 依存関係を分離するために仮想環境を使用してください。

## ステップ 1: HTML コンテンツを読み込む

最初のステップは `HTMLDocument` オブジェクトを作成することです。Aspose.HTML は文字列、ファイルパス、または URL を受け付けるため、プロジェクトに合ったソースを選択できます。

```python
from aspose.html import HTMLDocument

# Example 1: Load from a raw HTML string
html_string = "<h1>Title</h1><p>Sample <a href='https://example.com'>link</a></p>"
html_doc = HTMLDocument(html_string)

# Example 2: Load from a local file
# html_doc = HTMLDocument("input.html")

# Example 3: Load from a remote URL
# html_doc = HTMLDocument("https://www.example.com")
```

> **重要な理由:** ドキュメントを一度読み込むことで、コンバータが走査できる DOM に似たオブジェクトが得られ、すべてのリンクと段落ノードが抽出可能になります。

## ステップ 2: Markdown 保存オプションを設定する

`MarkdownSaveOptions` を使用すると、出力形式や変換する HTML 機能を制御できます。段落を保持しながら **HTML からリンクを抽出** するには、`LINK` と `PARAGRAPH` 機能を有効にし、GitLab フォーマッタを選択します。

```python
from aspose.html import MarkdownSaveOptions

save_options = MarkdownSaveOptions()
# Use GitLab‑flavored Markdown (supports task lists, tables, etc.)
save_options.formatter = MarkdownSaveOptions.Formatter.GIT

# Export only links and paragraphs – other tags (e.g., images) are ignored
save_options.features = (
    MarkdownSaveOptions.Features.LINK |
    MarkdownSaveOptions.Features.PARAGRAPH
)
```

> **重要な理由:** 機能を限定することで出力のノイズが減り、生成された Markdown に必要な要素だけが含まれることが保証されます。ドキュメントパイプラインや静的サイトジェネレータに最適です。

## ステップ 3: HTML ドキュメントを変換し、ファイルに書き込む

次に `Converter.convert_html` を呼び出し、ドキュメント、オプション、出力先パスを渡します。

```python
from aspose.html import Converter

output_path = "output.md"  # Change to your desired directory/file name
Converter.convert_html(html_doc, save_options, output_path)
print(f"Markdown file saved to {output_path}")
```

スクリプトを実行すると、以下の内容の `output.md` ファイルが生成されます:

```markdown
# Title

Sample [link](https://example.com)
```

見てみると、見出し、段落、リンクだけが出力されており、`save_options` の設定通りになっています。

## 一般的なバリエーションとエッジケースの処理

### 複数の入力ソース

HTML ファイルが入ったフォルダをバッチ処理したい場合は、変換処理をループで囲みます:

```python
import pathlib
from aspose.html import HTMLDocument, MarkdownSaveOptions, Converter

input_folder = pathlib.Path("html_inputs")
output_folder = pathlib.Path("markdown_outputs")
output_folder.mkdir(exist_ok=True)

options = MarkdownSaveOptions()
options.formatter = MarkdownSaveOptions.Formatter.GIT
options.features = (
    MarkdownSaveOptions.Features.LINK |
    MarkdownSaveOptions.Features.PARAGRAPH
)

for html_path in input_folder.glob("*.html"):
    doc = HTMLDocument(str(html_path))
    md_path = output_folder / (html_path.stem + ".md")
    Converter.convert_html(doc, options, str(md_path))
    print(f"Converted {html_path.name} → {md_path.name}")
```

### リンクが欠如している場合

HTML ドキュメントに `<a>` 要素が全く含まれていない場合でも、コンバータは許可された段落だけを含む有効な Markdown ファイルを作成します。追加のエラーハンドリングは不要ですが、リンクの存在を強制したい場合は `save_options.features` を確認できます。

### カスタム出力エンコーディング

対象システムが BOM 付き UTF‑8 を期待する場合は、`MarkdownSaveOptions` のエンコーディングを設定します:

```python
save_options.encoding = "utf-8-sig"
```

## 完全な実行可能例

すべてをまとめると、以下のようにコピー＆ペーストしてすぐに実行できる単体スクリプトになります:

```python
# convert_html_to_markdown.py
# -------------------------------------------------
# Demonstrates how to convert HTML to Markdown while
# extracting only links and paragraphs using Aspose.HTML.
# -------------------------------------------------

from aspose.html import HTMLDocument, MarkdownSaveOptions, Converter

def main():
    # 1️⃣ Load HTML – replace this with your own source if needed
    html = "<h1>Title</h1><p>Sample <a href='https://example.com'>link</a></p>"
    document = HTMLDocument(html)

    # 2️⃣ Configure Markdown options (GitLab flavor, links + paragraphs only)
    options = MarkdownSaveOptions()
    options.formatter = MarkdownSaveOptions.Formatter.GIT
    options.features = (
        MarkdownSaveOptions.Features.LINK |
        MarkdownSaveOptions.Features.PARAGRAPH
    )

    # 3️⃣ Convert and save
    output_file = "output.md"
    Converter.convert_html(document, options, output_file)
    print(f"✅ Markdown saved to {output_file}")

if __name__ == "__main__":
    main()
```

以下のコマンドで実行します:

```bash
python convert_html_to_markdown.py
```

`output.md` に期待通りの Markdown 表現が出力されているのが確認できます。

## 結論

これで、Python で **HTML を Markdown に変換** し、HTML からリンクを抽出し、`MarkdownSaveOptions` で出力形式を制御する方法が分かりました。この手法は単一ファイル、バッチ、あるいはリモート URL にも対応でき、ドキュメントジェネレータ、静的サイトパイプライン、データ抽出スクリプトの柔軟な基盤となります。

**次のステップ**

- `TABLE` や `IMAGE` など、他の `MarkdownSaveOptions.Features` を試して、より多くの HTML 要素を含めてみましょう。
- 厳密な CommonMark 準拠が必要な場合は、フォーマッタを `MarkdownSaveOptions.Formatter.CommonMark` に切り替えてください。
- この変換を静的サイトジェネレータ（例: MkDocs）と組み合わせて、コンテンツ公開を自動化しましょう。

コーディングを楽しんでください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [HTML を Markdown に変換（Python） – リンクと段落を抽出](/html/english/python/general/convert-html-to-markdown-python-extract-links-paragraphs/)
- [Python で HTML を Markdown に変換 – GitLab 風ガイド](/html/english/python/general/convert-html-to-markdown-in-python-gitlab-flavored-guide/)
- [Python で HTML を Markdown に変換 – 完全ガイド](/html/english/python/general/convert-html-to-markdown-with-python-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}