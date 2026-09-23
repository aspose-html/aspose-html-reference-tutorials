---
category: general
date: 2026-09-23
description: Pythonを使ってHTMLファイルの要素テキストを変更する。HTMLファイルの読み込み方法、titleタグの編集、HTMLタイトルの効率的な更新方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change element text
- how to change title
- edit title tag
- load html file
- update html title
language: ja
lastmod: 2026-09-23
og_description: Python を使用して HTML ドキュメントの要素テキストを変更する。このチュートリアルでは、HTML ファイルの読み込み、title
  タグの編集、そして数行のコードで HTML のタイトルを更新する方法を示します。
og_image_alt: Screenshot showing change element text in HTML using Python code
og_title: PythonでHTMLの要素テキストを変更する – クイックガイド
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Change element text in an HTML file using Python. Learn how to load
    HTML file, edit title tag, and update HTML title efficiently.
  headline: Change element text in HTML with Python – step‑by‑step guide
  type: TechArticle
- description: Change element text in an HTML file using Python. Learn how to load
    HTML file, edit title tag, and update HTML title efficiently.
  name: Change element text in HTML with Python – step‑by‑step guide
  steps:
  - name: 'Edge case: Multiple `<title>` tags'
    text: 'HTML standards allow only one `<title>` element, but malformed files sometimes
      contain more. If you need to handle that situation, iterate over all matches:'
  - name: Editing other elements (e.g., `<h1>`)
    text: 'If you need to **change element text** for a heading instead of the title,
      adjust the XPath:'
  - name: Preserving existing whitespace
    text: 'When the original HTML uses indentation inside tags, `pretty_print` may
      reformat it. To keep the original formatting, omit `pretty_print`:'
  - name: Working with Unicode characters
    text: '`lxml` handles Unicode automatically. Ensure the source file is saved with
      UTF‑8 encoding; otherwise, specify the correct encoding when opening the file.'
  type: HowTo
tags:
- Python
- HTML manipulation
- Web scraping
title: PythonでHTMLの要素テキストを変更する – ステップバイステップガイド
url: /ja/python/general/change-element-text-in-html-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML の要素テキストを Python で変更する – ステップバイステップガイド

HTML ドキュメント内の **要素テキストを変更** したい場合、このガイドでは Python を使って正確に行う方法を示します。古くなった `<title>` タグを修正する場合でも、他の要素を更新する場合でも、**HTML ファイルの読み込み**、テキストの変更、そして **HTML タイトルの更新**（または任意の要素）を安全に行う方法を学べます。

ウェブページのタイトルを変更することは、スクレイピングしたデータのクリーンアップ、静的サイトページの生成、SEO 更新の自動化などでよくある作業です。このチュートリアルでは以下を行います。

* ディスク上の HTML ファイルを読み込む。
* `<title>` 要素を見つけて **title タグを編集**。
* 変更後のドキュメントを保存し、実質的に **HTML タイトルを更新**。

必要なコードはすべて掲載されており、各ステップでは **何を入力するか** だけでなく、**なぜその操作が重要か** も解説します。

## 前提条件

開始する前に、以下がインストールされていることを確認してください。

* Python 3.9 以上
* `lxml` ライブラリ（`pip install lxml`）  
  `lxml` は高速で標準に準拠した HTML パースと操作を提供します。
* 編集したい HTML ファイルが格納されたディレクトリ（`YOUR_DIRECTORY` を実際のパスに置き換えてください）

## 手順 1: HTML ファイルを読み込む

最初のステップは **HTML ファイルを読み込み**、Python が操作できる DOM（Document Object Model）ツリーに変換することです。`lxml.html` を使用すると XPath が利用でき、要素の取り扱いが信頼性の高いものになります。

```python
from pathlib import Path
from lxml import html

# Path to the source HTML document
source_path = Path("YOUR_DIRECTORY/page.html")

# Parse the file into an HTML tree
doc = html.parse(str(source_path))
```

**この操作が重要な理由:**  
パースによりページの構造化された表現が生成され、要素を直接クエリできるようになります。ファイルを読み込まずに生の文字列で作業すると、エラーが発生しやすく **要素テキストの変更** が安全に行えません。

## 手順 2: `<title>` 要素を見つけて **要素テキストを変更**

ドキュメントがロードされたら、**title タグを編集** できます。XPath 式 `".//title"` はドキュメント階層内の最初の `<title>` 要素を取得します。

```python
# Find the <title> element (the first occurrence)
title_elem = doc.find(".//title")

# Guard against missing <title>
if title_elem is None:
    raise ValueError("The document does not contain a <title> element.")

# Change the text inside the <title> tag
title_elem.text = "New Title"
```

**この操作が重要な理由:**  
`title_elem.text` に直接代入することで、周囲のマークアップを変更せずに **要素テキストを変更** できます。この方法は空白、コメント、他のタグを保持し、出力が有効な HTML であり続けることを保証します。

### 例外ケース: 複数の `<title>` タグがある場合

HTML 標準では `<title>` 要素は一つだけですが、破損したファイルでは複数存在することがあります。そのような状況に対処するには、すべてのマッチに対して反復処理します。

```python
for t in doc.findall(".//title"):
    t.text = "New Title"
```

## 手順 3: 変更後のドキュメントを保存 – **HTML タイトルを更新**

変更が完了したら、ツリーをディスクに書き戻します。`pretty_print=True` を指定すると、ファイルが読みやすい形で保存されます。

```python
# Destination path for the updated file
output_path = Path("YOUR_DIRECTORY/updated.html")

# Write the updated HTML back to a file
doc.write(str(output_path), encoding="utf-8", pretty_print=True)
print(f"HTML saved to {output_path}")
```

**この操作が重要な理由:**  
保存により **要素テキストの変更** が反映された新しいファイルが生成されます。元のファイルを上書きしたい場合は、`output_path` に同じパスを指定すれば完了です。

## すべてを一つのブロックにまとめた完全スクリプト

以下は **HTML ファイルの読み込み**、**要素テキストの変更**、そして **HTML タイトルの更新** を行う、自己完結型スクリプトです。

```python
"""Change element text in an HTML document – update the <title> tag."""

from pathlib import Path
from lxml import html

def change_title(source: str, new_title: str, destination: str) -> None:
    """Load an HTML file, edit its title, and save the result."""
    # Load the HTML document
    doc = html.parse(source)

    # Locate the <title> element
    title_elem = doc.find(".//title")
    if title_elem is None:
        raise ValueError("No <title> element found in the document.")

    # Change element text
    title_elem.text = new_title

    # Save the updated document
    doc.write(destination, encoding="utf-8", pretty_print=True)

if __name__ == "__main__":
    src = "YOUR_DIRECTORY/page.html"
    dst = "YOUR_DIRECTORY/updated.html"
    change_title(src, "New Title", dst)
    print(f"Updated title saved to {dst}")
```

このスクリプトを実行すると、`updated.html` が生成され、`<title>` が **New Title** に置き換わります。

## 手法の一般的なバリエーション

### 他の要素を編集する（例: `<h1>`）

タイトルではなく見出しのテキストを **要素テキストを変更** したい場合は、XPath を調整します。

```python
heading = doc.find(".//h1")
if heading is not None:
    heading.text = "Updated Heading"
```

### 既存の空白を保持する

元の HTML がタグ内部でインデントされている場合、`pretty_print` が再フォーマットしてしまうことがあります。元のフォーマットを保持したいときは `pretty_print` を省略してください。

```python
doc.write(destination, encoding="utf-8")
```

### Unicode 文字の取り扱い

`lxml` は Unicode を自動的に処理します。ソースファイルが UTF‑8 で保存されていることを確認してください。別のエンコーディングで保存されている場合は、ファイルを開く際に適切なエンコーディングを指定します。

## プロのコツと落とし穴

* **プロのコツ:** 要素を変更せずにテキストだけが必要な場合は `doc.xpath("//title/text()")` を使用します。  
* **注意点:** `<svg>` などの非 HTML 名前空間内に `<title>` が含まれる HTML ファイルがあります。そのようなケースでは XPath を絞り、`doc.find(".//head/title")` のように `<head>` セクションを対象にしてください。  
* **パフォーマンスのコツ:** 数千ファイルをバッチ処理する場合、同じパーサーインスタンスを再利用してオーバーヘッドを削減します。

## 結論

これで Python を使って HTML ドキュメント内の **要素テキストを変更** する方法、具体的には **HTML ファイルの読み込み**、**title タグの編集**、そして **HTML タイトルの更新** が分かりました。完全な例は、整形式でも多少破損している HTML でも信頼できるライブラリベースのアプローチを示しています。

ここからは次のように応用できます。

* 同様のパターンを他のタグ（`<h2>`、`<meta>` など）に適用する。  
* このスクリプトをウェブスクレイピングパイプラインに組み込み、大量のページを一括でクリーンアップする。  
* `lxml` の豊富な API を活用し、属性操作、CSS セレクタ、HTML シリアライズなどを探求する。

Happy coding, and feel free to experiment with different elements to master HTML manipulation in Python!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法に基づく関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、API の追加機能を習得したり、代替実装アプローチを自分のプロジェクトで試したりするのに役立ちます。

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Parse HTML Java – Load, Query & Count Elements](/html/english/java/creating-managing-html-documents/how-to-parse-html-java-load-query-count-elements/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}