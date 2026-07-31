---
category: general
date: 2026-07-31
description: SVGドキュメントの作成方法、円の追加方法、そしてSVGファイルの迅速な保存方法を学びましょう。数行のPythonコードでグラフィックをSVGとしてエクスポートできます。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg document
- save svg file
- export graphic as svg
- add circle to svg
language: ja
lastmod: 2026-07-31
og_description: SVGドキュメントを作成し、円を追加して、数秒でSVGファイルを保存します。このガイドでは、明確で実行可能なコードを使ってグラフィックをSVGとしてエクスポートする方法を示します。
og_image_alt: Screenshot of a red circle inside an SVG file named circle.svg
og_title: SVGドキュメントを作成 – 円を追加してSVGとして保存
schemas:
- author: Aspose
  dateModified: '2026-07-31'
  description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  headline: Create SVG Document – Add a Circle and Save as SVG
  type: TechArticle
- description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  name: Create SVG Document – Add a Circle and Save as SVG
  steps:
  - name: Pro tip
    text: If you plan to generate many files in a loop, give each `Drawing` a unique
      name or use `io.BytesIO` to keep everything in memory until you’re ready to
      write.
  - name: Edge case – Transparent background
    text: 'If you need a transparent background (the default for SVG), you can skip
      setting a `fill` on the root. For a white background, add:'
  - name: 'Bonus: Export graphic as SVG programmatically'
    text: 'If you need the SVG content as a string—for example, to embed it in an
      HTML email—you can call `dwg.tostring()` instead of `save()`:'
  type: HowTo
- questions:
  - answer: Swap `dwg.circle` for `dwg.rect`, `dwg.ellipse`, or even a custom `<path>`
      string. The API is consistent across shapes.
    question: What if I want a different shape?
  - answer: Absolutely. The file you just created can be referenced with `<img src="circle.svg"
      alt="Red circle">` or inlined with `<svg>` tags.
    question: Can I embed the SVG directly in HTML?
  - answer: You could, but libraries like `svgwrite` handle namespace quirks and make
      the code far more maintainable—especially when you start adding gradients or
      animations.
    question: Why not write raw XML?
  type: FAQPage
tags:
- svg
- python
- vector-graphics
- programming-tutorial
title: SVGドキュメントの作成 – 円を追加し、SVGとして保存
url: /ja/python/general/create-svg-document-add-a-circle-and-save-as-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SVG ドキュメントの作成 – 円を追加して SVG として保存

コードから **create SVG document** が必要だったことはありますか、でもどこから始めればいいか分からなかったことはありませんか？ あなたは一人ではありません。ベクターグラフィックに初めて触れる多くの開発者が同じ壁にぶつかります。このチュートリアルでは、**add circle to SVG** の方法と **save SVG file** の手順を示す、非常に小さく自己完結型の例を通して、ウェブやデザインツールで使用できるように **export graphic as SVG** する方法を解説します。

軽量に保ちます：Python の数行、人気の SVG ヘルパーライブラリ、そして少しの解説だけです。最後までに、フォルダーに `circle.svg` が作成され、各ステップがなぜ重要かが理解できるようになります—曖昧な “see docs” のようなショートカットはありません。

## 必要なもの

- Python 3.8+（最新バージョンであればどれでも可）
- `svgwrite` パッケージ – `pip install svgwrite` でインストール
- テキストエディタまたは IDE（VS Code、PyCharm、または Notepad でも可）
- ファイルを保存したいディレクトリへの書き込み権限

以上です。重い依存関係も外部サービスも不要です。

## ステップ 1: SVG ドキュメントの設定

SVG ドキュメントの作成は、`svgwrite` の `Drawing` オブジェクトをインスタンス化するだけで簡単です。このオブジェクトは、すべての形状が配置される空白のキャンバスと考えてください。

```python
import svgwrite

# Step 1: Create a new SVG document (canvas) 800×800 pixels
dwg = svgwrite.Drawing(filename="circle.svg", size=("200px", "200px"))
```

> **この重要性:** `Drawing` クラスは XML の定型部分（名前空間、ヘッダー、ルート `<svg>` 要素）をすべて処理してくれます。最初にファイル名を指定しておくことで、ファイルの保存先が分かっており、後の **save svg file** 手順が簡単になります。

### プロのコツ

ループで多数のファイルを生成する予定がある場合は、各 `Drawing` にユニークな名前を付けるか、`io.BytesIO` を使用して書き込む準備ができるまでメモリ上に保持してください。

## ステップ 2: SVG に円を追加

ドキュメントが作成されたので、**add circle to SVG** しましょう。`add()` メソッドは任意の形状オブジェクトを受け取ります。`Circle` は中心にシンプルな赤い点を描くのに最適です。

```python
# Step 2: Add a red circle element to the SVG root
center = (100, 100)          # x, y coordinates (half of 200px canvas)
radius = 80                  # radius in pixels
circle = dwg.circle(center=center, r=radius, fill='red')
dwg.add(circle)
```

> **なぜ `center` と `radius` 変数を使うか:** 数字をハードコーディングするとコードの可読性と保守性が低下します。値に名前を付けることで意図が明確になり、この円は 200 × 200 のキャンバスの真ん中に位置し、目立つほどの大きさになります。

### エッジケース – 透明な背景

透明な背景（SVG のデフォルト）が必要な場合は、ルート要素の `fill` を設定しなくて構いません。白い背景が必要な場合は、次のように追加します：

```python
dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))
```

円を追加する前にこれを配置し、矩形が円の下に来るようにします。

## ステップ 3: SVG ファイルの保存

形状が配置されたら、最後のステップは **save SVG file** です。`save()` メソッドは XML をディスクに書き込み、すでに `Drawing` にファイル名を設定しているので、1 回の呼び出しで完了します。

```python
# Step 3: Save the SVG document to a file
dwg.save()
print("✅ circle.svg has been created in the current directory.")
```

> **内部で何が起きているか:** `svgwrite` は要素ツリーを文字列にシリアライズし、XML 宣言を追加して UTF‑8 エンコーディングで書き込みます。対象ディレクトリが存在しない場合、Python は `FileNotFoundError` を発生させます。パスが有効か確認するか、`os.makedirs()` で作成してください。

### ボーナス: プログラムで SVG としてグラフィックをエクスポート

SVG コンテンツを文字列として必要な場合（例: HTML メールに埋め込む）には、`save()` の代わりに `dwg.tostring()` を呼び出すことができます：

```python
svg_content = dwg.tostring()
# Now you can send svg_content over a network, store it in a DB, etc.
```

## 完全な動作例

すべてをまとめると、以下が完全で実行可能なスクリプトです：

```python
import svgwrite
import os

def create_svg_with_circle(output_path: str):
    """
    Creates an SVG file containing a single red circle.
    Parameters
    ----------
    output_path: str
        Full path where the SVG file will be saved.
    """
    # Ensure the directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Initialise the SVG document (800×800 canvas)
    dwg = svgwrite.Drawing(filename=output_path, size=("200px", "200px"))

    # Optional: add a white background rectangle
    dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))

    # Add a red circle in the centre
    center = (100, 100)
    radius = 80
    circle = dwg.circle(center=center, r=radius, fill='red')
    dwg.add(circle)

    # Save the file – this is the key step to **save svg file**
    dwg.save()
    print(f"✅ SVG saved to {output_path}")

if __name__ == "__main__":
    # Change this path to wherever you want the file
    output_file = os.path.join(os.getcwd(), "circle.svg")
    create_svg_with_circle(output_file)
```

**期待される出力:** スクリプトを実行すると、同じフォルダーに `circle.svg` ファイルが作成されます。ブラウザやベクターエディタで開くと、白い四角の中央に赤い円が表示されます—まさにプログラムした通りです。

## よくある質問と落とし穴

- **別の形状が欲しい場合は？** `dwg.circle` を `dwg.rect`、`dwg.ellipse`、あるいはカスタムの `<path>` 文字列に置き換えてください。API は形状間で一貫しています。
- **SVG を直接 HTML に埋め込めますか？** もちろんです。作成したファイルは `<img src="circle.svg" alt="Red circle">` で参照するか、`<svg>` タグでインライン化できます。
- **なぜ生の XML を書かないのですか？** 書くことは可能ですが、`svgwrite` のようなライブラリは名前空間の問題を処理し、コードの保守性を大幅に向上させます—特にグラデーションやアニメーションを追加し始めたときに有用です。

## 結論

これで **create SVG document**、**add circle to SVG**、**save SVG file** の方法が分かり、数行の Python で **export graphic as SVG** できるようになりました。このパターンは拡張性があり、円を任意のベクター形状に置き換えたり、データをループしてチャートを生成したり、デザインシステムのアセットをバッチ処理したりできます。

次のステップは？ テキストラベルを追加したり、グラデーションを試したり、1 つのスクリプトでアイコンのギャラリー全体を生成してみてください。より高度な機能に興味がある場合は、`svgwrite` のドキュメントでグループ（`<g>`）、変換、アニメーションサポートを確認してください。

コーディングを楽しんで、ベクターが常に鮮明でありますように！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックをカバーしています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [Aspose.HTML for Java で SVG ドキュメントを保存](/html/english/java/saving-html-documents/save-svg-document/)
- [Aspose.HTML for Java で SVG ドキュメントを作成および管理](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Aspose.HTML for Java で SVG を画像に変換](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}