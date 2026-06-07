---
category: general
date: 2026-06-07
description: PythonでHTMLからMarkdownを素早く作成する。HTMLをMarkdownに変換する方法、エッジケースの処理、そしてHTMLからMarkdownへのPythonワークフローを自動化する方法を学びましょう。
draft: false
keywords:
- create markdown from html
- convert html to markdown
- how to convert html
- html to markdown conversion
- html to markdown python
language: ja
og_description: Python を使用して HTML から Markdown を作成します。このチュートリアルでは、HTML を Markdown に変換する方法を示し、一般的な落とし穴とベストプラクティスをカバーします。
og_title: PythonでHTMLからMarkdownを作成する – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-07'
  description: Create markdown from html quickly with Python. Learn how to convert
    html to markdown, handle edge cases, and automate the html to markdown python
    workflow.
  headline: Create Markdown from HTML in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create markdown from html quickly with Python. Learn how to convert
    html to markdown, handle edge cases, and automate the html to markdown python
    workflow.
  name: Create Markdown from HTML in Python – Full Step‑by‑Step Guide
  steps:
  - name: Why this function works
    text: '- **`pathlib.Path`** gives you OS‑independent file handling—no more fiddling
      with slashes. - **`markdownify`** does the heavy lifting of the **html to markdown
      conversion**. It respects heading levels, list nesting, and even converts `<code>`
      blocks. - The optional arguments let you tweak the output'
  - name: How this helps with **html to markdown python** projects
    text: '- **Preserves hierarchy** – subfolders stay intact, which is crucial for
      navigation‑aware static sites. - **Zero‑configuration defaults** – just point
      to the source folder and let the script do the rest. - **Extensible** – you
      can add a `post_process` callback to further clean up the Markdown (e.g.,'
  - name: 5.1 Tables
    text: '`markdownify` renders tables as pipe‑separated Markdown by default, but
      some older versions struggle with colspan/rowspan. If you hit malformed tables,
      consider a fallback to `pandas.read_html` + `to_markdown`.'
  - name: 5.2 Code Blocks with Language Hints
    text: 'HTML often uses `<pre><code class="language-python">`. `markdownify` will
      keep the code but lose the language hint. A quick post‑process step restores
      it:'
  - name: 5.3 Relative Image Paths
    text: 'If your HTML references images like `<img src="assets/img.png">`, the generated
      Markdown will keep the same relative path, which may break when the Markdown
      file lives elsewhere. Solve it by passing a `base_url` parameter to the converter:'
  type: HowTo
tags:
- markdown
- python
- html
- conversion
title: PythonでHTMLからMarkdownを作成する – 完全ステップバイステップガイド
url: /ja/python/general/create-markdown-from-html-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでHTMLからMarkdownを作成する – 完全ステップバイステップガイド

HTMLから **markdown を作成** したいことはありますか？どのライブラリを選べば良いか分からないときも多いでしょう。ドキュメント自動化パイプラインで壁にぶつかる開発者は少なくありません。良いニュースは、数行の Python だけで **html を markdown に変換** でき、テーブル、コードスニペット、Unicode 文字などのエッジケースも完全にコントロールできるようになることです。

このガイドでは、適切なパッケージのインストールから、厄介なマークアップの処理まで、すべてを順を追って解説します。コードは読みやすく、出力はクリーンに保ちます。最後まで読めば、 “**html をどうやって変換するか**” と自信を持って答えられ、 **html to markdown python** のプロセスを任意の CI/CD ワークフローに組み込めるようになります。

## 学べること

- **html to markdown conversion** 用の軽量ライブラリをインストール・設定する方法。  
- HTML ファイルを受け取り、Markdown ファイルを出力する再利用可能な関数を書く方法。  
- 入れ子リスト、相対画像 URL、HTML エンティティなど、一般的な落とし穴への対処法。  
- 複数の HTML ファイルがあるディレクトリ全体をバッチ処理する方法の拡張。

Markdown ライブラリの事前知識は不要です。Python 3 が動作すれば、きれいなドキュメント作成への好奇心さえあれば始められます。

## 前提条件

| 要件 | なぜ重要か |
|------|------------|
| Python 3.8 以降 | `markdownify` パッケージとの互換性が保証されます。 |
| `pip`（Python パッケージマネージャ） | サードパーティライブラリのインストールに必要です。 |
| 小さな HTML ファイル（例：`input.html`） | **html to markdown conversion** デモ用の具体的な入力ソースを提供します。 |

Python がすでにセットアップ済みなら、すぐに始められます。

## Step 1 – `markdownify` パッケージをインストール

**HTML から markdown を作成** するために、人気の `markdownify` ライブラリを使用します。サイズが小さく、純粋な Python 実装で、ほとんどの HTML タグをデフォルトで処理します。

```bash
pip install markdownify
```

> **プロのコツ:** 仮想環境内で作業している場合（強く推奨）、まず仮想環境を有効化してください。これにより、他のプロジェクトとのバージョン衝突を防げます。

## Step 2 – シンプルなコンバータ関数を書く

以下は、HTML ファイルを読み込み、変換し、結果を Markdown ファイルに書き出す、完全に実行可能なスクリプトです。関数は意図的に小さく作られているので、どんなプロジェクトにもすぐに組み込めます。

```python
# convert_html_to_md.py
import pathlib
from markdownify import markdownify as md

def create_markdown_from_html(
    html_path: pathlib.Path,
    markdown_path: pathlib.Path,
    *,
    heading_style: str = "ATX",   # ATX => # Heading, Setext => Underline style
    strip: bool = True,
    convert_links: bool = True,
) -> None:
    """
    Convert an HTML document to Markdown.

    Parameters
    ----------
    html_path : pathlib.Path
        Path to the source HTML file.
    markdown_path : pathlib.Path
        Destination path for the generated .md file.
    heading_style : str, optional
        Either "ATX" (default) or "Setext". Controls how headings are rendered.
    strip : bool, optional
        Remove leading/trailing whitespace from the output.
    convert_links : bool, optional
        Preserve <a> tags as Markdown links when True.

    Returns
    -------
    None
    """
    # 1️⃣ Load the source HTML document
    raw_html = html_path.read_text(encoding="utf-8")

    # 2️⃣ Convert HTML to Markdown using markdownify's options
    markdown_text = md(
        raw_html,
        heading_style=heading_style,
        strip=strip,
        convert_links=convert_links,
    )

    # 3️⃣ Save the result to the target file
    markdown_path.write_text(markdown_text, encoding="utf-8")
    print(f"✅ {html_path.name} → {markdown_path.name} completed.")
```

### この関数が機能する理由

- **`pathlib.Path`** は OS に依存しないファイル操作を提供し、スラッシュの扱いに悩む必要がなくなります。  
- **`markdownify`** が **html to markdown conversion** の重い作業を担当します。見出しレベル、リストの入れ子、さらには `<code>` ブロックまで正しく変換します。  
- オプション引数により、コアロジックに手を加えずに出力を微調整でき、特定プラットフォーム向けに別の見出しスタイルが必要なときに便利です。

## Step 3 – 単一ファイルでコンバータを実行

スクリプトと同じフォルダに小さな `input.html` を作成します:

```html
<!-- input.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Sample Document</title>
</head>
<body>
  <h1>Welcome to the Demo</h1>
  <p>This paragraph contains <strong>bold</strong> and <em>italic</em> text.</p>
  <ul>
    <li>First item</li>
    <li>Second item with <a href="https://example.com">a link</a></li>
  </ul>
  <pre><code>print("Hello, world!")</code></pre>
</body>
</html>
```

次に、短いドライバースクリプトから関数を呼び出します:

```python
# run_converter.py
from pathlib import Path
from convert_html_to_md import create_markdown_from_html

if __name__ == "__main__":
    src = Path("input.html")
    dst = Path("output.md")
    create_markdown_from_html(src, dst)
```

`python run_converter.py` を実行すると、`output.md` が生成され、以下の内容が出力されます:

```markdown
# Welcome to the Demo

This paragraph contains **bold** and *italic* text.

- First item
- Second item with [a link](https://example.com)

```python
print("Hello, world!")
```
```

> **何が起きたのか？** スクリプトは **HTML から markdown を作成** し、元の HTML を `markdownify` に渡すことで、元の構造を保持したクリーンな Markdown を返しました。

## Step 4 – ディレクトリ全体をバッチ処理

実務では、数十から数百の HTML ファイル（エクスポートされた Confluence ページ、レガシードキュメント、静的サイトジェネレータなど）を扱うことが一般的です。以下のスニペットは、前述の関数を拡張し、ディレクトリツリーを走査して自動的にすべて変換します。

```python
# batch_convert.py
import pathlib
from convert_html_to_md import create_markdown_from_html

def batch_convert_html_to_md(
    source_dir: pathlib.Path,
    target_dir: pathlib.Path,
    *,
    pattern: str = "*.html"
) -> None:
    """
    Walk `source_dir`, convert each HTML file to Markdown,
    and preserve the original folder structure inside `target_dir`.
    """
    for html_file in source_dir.rglob(pattern):
        # Preserve sub‑folder layout
        relative_path = html_file.relative_to(source_dir).with_suffix(".md")
        markdown_file = target_dir / relative_path
        markdown_file.parent.mkdir(parents=True, exist_ok=True)

        create_markdown_from_html(html_file, markdown_file)

    print(f"✅ Batch conversion complete: {source_dir} → {target_dir}")

if __name__ == "__main__":
    batch_convert_html_to_md(
        source_dir=pathlib.Path("html_docs"),
        target_dir=pathlib.Path("markdown_docs")
    )
```

### **html to markdown python** プロジェクトでの活用方法

- **階層を保持** – サブフォルダがそのまま残るため、ナビゲーション対応の静的サイトにとって重要です。  
- **設定不要のデフォルト** – ソースフォルダを指定すれば、残りはスクリプトが自動で処理します。  
- **拡張性** – `post_process` コールバックを追加して、Markdown のさらなるクリーンアップ（例：画像 URL の置換）を行えます。

## Step 5 – エッジケースの処理

`markdownify` は多くの場合で十分に機能しますが、いくつかの HTML パターンは追加の注意が必要です。以下に一般的な落とし穴とその対処法を示します。

### 5.1 テーブル

`markdownify` はデフォルトでテーブルをパイプ区切りの Markdown に変換しますが、古いバージョンでは colspan/rowspan に対応できないことがあります。テーブルが崩れる場合は、`pandas.read_html` と `to_markdown` の組み合わせをフォールバックとして検討してください。

```python
import pandas as pd

def table_to_markdown(html_table: str) -> str:
    df = pd.read_html(html_table)[0]   # grabs the first table
    return df.to_markdown(index=False)
```

この処理は、HTML 文字列を正規表現で前処理し、`<table>` ブロックを抽出して関数の出力に置き換えることでコンバータに組み込めます。

### 5.2 言語ヒント付きコードブロック

HTML では `<pre><code class="language-python">` のように言語情報が付与されることがありますが、`markdownify` はコードは保持するものの言語ヒントを失います。簡単なポストプロセスで言語ヒントを復元できます:

```python
import re

def add_language_hints(md_text: str) -> str:
    pattern = r"```(\n)(.+?)```"
    return re.sub(pattern, r"```python\1\2```", md_text, flags=re.DOTALL)
```

ディスクに書き込む前に、結果に対して `add_language_hints` を呼び出してください。

### 5.3 相対画像パス

HTML が `<img src="assets/img.png">` のように画像を参照している場合、生成された Markdown も同じ相対パスを保持します。Markdown ファイルが別の場所に置かれるとパスが壊れる可能性があります。コンバータに `base_url` パラメータを渡すことで解決できます:

```python
def create_markdown_from_html(..., base_url: str = ""):
    # inside the function, after markdownify:
    if base_url:
        md_text = md_text.replace("](", f"]({base_url}")
    # then write out
```

資産がホストされる場所が分かっているときは、`base_url="https://mycdn.example.com/"` を設定してください。

## Step 6 – 出力の検証

簡単なサニティチェックを行うだけで、後々のデバッグ時間を大幅に削減できます。以下は、Markdown ファイルが空でなく、少なくとも1つの見出しを含んでいることをアサートする小さなヘルパーです。

```python
def verify_markdown(md_path: pathlib.Path) -> bool:
    content = md_path.read_text(encoding="utf-8")
    if not content.strip():
        raise ValueError("Generated Markdown is empty.")
    if not any(line.startswith("#") for line in content.splitlines()):
        raise ValueError("No top‑level heading found.")
    return True
```

統合

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックをカバーしています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [Aspose.HTML for Java で HTML を Markdown に変換](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Aspose.HTML を使用した .NET で HTML を Markdown に変換](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Markdown から HTML へ Java - Aspose.HTML で変換](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}