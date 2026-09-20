---
category: general
date: 2026-09-19
description: PythonでHTMLファイルのタイトルを変更する方法を学びましょう。このガイドでは、HTMLの読み込み、titleタグの更新、そして変更後のHTMLの保存について解説します。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to change title
- update html title
- read html with python
- load html file python
- save modified html
language: ja
lastmod: 2026-09-19
og_description: PythonでHTMLファイルのタイトルを変更する方法。HTMLを読み込み、titleタグを更新し、変更されたドキュメントを保存する完全な例をご覧ください。
og_image_alt: Diagram showing how to change title in an HTML file using Python
og_title: Python を使って HTML ファイルのタイトルを変更する方法 – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-09-19'
  description: Learn how to change title in an HTML file with Python. This guide covers
    reading HTML, updating the title tag, and saving the modified HTML.
  headline: How to change title in an HTML file using Python
  type: TechArticle
tags:
- Python
- HTML
- Web scraping
title: Python を使って HTML ファイルのタイトルを変更する方法
url: /ja/python/general/how-to-change-title-in-an-html-file-using-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでHTMLファイルのタイトルを変更する方法

HTMLドキュメントの **タイトルの変更方法** をプログラムで行いたい場合、Pythonなら簡単に実装できます。このチュートリアルでは、HTMLファイルを読み込み、`<title>` 要素を更新し、変更後のHTMLをディスクに保存する手順を、実行可能なコードとともに解説します。

ページタイトルの変更は、静的サイトを生成したり、スクレイピングしたページをカスタマイズしたり、SEO の自動更新を行う際に頻繁に行われます。このガイドを終える頃には、**HTML タイトルの更新**、**PythonでHTMLを読む**、そして **変更したHTMLを安全に保存** する方法が身についているはずです。

## 前提条件

開始する前に、以下が揃っていることを確認してください。

- Python 3.8 以上がインストールされていること  
- `beautifulsoup4` パッケージ（`pip install beautifulsoup4`）  
- 編集したい HTML ファイル（例では任意のフォルダーにある `index.html` を使用）  

外部サービスは不要で、すべてローカルで実行できます。

## 手順 1: PythonでHTMLファイルを読み込む  

最初のタスクは **PythonでHTMLファイルを読み込む** ことです。`BeautifulSoup` を使うと、多少不完全なマークアップでも寛容にパースできます。

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Define the directory that holds the original HTML
html_dir = Path("YOUR_DIRECTORY")
original_path = html_dir / "index.html"

# Read the file contents (this is how you **read html with python**)
with original_path.open(encoding="utf-8") as f:
    html_content = f.read()

# Parse the document
soup = BeautifulSoup(html_content, "html.parser")
```

*このステップが重要な理由:*  
`BeautifulSoup` はツリー構造を構築し、文字列操作をせずに要素の検索や変更が可能になります。組み込みの `html.parser` は高速で、追加のバイナリも不要です。

## 手順 2: `<title>` 要素を取得する  

HTML 文書は通常、`<head>` 内に 1 つの `<title>` タグを持ちます。最初に見つかったものを取得すれば、**HTML タイトルの更新** 要件を満たせます。

```python
# Find the first <title> element; BeautifulSoup returns None if missing
title_tag = soup.find("title")

if title_tag is None:
    # If the document lacks a <title>, create one inside <head>
    head_tag = soup.find("head")
    if head_tag is None:
        # As a safety net, add a <head> element at the top
        head_tag = soup.new_tag("head")
        soup.insert(0, head_tag)
    title_tag = soup.new_tag("title")
    head_tag.append(title_tag)

# Show the current title (useful for debugging)
print("Current title:", title_tag.string)
```

*`None` をチェックする理由:*  
HTML の一部断片にはタイトルが含まれないことがあります。自動で追加しておくと、後続のエラーを防ぎ、スクリプトの堅牢性が向上します。

## 手順 3: タイトルテキストを変更する  

ここで **HTML タイトルを更新** し、タグの文字列に新しいテキストを代入します。これが **タイトルの変更方法** の核心です。

```python
new_title = "New Title"

# Replace the existing title text
title_tag.string = new_title

print("Updated title:", title_tag.string)
```

`string` 属性は `<title>` 内のテキストノードを表します。上書きすることで、メモリ上の DOM が更新されます。

## 手順 4: 変更後のHTMLを保存する  

最後に、変更されたドキュメントを新しいファイルに書き出します。これで **変更したHTMLの保存** が完了し、元のファイルはそのまま残ります。

```python
# Define the output path
modified_path = html_dir / "index_modified.html"

# Write the prettified HTML back to disk
with modified_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())

print(f"Modified HTML saved to {modified_path}")
```

`prettify()` はインデント付きで出力を整形し、変更後のファイルを読みやすくします。

### 期待される出力

サンプルの `index.html`（元の内容は以下）でスクリプトを実行すると、コンソール出力は次のようになります。

```html
<!DOCTYPE html>
<html>
<head>
    <title>Old Title</title>
</head>
<body>
    <h1>Welcome</h1>
</body>
</html>
```

```
Current title: Old Title
Updated title: New Title
Modified HTML saved to YOUR_DIRECTORY/index_modified.html
```

保存された `index_modified.html` の冒頭は次のようになります。

```html
<!DOCTYPE html>
<html>
 <head>
  <title>
   New Title
  </title>
 </head>
 <body>
  <h1>
   Welcome
  </h1>
 </body>
</html>
```

## すぐにコピー＆ペーストできる完全スクリプト

以下は 4 つの手順をすべて組み合わせた、実行可能な完全プログラムです。`change_title.py` として保存し、`YOUR_DIRECTORY` を適切に設定してください。

```python
# change_title.py
from pathlib import Path
from bs4 import BeautifulSoup

# ----------------------------------------------------------------------
# Configuration – change these values to match your environment
# ----------------------------------------------------------------------
html_dir = Path("YOUR_DIRECTORY")          # Folder containing index.html
original_file = html_dir / "index.html"
modified_file = html_dir / "index_modified.html"
new_title = "New Title"                    # Desired title text
# ----------------------------------------------------------------------

# 1️⃣ Load the HTML file (read html with python)
with original_file.open(encoding="utf-8") as f:
    html_content = f.read()

soup = BeautifulSoup(html_content, "html.parser")

# 2️⃣ Locate or create the <title> element
title_tag = soup.find("title")
if title_tag is None:
    head_tag = soup.find("head")
    if head_tag is None:
        head_tag = soup.new_tag("head")
        soup.insert(0, head_tag)
    title_tag = soup.new_tag("title")
    head_tag.append(title_tag)

print("Current title:", title_tag.string)

# 3️⃣ Update the title (how to change title)
title_tag.string = new_title
print("Updated title:", title_tag.string)

# 4️⃣ Save the modified HTML (save modified html)
with modified_file.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())

print(f"Modified HTML saved to {modified_file}")
```

スクリプトを実行:

```bash
python change_title.py
```

コンソールメッセージとともに、タイトルが更新された新しい `index_modified.html` が生成されます。

## 追加のヒントとエッジケース

| 状況 | 対処方法 |
|-----------|------------|
| **複数の `<title>` タグがある** | `soup.find_all("title")` はリストを返すので、最初の要素を更新するか、すべて変更したい場合はループで処理します。 |
| **エンコーディングの問題** | BOM がある場合は `encoding="utf-8-sig"` で開くか、`chardet` でエンコーディングを検出します。 |
| **大容量のHTMLファイル** | パフォーマンス向上のため `lxml` パーサー (`BeautifulSoup(html_content, "lxml")`) を使用します。 |
| **元のフォーマットを保持したい** | 正確な空白を保ちたい場合は `prettify()` の代わりに `str(soup)` を書き出します。 |
| **多数のファイルを自動処理** | ロジックを関数化し、`Path.rglob("*.html")` でループ処理します。 |

これらのバリエーションは、**タイトルの変更方法** のコアロジックを保ちつつ、実務での様々なケースに対応できます。

## 結論

これで、Python を使って任意の HTML ドキュメントの **タイトルの変更方法** が習得できました。チュートリアルでは、HTML の読み込み、`<title>` タグの取得、テキストの更新、そして **変更したHTMLの安全な保存** までを解説しました。完全スクリプトを活用すれば、静的サイトジェネレータや SEO パイプライン、その他タイトルを動的に変更する自動化タスクに簡単に組み込めます。

次は、**PythonでHTMLを読む** 方法でメタタグ抽出を学んだり、**HTMLファイルをPythonで読み込む** テクニックで不正確なマークアップの処理に挑戦してみましょう。バッチ処理でサイト全体のタイトルを一括更新すれば、あなたの新しいスキルは多くのウェブ自動化タスクの基盤となります。コーディングを楽しんでください！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、API の追加機能を習得したり、独自の実装アプローチを探求したりするのに役立ちます。

- [How to Save HTML with Aspose.Html – Complete C# Guide](/html/english/net/working-with-html-documents/how-to-save-html-with-aspose-html-complete-c-guide/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Render HTML to PNG – Complete Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-render-html-to-png-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}