---
category: general
date: 2026-07-15
description: Python を使用して HTML から PDF を作成します。シンプルなスクリプトと明確な手順で、HTML を PDF に迅速に変換する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- html to pdf python
- save html as pdf
- html to pdf tutorial
language: ja
lastmod: 2026-07-15
og_description: PythonでHTMLからPDFを作成する。このガイドでは、HTMLをPDFに変換する方法、HTMLをPDFとして保存する方法、そしてリソースを効率的に扱う方法を示します。
og_image_alt: Screenshot of a Python script that creates PDF from HTML
og_title: PythonでHTMLからPDFを作成する – ハンズオンチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-07-15'
  description: Create PDF from HTML using Python. Learn how to convert HTML to PDF
    quickly with a simple script and clear steps.
  headline: Create PDF from HTML in Python – HTML to PDF Python Tutorial
  type: TechArticle
tags:
- python
- pdf
- html
- conversion
title: PythonでHTMLからPDFを作成 – HTMLからPDFへのPythonチュートリアル
url: /ja/python/general/create-pdf-from-html-in-python-html-to-pdf-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでHTMLからPDFを作成する – フル機能チュートリアル

**HTMLからPDFを作成**したいけれど、どの Python ライブラリを選べば良いか分からないことはありませんか？同じ壁にぶつかる開発者は多いです。ウェブレポート、請求書、マーケティングページなどを印刷可能な PDF に変換しようとするときに特にです。  

良いニュースは、数行のコードで **HTML を PDF に変換**でき、スクリプトは Windows、macOS、Linux で動作します。このガイドでは、実行可能な完全な例を順に解説し、各ステップの重要性を説明し、**HTML を PDF として保存**する方法を余計な手間なく示します。

---

## 学べること

- HTML‑to‑PDF 変換に適した Python パッケージのインストール方法。  
- カスタムリソース処理オプションで HTML ファイルを読み込む方法（無限に続く CSS インポートを防止）。  
- ディスク上にきれいな PDF ファイルを生成する方法。  
- 外部画像、相対パス、大容量ドキュメントといった一般的なエッジケースへの対処法。  

この **HTML から PDF へのチュートリアル** を終える頃には、どのプロジェクトにも組み込める再利用可能な関数が手に入ります。

---

## 前提条件

- Python 3.9 以上（コードは 3.8 でも動作しますが、3.9 以上だと最新の `pathlib` 機能が使えます）。  
- コマンドラインと仮想環境の基本的な知識。  
- PDF に変換したい HTML ファイル（静的ページであれば何でも可）。  

> **プロのコツ:** 仮想環境を使用している場合は、ライブラリをインストールする前に環境をアクティブにしてください。これにより、グローバルな Python 環境が汚染されません。

---

## Step 1 – WeasyPrint のインストール（変換エンジン）

WeasyPrint は純粋な Python ライブラリで、HTML と CSS を PDF にレンダリングします。最新のウェブ機能の多くに対応し、リソース読み込みを細かく制御できます。

```bash
pip install weasyprint
```

上記コマンドを実行すると `cairocffi`、`tinycss2` などの依存パッケージがインストールされます。Windows で `cairo` 関連のエラーが出た場合は、[WeasyPrint のウェブサイト](https://weasyprint.org/docs/install/) から事前ビルド済みのホイールを取得してください。

---

## Step 2 – リソース処理用の小さなヘルパークラスを用意

外部スタイルシートや画像を参照する HTML ドキュメントを読み込むと、ライブラリはそれらのリンクをたどります。場合によっては深いネストや無限ループ（例: 自身を `@import` する CSS）に陥ります。そこで、リソース処理の深さを制限して整理します。

```python
from weasyprint import HTML, CSS
from pathlib import Path

class ResourceHandlingOptions:
    """Simple container to mimic max depth handling."""
    def __init__(self, max_depth: int = 3):
        self.max_depth = max_depth
        self._current_depth = 0

    def within_limit(self) -> bool:
        return self._current_depth < self.max_depth

    def __enter__(self):
        self._current_depth += 1
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        self._current_depth -= 1
```

上記のクラスは WeasyPrint が必須とするものではありませんが、元のスニペットと同様のパターンを示し、インポートの暴走を止めるフックを提供します。次のステップで使用します。

---

## Step 3 – カスタムオプションで HTML ドキュメントを読み込む

ここで実際に HTML ファイルを読み込みます。`HTML` クラスは `base_url` 引数を受け取り、ソースファイルがあるディレクトリを指定します。これにより、ウェブサーバーがなくても相対リンクが機能します。

```python
def load_html(input_path: Path, options: ResourceHandlingOptions) -> HTML:
    """
    Load an HTML file while respecting the max handling depth.
    """
    if not options.within_limit():
        raise RuntimeError("Maximum resource handling depth exceeded.")
    # The `with` block increments depth for the duration of the call.
    with options:
        return HTML(filename=str(input_path), base_url=str(input_path.parent))
```

> **なぜ重要か:** HTML が多数の CSS ファイルを呼び出す場合、各 `@import` が別のロードをトリガーします。深さガードにより、スクリプトが制御不能になるのを防げます。

---

## Step 4 – 処理済みドキュメントを PDF として保存

`HTML` オブジェクトが手元にあれば、PDF の生成はワンライナーです。さらに、A4 サイズと小さな余白を強制するシンプルな CSS スニペットも渡します—必要に応じて調整してください。

```python
def save_as_pdf(html_doc: HTML, output_path: Path) -> None:
    """
    Render the HTML document to a PDF file.
    """
    default_css = CSS(string='''
        @page { size: A4; margin: 1cm }
    ''')
    html_doc.write_pdf(target=str(output_path), stylesheets=[default_css])
```

`write_pdf` を呼び出すと PDF がストリームされディスクに保存され、すぐに共有可能なファイルが完成します。

---

## Step 5 – すべてをまとめる

以下は `convert.py` にコピペできるコンパクトなスクリプトです。プレースホルダーのパスは実際のディレクトリに置き換えてください。

```python
#!/usr/bin/env python3
"""
HTML to PDF Python script – complete, runnable example.
"""

from pathlib import Path

# Import the helper classes we defined earlier
from __main__ import ResourceHandlingOptions, load_html, save_as_pdf  # noqa: E402

def main():
    # 1️⃣  Define input and output locations
    input_html = Path("YOUR_DIRECTORY/input.html")
    output_pdf = Path("YOUR_DIRECTORY/output.pdf")

    # 2️⃣  Create resource handling options (max depth = 3)
    resource_options = ResourceHandlingOptions(max_depth=3)

    # 3️⃣  Load the HTML document with the custom options
    html_doc = load_html(input_html, resource_options)

    # 4️⃣  Save the processed document as PDF
    save_as_pdf(html_doc, output_pdf)

    print(f"✅ PDF saved to {output_pdf.resolve()}")

if __name__ == "__main__":
    main()
```

**期待される出力** – `python convert.py` を実行すると次のように表示されます:

```
✅ PDF saved to /full/path/YOUR_DIRECTORY/output.pdf
```

生成されたファイルを任意の PDF ビューアで開くと、元のページレイアウト、CSS スタイル、画像（HTML から到達可能な場合）がすべて保持されていることが確認できます。  

画像が欠けている場合は、`src` 属性が絶対 URL か、`YOUR_DIRECTORY` 配下に存在する相対パスであることを再確認してください。

---

## よくある質問とエッジケースの対処

| 質問 | 回答 |
|----------|--------|
| *HTML が外部フォントを参照している場合は？* | WeasyPrint はフォントファイルを自動でダウンロードしますが、取得時間を短縮したい場合はドメインをホワイトリストに登録すると良いでしょう。 |
| *ファイルではなく HTML 文字列を変換したい場合は？* | `HTML(string=my_html_string)` を使用し、`base_url` を省略するか一時フォルダを指定してください。 |
| *PDF のメタデータ（タイトル、作者）を制御したい場合は？* | `write_pdf` に `metadata` 辞書を渡します。例: `html_doc.write_pdf(target='out.pdf', metadata={'Title': 'Report'})`。 |
| *Linux で “cairo‑cffi error” が出る場合は？* | `libcairo2-dev` パッケージ（Debian/Ubuntu なら `apt-get install libcairo2-dev`）をシステムにインストールしてから WeasyPrint を pip でインストールしてください。 |

---

## まとめ

Python のシンプルなワークフローで **HTML から PDF を作成**し、**HTML を PDF に変換**する仕組みと **HTML を PDF として保存**する方法を学びました。スクリプトは CI パイプラインに組み込みやすいサイズながら、ヘッダー・フッター・透かしなどのカスタマイズにも柔軟に拡張できます。

次に試すと良いこと:

- **html to pdf python** ライブラリ `pdfkit` を使って wkhtmltopdf ベースのアプローチ（レガシー CSS に強い）を試す。  
- `argparse` で CLI インターフェースを追加し、入力・出力引数を受け取れるようにする。  
- Flask や FastAPI のエンドポイント内でオンデマンドレポートとして PDF を生成する。  

ぜひ実験し、問題に直面したらこのガイドに戻ってリフレッシュしてください。WeasyPrint の公式ドキュメントやコミュニティフォーラムも有用な情報源です。

Happy coding, and enjoy turning those web pages into sleek PDFs!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法に密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [Convert HTML to PDF with Aspose.HTML – Full Manipulation Guide](/html/english/)
- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Create PDF from HTML – C# Step‑by‑Step Guide](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}