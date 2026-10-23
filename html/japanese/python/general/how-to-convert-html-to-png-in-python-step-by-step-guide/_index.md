---
category: general
date: 2026-10-21
description: HTML を PNG に素早く変換する方法を学びましょう。このチュートリアルでは、ウェブページを PNG にエクスポートする方法や、Python
  を使って HTML ファイルを PNG に変換する方法も取り上げています。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to png
- export webpage to png
- how to convert html to image
- convert html file to png
language: ja
lastmod: 2026-10-21
og_description: PythonでHTMLをPNGに変換。ウェブページをPNGにエクスポートし、エッジケースに対応し、画像生成を自動化するための明確なガイドに従ってください。
og_image_alt: Screenshot of HTML page converted to PNG using Python
og_title: PythonでHTMLをPNGに変換する – 完全プログラミングガイド
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  headline: How to convert HTML to PNG in Python – step‑by‑step guide
  type: TechArticle
- description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  name: How to convert HTML to PNG in Python – step‑by‑step guide
  steps:
  - name: Expected output
    text: 'Running the script prints:'
  - name: Why adjust viewport size?
    text: Web pages designed for desktop screens often look cramped if rendered at
      a small width. By increasing the `width` and `height` options, you capture the
      full layout, which is especially useful for **export webpage to PNG** tasks.
  - name: 6.1 Large pages or infinite scroll
    text: 'For pages that load content lazily (e.g., infinite scroll), increase the
      JavaScript delay and optionally set a larger viewport:'
  - name: 6.2 Authentication‑protected pages
    text: 'If a page requires a session cookie, you can embed the cookie header:'
  - name: 6.3 Missing images or fonts
    text: '`wkhtmltoimage` respects the `--disable-local-file-access` flag for security.
      If your HTML references local assets, enable them explicitly:'
  type: HowTo
tags:
- python
- html conversion
- image processing
- web automation
title: PythonでHTMLをPNGに変換する方法 – ステップバイステップガイド
url: /ja/python/general/how-to-convert-html-to-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでHTMLをPNGに変換する – 完全プログラミングガイド

HTMLをPNGに変換する必要がある場合、このガイドではプレーンなPythonでそれを実現する信頼できる方法を示します。静的レポートのエクスポート、ギャラリー用サムネイルの生成、テスト用スクリーンショットの自動化など、数分で実行可能な完全なソリューションが手に入ります。

また、**export webpage to PNG** の方法を確認し、HTML ファイルとライブ URL の変換の違いを理解し、大規模ページや動的コンテンツの取り扱いに関するベストプラクティスを学びます。外部サービスは不要で、数個の Python パッケージと短いスクリプトだけで完了します。

## 前提条件

- Python 3.9+ がインストールされていること（コードは Windows、macOS、Linux で動作します）
- ターミナルまたはコマンドプロンプトへのアクセス
- Python のパッケージマネージャ (`pip`) の基本的な知識

`imgkit` パッケージ（`wkhtmltoimage` の薄いラッパー）と `wkhtmltoimage` バイナリ自体が必要です。どちらも無料でオープンソースです。

## ステップ 1: 必要なツールをインストール

最初のステップは `wkhtmltoimage` とそれと連携する Python ラッパーをインストールすることです。

```bash
# Install wkhtmltoimage (Linux example)
sudo apt-get update && sudo apt-get install -y wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf

# On Windows download the installer from:
# https://wkhtmltopdf.org/downloads.html
# and add the installation folder to your PATH.

# Install the Python wrapper
pip install imgkit
```

> **このステップが重要な理由** – `wkhtmltoimage` は WebKit エンジンを使用して HTML をレンダリングし、ピクセルパーフェクトな PNG を生成します。`imgkit` は単にオプションをバイナリに転送するだけなので、ブラウザと同等の品質が得られます。

## ステップ 2: インストールを確認

バイナリが Python から参照可能かどうかをすばやくチェックします。

```python
import imgkit

# This will raise an exception if wkhtmltoimage is not found
print("wkhtmltoimage version:", imgkit.config().wkhtmltoimage)
```

スクリプトが `wkhtmltoimage` のパスを出力すれば、HTML を PNG に変換する準備が整っています。`OSError` が出た場合は、バイナリがシステムの `PATH` に含まれているか再確認してください。

## ステップ 3: 再利用可能な変換関数を書く

ロジックを関数にカプセル化することで、プロジェクト内の任意の場所から **convert HTML file to PNG** や **export webpage to PNG** を簡単に実行できます。

```python
import os
import imgkit

def convert_html_to_png(source, output_path, *, options=None):
    """
    Convert an HTML file or URL to a PNG image.

    Parameters
    ----------
    source : str
        Path to a local HTML file (e.g., "report.html") or a URL
        (e.g., "https://example.com").
    output_path : str
        Destination file path for the PNG (e.g., "report.png").
    options : dict, optional
        imgkit options such as viewport size, zoom factor, or
        JavaScript delay. If omitted, sensible defaults are used.

    Returns
    -------
    bool
        True if the conversion succeeded, False otherwise.
    """
    # Use a default set of options if none are provided
    default_options = {
        "format": "png",
        "quality": "100",
        "encoding": "UTF-8",
        "quiet": "",
        # Render at 1280×720 – adjust for your layout
        "width": 1280,
        "height": 720,
        # Wait for JavaScript to finish (ms)
        "javascript-delay": 500,
    }
    # Merge user‑supplied options over defaults
    final_options = {**default_options, **(options or {})}

    try:
        # imgkit can handle both files and URLs transparently
        imgkit.from_file(source, output_path, options=final_options) \
            if os.path.isfile(source) else \
            imgkit.from_url(source, output_path, options=final_options)
        print(f"✅ Successfully saved PNG to: {output_path}")
        return True
    except Exception as e:
        print(f"❌ Conversion failed: {e}")
        return False
```

> **`from_file` と `from_url` の両方をラップする理由** – 同じ関数でローカルファイルとライブウェブページの両方に対して **HTML を画像に変換する方法** をサポートし、コードの DRY（Don’t Repeat Yourself）を保ちます。

## ステップ 4: ローカルの HTML ファイルを PNG に変換

`assets` フォルダーに `sample.html` という名前の HTML ファイルを配置します。次に、先ほど定義したヘルパー関数を呼び出します。

```python
if __name__ == "__main__":
    # Example: convert a static HTML file
    html_path = os.path.join("assets", "sample.html")
    png_path = os.path.join("output", "sample.png")

    # Ensure the output directory exists
    os.makedirs(os.path.dirname(png_path), exist_ok=True)

    # Perform the conversion
    success = convert_html_to_png(html_path, png_path)

    if success:
        # Show a tiny preview in the console (optional)
        from PIL import Image
        img = Image.open(png_path)
        img.thumbnail((200, 200))
        img.show()
```

### 期待される出力

スクリプトを実行すると次のように表示されます：

```
✅ Successfully saved PNG to: output/sample.png
```

新しいファイル `output/sample.png` には `sample.html` のピクセルパーフェクトなスナップショットが保存されます。任意の画像ビューアで開くと、ブラウザで表示されるページと全く同じレンダリング結果が確認できます。

## ステップ 5: ライブウェブページを PNG にエクスポート

頻繁に変化する URL（例: ダッシュボード）を **export webpage to PNG** したい場合は、ファイルパスの代わりに URL 文字列を渡すだけです。

```python
# Example: convert a live page
url = "https://developer.mozilla.org/en-US/docs/Web/HTML"
output_file = "output/mdn_homepage.png"

convert_html_to_png(url, output_file, options={"width": 1920, "height": 1080})
```

### ビューポートサイズを調整する理由

デスクトップ向けに設計されたウェブページは、幅が狭い状態でレンダリングすると窮屈に見えることがあります。`width` と `height` オプションを大きくすることで、レイアウト全体をキャプチャでき、特に **export webpage to PNG** のタスクで有用です。

## ステップ 6: 一般的なエッジケースの処理

### 6.1 大きなページまたは無限スクロール

コンテンツを遅延ロードするページ（例: 無限スクロール）では、JavaScript の遅延時間を伸ばし、必要に応じてビューポートを大きく設定します。

```python
options = {
    "javascript-delay": 2000,   # wait 2 seconds for JS to finish
    "width": 1440,
    "height": 3000,             # tall enough for the whole page
    "disable-smart-width": "", # forces the width we set
}
convert_html_to_png(url, "long_page.png", options=options)
```

### 6.2 認証保護されたページ

ページがセッション Cookie を必要とする場合、Cookie ヘッダーを埋め込むことができます。

```python
options = {
    "custom-header": [
        "Cookie: sessionid=YOUR_SESSION_ID"
    ]
}
convert_html_to_png("https://internal.example.com/report", "report.png", options=options)
```

### 6.3 画像やフォントが欠落している場合

`wkhtmltoimage` はセキュリティ上の理由で `--disable-local-file-access` フラグを尊重します。HTML がローカルアセットを参照している場合は、明示的にそれらへのアクセスを有効にしてください。

```python
options = {"enable-local-file-access": ""}
convert_html_to_png("assets/complex.html", "complex.png", options=options)
```

## ステップ 7: 結果をプログラムで検証する（オプション）

CI パイプラインなどで PNG が正しく生成されたか確認したいことがあります。以下のスニペットはファイルサイズと画像寸法をチェックします。

```python
from pathlib import Path
from PIL import Image

def verify_png(path):
    p = Path(path)
    if not p.is_file():
        raise FileNotFoundError(f"{path} does not exist")
    if p.stat().st_size < 10_000:  # arbitrary minimal size
        raise ValueError("Generated PNG seems too small")
    with Image.open(p) as img:
        print(f"Image size: {img.width}×{img.height}, mode: {img.mode}")

verify_png(png_path)
```

PNG がこれらのチェックを通過すれば、PDF 生成、メール添付、機械学習パイプラインなど、下流プロセスで安全に利用できます。

## 結論

これで Python を使って **convert HTML to PNG** する完全な本番環境向け手法が手に入りました。本ガイドで扱った内容は以下の通りです。

- `wkhtmltoimage` と `imgkit` のインストール
- 環境の検証
- ローカルファイルと URL の両方に対応する再利用可能な `convert_html_to_png` 関数
- 実際の例として **export webpage to PNG**、**how to convert HTML to image**、**convert HTML file to PNG**
- 大きなページ、認証、ローカルアセットに対するエッジケースの処理
- CI/CD パイプライン向けのオプション検証ステップ

`imgkit` の追加オプション（`zoom`、`crop-h`、`crop-w` など）を試して、特定のユースケースに合わせて出力を微調整してください。次のステップとしては、以下を検討できます。

- PNG を PDF レポートに変換する（`img2pdf` ライブラリ）
- HTML ファイルが入ったフォルダー全体のバッチ変換を自動化する
- 完全なブラウザレンダリングが必要なページ（例: 重い JavaScript フレームワーク）に Selenium を使用する

コーディングを楽しんで、ピクセルパーフェクトなスクリーンショットをお楽しみください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックをカバーしています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [HTML を PNG に変換 – 完全 Python ガイド](/html/english/python/general/convert-html-to-png-complete-python-guide/)
- [Python で HTML を PNG に変換 – 完全ストリーミング保存ガイド](/html/english/python/general/convert-html-to-png-in-python-complete-streaming-save-guide/)
- [Aspose.HTML を使用して Python で SVG を PNG に変換](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}