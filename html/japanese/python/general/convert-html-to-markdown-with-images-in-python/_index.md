---
category: general
date: 2026-11-17
description: PythonでHTMLを画像付きのMarkdownに変換 – 画像をそのままエクスポートしながら、HTMLを素早く変換する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- how to convert html
- export html with images
- markdown conversion with images
language: ja
lastmod: 2026-11-17
og_description: PythonでHTMLを画像付きのMarkdownに変換します。このチュートリアルでは、画像をエクスポートしながらHTMLを変換する方法を示し、完全な実行可能なソリューションを提供します。
og_image_alt: Diagram showing convert html to markdown workflow with image extraction
og_title: Pythonで画像付きHTMLをMarkdownに変換 – クイックガイド
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Convert HTML to markdown with images in Python – learn how to convert
    HTML quickly while exporting images intact.
  headline: Convert HTML to markdown with images in Python
  type: TechArticle
tags:
- HTML
- Markdown
- Python
- Image extraction
title: PythonでHTMLを画像付きMarkdownに変換する
url: /ja/python/general/convert-html-to-markdown-with-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pythonで画像付きHTMLをMarkdownに変換する

If you need to **convert HTML to markdown** while keeping images as separate files, this guide shows you exactly how to do it. You’ll get a complete, runnable example that handles external resources, so your markdown output references the original images correctly.

HTML を別ファイルとして保持しながら **HTMLをMarkdownに変換** したい場合、このガイドで具体的な手順を示します。外部リソースを処理する完全な実行可能サンプルが得られ、Markdown の出力が元の画像を正しく参照します。

Exporting HTML with images often trips up simple converters because they either drop the images or embed them as base64 strings. By configuring the resource handling options, you retain the original image files and produce clean markdown that can be version‑controlled or edited later.

画像付きHTMLをエクスポートする際、シンプルなコンバータは画像を削除したり base64 文字列として埋め込んだりして失敗しがちです。ResourceHandlingOptions を設定することで、元の画像ファイルを保持し、バージョン管理や後からの編集が可能なクリーンなMarkdownを生成できます。

In this tutorial you will:

このチュートリアルでは以下を行います：

* Load an HTML document from disk.  
  * ディスクからHTMLドキュメントを読み込む。  
* Configure the converter to **export HTML with images** as separate files.  
  * コンバータを **画像付きHTMLをエクスポート** するように設定し、画像を別ファイルとして保存する。  
* Save the result as markdown using the **markdown conversion with images** options.  
  * **画像付きMarkdown変換** オプションを使用して結果をMarkdownとして保存する。  

The only prerequisite is a recent version of the Aspose.HTML for Python library (or any compatible API that provides `HTMLDocument`, `ResourceHandlingOptions`, `MarkdownSaveOptions`, and `Converter`). You also need Python 3.8+ and write permission to the output folder.

必要条件は、Aspose.HTML for Python ライブラリの最新バージョン（または `HTMLDocument`、`ResourceHandlingOptions`、`MarkdownSaveOptions`、`Converter` を提供する互換 API）です。Python 3.8 以上と、出力フォルダーへの書き込み権限も必要です。

---

## 前提条件とインストール

1. Install the Aspose.HTML package:

   ```bash
   pip install aspose-html
   ```

2. Verify the installation:

   ```python
   import aspose.html as ah
   print(ah.__version__)   # should print the installed version, e.g., 22.9
   ```

> **プロのコツ:** 仮想環境を使用して、他のプロジェクトとのバージョン競合を回避しましょう。

---

## 手順 1: ソースHTMLドキュメントを読み込む

The first step is to create an `HTMLDocument` object that represents the source file. This object parses the markup and builds a DOM tree that the converter can traverse.

最初のステップは、ソースファイルを表す `HTMLDocument` オブジェクトを作成することです。このオブジェクトはマークアップを解析し、コンバータが走査できる DOM ツリーを構築します。

```python
from aspose.html import HTMLDocument

# Load the HTML file you want to convert
html_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(html_path)
```

*このステップが重要な理由* – ドキュメントを読み込むことで、ライブラリはマークアップを完全に制御でき、相対 URL の解決や後のリソース処理が可能になります。

---

## 手順 2: 外部リソースの処理を設定する

When you **export HTML with images**, you usually want the images saved beside the markdown file rather than embedded. The `ResourceHandlingOptions` class lets you specify that behavior.

**画像付きHTMLをエクスポート** する場合、画像を埋め込むのではなく Markdown ファイルの横に保存したいことが多いです。`ResourceHandlingOptions` クラスでその動作を指定できます。

```python
from aspose.html import ResourceHandlingOptions

resource_options = ResourceHandlingOptions()
resource_options.save_external_resources = True   # keep images as separate files
```

Setting `save_external_resources` to `True` instructs the converter to copy each external resource (images, CSS, fonts) to a folder next to the markdown output. The markdown file will contain relative links pointing to those copies.

`save_external_resources` を `True` に設定すると、コンバータは外部リソース（画像、CSS、フォント）を Markdown 出力の隣のフォルダーにコピーするよう指示します。Markdown ファイルにはそれらのコピーへの相対リンクが含まれます。

---

## 手順 3: リソース処理設定をMarkdownオプションに添付する

`MarkdownSaveOptions` controls how the conversion to markdown occurs. By assigning the `resource_handling_options` property, you enable the **markdown conversion with images** feature.

`MarkdownSaveOptions` は Markdown への変換方法を制御します。`resource_handling_options` プロパティを割り当てることで、**画像付きMarkdown変換** 機能が有効になります。

```python
from aspose.html import MarkdownSaveOptions

markdown_options = MarkdownSaveOptions()
markdown_options.resource_handling_options = resource_options
```

If you omit this step, the converter will strip image references or embed them as data URIs, which defeats the purpose of exporting images.

このステップを省略すると、コンバータは画像参照を削除するか、データ URI として埋め込んでしまい、画像をエクスポートする目的が失われます。

---

## 手順 4: 変換を実行する

Finally, call `Converter.convert` with the source document, the target path, and the options you prepared.

最後に、`Converter.convert` を呼び出し、ソースドキュメント、ターゲットパス、そして準備したオプションを渡します。

```python
from aspose.html import Converter

output_path = "YOUR_DIRECTORY/sample.md"
Converter.convert(html_doc, output_path, markdown_options)
```

After the call completes, you will find:

呼び出しが完了すると、以下が作成されます：

* `sample.md` – the markdown version of the original HTML.  
  * `sample.md` – 元のHTMLのMarkdown版。  
* A sub‑folder named `sample_files` (or similar) containing every image referenced in the HTML.  
  * `sample_files` というサブフォルダー（または類似名）に、HTMLで参照されたすべての画像が格納されます。

---

## 完全な動作スクリプト

Putting all pieces together gives you a single script you can run from the command line:

すべての要素を組み合わせると、コマンドラインから実行できる単一のスクリプトが得られます：

```python
# convert_html_to_markdown.py
import os
from aspose.html import HTMLDocument, ResourceHandlingOptions, MarkdownSaveOptions, Converter

def convert_html_to_markdown(html_file: str, markdown_file: str):
    """
    Convert an HTML file to markdown while exporting images as separate files.
    """
    # 1. Load the HTML document
    html_doc = HTMLDocument(html_file)

    # 2. Set up resource handling to keep images external
    res_opts = ResourceHandlingOptions()
    res_opts.save_external_resources = True

    # 3. Attach resource handling to markdown options
    md_opts = MarkdownSaveOptions()
    md_opts.resource_handling_options = res_opts

    # 4. Convert and save
    Converter.convert(html_doc, markdown_file, md_opts)
    print(f"Conversion complete: {markdown_file}")

if __name__ == "__main__":
    # Adjust these paths to your environment
    src_html = os.path.abspath("YOUR_DIRECTORY/sample.html")
    dst_md   = os.path.abspath("YOUR_DIRECTORY/sample.md")

    convert_html_to_markdown(src_html, dst_md)
```

**期待される出力**

```
Conversion complete: /absolute/path/YOUR_DIRECTORY/sample.md
```

After execution, open `sample.md` in any markdown editor. Image links will appear as:

実行後、任意のMarkdownエディタで `sample.md` を開きます。画像リンクは次のように表示されます：

```markdown
![Alt text](sample_files/image1.png)
```

The images themselves reside in the `sample_files` folder, ready for version control or further processing.

画像ファイル自体は `sample_files` フォルダーに格納され、バージョン管理やさらなる処理に利用できます。

---

## 一般的なエッジケースの対処

| Situation                              | Recommended approach |
|----------------------------------------|----------------------|
| **Missing image files**                | コンバータは警告をログに出力し、壊れたリンクを残します。変換前にすべての `<img src>` 属性が到達可能なリソースを指していることを確認してください。 |
| **Relative URLs that point outside the project folder** | `ResourceHandlingOptions.base_url` を使用してベースURLを指定し、コンバータがパスを正しく解決できるようにします。 |
| **Large HTML files with many images**  | 利用可能な場合は `resource_options.max_resource_size` を設定し、コピーされるリソースのサイズ上限を制限します。 |
| **Non‑PNG/JPEG image formats**        | ライブラリは元の形式を自動的にコピーします。対象のMarkdownビューアがその形式（例: SVG）をサポートしていることを確認してください。 |
| **Write‑permission errors**           | 適切な権限でスクリプトを実行するか、書き込み可能な出力ディレクトリを選択してください。 |

---

## スムーズな **画像付きMarkdown変換** のためのヒント

* 出力フォルダーを整理してください：毎回実行する前に `*_files` ディレクトリを削除すれば、画像の新しいセットが得られます。  
* 元のHTMLで意味のある `alt` 属性を使用してください。Markdown の画像キャプションとして自動的に反映されます。  
* 画像を base64 で埋め込む必要がある場合（単一ファイルのMarkdown用）、`resource_options.save_external_resources = False` を設定します。これは **画像付きHTMLをエクスポート** の逆操作ですが、メールやドキュメントへの埋め込みに便利です。  
* 複数ファイルを変換する場合、スクリプトをループで包み、`resource_options.resource_folder` を調整して名前衝突を防ぎます。

---

## よくある質問

**Q: 完全な `<html>` ラッパーがないHTMLフラグメントでも動作しますか？**  
A: はい。`HTMLDocument` はフラグメントを解析でき、コンバータはそれらを...

---

## 次に学ぶべきことは？

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれ、追加のAPI機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Python を使用した HTML から Markdown への変換で画像を埋め込む方法](/html/english/python/general/how-to-embed-images-in-html-to-markdown-conversion-using-pyt/)
- [HTML を Markdown に変換 – CSS と画像を含む完全ガイド](/html/english/python/general/convert-html-to-markdown-complete-guide-with-css-images/)
- [Aspose を使用した HTML から Markdown への変換 – 完全 Python ガイド](/html/english/python/general/convert-html-to-markdown-with-aspose-complete-python-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}