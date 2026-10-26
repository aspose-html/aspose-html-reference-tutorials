---
category: general
date: 2026-06-04
description: EPUBからテキストをすばやく取得し、EPUBファイルの読み取り方法、EPUBをテキストに変換する方法、そしてPythonを使って章を抽出する方法を学びましょう。
draft: false
keywords:
- get text from epub
- convert epub to text
- how to read epub
language: ja
og_description: Pythonで数分でEPUBからテキストを取得。このチュートリアルでは、EPUBファイルの読み取り方法、EPUBをテキストに変換する方法、そして一般的なエッジケースの処理方法を示します。
og_title: PythonでEPUBからテキストを取得する – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-04'
  description: Get text from EPUB quickly and learn how to read EPUB files, convert
    EPUB to text, and extract chapters using Python.
  headline: Get Text from EPUB in Python – Complete Guide
  type: TechArticle
- description: Get text from EPUB quickly and learn how to read EPUB files, convert
    EPUB to text, and extract chapters using Python.
  name: Get Text from EPUB in Python – Complete Guide
  steps:
  - name: Import Libraries and Load the EPUB
    text: '```python from pathlib import Path from ebooklib import epub from bs4 import
      BeautifulSoup'
  - name: Grab the First Chapter (First <section> Element)
    text: '```python # Find the first HTML document inside the EPUB first_item = None
      for item in book.get_items(): if item.get_type() == epub.ITEM_DOCUMENT: first_item
      = item break'
  - name: Strip Tags and Output Plain Text
    text: '```python # .get_text() removes all HTML tags and returns clean text chapter_text
      = first_chapter.get_text(separator="

      ", strip=True)'
  - name: Full Script – Ready to Run
    text: '```python #!/usr/bin/env python3 """ Get text from EPUB – extract the first
      chapter and print it as plain text. """'
  type: HowTo
- questions:
  - answer: Not directly. `.mobi` uses a different container format. Convert it to
      EPUB first (Calibre does a solid job), then apply the same script.
    question: Can I use this with a .mobi file?
  - answer: The fallback to `<body>` (shown in the code) covers that case. You can
      also look for `<div class="chapter">` if the publisher uses custom markup.
    question: What if the EPUB has no `<section>` tags?
  - answer: 'No. Alternatives include `zipfile` + manual HTML parsing, or `pypub`
      for a higher‑level API. `ebooklib` is popular because it abstracts the ZIP handling
      and gives you item types out of the box. --- ## Conclusion You now know how
      to **get text from EPUB** files using Python, whether you need just the'
    question: Is `ebooklib` the only library?
  type: FAQPage
tags:
- python
- epub
- text‑extraction
title: PythonでEPUBからテキストを取得する – 完全ガイド
url: /ja/python/general/get-text-from-epub-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでEPUBからテキストを取得する – 完全ガイド

大きなリーダーを開かずに **EPUBを読む** 方法を考えたことはありませんか？最初の章だけを分析したい場合や、**EPUBをテキストに変換** してすばやく検索したい場合など、どんなケースでもここが正解です。このチュートリアルでは、数行のPythonで **EPUBからテキストを取得** する方法を示し、各ステップの理由も解説しますので、任意の書籍に応用できます。

正しいライブラリのインストール、EPUBの読み込み、最初の `<section>` 要素の抽出、プレーンテキストの出力まで順を追って説明します。最後には、フォルダーに入れた任意のEPUBで動作する再利用可能なスクリプトが手に入ります。

## 前提条件

- Python 3.8+（コードは f‑strings と pathlib を使用）
- モダンなIDEまたはターミナル
- `ebooklib` と `beautifulsoup4` パッケージ（`pip install ebooklib beautifulsoup4` でインストール）

他に外部ツールは不要で、スクリプトは Windows、macOS、Linux いずれでも動作します。

---

## EPUBからテキストを取得する – 手順ごとに解説

以下はタイトルが約束する通り、**EPUBからテキストを取得**し最初の章を出力するコアロジックです。各行の意味が分かるように分解して説明します。

### 手順 1: ライブラリをインポートしてEPUBを読み込む

```python
from pathlib import Path
from ebooklib import epub
from bs4 import BeautifulSoup

# Path to the .epub file – change this to your own location
EPUB_PATH = Path("YOUR_DIRECTORY/book.epub")

# Load the EPUB container
book = epub.read_epub(EPUB_PATH)
```

*このステップの理由*  
`ebooklib` は ZIP ベースの EPUB 構造を理解し、`BeautifulSoup` は埋め込まれた HTML のパースを簡単にします。`Path` を使うことでコードが OS 非依存になります。

### 手順 2: 最初の章（最初の `<section>` 要素）を取得する

```python
# Find the first HTML document inside the EPUB
first_item = None
for item in book.get_items():
    if item.get_type() == epub.ITEM_DOCUMENT:
        first_item = item
        break

if not first_item:
    raise ValueError("No HTML content found in the EPUB.")

# Parse the HTML with BeautifulSoup
soup = BeautifulSoup(first_item.get_content(), "html.parser")

# Retrieve the first <section> element – this usually holds a chapter
first_chapter = soup.find("section")
if not first_chapter:
    # Fallback: use the first <body> if no <section> exists
    first_chapter = soup.body
```

*このステップの理由*  
EPUB は各章を HTML ファイルとして格納しています。ループは最初のドキュメントで止まりますが、これは通常カバーや序文です。最初の `<section>` を対象にすることで実際の最初の章に直接アクセスできます。セクションがない本に備えて `<body>` 要素へのフォールバックも用意しています。

### 手順 3: タグを除去してプレーンテキストを出力する

```python
# .get_text() removes all HTML tags and returns clean text
chapter_text = first_chapter.get_text(separator="\n", strip=True)

print(chapter_text)
```

*このステップの理由*  
`get_text()` は **EPUBをテキストに変換** する最もシンプルな方法です。`separator` 引数によりブロック要素ごとに改行が入るので、出力が読みやすくなります。

### 完全スクリプト – 実行可能な形

```python
#!/usr/bin/env python3
"""
Get text from EPUB – extract the first chapter and print it as plain text.
"""

from pathlib import Path
from ebooklib import epub
from bs4 import BeautifulSoup

def extract_first_chapter(epub_path: Path) -> str:
    """Return the plain‑text of the first chapter in an EPUB file."""
    book = epub.read_epub(epub_path)

    # Locate the first HTML document
    first_item = next(
        (i for i in book.get_items() if i.get_type() == epub.ITEM_DOCUMENT),
        None,
    )
    if not first_item:
        raise ValueError("The EPUB does not contain any HTML documents.")

    soup = BeautifulSoup(first_item.get_content(), "html.parser")

    # Try to find a <section>; otherwise fall back to <body>
    chapter_tag = soup.find("section") or soup.body
    if not chapter_tag:
        raise ValueError("No readable content found in the first HTML document.")

    # Clean the text
    return chapter_tag.get_text(separator="\n", strip=True)


if __name__ == "__main__":
    # Replace with the actual path to your EPUB file
    EPUB_PATH = Path("YOUR_DIRECTORY/book.epub")
    try:
        text = extract_first_chapter(EPUB_PATH)
        print(text)
    except Exception as e:
        print(f"Error: {e}")
```

このファイルを `extract_epub.py` として保存し、`python extract_epub.py` を実行してください。環境が正しく設定されていれば、最初の章のテキストがコンソールに表示されます。

![端末出力のスクリーンショット（抽出されたEPUBテキストを表示）](get-text-from-epub.png "EPUBからテキストを取得した例の出力")

---

## EPUBをテキストに変換する – スケールアップ

上記スニペットは単一章のみを処理しますが、ほとんどのプロジェクトでは書籍全体を 1 つの大きな文字列として取得したいでしょう。以下は **すべて** のドキュメントアイテムをループし、クリーンなテキストを連結して `.txt` ファイルに書き出す拡張例です。

```python
def convert_epub_to_text(epub_path: Path, output_path: Path) -> None:
    """Convert an entire EPUB into a plain‑text file."""
    book = epub.read_epub(epub_path)
    all_text = []

    for item in book.get_items():
        if item.get_type() == epub.ITEM_DOCUMENT:
            soup = BeautifulSoup(item.get_content(), "html.parser")
            # Grab everything inside <body> – safe for most EPUBs
            body = soup.body
            if body:
                all_text.append(body.get_text(separator="\n", strip=True))

    output_path.write_text("\n\n".join(all_text), encoding="utf-8")
    print(f"✅ EPUB converted – saved to {output_path}")

# Example usage
if __name__ == "__main__":
    EPUB_PATH = Path("YOUR_DIRECTORY/book.epub")
    TXT_PATH = Path("YOUR_DIRECTORY/book.txt")
    convert_epub_to_text(EPUB_PATH, TXT_PATH)
```

**プロのコツ:** 一部の EPUB にはスクリプトやスタイルタグが埋め込まれており、`BeautifulSoup` が混乱することがあります。文字化けが発生したら `soup = BeautifulSoup(item.get_content(), "lxml")` とし、より厳格なパーサー用に `lxml` をインストールしてください。

---

## EPUBファイルを効率的に読む – よくある落とし穴

1. **エンコーディングの予期せぬ挙動** – EPUB は UTF‑8 の HTML を含む ZIP ファイルです。`UnicodeDecodeError` が出たら、読み取り時に UTF‑8 を強制してください: `item.get_content().decode("utf-8", errors="ignore")`。
2. **多言語対応** – 言語が混在する書籍は言語ごとに別々の `<section>` タグを持つことがあります。必要に応じて `soup.find_all("section")` で取得し、`lang` 属性でフィルタリングしてください。
3. **画像と脚注** – スクリプトはタグを除去するため、画像の alt テキストは失われます。必要なら `<img>` の `alt` 属性や脚注の `<a>` リンクをクリーン前に抽出しましょう。
4. **大容量の書籍** – 各章をメモリに保持すると RAM が逼迫します。クリーンした章を逐次ファイルに追記モードで書き出すことでメモリ使用量を抑えられます。

---

## FAQ – 典型的な質問への簡潔な回答

**Q: .mobi ファイルでも使えますか？**  
A: 直接はできません。`.mobi` は別のコンテナ形式です。まず Calibre などで EPUB に変換し、同じスクリプトを適用してください。

**Q: EPUB に `<section>` タグが全くない場合は？**  
A: コードに示した `<body>` へのフォールバックがそのケースをカバーします。出版社が独自のマークアップ（例: `<div class="chapter">`）を使っている場合はそれを検索してください。

**Q: `ebooklib` だけが唯一の選択肢ですか？**  
A: いいえ。`zipfile` と手動 HTML パースの組み合わせや、より高レベルな API を提供する `pypub` などの代替もあります。`ebooklib` が人気なのは、ZIP 処理を抽象化し、アイテムタイプをすぐに取得できる点です。

---

## 結論

Python を使って **EPUBからテキストを取得** する方法が分かりました。最初の章だけでも、書籍全体でも、**EPUBをテキストに変換** する基本手順と各行の意図、考慮すべきエッジケースを網羅しました。

次は `book.get_metadata('DC', 'title')` でメタデータ（タイトル、著者）を抽出したり、出力形式を Markdown や JSON に変えてみたりしてください。同じ原則が適用できるので、類似のファイルパース課題にも自信を持って取り組めます。

楽しいコーディングを！問題があればコメントで遠慮なく質問してください。

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能をマスターしたり、代替実装アプローチを自分のプロジェクトに取り入れたりするのに役立ちます。

- [How to Convert EPUB to PDF with Java – Using Aspose.HTML](/html/english/java/converting-epub-to-pdf/convert-epub-to-pdf/)
- [Convert EPUB to Images Using Aspose HTML for Java](/html/english/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)
- [Convert EPUB to PDF and Images with Aspose.HTML for Java](/html/english/java/conversion-epub-to-image-and-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}