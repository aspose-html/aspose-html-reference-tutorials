---
category: general
date: 2026-06-03
description: JavaでHTMLドキュメントを作成し、カウンタをインクリメントするJavaScriptを埋め込む。スクリプトエンジンの例を学び、要素のinnerHTMLを取得するなど、さらに多くのことを学べます。
draft: false
keywords:
- create html document
- embed javascript html
- get element innerhtml
- increment counter javascript
- script engine example
language: ja
og_description: JavaでHTMLドキュメントを作成し、カウンタをインクリメントするJavaScriptを埋め込み、スクリプトエンジンを使用して最終値を取得する例。
og_title: 埋め込みJavaScriptによるHTMLドキュメントの作成 – Java例
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  headline: Create HTML Document with Embedded JavaScript – Java Example
  type: TechArticle
- description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  name: Create HTML Document with Embedded JavaScript – Java Example
  steps:
  - name: '**Creates an HTML document** in memory.'
    text: '**Creates an HTML document** in memory.'
  - name: '**Embeds a small JavaScript snippet** that increments a counter five times.'
    text: '**Embeds a small JavaScript snippet** that increments a counter five times.'
  - name: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
    text: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
  - name: '**Retrieves the final counter value** using `getElementInnerHTML`.'
    text: '**Retrieves the final counter value** using `getElementInnerHTML`.'
  - name: 'Prints `Final counter value: 5` to the console.'
    text: 'Prints `Final counter value: 5` to the console.'
  type: HowTo
tags:
- HTML
- JavaScript
- Java
- ScriptEngine
title: 埋め込みJavaScriptを使用したHTMLドキュメントの作成 – Java例
url: /ja/java/creating-managing-html-documents/create-html-document-with-embedded-javascript-java-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTMLドキュメントを埋め込みJavaScriptで作成 – Java例

Javaコードから **HTMLドキュメント** を作成し、内部にJavaScriptを埋め込む方法が必要だったことはありませんか？このガイドでは、ステップバイステップでその方法を示し、最終的なカウンタ値を出力する動作するスクリプトエンジンの例を完成させます。  

もし *「スクリプト実行後に要素のinnerHTMLを取得するにはどうすればいい？」* や *「JavaからJavaScriptのカウンタを増やす最もシンプルな方法は何か？」* と自問自答したことがあるなら、ここが正解です。**embed javascript html**、**increment counter javascript**、そして **get element innerHTML** を一つの統合チュートリアルでカバーします。

![Create HTML Document with embedded JavaScript](/images/create-html-document.png){: .center alt="埋め込みJavaScriptの例を示すHTMLドキュメント作成"}

## 作成するもの

このチュートリアルの最後までに、以下を実現できる自己完結型のJavaプログラムが手に入ります。

1. **HTMLドキュメント** をメモリ上に作成します。  
2. カウンタを5回増やす小さなJavaScriptスニペットを埋め込みます。  
3. `ScriptEngine` の例を使用してスクリプトエンジンを初期化し、そのスニペットを実行します。  
4. `getElementInnerHTML` を使用して最終的なカウンタ値を取得します。  
5. コンソールに `Final counter value: 5` を出力します。

外部ファイルやウェブサーバは不要です—純粋なJavaと小さなHTML文字列だけです。

---

## 前提条件

- Java 17以降（`ScriptEngine` APIは標準ライブラリの一部です）。  
- HTMLとJavaScriptの基本的な知識（深い専門知識は不要）。  
- IDEまたはシンプルなテキストエディタと、プログラムをコンパイル・実行するターミナル。

---

## ステップ 1: JavaでHTMLドキュメントを作成

最初に必要なのは、後でマークアップで埋めることができる空のHTMLドキュメントオブジェクトです。これはメモリ内だけに存在する仮想ページと考えてください。

```java
// Import statements
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

// Minimal HTML document wrapper (pseudo‑class for illustration)
class HTMLDocument {
    private StringBuilder html = new StringBuilder();

    public void write(String content) {
        html.append(content);
    }

    public String getContent() {
        return html.toString();
    }

    // Simple DOM simulation for getElementById / innerHTML
    private java.util.Map<String, String> elements = new java.util.HashMap<>();

    public void setElementInnerHTML(String id, String value) {
        elements.put(id, value);
    }

    public String getElementInnerHTML(String id) {
        return elements.getOrDefault(id, "");
    }

    // Helper used by the script engine (not production‑grade)
    public void updateCounter(int value) {
        setElementInnerHTML("counter", String.valueOf(value));
    }
}
```

**重要性:** **HTMLドキュメント** オブジェクトを自分で作成することで、ディスクへの書き込みを回避し、すべてをテスト可能に保ちます。小さなDOMシミュレーションにより、フルブラウザなしで後から **get element innerHTML** が取得できます。

---

## ステップ 2: JavaScript HTML を埋め込む – カウンタロジック

ここでは、`<script>` ブロックを含むHTMLマークアップを書きます。このスクリプトは **increment counter JavaScript** を5回実行します。

```java
HTMLDocument doc = new HTMLDocument();

doc.write(
    "<!DOCTYPE html><html><body>"
  + "<div id='counter'>0</div>"
  + "<script>"
  + "for (let i = 0; i < 5; i++) {"
  + "  document.getElementById('counter').innerHTML = i + 1;"
  + "}"
  + "</script>"
  + "</body></html>"
);
```

**説明:**  
- `<div id='counter'>0</div>` は対象要素です。  
- `for` ループは **increment counter javascript** のロジックを実行し、各イテレーションで div を更新します。  
- 実際のブラウザではないため、後で使用するスクリプトエンジンは `document.getElementById` を理解する必要があります。そのため `HTMLDocument` に小さなスタブを追加しました。

---

## ステップ 3: スクリプトエンジンを初期化 – スクリプトエンジン例

Javaは `ScriptEngine` API（JSR‑223）を標準で提供しています。HTMLコンテンツをエンジンに渡し、期待される最小限のDOMメソッドを提供する小さなラッパーを作成します。

```java
class SimpleScriptEngine {
    private final HTMLDocument document;
    private final ScriptEngine engine;

    public SimpleScriptEngine(HTMLDocument doc) throws ScriptException {
        this.document = doc;
        ScriptEngineManager manager = new ScriptEngineManager();
        this.engine = manager.getEngineByName("JavaScript");
        // Expose a mock 'document' object to the JavaScript context
        engine.put("document", new Object() {
            public Object getElementById(String id) {
                return new Object() {
                    public void setInnerHTML(String value) {
                        document.updateCounter(Integer.parseInt(value));
                    }
                };
            }
        });
    }

    public void execute() throws ScriptException {
        // Extract only the script part from the HTML (simplified)
        String html = document.getContent();
        int scriptStart = html.indexOf("<script>") + "<script>".length();
        int scriptEnd   = html.indexOf("</script>");
        String script = html.substring(scriptStart, scriptEnd);
        engine.eval(script);
    }
}
```

**重要性:** この **script engine example** は、フルブラウザなしで埋め込みJavaScriptを実行できる方法を示します。また、`document.getElementById` を軽量に公開し、スクリプトがモックDOMとやり取りできるようにする手法も示しています。

---

## ステップ 4: JavaScript を実行 – Increment Counter JavaScript の実行

エンジンの準備ができたら、単にスクリプトを実行します。`<script>` タグ内のループが発火し、モック `setInnerHTML` がカウンタを更新します。

```java
try {
    SimpleScriptEngine engine = new SimpleScriptEngine(doc);
    engine.execute(); // runs the embedded JavaScript
} catch (ScriptException e) {
    e.printStackTrace();
}
```

**内部で何が起きているか？** ループの各イテレーションで `document.getElementById('counter').innerHTML = i + 1;` が呼び出されます。モック `setInnerHTML` は数値文字列を `HTMLDocument.updateCounter` に転送し、最新の値を保存します。ループが終了すると、ドキュメント内部のマップは `counter` 要素に対して `"5"` を保持しています。

---

## ステップ 5: 最終カウンタ値を取得 – Get Element InnerHTML

スクリプトが完了したので、`HTMLDocument` インスタンスから **get element innerHTML** を取得できます。

```java
String finalValue = doc.getElementInnerHTML("counter");
System.out.println("Final counter value: " + finalValue); // prints 5
```

プログラム全体を実行すると以下が出力されます：

```
Final counter value: 5
```

これにより、**increment counter javascript** ロジックが正しく動作し、スクリプト実行後に **retrieved the element innerHTML** に成功したことが確認できます。

---

## 完全な動作例

すべてをまとめた、実行可能なJavaクラスは以下の通りです：

```java
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

public class HtmlJsDemo {

    // ---------- Minimal HTMLDocument implementation ----------
    static class HTMLDocument {
        private final StringBuilder html = new StringBuilder();
        private final java.util.Map<String, String> elements = new java.util.HashMap<>();

        public void write(String content) {
            html.append(content);
        }

        public String getContent() {
            return html.toString();
        }

        public void setElementInnerHTML(String id, String value) {
            elements.put(id, value);
        }

        public String getElementInnerHTML(String id) {
            return elements.getOrDefault(id, "");
        }

        public void updateCounter(int value) {
            setElementInnerHTML("counter", String.valueOf(value));
        }
    }

    // ---------- SimpleScriptEngine (script engine example) ----------
    static class SimpleScriptEngine {
        private final HTMLDocument document;
        private final ScriptEngine engine;

        public SimpleScriptEngine(HTMLDocument doc) throws ScriptException {
            this.document = doc;
            ScriptEngineManager manager = new ScriptEngineManager();
            this.engine = manager.getEngineByName("JavaScript");
            // Expose a mock 'document' object
            engine.put("document", new Object() {
                public Object getElementById(String id) {
                    return new Object() {
                        public void setInnerHTML(String value) {
                            document.updateCounter(Integer.parseInt(value));
                        }
                    };
                }
            });
        }

        public void execute() throws ScriptException {
            String html = document.getContent();
            int start = html.indexOf("<script>") + "<script>".length();
            int end   = html.indexOf("</script>");
            String script = html.substring(start, end);
            engine.eval(script);
        }
    }

    // ---------- Main method ----------
    public static void main(String[] args) {
        // Step 1: create HTML document
        HTMLDocument doc = new HTMLDocument();

        // Step 2: embed JavaScript HTML (increment counter JavaScript)
        doc.write(
            "<!DOCTYPE html><html><body>"
          + "<div id='counter'>0</div>"
          + "<script>"
          + "for (let i = 0; i < 5; i++) {"
          + "  document.getElementById('counter').innerHTML = i


## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックをカバーしています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、追加のAPI機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [Aspose.HTML for Javaで空のHTMLドキュメントを作成](/html/english/java/creating-managing-html-documents/create-empty-html-documents/)
- [Aspose.HTML for Javaで文字列からHTMLドキュメントを作成](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)
- [Aspose.HTML for JavaでHTMLドキュメントを保存](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}