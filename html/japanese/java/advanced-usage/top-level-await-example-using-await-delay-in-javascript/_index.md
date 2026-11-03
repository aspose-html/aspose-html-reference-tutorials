---
category: general
date: 2026-03-26
description: トップレベルawaitの例として、await delay（JavaScript）、インクリメントカウンタクラス、パブリッククラスフィールド（JavaScript）をライブデモで紹介。
draft: false
keywords:
- top level await example
- await delay javascript
- increment counter class
- public class fields javascript
- javascript class public field
language: ja
og_description: トップレベルawaitの例で、await delay JavaScript、インクリメントカウンタクラス、パブリッククラスフィールドJavaScriptを簡潔なチュートリアルとして示します。
og_title: トップレベルawaitの例 – JavaScriptでawait delayを使用する
tags:
- JavaScript
- ES2022
- async‑await
- classes
title: トップレベルawaitの例 – JavaScriptでawait delayを使用する
url: /ja/java/advanced-usage/top-level-await-example-using-await-delay-in-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# トップレベルawaitの例 – JavaScriptでawait delayを使用する

モジュールの実行を async IIFE でラップせずに一時停止させる方法を考えたことはありますか？それこそが **top level await example** が可能にすることです。このチュートリアルでは、`await delay javascript` を使って処理を遅延させ、**public class fields javascript** を活用した `increment counter class` を作成する小さなウェブページを順に解説します。最後まで読むと、任意のモダンブラウザで動作する完全なコピー＆ペースト可能なスニペットが手に入ります。

クラスをパブリックフィールドで定義することから、シンプルな Promise ベースの遅延ヘルパーを組み立てるまで、すべてをカバーします。外部ライブラリやビルドステップは不要で、純粋な HTML と `<script type="module">`、そして最新の ECMAScript 機能だけです。async 関数に慣れている方なら、top‑level await が自然な拡張に感じられる理由が分かります。**javascript class public field** 構文が初めての方でも安心してください—各行の背後にある理由を解説します。

## 学べること

- **top level await example** がモジュールスクリプト内でどのように機能するか。
- `await delay javascript` ヘルパーのパターン（`setTimeout` を Promise で模倣）。
- パブリックフィールド (`count`) と static 初期化ブロックを使用した **increment counter class** の書き方。
- 期待されるコンソール出力と、static ブロックがスクリプトの残りより先に実行されることを確認する方法。
- top‑level await をサポートしない古いブラウザなど、一般的な落とし穴のトラブルシューティングのヒント。

> **Pro tip:** 現代のブラウザ（Chrome 106+、Firefox 102+、Edge 106+）はすでに top‑level await をサポートしています。古い環境をサポートする必要がある場合は、Vite や Babel などのツールでバンドルすることを検討してください。

## ステップ 1 – パブリックフィールドと static ブロックを持つクラスを定義する

デモの最初のパーツは数値カウンタを保持するクラスです。`count = 0;` 行に注目してください—これは ES2022 で導入された **public class fields javascript** 構文です。コンストラクタなしでインスタンスプロパティを作成します。

```html
<!DOCTYPE html>
<html>
<head>
    <title>ECMAScript 2022 Demo</title>
</head>
<body>
<img src="placeholder.png" alt="top level await example screenshot" title="top level await example">

<script type="module">
    // Step 1: Class definition
    class Counter {
        // Public field holds the current count
        count = 0;

        // Static block runs once when the class is first evaluated
        static {
            console.log('Counter class initialized');
        }

        // Simple method that increments the public field
        increment() {
            this.count++;
        }
    }
```

**static ブロックの理由は？** モジュールが解析された瞬間に（top‑level await が実行される *前に*）一度だけの初期化ロジック（例: ロギング）を実行できます。これにより、メッセージがコンソールに最初に表示され、クラスが早期に評価されたことが証明されます。

## ステップ 2 – `await delay javascript` ヘルパーを作成する

次に、ちょっとした Promise ベースの遅延関数が必要です。これは本質的に `setTimeout` のラッパーですが、Promise を返すことで await 可能になります。

```javascript
    // Step 2: Promise‑based delay helper
    const delay = ms => new Promise(resolve => setTimeout(resolve, ms));
```

**エッジケース:** `ms` が負の数または数値でない場合、`setTimeout` は `0` とみなします。検証を追加することもできますが、デモではワンライナーの方が読みやすいです。

## ステップ 3 – Top‑Level Await を使って実行を一時停止する

いよいよ本題のトップレベル await です。スクリプトがモジュール（`type="module"`）であるため、`await` をトップスコープに直接置くことができます。これにより、Promise が解決するまでモジュールが一時停止し、副作用の順序を制御できます。

```javascript
    // Step 3: Top‑level await – delay half a second
    await delay(500);   // Wait 500 ms so the static block logs first
```

**よくある質問:** “通常の `<script>` タグで top‑level await を使えますか？” いいえ、モジュールスクリプトだけがサポートします。`type="module"` を忘れると構文エラーになります。

## ステップ 4 – クラスをインスタンス化し、インクリメントして結果をログに出す

最後にすべてを組み合わせます：インスタンスを作成し、`increment()` を呼び出し、最終的なカウントを出力します。これにより **increment counter class** の動作が示されます。

```javascript
    // Step 4: Work with the Counter instance
    const counterInstance = new Counter();
    counterInstance.increment();               // count becomes 1
    console.log('Final count:', counterInstance.count);
</script>
</body>
</html>
```

### 期待されるコンソール出力

```
Counter class initialized
Final count: 1
```

DevTools でページを開くと、static‑block のメッセージが遅延が完了する **前に** 表示され、クラスが最初に評価されたことが確認できます。

## ステップ 5 – コンストラクタの代わりにパブリッククラスフィールドを使う理由

なぜ次のように書かなかったのか疑問に思うかもしれません：

```javascript
class Counter {
    constructor() {
        this.count = 0;
    }
}
```

どちらのアプローチも機能しますが、**public class fields javascript** はよりクリーンで宣言的な構文を提供します。フィールドは一度だけ定義され、各コンストラクタ呼び出し内に入れません。そのため、クラスが大きくなると読みやすくなります。さらに、static ブロックはコンストラクタ内に置けないため、初期化ロジックを分離するのが自然です。

## ステップ 6 – 実際のアプリ向けに例を適応する

本番環境では、単一のカウンタだけでは足りないことが多いです。以下は簡単なアイデアです：

- **複数カウンタ:** 識別子をキーとした `Map` に格納する。
- **永続化状態:** `console.log` を `localStorage` への書き込みに置き換える。
- **非同期初期化:** static ブロックを使ってインスタンス生成前にサーバーから設定を取得する。

これらすべてのパターンは top‑level await の恩恵を受けます。モジュール読み込み時にデータを一度取得すれば、すべての利用者がすぐに使用可能になるからです。

## よくある質問

**Q: top‑level await は他のモジュールをブロックしますか？**  
A: いいえ。各モジュールは独立して実行されます。await を含むモジュールだけが一時停止し、他のモジュールは並行して読み込みを続けます。

**Q: delay の Promise が reject したらどうなりますか？**  
A: ハンドリングされないリジェクションはモジュール評価を中止し、コンソールにエラーとして表示されます。優雅なフォールバックが必要な場合は `try…catch` で await をラップしてください。

**Q: `static` キーワードは必須ですか？**  
A: カウンタ自体には必要ありませんが、static ブロックはコードがロード時に *一度* 実行されることを示す便利な手段です—ロギングや機能検出に最適です。

## 結論

あなたは **top level await example** を構築し、`await delay javascript`、**increment counter class**、そして **public class fields javascript** の力を示しました。完全な実行可能スニペットは上部にあり、コンソール出力は static ブロックが遅延コードより先に実行されることを証明しています。

ここからは、より複雑な非同期フローを試したり、遅延を実際の API 呼び出しに置き換えたり、クラスに追加メソッドを拡張したりできます。モダンな JavaScript では、モジュールをファーストクラスの非同期エンティティとして扱えることを覚えておいてください—余分なラッパーは不要です。

コーディングを楽しんで、コメントであなたのバリエーションをぜひ共有してください。このガイドが役立ったら、async パターンに苦戦しているチームメイトと共有しましょう！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}