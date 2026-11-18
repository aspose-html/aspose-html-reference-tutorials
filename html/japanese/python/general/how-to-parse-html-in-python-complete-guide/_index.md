---
category: general
date: 2026-05-28
description: PythonでHTMLを素早く解析する方法—HTMLファイルを読み込み、CSSセレクタを使用し、XPathのcontains例でhref属性を抽出する。
draft: false
keywords:
- how to parse html
- get href attribute
- load html file
- use css selector
- xpath contains example
language: ja
og_description: PythonでHTMLを解析する方法：HTMLファイルの読み込み、CSSセレクタの使用、XPath contains を使った href
  属性の取得例を学ぶ。
og_title: PythonでHTMLを解析する方法 – ステップバイステップ
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  headline: How to Parse HTML in Python – Complete Guide
  type: TechArticle
- description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  name: How to Parse HTML in Python – Complete Guide
  steps:
  - name: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
    text: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
  - name: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
    text: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
  - name: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
    text: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
  - name: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
    text: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
  type: HowTo
tags:
- html parsing
- python
- web scraping
title: PythonでHTMLを解析する方法 – 完全ガイド
url: /ja/python/general/how-to-parse-html-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでHTMLを解析する方法 – 完全ガイド

重いブラウザを使わずに **Python スクリプトで HTML を解析する方法** を考えたことはありませんか？ あなただけではありません。多くの人は **HTML ファイルを読み込み**、いくつかの見出しをスクレイプし、場合によってはダウンロードリンクを取得したいだけです。このチュートリアルでは、軽量ライブラリと CSS セレクタ、そして XPath contains の例を使って **href 属性** の値を取得する方法を実演します。

ローカルの HTML ドキュメントを読み込むところから、必要なデータを出力するまでの全工程を解説します。余計な説明は省き、すぐに自分のプロジェクトに組み込める実用的なサンプルを提供します。

## 学べること

- 軽量パーサで **HTML ファイルを読み込む** 方法
- **CSS セレクタ** 構文を使って記事の見出しを取得する方法
- リンクを絞り込む **XPath contains の例** の作り方
- マッチしたノードから安全に **href 属性** の値を取得する方法
- 不正なマークアップへの対処法やスクリプトの拡張方法

必要なのは Python 3.8+ と `lxml`、`cssselect` パッケージだけです。どちらも `pip` コマンド一つでインストールできます。

---

## Step 1: Load the HTML File

まず最初に、HTML コンテンツをメモリ上に読み込む必要があります。`lxml.html` モジュールの便利な `fromstring` ヘルパーもありますが、ディスク上にファイルがある場合は `parse` 関数の方がシンプルです。

```python
# Step 1: Load the HTML file
from lxml import html

# Replace the path with the location of your HTML document
html_path = "YOUR_DIRECTORY/news.html"
doc = html.parse(html_path)

# The root element gives us access to CSS and XPath methods
root = doc.getroot()
```

> **Why this matters:** ファイルを一度だけ読み込むことでメモリ使用量を抑え、CSS セレクタと XPath クエリの両方に対応した単一の `root` オブジェクトを取得できます。ファイルが存在しない、または読み取れない場合は `html.parse` が明確な `OSError` を投げるので、後で捕捉できます。

### Pro tip
文字列から解析したい場合は、`html.parse` の代わりに `html.fromstring(your_html_string)` を使用してください。

---

## Step 2: Use CSS Selector to Get Headlines

CSS セレクタは簡潔で、スタイルシートを書いたことがある人なら誰でも馴染みがあります。ここでは `<article>` 内のすべての `<h2>` を取得し、ニュースの見出しを抽出します。

```python
# Step 2: Find all article headlines using a CSS selector
headline_nodes = root.cssselect("article h2")

# Print each headline's text content
for node in headline_nodes:
    print(node.text_content().strip())
```

**Expected output** (サンプル HTML に 2 件の article があると仮定):

```
Breaking News: Python Takes Over the World
Local Developer Solves HTML Parsing Puzzle
```

> **Why CSS?** 読みやすく高速で、`lxml` ではデフォルトで利用可能です。`cssselect` メソッドは内部でセレクタを XPath 式に変換するため、両方の長所を活かせます。

---

## Step 3: XPath Contains Example – Find “download” Links

CSS だけでは実現しにくい細かい条件が必要なときは、XPath の `contains()` 関数が便利です。属性内の部分文字列にマッチさせることで、ダウンロードリンクだけを抽出できます。

```python
# Step 3: Find all links that contain the word "download" using XPath
download_link_nodes = root.xpath("//a[contains(@href, 'download')]")

# Extract and print the href attribute from each matching node
for node in download_link_nodes:
    href = node.get("href")
    print(href)
```

**Sample output**:

```
/files/report_download.pdf
https://example.com/downloads/setup.exe
```

> **Why XPath contains?** 余計な Python ループを書かずに属性値で直接フィルタリングできる点が魅力です。チュートリアルでよく見かける **xpath contains example** を実務的なケースに当てはめた例です。

---

## Step 4: Wrap It All Into a Reusable Function

テスト用にパスや `print` をハードコーディングするのは手軽ですが、実際のプロダクションコードでは関数化が望まれます。以下は見出しとダウンロードリンクの両方を返すコンパクトなヘルパーです。

```python
def parse_news_html(file_path):
    """
    Parse a news HTML file and return headlines plus download URLs.

    Parameters
    ----------
    file_path : str
        Path to the local HTML document.

    Returns
    -------
    dict
        {
            "headlines": list of strings,
            "download_links": list of href strings
        }
    """
    doc = html.parse(file_path)
    root = doc.getroot()

    # Headlines via CSS selector
    headlines = [
        node.text_content().strip()
        for node in root.cssselect("article h2")
    ]

    # Download links via XPath contains
    download_links = [
        node.get("href")
        for node in root.xpath("//a[contains(@href, 'download')]")
    ]

    return {"headlines": headlines, "download_links": download_links}
```

関数を呼び出して結果を整形して表示できます：

```python
if __name__ == "__main__":
    results = parse_news_html("YOUR_DIRECTORY/news.html")
    print("Headlines:")
    for h in results["headlines"]:
        print(f"- {h}")

    print("\nDownload Links:")
    for link in results["download_links"]:
        print(f"- {link}")
```

スクリプトを実行すると前述と同じ出力が得られますが、再利用しやすい形にまとめられています。

---

## Step 5: Handling Edge Cases and Common Pitfalls

1. **Missing `href` attribute** – XPath は `href` が無くても `<a>` ノードを返します。`None` に対するガードが必要です：

   ```python
   href = node.get("href")
   if href:
       download_links.append(href)
   ```

2. **Relative vs. absolute URLs** – リンクが相対パスの場合は、ベース URL に対して解決することを検討してください：

   ```python
   from urllib.parse import urljoin
   base_url = "https://example.com"
   absolute = urljoin(base_url, href)
   ```

3. **Malformed HTML** – `lxml` は寛容ですが、極端に壊れたマークアップは `html.parse` が `XMLSyntaxError` を投げることがあります。`try/except` でラップしてエラーログを残し、問題のあるファイルはスキップしましょう。

4. **Performance with large files** – 数メガバイト規模のページを扱う場合は、DOM 全体をメモリに読み込む代わりに `iterparse` を使ったストリーミング解析を検討してください。

---

## Visual Overview (optional)

![How to parse HTML flow diagram showing load file → CSS selector → XPath contains → get href attribute](how-to-parse-html-flow.png "How to parse HTML flow diagram")

*Alt text includes the primary keyword to satisfy SEO.*

---

## Conclusion

**Python で HTML を解析する方法** を、HTML ファイルの読み込み、CSS セレクタで記事見出しを取得、XPath contains でダウンロードリンクを抽出、そして安全に **href 属性** を取得するまで、ステップバイステップで解説しました。再利用可能な `parse_news_html` 関数は、どんなスクレイピングタスクにも応用できるクリーンで保守性の高い実装例です。

次のチャレンジに挑戦してみませんか？

- `//table//tr` XPath クエリでテーブルを解析する
- 別の **xpath contains example** を使って画像の `src` 属性を抽出する
- ライブページ向けに `aiohttp` を使った非同期取得に切り替える

楽しく解析しましょう。疑問や問題があればコメントで教えてください—一緒に解決していきましょう！

## Related Tutorials

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}