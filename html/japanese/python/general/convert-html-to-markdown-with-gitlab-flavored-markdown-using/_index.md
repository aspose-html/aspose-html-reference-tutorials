---
category: general
date: 2026-11-27
description: Python を使用して HTML を Markdown に変換し、GitLab 風 Markdown のサポートで HTML から Markdown
  を生成します。Markdown フォーマッタの設定方法と、HTML を Markdown としてエクスポートする方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- gitlab flavored markdown
- export html as markdown
- generate markdown from html
- set markdown formatter
language: ja
lastmod: 2026-11-27
og_description: Python と GitLab 風マークダウンを使用して HTML をマークダウンに変換します。このガイドでは、マークダウンフォーマッタを設定し、HTML
  をマークダウンとしてエクスポートする手順を数ステップで紹介します。
og_image_alt: Diagram illustrating how to convert html to markdown using a Python
  script
og_title: PythonでGitLabフレーバーのMarkdownを使用してHTMLをMarkdownに変換する
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Convert html to markdown using Python and generate markdown from html
    with GitLab‑flavored markdown support. Learn how to set markdown formatter and
    export html as markdown.
  headline: Convert html to markdown with GitLab‑flavored Markdown using Python
  type: TechArticle
tags:
- HTML
- Markdown
- Python
title: Python を使って GitLab 風 Markdown で HTML を Markdown に変換する
url: /ja/python/general/convert-html-to-markdown-with-gitlab-flavored-markdown-using/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML を GitLab 形式の Markdown に変換する（Python 使用）

HTML を **HTML を Markdown に変換** する必要がある場合、このガイドでは完全な、すぐに実行できるソリューションを示します。**HTML を Markdown としてエクスポート**する方法、**GitLab 形式の Markdown**フォーマットの選択方法、そして出力がリポジトリのレンダリングルールに合うように **markdown formatter** オプションを **設定**する方法が分かります。

以下のセクションでは、コードの各行を順に解説し、各設定が重要な理由を説明するとともに、リンクと段落だけを残す場合やデフォルトのフレーバーに切り替える場合など、一般的なバリエーションも取り上げます。最後まで読めば、**HTML から Markdown を生成**する関数呼び出しを 1 回で実行できるようになります。

## Prerequisites

開始する前に、以下がインストールされていることを確認してください。

* Python 3.8+ がインストール済み  
* `aspose.words`（または `HTMLDocument`、`MarkdownSaveOptions`、`Converter` を提供する類似ライブラリ）を `pip install aspose-words` でインストール  
* 変換したい小さな HTML ファイル（例: 既知のディレクトリにある `sample.html`）  

追加のツールは不要です。本チュートリアルはライブラリ内蔵の変換エンジンだけを使用します。

## Step 1: Load the HTML document you want to convert

変換パイプラインは、ソースファイルを `HTMLDocument` オブジェクトに読み込むことから始まります。このオブジェクトは HTML マークアップを解析し、変換の準備を行います。

```python
from aspose.words import HTMLDocument, MarkdownSaveOptions, MarkdownFeatures, Converter

# Load the HTML file you wish to convert
html_doc = HTMLDocument("YOUR_DIRECTORY/sample.html")
```

*Why this step matters*: `HTMLDocument` は HTML 構造を正規化し、相対 URL を解決し、Markdown エンジンが走査できる DOM を作成します。このステップを省略すると、コンバータは生テキストを読み取ることになり、タグが欠落したりリンクが壊れたりします。

## Step 2: Create Markdown save options and configure the desired flavor and features

ここでは **markdown formatter** のオプションを設定します。`format` プロパティで Markdown のフレーバーを選択します—`"GIT"` は **GitLab 形式の Markdown** を生成し、`"DEFAULT"` は標準的な CommonMark を生成します。

```python
# Create a MarkdownSaveOptions instance
md_options = MarkdownSaveOptions()

# Set the formatter to GitLab‑flavored markdown
md_options.formatter = "GIT"  # alternatives: "DEFAULT", "MARKDOWN"

# Choose which markdown features to keep.
# In this example we keep only links and paragraphs.
md_options.features = (
    MarkdownFeatures.LINK |
    MarkdownFeatures.PARAGRAPH
)
```

*Why this matters*: GitHub、GitLab、Bitbucket などプラットフォームごとに Markdown の解釈が若干異なります。**markdown formatter** を `"GIT"` に **設定**することで、テーブルやタスクリストなど GitLab 固有の構文が正しくレンダリングされます。`features` フラグを使うと **HTML を Markdown としてエクスポート**しながら不要な要素を除去でき、ドキュメントや README 用に出力をすっきりさせられます。

## Step 3: Convert the HTML document to Markdown using the configured options

ソースがロードされ、オプションが準備できたら、静的な `convert` メソッドを呼び出します。この 1 回の呼び出しで変換の本体が実行されます。

```python
# Perform the conversion and write the result to a .md file
Converter.convert(html_doc, md_options, "YOUR_DIRECTORY/sample.md")
```

*Why this matters*: `Converter` クラスは変換パイプライン全体を抽象化します。`HTMLDocument` から DOM を読み取り、**markdown formatter** に **設定**したフォーマッタを適用し、選択した `features` を尊重して最終的な Markdown ファイルを書き出します。結果は GitLab 互換の `.md` ファイルとなり、バージョン管理にすぐ使えます。

## Expected output

`sample.html` にシンプルな段落とリンクが含まれていると仮定します。

```html
<p>Check out the <a href="https://example.com">example site</a> for more info.</p>
```

生成される `sample.md` は次のようになります。

```markdown
Check out the [example site](https://example.com) for more info.
```

`features` を `LINK` と `PARAGRAPH` のみに限定したため、元の HTML に含まれる画像、テーブル、スクリプトはすべて除外されています。よりリッチな変換が必要な場合は、`md_options.features` に `MarkdownFeatures.IMAGE` などを追加してください。

## Step 4: Verify the conversion and handle edge cases

バッチ処理で多数のファイルを変換する際は、出力ファイルを Python で再度読み込み、変換が正しく行われたか確認するのがベストプラクティスです。

```python
# Verify the markdown file exists and print its first lines
import pathlib

output_path = pathlib.Path("YOUR_DIRECTORY/sample.md")
if output_path.is_file():
    print("Conversion succeeded. First 3 lines:")
    print("\n".join(output_path.read_text().splitlines()[:3]))
else:
    raise FileNotFoundError("The markdown file was not created.")
```

**Common edge cases**

| Situation | How to address it |
|-----------|-------------------|
| **Relative image URLs** – they become broken in markdown | `md_options.features |= MarkdownFeatures.IMAGE` を使用し、変換後に画像パスを書き換える処理を追加します。 |
| **Complex tables** – GitLab has limited table support | デフォルトのフォーマッタ（`"DEFAULT"`）を使用するか、変換後に手動でテーブル構文を調整します。 |
| **Unicode characters** – may appear as escaped sequences | Python スクリプトでファイルを `encoding="utf-8"` で開き、ライブラリが提供する場合は `md_options.encoding = "UTF-8"` を設定します。 |

## Pro tip: Batch conversion for an entire folder

多数のファイルに対して **HTML から Markdown を生成** したい場合は、以下のように 3 つのステップをループで回します。

```python
import os

source_dir = "YOUR_DIRECTORY"
target_dir = "YOUR_DIRECTORY/markdown"

os.makedirs(target_dir, exist_ok=True)

for filename in os.listdir(source_dir):
    if filename.lower().endswith(".html"):
        html_path = os.path.join(source_dir, filename)
        md_path = os.path.join(target_dir, os.path.splitext(filename)[0] + ".md")

        html_doc = HTMLDocument(html_path)
        md_options = MarkdownSaveOptions()
        md_options.formatter = "GIT"
        md_options.features = MarkdownFeatures.LINK | MarkdownFeatures.PARAGRAPH

        Converter.convert(html_doc, md_options, md_path)
        print(f"Converted {filename} → {os.path.basename(md_path)}")
```

このスクリプトはフォルダ内のすべての `.html` ファイルに対して **HTML を Markdown としてエクスポート** し、バッチ全体で GitLab フレーバーを保持します。

## Conclusion

これで **HTML を Markdown に変換** し、**GitLab 形式の Markdown** 出力を選択し、プロジェクトの要件に合った **markdown formatter** オプションを **設定**する完全な本番レベルの手法が手に入りました。上記の手順に従えば、確実に **HTML を Markdown としてエクスポート** でき、**HTML から Markdown を生成** できるだけでなく、バルク処理やカスタム機能セットにも柔軟に対応できます。

次に検討すべきこと:

* `MarkdownFeatures.IMAGE` を追加して、**HTML を Markdown としてエクスポート** 時にインライン画像を保持し、よりリッチなドキュメントを作成する。  
* より汎用的な Markdown が必要な場合は、フォーマッタを `"DEFAULT"` に切り替える。  
* この変換を CI/CD パイプラインに組み込み、HTML レポートが自動的に Markdown アーティファクトになるようにする。

Happy coding, and enjoy the seamless transition from HTML to clean, GitLab‑ready markdown!

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示した手法を応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、API の追加機能を習得したり、代替実装アプローチを自分のプロジェクトで試したりするのに役立ちます。

- [How to convert HTML to Markdown with a custom formatter in Python](/html/english/python/general/how-to-convert-html-to-markdown-with-a-custom-formatter-in-p/)
- [How to convert HTML to markdown with images using Python](/html/english/python/general/how-to-convert-html-to-markdown-with-images-using-python/)
- [How to convert HTML to Markdown with Python – complete guide](/html/english/python/general/how-to-convert-html-to-markdown-with-python-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}