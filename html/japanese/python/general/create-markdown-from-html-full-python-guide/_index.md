---
category: general
date: 2026-06-07
description: HTMLからマークダウンを素早く作成する。PythonでHTMLをマークダウンに変換する方法、HTMLをマークダウンにエクスポートする方法、そしてエッジケースを処理する方法を学びましょう。
draft: false
keywords:
- create markdown from html
- convert html to markdown
- how to convert html
- html to markdown python
- export html to markdown
language: ja
og_description: PythonでHTMLからMarkdownを作成する。このガイドでは、HTMLをMarkdownに変換する方法、HTMLをMarkdownにエクスポートする方法、そして一般的な落とし穴への対処方法を示します。
og_title: HTMLからMarkdownを作成 – 完全なPythonチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-07'
  description: Create markdown from HTML quickly. Learn how to convert HTML to markdown
    in Python, export html to markdown and handle edge cases.
  headline: Create markdown from HTML – Full Python Guide
  type: TechArticle
- description: Create markdown from HTML quickly. Learn how to convert HTML to markdown
    in Python, export html to markdown and handle edge cases.
  name: Create markdown from HTML – Full Python Guide
  steps:
  - name: 1. Tables That Look Wonky
    text: '`markdownify` converts `<table>` tags into pipe‑separated Markdown tables.
      However, if your source HTML uses `colspan` or `rowspan`, the conversion may
      lose alignment. A quick fix is to pre‑process the HTML with **BeautifulSoup**:'
  - name: 2. Code Blocks Need Fencing
    text: 'If the HTML contains `<pre><code>` blocks, `markdownify` will output them
      as indented blocks, which some Markdown parsers misinterpret. Pass the option
      `code_language="python"` (or whatever language you expect) to force fenced code
      blocks:'
  - name: 3. Unicode and Emojis
    text: 'Python’s default UTF‑8 handling usually does the trick, but if you encounter
      mojibake, explicitly encode/decode:'
  type: HowTo
tags:
- python
- markdown
- html
title: HTMLからMarkdownを作成する – 完全Pythonガイド
url: /ja/python/general/create-markdown-from-html-full-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML から Markdown を作成 – 完全 Python ガイド

HTML から **markdown を作成** したいけど、手間取っていませんか？ あなた一人だけではありません。ブログをスクレイピングしたり、メールを取得したり、ドキュメントを整頓したりする際に、HTML をきれいな Markdown に変換するのは、まるで野鳥追いのように感じられることがあります。

朗報です！このガイドでは、純粋な Python だけで **HTML を markdown に変換** するシンプルでエンドツーエンドな解決策をステップバイステップで解説します。各ステップの *理由* を説明し、完全に実行可能なスクリプトを提示し、HTML を markdown に確実にエクスポートするためのプロのコツも少し紹介します。

---

## このチュートリアルでカバーする内容

- **前提条件**: Python 3.9 以上、ちょっとしたサードパーティライブラリ、サンプル HTML ファイル。  
- **ステップバイステップのコード**: HTML ドキュメントを読み込み、変換オプションを設定し、結果の Markdown をディスクに書き出す方法。  
- **なぜこのアプローチが有効なのか** – 組み込みの `html2text` と、より柔軟な `markdownify` を比較します。  
- **エッジケースの処理**: テーブル、コードブロック、Unicode 文字。  
- **次のステップ**: バッチ処理、カスタムフィルタ、CI パイプラインへの統合。

この記事を読み終えると、**html を markdown にエクスポート** する自信がつき、プロジェクトに合わせてプロセスを調整する方法が理解できるようになります。

---

## 前提条件

始める前に、以下を用意してください。

1. **Python 3.9 以上** – `typing` の改善により可読性が向上します。  
2. **pip** – 標準のパッケージインストーラ。  
3. **サンプル HTML ファイル** (`input.html`) を、管理しやすいフォルダに配置。

すでに揃っていれば、次へ進みましょう。まだの場合は、`python --version` でバージョンを確認し、`pip install --upgrade pip` でインストーラを最新にしてください。

---

## 手順 1: HTML から Markdown を作成 – ファイルを読み込む

まず最初に、HTML ソースをメモリに読み込む方法が必要です。ここで主要なキーワードが登場します。

```python
# step1_load_html.py
from pathlib import Path

def load_html(file_path: str) -> str:
    """
    Reads an HTML file and returns its contents as a string.
    """
    html_path = Path(file_path)
    if not html_path.is_file():
        raise FileNotFoundError(f"HTML file not found: {file_path}")
    return html_path.read_text(encoding="utf-8")

# Example usage
html_content = load_html("YOUR_DIRECTORY/input.html")
print("✅ HTML loaded – length:", len(html_content))
```

**重要なポイント:**  
- `pathlib.Path` を使うことで OS に依存しないパス処理が可能です。  
- 明確な `FileNotFoundError` を投げることで、後で発生する謎の `NoneType` エラーを防げます。

---

## 手順 2: 適切なコンバータを選択 – HTML を変換する方法

Python にはこの作業に適したライブラリがいくつかあります。最も人気のある 2 つは次の通りです。

| ライブラリ | 長所 | 短所 |
|-----------|------|------|
| `html2text` | 高速でシンプルなページに向いている | 複雑なテーブルの処理が苦手 |
| `markdownify` | テーブル、コードブロック、カスタムコールバックに対応 | やや遅い、依存関係が増える |

バランスの取れた解決策として **markdownify** を使用します。細かい制御が可能で、**html を markdown にエクスポート** する本番パイプラインに最適です。

```bash
pip install markdownify
```

次に、変換処理を再利用可能な関数にラップします。

```python
# step2_convert.py
from markdownify import markdownify as md

def convert_html_to_markdown(html: str, **options) -> str:
    """
    Converts HTML string to Markdown using markdownify.
    Accepts any markdownify options via **options.
    """
    # Default options can be overridden by callers
    defaults = {
        "heading_style": "ATX",   # # Heading
        "bullets": "*",           # bullet list marker
        "strip": ["script", "style"],  # remove these tags
        "convert": ["a", "img", "code"],  # explicit conversion list
    }
    defaults.update(options)
    return md(html, **defaults)

# Example usage
markdown_content = convert_html_to_markdown(html_content)
print("✅ Conversion done – preview:")
print(markdown_content[:200] + "...")
```

**このアプローチの理由:**  
`markdownify` は `strip` や `convert` といったオプションを受け取れるため、どのタグを除去または変換するかを細かく指定できます。この柔軟性は、**convert html to markdown python** スクリプトで多様な入力に対応する際に重要です。

---

## 手順 3: HTML を Markdown にエクスポート – 結果を保存

Markdown 文字列が手に入ったら、最後のステップはそれをファイルに書き出すことです。ここで *export html to markdown* のフレーズが活きてきます。

```python
# step3_save.py
from pathlib import Path

def save_markdown(markdown: str, output_path: str) -> None:
    """
    Writes the Markdown string to the given file.
    Creates parent directories if they don't exist.
    """
    out_path = Path(output_path)
    out_path.parent.mkdir(parents=True, exist_ok=True)
    out_path.write_text(markdown, encoding="utf-8")
    print(f"✅ Markdown saved to {out_path}")

# Example usage
save_markdown(markdown_content, "YOUR_DIRECTORY/output.md")
```

**ヘルパー関数を作る理由:**  
I/O と変換ロジックを分離することで、コードのテストがしやすくなります。これにより、ファイルシステムに触れずに `convert_html_to_markdown` をユニットテストできるようになり、熟練開発者が推奨するパターンです。

---

## 完全エンドツーエンドスクリプト

以下は、3 つの手順をすべて組み合わせた実行可能なスクリプトです。`html_to_md.py` という名前で保存し、パスを調整した上で `python html_to_md.py` を実行してください。

```python
#!/usr/bin/env python3
"""
html_to_md.py – Convert an HTML file to Markdown and save the result.
Demonstrates how to create markdown from html, convert html to markdown,
and export html to markdown using Python.
"""

from pathlib import Path
from markdownify import markdownify as md

def load_html(file_path: str) -> str:
    html_path = Path(file_path)
    if not html_path.is_file():
        raise FileNotFoundError(f"HTML file not found: {file_path}")
    return html_path.read_text(encoding="utf-8")

def convert_html_to_markdown(html: str, **options) -> str:
    defaults = {
        "heading_style": "ATX",
        "bullets": "*",
        "strip": ["script", "style"],
        "convert": ["a", "img", "code"],
    }
    defaults.update(options)
    return md(html, **defaults)

def save_markdown(markdown: str, output_path: str) -> None:
    out_path = Path(output_path)
    out_path.parent.mkdir(parents=True, exist_ok=True)
    out_path.write_text(markdown, encoding="utf-8")
    print(f"✅ Markdown saved to {out_path}")

def main():
    # Adjust these paths to your environment
    input_html = "YOUR_DIRECTORY/input.html"
    output_md = "YOUR_DIRECTORY/output.md"

    # Load, convert, and save
    html = load_html(input_html)
    markdown = convert_html_to_markdown(html)
    save_markdown(markdown, output_md)

if __name__ == "__main__":
    main()
```

**期待される出力:** 実行後、コンソールに次のようなメッセージが表示されます。

```
✅ Markdown saved to YOUR_DIRECTORY/output.md
```

`output.md` を開くと、見出し、リスト、リンク、そして HTML にテーブルが含まれていればテーブルまで、きれいに整形された Markdown が確認できます。

---

## 一般的なエッジケースの処理

### 1. ずれやすいテーブル

`markdownify` は `<table>` タグをパイプ区切りの Markdown テーブルに変換します。ただし、元の HTML が `colspan` や `rowspan` を使用している場合、変換後の整列が崩れることがあります。簡単な対策として **BeautifulSoup** で事前に正規化しましょう。

```python
from bs4 import BeautifulSoup

def normalize_tables(html: str) -> str:
    soup = BeautifulSoup(html, "html.parser")
    for table in soup.find_all("table"):
        # Remove colspan/rowspan attributes (Markdown can't express them)
        for cell in table.find_all(["td", "th"]):
            cell.attrs.pop("colspan", None)
            cell.attrs.pop("rowspan", None)
    return str(soup)
```

`convert_html_to_markdown` に渡す前に `normalize_tables(html)` を呼び出してください。

### 2. コードブロックのフェンシング

HTML に `<pre><code>` ブロックが含まれると、`markdownify` はインデントブロックとして出力しますが、Markdown パーサによっては正しく解釈されないことがあります。`code_language="python"`（または期待する言語）オプションを渡すと、フェンス付きコードブロックに強制変換できます。

```python
markdown = convert_html_to_markdown(html, code_language="python")
```

### 3. Unicode と絵文字

Python のデフォルト UTF‑8 処理でほとんどの場合問題ありませんが、文字化けが発生した場合は明示的にエンコード/デコードを行いましょう。

```python
html = load_html(input_html).encode("utf-8", errors="ignore").decode()
```

---

## プロのコツ & 注意点

- **バッチ変換**: `main()` のロジックを `Path.glob("*.html")` でループさせ、ディレクトリ全体を処理。  
- **カスタムリンク処理**: 相対 URL を書き換える必要がある場合は、`markdownify` に `link_callback` を提供。  
- **パフォーマンス**: 数千ファイルを処理する場合は、`multiprocessing.Pool` を使って変換ステップを並列化。  
- **テスト**: 既知の出力 `.md` フィクスチャを数個用意し、変換結果と比較してアサート。CI に最適です。

---

## 結論

Python を使って **html から markdown を作成** するフルガイドを完了しました。スクリプトは HTML ドキュメントを読み込み、賢く Markdown に変換し、そして **html を markdown にエクスポート** します。ライブラリ選択、テーブル処理、安全なファイル I/O という各ステップの *なぜ* を理解したことで、実務プロジェクトでこのプロセスをスケールさせるための確固たる基盤が手に入りました。

次のチャレンジに挑戦してみませんか？このスクリプトを静的サイトジェネレータに組み込んだり、HTML ペイロードを受け取って即座に Markdown を返す小さな Flask エンドポイントを作ったり。可能性は無限大です。ぜひ実装してみてください。

質問や独自の工夫があれば、下のコメントでシェアしてください。会話を続けましょう。ハッピーコーディング！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した、密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}