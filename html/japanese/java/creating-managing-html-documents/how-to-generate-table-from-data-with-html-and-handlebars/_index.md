---
category: general
date: 2026-10-12
description: Handlebars を使用してデータからテーブルを生成し、JSON でテーブルにデータを埋め込む方法を学びましょう。動的 HTML テーブルで行を繰り返すためのステップバイステップガイドです。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate table from data
- populate table from json
- repeat table rows
- dynamic html table
- dynamic table rows
language: ja
lastmod: 2026-10-12
og_description: データからテーブルを生成し、Handlebars を使用して JSON からテーブルにデータを埋め込みます。このチュートリアルに従って、繰り返し行を持つ動的な
  HTML テーブルを作成してください。
og_image_alt: Screenshot showing generated table from data in a web page
og_title: Handlebarsでデータからテーブルを生成する – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-10-12'
  description: Learn how to generate table from data and populate table from JSON
    using Handlebars. Step‑by‑step guide for repeat table rows in dynamic HTML tables.
  headline: How to generate table from data with HTML and Handlebars
  type: TechArticle
- description: Learn how to generate table from data and populate table from JSON
    using Handlebars. Step‑by‑step guide for repeat table rows in dynamic HTML tables.
  name: How to generate table from data with HTML and Handlebars
  steps:
  - name: 1. Empty data sets
    text: 'If the JSON array is empty, Handlebars will still render the header row
      but no data rows. To display a friendly message, wrap the table in a conditional
      block:'
  - name: 2. Nested loops (e.g., multiple addresses per person)
    text: 'When a person can have several addresses, you can nest another `{{#foreach}}`
      inside the row:'
  - name: 3. Using a real API
    text: 'Replace the static `<script id="people-data">` with a fetch call:'
  - name: 4. Accessibility considerations
    text: '* Add `scope="col"` to `<th>` elements. * Use `<caption>` to describe the
      table purpose. * Ensure sufficient color contrast if you apply custom CSS.'
  type: HowTo
tags:
- HTML
- Handlebars
- JSON
- templating
title: HTML と Handlebars を使ってデータからテーブルを生成する方法
url: /ja/java/creating-managing-html-documents/how-to-generate-table-from-data-with-html-and-handlebars/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML と Handlebars を使用してデータからテーブルを生成する方法

Web ページで **generate table from data** が必要な場合、このチュートリアルでは正確な手順を示します。シンプルな Handlebars ループを使用すると、**populate table from JSON** ができ、**repeat table rows** を作成し、ソースが変更されるたびに更新される完全な **dynamic HTML table** が完成します。

次の数分で、完全な実行可能な例を見て、各要素がなぜ重要かを理解し、条件付き列や入れ子オブジェクトなど、より複雑なシナリオにパターンを適用する方法を学びます。

## 作成するもの

We’ll create an HTML table that:

* JSON ペイロードに含まれる人物リストを読み取ります。
* 各人物に対してテーブル行を繰り返します（`repeat table rows`）。
* 各人物の名、姓、住所を適切なセルに挿入します。
* サーバーサイドレンダリングなしで動作します – すべての処理はブラウザ内で行われます。

**前提条件**

* HTML と JavaScript の基本知識。
* 最新のブラウザ (Chrome、Edge、Firefox、または Safari)。
* Handlebars.js – CDN からロードするので、ビルドツールは不要です。

---

## 手順 1: JSON データソースの準備

最初のステップは、API から受け取る JSON を模倣した JavaScript オブジェクトを定義することです。Handlebars はプレーンオブジェクトで動作するため、デモ用にデータを `<script>` タグに直接埋め込むことができます。

```html
<script id="people-data" type="application/json">
{
  "Persons": {
    "Person": [
      {
        "FirstName": "Alice",
        "LastName": "Anderson",
        "Address": {
          "Street": "Maple",
          "Number": "123",
          "City": "Springfield"
        }
      },
      {
        "FirstName": "Bob",
        "LastName": "Baker",
        "Address": {
          "Street": "Oak",
          "Number": "456",
          "City": "Rivertown"
        }
      }
    ]
  }
}
</script>
```

**なぜ重要か** – データを別々の `<script>` 要素に保持することで、後で実際の AJAX 呼び出しに簡単に置き換えることができます。`(`Persons.Person`)` の構造は Handlebars の `{{#foreach Persons.Person}}` ブロックで使用されるパスと一致し、**populate table from JSON** に不可欠です。

---

## 手順 2: 行を繰り返す Handlebars テンプレートの作成

次に、テーブルのマークアップを含む `<script type="text/x-handlebars-template">` ブロックを作成します。Handlebars はプレースホルダーを実際の値に置き換え、各人物に対して `<tr>` を繰り返します。

```html
<script id="table-template" type="text/x-handlebars-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <!-- Header row describing the columns -->
  <tr>
    <th>Person</th>
    <th>Address</th>
  </tr>
  <!-- Data row – this block is repeated for each Person -->
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
</table>
</script>
```

**主要部分の説明**

* `{{#foreach Persons.Person}}` は Handlebars に `Persons.Person` 配列の各エントリに対して **repeat table rows** を指示します。
* `{{FirstName}} {{LastName}}` と `{{Address.*}}` の式は、現在の配列要素から値を取得します。
* テーブル全体を `data_merge` 属性でラップするのはオプションです。下流の処理や CSS セレクタに役立つことがあります。

## 手順 3: Handlebars をロードしてテンプレートをコンパイルする

CDN から Handlebars を取得し、JSON を解析し、テンプレートをコンパイルして、最終的な HTML をページに挿入します。

```html
<script src="https://cdn.jsdelivr.net/npm/handlebars@4.7.7/dist/handlebars.min.js"></script>
<script>
  // Parse the JSON stored in the <script id="people-data">
  const rawData = document.getElementById('people-data').textContent;
  const context = JSON.parse(rawData);

  // Grab the template markup and compile it
  const source = document.getElementById('table-template').innerHTML;
  const template = Handlebars.compile(source);

  // Generate the final HTML by applying the context
  const html = template(context);

  // Insert the generated table into the DOM
  document.getElementById('output').innerHTML = html;
</script>
```

**実行時にコンパイルする理由は？** – テンプレートを一度コンパイルして再利用することで、特にデータが頻繁に変わる場合にページの速度が保たれます。このパターンにより、ページをリロードせずに **populate table from JSON** を複数回実行することが簡単になります。

## 手順 4: 生成されたテーブル用のコンテナを確保する

動的テーブルが表示されるプレースホルダー `<div>` を追加します。これによりマークアップがすっきりし、静的レイアウトと生成コンテンツの関心が分離されます。

```html
<div id="output"></div>
```

手順 3 のスクリプトが実行されると、`<div id="output">` に完全な `<table>` 要素が含まれ、スタイリングやさらなる操作の準備が整います。

## 手順 5: 出力を確認しテーブルをスタイル設定する（オプション）

ブラウザでページを開くと、以下のようなテーブルが表示されます。

![Screenshot showing generated table from data](image.png "Screenshot showing generated table from data")

```html
<table border="1" data_merge="true">
  <tr>
    <th>Person</th>
    <th>Address</th>
  </tr>
  <tr>
    <td>Alice Anderson</td>
    <td>Maple 123, Springfield</td>
  </tr>
  <tr>
    <td>Bob Baker</td>
    <td>Oak 456, Rivertown</td>
  </tr>
</table>
```

**オプションのスタイリング** – よりすっきりした外観にしたい場合は、いくつかの CSS ルールを追加します：

```html
<style>
  table { border-collapse: collapse; width: 100%; }
  th, td { padding: 8px; text-align: left; }
  th { background-color: #f2f2f2; }
</style>
```

## エッジケースと一般的なバリエーションの処理

### 1. 空のデータセット

JSON 配列が空の場合、Handlebars はヘッダー行はレンダリングしますがデータ行は表示しません。フレンドリーなメッセージを表示するには、テーブルを条件ブロックでラップします。

```handlebars
{{#if Persons.Person.length}}
  {{!-- existing table markup --}}
{{else}}
  <p>No persons found.</p>
{{/if}}
```

### 2. ネストされたループ（例：人物ごとの複数の住所）

人物が複数の住所を持つ場合、行の中に別の `{{#foreach}}` をネストできます。

```handlebars
{{#foreach Persons.Person}}
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>
      {{#foreach Address}}
        {{Street}} {{Number}}, {{City}}<br>
      {{/foreach}}
    </td>
  </tr>
{{/foreach}}
```

### 3. 実際の API を使用する

静的な `<script id="people-data">` を fetch 呼び出しに置き換えます。

```javascript
fetch('/api/persons')
  .then(r => r.json())
  .then(context => {
    const html = template(context);
    document.getElementById('output').innerHTML = html;
  });
```

これは、ライブデータを取得しながら同じ **dynamic table rows** 手法を示しています。

### 4. アクセシビリティの考慮事項

* `<th>` 要素に `scope="col"` を追加します。
* テーブルの目的を説明するために `<caption>` を使用します。
* カスタム CSS を適用する場合は、十分な色のコントラストを確保します。

---

## 完全な実行可能例

以下のブロックを `index.html` ファイルにコピーし、ブラウザで開きます。ページは **generate table from data**、**populate table from JSON** を行い、行を自動的に繰り返します。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Dynamic table from JSON</title>
  <style>
    table { border-collapse: collapse; width: 100%; }
    th, td { padding: 8px; text-align: left; border: 1px solid #ddd; }
    th { background-color: #f2f2f2; }
  </style>
</head>
<body>

<!-- Step 1: JSON data source -->
<script id="people-data" type="application/json">
{
  "Persons": {
    "Person": [
      {
        "FirstName": "Alice",
        "LastName": "Anderson",
        "Address": {
          "Street": "Maple",
          "Number": "123",
          "City": "Springfield"
        }
      },
      {
        "FirstName": "Bob",
        "LastName": "Baker",
        "Address": {
          "Street": "Oak",
          "Number": "456",
          "City": "Rivertown"
        }
      }
    ]
  }
}
</script>

<!-- Step 2: Handlebars template -->
<script id="table-template" type="text/x-handlebars-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <tr>
    <th scope="col">Person</th>
    <th scope="col">Address</th>
  </tr>
  {{#foreach Persons.Person}}
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
  {{/foreach}}
</table>
</script>

<!-- Step 4: Container for the generated table -->
<div id="output"></div>

<!-- Step 3: Load Handlebars, compile, and render -->
<script src="https://cdn.jsdelivr.net/npm/handlebars@4.7.7/dist/handlebars.min.js"></script>
<script>
  const raw = document.getElementById('people-data').textContent;
  const context = JSON.parse(raw);
  const source = document.getElementById('table-template').innerHTML;
  const template = Handlebars.compile(source);
  document.getElementById('output').innerHTML = template(context);
</script>

</body>
</html>
```

**期待される結果**

ヘッダーに加えて 2 行のテーブルが表示され、“Alice Anderson” と “Bob Baker” のそれぞれの住所が示されます。ページはオフラインでも動作し、サーバーコンポーネントなしで **generate table from data** が可能であることが証明されます。

## 結論

これで、Handlebars テンプレートを使用して **generate table from data**、**populate table from JSON**、そして **repeat table rows** を作成し、**dynamic HTML table** を構築する方法が分かりました。このパターンは、より大規模なデータセット、入れ子構造、ライブ API 呼び出しにもスケールし、クライアントサイドのレポーティングや管理 UI の堅牢な基盤を提供します。

**次のステップ**

* 日付や数値のフォーマット用に Handlebars ヘルパーを探求する。
* この手法を CSS Grid や Flexbox と組み合わせて、レスポンシブなテーブルレイアウトを実現する。
* 非常に大規模なデータセットを扱うために、ページネーションやソート用のライブラリを統合する。

さまざまな JSON 形状で実験したり、条件付き列を追加したり、Handlebars を別のテンプレートエンジンに置き換えたりして構いません。新たに身につけたスキルにより、柔軟でデータ駆動型のインターフェースを迅速かつ確実に構築できます。

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックをカバーしています。各リソースには、ステップバイステップの解説付きの完全な動作コード例が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [Java で HTML ドキュメントを作成 – JSON を取得してコンテンツを生成](/html/english/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/)
- [Aspose.HTML for Java におけるデータ処理とストリーム管理](/html/english/java/data-handling-stream-management/)
- [Java で HTML をロードする方法 – ステップバイステップガイド](/html/english/java/creating-managing-html-documents/how-to-load-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}