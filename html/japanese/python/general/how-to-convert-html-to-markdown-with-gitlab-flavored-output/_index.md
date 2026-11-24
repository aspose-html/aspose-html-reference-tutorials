---
category: general
date: 2026-11-24
description: GitLab 風のオプションを使用して Python で HTML を Markdown に変換し、リンクを簡単に抽出できる。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- gitlab flavored markdown
- save html as markdown
- html to markdown conversion
- extract links to markdown
language: ja
lastmod: 2026-11-24
og_description: GitLab 風オプションを使用して Python で HTML を Markdown に変換し、HTML を Markdown として保存し、リンクを
  Markdown に抽出する完全な例。
og_image_alt: Screenshot of a Python script converting HTML to GitLab‑flavored Markdown
og_title: GitLab 風出力で HTML を Markdown に変換 – Python ガイド
schemas:
- author: Aspose
  dateModified: '2026-11-24'
  description: Convert HTML to Markdown in Python using GitLab‑flavored options and
    extract links easily.
  headline: How to convert HTML to Markdown with GitLab‑flavored output in Python
  type: TechArticle
tags:
- HTML
- Markdown
- Python
- Conversion
- GitLab
title: PythonでGitLab風の出力を使用してHTMLをMarkdownに変換する方法
url: /ja/python/general/how-to-convert-html-to-markdown-with-gitlab-flavored-output/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GitLab 風の出力で HTML を Markdown に変換する方法（Python）

HTML を **Markdown に変換** したい場合、このガイドは実行可能な完全なソリューションを示します。GitLab 風のフォーマットで HTML を Markdown として保存する方法と、コードから離れずにリンクを Markdown に抽出する方法が分かります。

このアプローチは Aspose.HTML for Python ライブラリを使用します。ライブラリはワンラインの変換 API と、Markdown のフレーバーに対する細かな制御を提供します。チュートリアルの最後までに、クリーンな GitLab 風 Markdown ファイルと抽出されたリンク一覧を生成するスクリプトが手に入ります。

## 前提条件

開始する前に、以下を確認してください。

* Python 3.8 以上がインストールされていること。
* パッケージインストール用に `pip` が利用できること。
* 変換したいローカルの HTML ファイル（例: `article.html`）。
* コマンドラインから Python スクリプトを実行する基本的な知識。

追加ツールは不要です。ライブラリが解析、変換、リンク抽出を内部で処理します。

## Aspose.HTML for Python ライブラリのインストール

変換 API は `aspose.html` パッケージに含まれています。`pip` でインストールします。

```bash
pip install aspose-html
```

このパッケージには、後述のスクリプトで使用する `HTMLDocument`、`MarkdownSaveOptions`、`Converter` クラスが同梱されています。インストールは数秒で完了し、別途ランタイムを用意する必要はありません。

## HTML ドキュメントの読み込み

`HTMLDocument` オブジェクトを作成すると、ソースファイルがメモリにロードされます。コンストラクタはファイルパスまたは URL を受け取ります。

```python
from aspose.html import HTMLDocument

# Load the HTML file you want to convert.
doc = HTMLDocument("YOUR_DIRECTORY/article.html")
```

`doc` インスタンスは現在、完全な DOM ツリーを表しており、リンクや段落タグを含むすべての要素をコンバータが参照できるようになります。

## GitLab 風 Markdown オプションの設定

GitLab 風 Markdown は、標準の CommonMark と比べてリンクや段落の扱いが異なります。`MarkdownSaveOptions` クラスでフォーマッタと必要な機能セットを指定します。

```python
from aspose.html import MarkdownSaveOptions

# Configure options for GitLab‑flavored output.
#   formatter="GIT"  -> GitLab markdown
#   features=["Link", "Paragraph"] -> keep only links and paragraphs.
opts = MarkdownSaveOptions(formatter="GIT", features=["Link", "Paragraph"])
```

`features` を `["Link", "Paragraph"]` に設定すると、リンク抽出に重点を置きつつ段落構造を保持します。これはドキュメントや変更ログの生成に最適です。

## 変換を実行し、Markdown として保存

ドキュメントがロードされ、オプションが設定されたら、静的メソッド `Converter.convert` を呼び出します。結果は直接ターゲットファイルに書き込まれます。

```python
from aspose.html import Converter

# Perform the conversion and write the markdown file.
Converter.convert(doc, "YOUR_DIRECTORY/article.md", opts)
```

実行後、`article.md` には元の HTML のリンクと段落を反映した GitLab 風 Markdown が格納されています。

## 出力を確認し、リンクを Markdown に抽出

生成されたファイルを開いて変換結果を確認します。リンク構文（`[text](url)`）と段落改行がソースと一致しているはずです。

```python
# Quick verification: read and print the first 10 lines.
with open("YOUR_DIRECTORY/article.md", "r", encoding="utf-8") as f:
    for i, line in enumerate(f):
        if i >= 10:
            break
        print(line.rstrip())
```

さらに、変換前に `HTMLDocument` から URL の生リストを取得したい場合は次のようにします。

```python
# Extract all anchor href attributes.
links = [a.get_attribute("href") for a in doc.get_elements_by_tag_name("a")]
print("Extracted links:", links)
```

この手順は、**リンクを Markdown に抽出** する方法を示しており、二度目のパースを回避できます。

## 完全なスクリプト

すべてをまとめると、任意のプロジェクトにそのまま投入できる単一スクリプトが完成します。

```python
# convert_html_to_gitlab_md.py
from aspose.html import HTMLDocument, MarkdownSaveOptions, Converter

def convert_html_to_markdown(src_path: str, dst_path: str) -> list:
    """
    Convert an HTML file to GitLab‑flavored Markdown and return a list of extracted links.

    Args:
        src_path: Path to the source HTML file.
        dst_path: Path where the Markdown file will be saved.

    Returns:
        A list of URLs found in the HTML document.
    """
    # Load the HTML document.
    doc = HTMLDocument(src_path)

    # Configure GitLab‑flavored Markdown options (links and paragraphs only).
    opts = MarkdownSaveOptions(formatter="GIT", features=["Link", "Paragraph"])

    # Convert and save as Markdown.
    Converter.convert(doc, dst_path, opts)

    # Extract links for additional processing.
    links = [a.get_attribute("href") for a in doc.get_elements_by_tag_name("a")]
    return links

if __name__ == "__main__":
    source = "YOUR_DIRECTORY/article.html"
    target = "YOUR_DIRECTORY/article.md"
    extracted_links = convert_html_to_markdown(source, target)

    print(f"Conversion complete. Markdown saved to {target}")
    print("Extracted links:", extracted_links)
```

スクリプトを実行すると:

```bash
python convert_html_to_gitlab_md.py
```

`article.md` が GitLab 風 Markdown として生成され、抽出された URL の一覧がコンソールに出力されます。

## よくあるバリエーションとエッジケース

| シナリオ | 調整 |
|---|---|
| **フル HTML（画像、テーブル等）** | `features` に `"Image"` や `"Table"` を追加してそれらの要素を保持します。 |
| **別の Markdown フレーバー** | `formatter="GIT"` を `"COMMONMARK"` や `"GFM"` に変更して他プラットフォーム向けに出力します。 |
| **大容量ファイル（> 50 MB）** | ストリーミング API（`HTMLDocument.open`）を使用し、ファイル全体をメモリに読み込まないようにします。 |
| **Unicode 文字** | ソースファイルが UTF‑8 エンコードであることを確認してください。ライブラリはエンコードを保持します。 |

これらのバリエーションにより、**HTML を Markdown として保存** するパターンをさまざまな状況で再利用できます。

## プロのコツ

* **オプションを再利用:** バッチジョブで複数ファイルを変換する場合、`MarkdownSaveOptions` のインスタンスを1つ作成し、必要に応じて渡し回すと効率的です。 |
* **リンクの検証:** 抽出後にシンプルな `requests.head(url)` を実行し、破損した URL をフラグ付けします。 |
* **バージョン固定:** 予期しない API 変更を防ぐため、`aspose-html==23.10` のようにバージョンを固定します。 |

## 結論

これで **HTML を Markdown に変換** し、GitLab 風フォーマッタで保存し、**リンクを Markdown に抽出** する簡潔な Python スクリプトの作成方法が分かりました。ソリューションはすぐに使える状態で、典型的なエッジケースに対応し、他の Markdown フレーバーや追加の HTML 機能にも拡張可能です。

### 次のステップ

* `features` リストを調査し、画像、テーブル、コードブロックなどを含める方法を学びましょう。 |
* このスクリプトを CI パイプラインに組み込み、HTML ソースから自動的にドキュメントを生成します。 |
* 抽出したリンクをリンクチェックサービスと組み合わせ、参照の健全性を維持します。

スクリプトを自分のワークフローに合わせてカスタマイズし、コミュニティと結果を共有してください！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法に基づく関連トピックを扱っています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、代替実装アプローチを自分のプロジェクトで試したりするのに役立ちます。

- [Convert HTML to Markdown Python – extract links & paragraphs](/html/english/python/general/convert-html-to-markdown-python-extract-links-paragraphs/)
- [How to convert HTML to Markdown with GitLab‑flavored markdown in Python](/html/english/python/general/how-to-convert-html-to-markdown-with-gitlab-flavored-markdow/)
- [convert html to markdown python – save markdown file with python](/html/english/python/general/convert-html-to-markdown-python-save-markdown-file-with-pyth/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}