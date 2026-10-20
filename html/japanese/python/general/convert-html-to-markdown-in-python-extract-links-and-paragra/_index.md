---
category: general
date: 2026-09-26
description: PythonでHTMLをMarkdownに変換し、HTMLからリンクを抽出してMarkdownとして保存します。HTMLの変換方法をステップバイステップで学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- save html as markdown
- how to convert html
- extract paragraphs from html
language: ja
lastmod: 2026-09-26
og_description: PythonでHTMLをMarkdownに変換し、HTMLからリンクを抽出してMarkdownとして保存します。この完全なガイドに従ってください。
og_image_alt: Screenshot of Python code converting HTML to Markdown and showing extracted
  links
og_title: PythonでHTMLをMarkdownに変換 – リンクと段落を抽出
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Convert HTML to Markdown with Python, extracting links from HTML and
    saving HTML as Markdown. Learn how to convert HTML step‑by‑step.
  headline: Convert HTML to Markdown in Python – extract links and paragraphs easily
  type: TechArticle
- description: Convert HTML to Markdown with Python, extracting links from HTML and
    saving HTML as Markdown. Learn how to convert HTML step‑by‑step.
  name: Convert HTML to Markdown in Python – extract links and paragraphs easily
  steps:
  - name: Expected output
    text: 'Running the script generates a file similar to the following (the exact
      content depends on the source HTML):'
  - name: 1. Extract only links
    text: '```python md_options.features = MarkdownFeatures.LINKS # No paragraphs
      ```'
  - name: 2. Extract only paragraphs
    text: '```python md_options.features = MarkdownFeatures.PARAGRAPHS # No links
      ```'
  type: HowTo
- questions:
  - answer: Yes. `HTMLDocument` accepts any well‑formed fragment; the converter treats
      the fragment as the document body.
    question: Does this work with HTML fragments (no `<html>` root tag)?
  - answer: 'Add `MarkdownFeatures.IMAGES` to the `features` flag: ```python md_options.features
      = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
      ```'
    question: Can I keep images as Markdown image syntax?
  - answer: 'Wrap `convert_html_to_markdown` in a loop that walks the directory with
      `os.listdir` or `pathlib.Path.rglob("*.html")`. --- ## Conclusion You now know
      how to **convert HTML to Markdown** in Python while selectively **extracting
      links from HTML** and **extracting paragraphs from HTML**. The script de'
    question: How do I convert many files in a directory?
  type: FAQPage
tags:
- html
- markdown
- python
- data‑extraction
title: PythonでHTMLをMarkdownに変換 – リンクと段落を簡単に抽出
url: /ja/python/general/convert-html-to-markdown-in-python-extract-links-and-paragra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでHTMLをMarkdownに変換 – リンクと段落を簡単に抽出

HTMLを**Markdownに変換**し、必要な部分だけを残したい場合、このガイドではPython数行でその方法を示します。ブログ記事のスクレイピング、ドキュメントのアーカイブ、メール本文のクリーンアップなど、HTMLからリンクを抽出し、HTMLをMarkdownとして保存する信頼できる方法を学べます。

このチュートリアルでは、必要なパッケージのインストールから、空の `<a>` タグや入れ子になった段落といったエッジケースの処理まで網羅しています。最後まで読むと、**HTMLをMarkdownに変換**し、HTMLからリンクを抽出し、必要に応じてHTMLから段落も抽出できる、すぐに実行可能なスクリプトが手に入ります。

---

## 前提条件

* Python 3.8 以上がインストールされていること  
* `groupdocs-conversion` Python パッケージへのアクセス（`HTMLDocument`、`MarkdownSaveOptions`、`Converter` を提供するライブラリ）  
* 処理したいローカルの HTML ファイル（例: `article.html`）

pipでライブラリをインストールできます:

```bash
pip install groupdocs-conversion
```

> **Pro tip:** 仮想環境（`python -m venv venv`）を使用して、依存関係を分離しましょう。

---

## 手順 1: ソース HTML ドキュメントを読み込む

最初の操作は、ソースファイルを指す `HTMLDocument` オブジェクトを作成することです。このオブジェクトは生の HTML を抽象化し、コンバータにクリーンなエントリーポイントを提供します。

```python
from groupdocs.conversion import HTMLDocument

# Load the HTML file you want to transform
html_doc = HTMLDocument("YOUR_DIRECTORY/article.html")
```

*なぜ重要か:* この方法でドキュメントを読み込むと、ライブラリが DOM を一度だけ解析するため、後続の操作（リンクや段落の抽出など）が高速かつメモリ効率的になります。

---

## 手順 2: Markdown の保存オプションを作成し、必要な機能を選択する

`MarkdownSaveOptions` を使うと、変換後に残す HTML 要素を決められます。`features` フラグはビット単位の OR でオプションを組み合わせます。

```python
from groupdocs.conversion import MarkdownSaveOptions, MarkdownFeatures

# Keep only links and paragraphs in the resulting Markdown
md_options = MarkdownSaveOptions()
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS
```

*なぜ重要か:* `LINKS` と `PARAGRAPHS` を指定すると、**HTMLからリンクを抽出**し、**HTMLから段落を抽出**しながら、他のすべて（スタイル、スクリプト、画像）を破棄します。後でリンクだけが必要な場合は、`MarkdownFeatures.PARAGRAPHS` を `0` に置き換える（または省略する）だけです。

---

## 手順 3: 設定したオプションで HTML を Markdown に変換する

次に、静的メソッド `convert_html` を呼び出し、ソースドキュメント、出力パス、先ほど作成したオプションを渡します。

```python
from groupdocs.conversion import Converter

# Perform the conversion and write the Markdown file
Converter.convert_html(html_doc, "YOUR_DIRECTORY/article_links.md", md_options)
```

*なぜ重要か:* 変換は単一パスで実行され、定義した機能フィルタが適用されます。生成されたファイル（`article_links.md`）には、Markdown 形式のリンクと段落だけが含まれ、下流処理のために **HTMLをMarkdownとして保存** したいときにまさに必要なものです。

---

## 完全スクリプト – すべてまとめ

以下は、`html_to_md.py` という名前のファイルにコピー＆ペーストできる、完全で実行可能なスクリプトです。環境に合わせてパスを調整してください。

```python
# html_to_md.py
# -------------------------------------------------
# Convert HTML to Markdown, keeping only links and paragraphs.
# -------------------------------------------------

from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeatures, Converter

def convert_html_to_markdown(source_path: str, target_path: str) -> None:
    """
    Convert an HTML file to Markdown, extracting only links and paragraphs.

    Args:
        source_path: Path to the source HTML file.
        target_path: Path where the Markdown file will be saved.
    """
    # Load the HTML document
    html_doc = HTMLDocument(source_path)

    # Configure conversion to keep links and paragraphs
    md_options = MarkdownSaveOptions()
    md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS

    # Run the conversion
    Converter.convert_html(html_doc, target_path, md_options)
    print(f"✅ Conversion complete – Markdown saved to: {target_path}")

if __name__ == "__main__":
    # Example usage – replace with your actual file locations
    src = "YOUR_DIRECTORY/article.html"
    dst = "YOUR_DIRECTORY/article_links.md"
    convert_html_to_markdown(src, dst)
```

### 期待される出力

スクリプトを実行すると、以下のようなファイルが生成されます（正確な内容はソース HTML に依存します）。

```markdown
[OpenAI](https://openai.com)

This is the first paragraph of the article.

[GitHub](https://github.com)

Another paragraph that explains the next topic.
```

リンクテキストと段落テキストだけが残り、他のすべての HTML 要素は除去されます。

---

## リンクだけまたは段落だけを抽出する（高度なバリエーション）

場合によっては、**HTMLを変換**して、特定の要素だけを含む Markdown ファイルが必要になることがあります。

### 1. リンクだけを抽出

```python
md_options.features = MarkdownFeatures.LINKS   # No paragraphs
```

### 2. 段落だけを抽出

```python
md_options.features = MarkdownFeatures.PARAGRAPHS   # No links
```

どちらのバリエーションも同じ `convert_html` 呼び出しを再利用するため、別々の変換ロジックを書く必要はありません。

---

## エッジケースの処理

| Situation                               | Recommended fix |
|----------------------------------------|-----------------|
| HTML ファイルに空の `<a>` タグが含まれている | コンバータは空のリンクを自動的にスキップします。もし不要な `[]()` が出てきたら、`md_options.removeEmptyLinks = True` を設定してください。 |
| 入れ子になった段落（`<div>` 内の `<p>`） | ライブラリは入れ子の段落をフラット化し、テキスト順序を保持します。追加のコードは不要です。 |
| リンクタイトルに非 ASCII 文字が含まれる | Python ファイルが UTF-8 エンコーディングで保存されていることを確認し、後で出力ファイルを読む際は `encoding="utf-8"` を指定して開いてください。 |
| 非常に大きな HTML ファイル（≥ 50 MB） | `HTMLDocument(stream=io.BytesIO(...))` を使用してファイルをチャンク単位で処理し、メモリに全体を読み込むのを回避します。 |

---

## よくある質問

**Q: この方法は `<html>` ルートタグがない HTML フラグメントでも機能しますか？**  
A: はい。`HTMLDocument` は任意の整形式フラグメントを受け入れ、コンバータはフラグメントをドキュメント本文として扱います。

**Q: 画像を Markdown の画像構文として保持できますか？**  
A: `features` フラグに `MarkdownFeatures.IMAGES` を追加してください:  
```python
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
```

**Q: ディレクトリ内の多数のファイルを変換するにはどうすればよいですか？**  
A: `convert_html_to_markdown` を `os.listdir` や `pathlib.Path.rglob("*.html")` でディレクトリを走査するループでラップします。

---

## 結論

これで、Python で **HTMLをMarkdownに変換**しながら、**HTMLからリンクを抽出**し、**HTMLから段落を抽出**する方法が分かりました。このスクリプトは標準的な手順（ドキュメントの読み込み、`MarkdownSaveOptions` の設定、`Converter.convert_html` の実行）を示しています。少し調整すれば、リンクだけ、段落だけ、または完全な忠実な表現を含む **HTMLをMarkdownとして保存** することも可能です。

次に、以下を検討してみてください：

* `MarkdownFeatures.HEADINGS` を追加してセクションタイトルを保持する。  
* 生成された Markdown を MkDocs や Hugo などの静的サイトジェネレータの入力として使用する。  
* ドキュメントリポジトリ全体の一括変換を自動化する。

変換を楽しんでください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.HTML を使用した .NET での HTML から Markdown への変換](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Aspose.HTML for Java での HTML から Markdown への変換](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Java で HTML を Markdown に変換する際のオフセット設定方法](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}