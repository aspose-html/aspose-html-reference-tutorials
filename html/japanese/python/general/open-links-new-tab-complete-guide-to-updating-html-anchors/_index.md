---
category: general
date: 2026-07-05
description: Pythonでリンクを新しいタブで開く – target="_blank" を追加する方法、リンクのターゲットを変更する方法、属性containsセレクタを使用する方法、そして修正したHTMLを手軽に保存する方法を学びましょう。
draft: false
keywords:
- open links new tab
- add target blank
- change link target
- attribute contains selector
- save modified html
language: ja
og_description: リンクをすばやく新しいタブで開く。このチュートリアルでは、target="_blank" を追加し、リンクのターゲットを変更し、Pythonで変更した
  HTML を保存する方法を示します。
og_title: リンクを新しいタブで開く – ステップバイステップ HTML 更新ガイド
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  headline: Open Links New Tab – Complete Guide to Updating HTML Anchors
  type: TechArticle
- description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  name: Open Links New Tab – Complete Guide to Updating HTML Anchors
  steps:
  - name: Expected Result
    text: 'Suppose `links.html` originally contained:'
  - name: What if a link already has a `rel` attribute?
    text: 'Our loop overwrites it with `"noopener"`. If you need to preserve existing
      values (e.g., `"nofollow"`), concatenate instead:'
  - name: How to handle multiple domains?
    text: 'Just expand the selector list:'
  - name: Does `prettify()` change the original HTML structure?
    text: It re‑indents but doesn’t alter tag order or attribute values. If you must
      keep the exact original whitespace, replace `prettify()` with `str(soup)` as
      mentioned earlier.
  type: HowTo
tags:
- HTML manipulation
- Python
- web automation
title: リンクを新しいタブで開く – HTMLアンカーの更新完全ガイド
url: /ja/python/general/open-links-new-tab-complete-guide-to-updating-html-anchors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# リンクを新しいタブで開く – HTMLアンカー更新の完全ガイド

静的なHTMLページで **リンクを新しいタブで開く** 必要があったけど、どこから始めればいいか分からなかったことはありませんか？ あなたは一人ではありません。レガシーサイトのクリーンアップやアクセシビリティの調整を行う際、多くの開発者がこの壁にぶつかります。このチュートリアルでは、**target blank を追加**し、**リンクのターゲットを変更**し、**変更したHTMLを安全に保存**する実用的な解決策を、数行のPythonで解説します。

また、**属性含有セレクタ**の使い方も紹介します。これにより、実際に必要なアンカー（例: *example.com* を指すすべてのリンク）だけを対象にできます。最後まで読むと、規模に関係なくどのプロジェクトにも組み込める再利用可能なスクリプトが手に入ります。

## 学べること

- HTMLファイルを操作可能なドキュメントオブジェクトに読み込む。  
- `href`属性に特定の部分文字列を含む `<a>` 要素を選択する。  
- **target blank を追加**し、`rel="noopener"`属性を設定してセキュリティを向上させる。  
- **変更したHTMLを保存**し、書式を失わずにディスクに書き込む。  

標準ライブラリと **beautifulsoup4**（ごく小さなインストール）以外の外部依存はありません。別のパーサーを使用している場合でも、概念はそのまま適用できます。

---

## 前提条件

- Python 3.8 以上がマシンにインストールされていること。  
- HTML と Python の基本的な知識があること。  
- `beautifulsoup4` パッケージ（`pip install beautifulsoup4`）。  

以上です—重厚なフレームワークは不要です。

---

## 手順 1: HTML ドキュメントを読み込む

まず最初に、ソースファイルを読み込み、BeautifulSoup に渡す必要があります。これは新しい属性を書き込める空白のキャンバスを開くようなものです。

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Path to the original HTML file
html_path = Path("YOUR_DIRECTORY/links.html")

# Read the file content
with html_path.open(encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")
```

> **なぜ重要か:** `Path` を使用するとコードが OS 非依存になり、`html.parser` は組み込みなので、シンプルなタスクに追加のパーサーは不要です。

---

## 手順 2: 属性含有セレクタを使用して対象リンクを見つける

対象とするのは *example.com* を指すアンカーだけです。CSS セレクタ `a[href*='example.com']` はまさにそれを行います—`*=` は「含む」ことを意味します。BeautifulSoup の `select` メソッドはこの構文を理解します。

```python
# Find all <a> tags whose href contains 'example.com'
selector = "a[href*='example.com']"
anchor_elements = soup.select(selector)
```

> **プロのコツ:** 大文字小文字を区別しないマッチが必要な場合は、`if 'example.com' in a.get('href', '').lower()` のような小さなループに切り替えてください。

これで `anchor_elements` には対象となるすべてのリンクが格納され、次の変換の準備が整いました。

---

## 手順 3: リンクのターゲットを変更 – target blank を追加しリンクを保護する

新しいタブでリンクを開くには `target="_blank"` を設定すれば完了です。ただし、モダンブラウザは `rel="noopener"`（または `noreferrer`）も追加することを推奨しています。これにより、新しく開いたページが `window.opener` を介して元のウィンドウにアクセスするのを防ぎます。この小さなセキュリティ対策はフィッシング攻撃を防止できます。

```python
for anchor in anchor_elements:
    # Open in a new tab
    anchor['target'] = "_blank"          # add target blank
    # Harden security
    anchor['rel'] = "noopener"           # prevent access to the opener page
```

> **直接辞書代入を使う理由:** 属性が存在しない場合は自動で作成し、既に存在する場合は上書きします—**リンクのターゲット変更** 操作に最適です。

---

## 手順 4: 変更した HTML をディスクに保存する

最終ステップは、更新したマークアップを新しいファイルに書き込むことです。元のファイルをそのまま残しておくことで、問題が発生した際に元に戻すことができます。

```python
# Destination path for the updated HTML
output_path = Path("YOUR_DIRECTORY/links-updated.html")

# Write the prettified HTML (preserves indentation)
with output_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())
```

> **`prettify()` の役割:** HTML を見やすいインデントで整形し、保存したファイルを後で読みやすく、差分を取りやすくします。元の空白文字を保持したい場合は、`prettify()` を `str(soup)` に置き換えてください。

---

## 完全スクリプト – ワンクリックソリューション

以下に、完全で実行可能なスクリプトを示します。`update_links.py` として保存し、ターミナルで `python update_links.py` を実行してください。

```python
#!/usr/bin/env python3
"""
Open Links New Tab – script that adds target blank,
sets rel="noopener", and saves modified html.
"""

from pathlib import Path
from bs4 import BeautifulSoup

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Load the HTML document
    # ------------------------------------------------------------------
    html_path = Path("YOUR_DIRECTORY/links.html")
    with html_path.open(encoding="utf-8") as f:
        soup = BeautifulSoup(f, "html.parser")

    # ------------------------------------------------------------------
    # 2️⃣ Select anchors with an attribute contains selector
    # ------------------------------------------------------------------
    selector = "a[href*='example.com']"
    anchors = soup.select(selector)

    # ------------------------------------------------------------------
    # 3️⃣ Change link target – add target blank & secure the link
    # ------------------------------------------------------------------
    for a in anchors:
        a['target'] = "_blank"          # add target blank
        a['rel'] = "noopener"           # prevent opener access

    # ------------------------------------------------------------------
    # 4️⃣ Save modified html to a new file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/links-updated.html")
    with output_path.open("w", encoding="utf-8") as f:
        f.write(soup.prettify())

    print(f"✅ Updated {len(anchors)} link(s) and saved to {output_path}")

if __name__ == "__main__":
    main()
```

### 期待される結果

例えば、`links.html` が元々次のような内容だったとします:

```html
<a href="https://example.com/page1">Page 1</a>
<a href="https://other.com/home">Home</a>
```

スクリプトを実行した後、`links-updated.html` は次のようになります:

```html
<a href="https://example.com/page1" target="_blank" rel="noopener">Page 1</a>
<a href="https://other.com/home">Home</a>
```

*example.com* へのリンクだけが **add target blank** 属性を受け取り、**属性含有セレクタ** が意図通りに機能したことが示されています。

---

## よくある質問とエッジケース

### リンクにすでに `rel` 属性がある場合は？

ループはそれを "noopener" で上書きします。既存の値（例: "nofollow"）を保持したい場合は、代わりに連結してください:

```python
existing = a.get('rel', '')
a['rel'] = f"{existing} noopener".strip()
```

### 複数ドメインを扱うには？

セレクタリストを拡張すれば済みます:

```python
domains = ["example.com", "sample.org"]
selector = ",".join([f"a[href*='{d}']" for d in domains])
anchors = soup.select(selector)
```

### `prettify()` は元の HTML 構造を変更しますか？

インデントは整えますが、タグの順序や属性値は変更しません。元の空白文字を完全に保持する必要がある場合は、前述の通り `prettify()` を `str(soup)` に置き換えてください。

---

## 本番環境向けスクリプトのプロティップ

- **上書き前にバックアップ:** コピー手順（`shutil.copy`）を追加して元ファイルを安全に保管する。  
- **print の代わりにロギング:** スケーラブルなプロジェクトには `logging` モジュールを使用する。  
- **バッチ処理:** `Path.rglob("*.html")` でディレクトリをループし、一度の実行で多数のファイルを更新する。  

これらの調整により、シンプルな **open links new tab** スクリプトが、あらゆるウェブ保守ワークフローに対応できる堅牢なユーティリティへと変わります。

---

## 結論

これで、任意の静的HTMLコレクション全体で **open links new tab** を実現する、堅牢で再利用可能な方法が手に入りました。**属性含有セレクタ** を活用すれば、必要な場所で正確に **change link target** ができ、**add target blank** を行い、**save modified html** しても書式を失いません。

まずテストページで試してみてから、サイト全体に拡張してください。PDF や他のドメイン用にセレクタを調整する必要がありますか？ CSS 文字列を変更すれば、他はそのままです。

問題が発生したら遠慮なくコメントを残すか、スクリプトを自分のプロジェクトで拡張した方法を共有してください。コーディングを楽しんで、すべてのアンカーが思い通りの場所で開くことを願っています！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説付きの完全なコード例が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [Aspose.HTML for Java を使用した HTML 編集方法](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Aspose.HTML for Java で HTML ドキュメントに CSS を追加 – インライン CSS](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}