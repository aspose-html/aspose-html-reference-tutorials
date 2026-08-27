---
category: general
date: 2026-01-01
description: C# と CSS を使用して見出しを太字にし、イタリック体を適用する方法。見出しのフォントウェイトの設定、太字とイタリックの適用、そして見出しを素早くスタイリングする方法を学びましょう。
draft: false
keywords:
- how to bold heading
- how to apply italic
- apply bold and italic
- how to apply bold
- set heading font weight
language: ja
og_description: 最初の文で見出しを太字にし、次にイタリック体の適用方法を学び、太字とイタリック体を組み合わせ、見出しのフォントウェイトを設定する方法を明確な例とともに。
og_title: 見出しを太字にする方法 – CSS と C# の完全ガイド
tags:
- CSS
- C#
- Web Development
title: CSS と C# で見出しを太字にする方法 – 完全ステップバイステップガイド
url: /ja/net/working-with-html-documents/how-to-bold-heading-with-css-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 見出しを太字にする方法 – CSS と C# の完全ガイド

ウェブページで **見出しを太字にする方法** を、膨大なドキュメントを探さずに知りたくなったことはありませんか？ あなただけではありません。HTML、CSS、そして UI を制御する少しの C# を組み合わせる際に、すぐに視覚的な調整が必要になる開発者は多いです。

このチュートリアルでは、`<h1>` 要素に太字、斜体、そしてそれらを組み合わせたスタイルを適用する完全な実行可能サンプルを順に解説します。その過程で **斜体の適用方法**、**太字と斜体を同時に適用する方法**、そして CSS の `font-weight` と低レベルの `WebFontStyle` API を使う微妙な違いについても触れます。最後まで読めば、使用しているスタックに関係なく **見出しのフォントウェイトを設定** できる自信がつくでしょう。

## 前提条件

- .NET 6+（または .NET Framework 4.8 でも可）
- Visual Studio 2022 または任意の C# 対応 IDE
- HTML と CSS の基本知識
- WebView2 コントロールをホストするシンプルな WinForms または WPF プロジェクト（例は WinForms）

これらに心当たりがない場合でも慌てないでください。必要最小限のコードを示すので、そのまま新しいプロジェクトにコピーペーストすれば動作します。

---

## Step 1: 最小限の HTML ページを作成

まず、WebView2 コントロールが読み込める HTML ファイルが必要です。以下を `index.html` という名前でプロジェクトの出力フォルダー（例: `bin\Debug\net6.0-windows`）に保存してください。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Heading Styling Demo</title>
    <style>
        /* Default styling – we’ll override this from C# */
        h1 {
            font-family: 'Arial', sans-serif;
            font-weight: normal;
            font-style: normal;
        }
    </style>
</head>
<body>
    <h1 id="title">Dynamic Heading</h1>
    <p>Open the C# console or UI to see the heading change.</p>
</body>
</html>
```

> **Why this matters:** CSS を最小限に抑えることで、C# のコードが実際に何をしているかをクリアに確認できます。`id="title"` 属性はスクリプトから見出しを簡単に対象にできるようにしています。

---

## Step 2: WebView2 で WinForms プロジェクトを設定

新しい **Windows Forms App**（`.NET 6`）を作成し、**Microsoft.Web.WebView2** NuGet パッケージを追加します。`WebView2` コントロールをフォームにドラッグし、名前を `webView`、`Dock` プロパティを `Fill` に設定します。

```csharp
using System;
using System.Windows.Forms;
using Microsoft.Web.WebView2.Core;

namespace HeadingStyler
{
    public partial class MainForm : Form
    {
        public MainForm()
        {
            InitializeComponent();
            InitializeAsync();
        }

        private async void InitializeAsync()
        {
            // Ensure the WebView2 runtime is available
            await webView.EnsureCoreWebView2Async();

            // Load the local HTML file
            var htmlPath = System.IO.Path.Combine(
                AppDomain.CurrentDomain.BaseDirectory, "index.html");
            webView.CoreWebView2.Navigate($"file:///{htmlPath}");
        }
    }
}
```

> **Pro tip:** ナビゲーションが失敗する場合は、`index.html` が出力フォルダーにコピーされているか確認してください（*Copy to Output Directory* → *Copy always*）。

---

## Step 3: C# で見出し要素を取得

ページの読み込みが完了したら、`<h1>` 要素を取得します。`CoreWebView2` API の `ExecuteScriptAsync` メソッドで JavaScript を実行し結果を取得できますが、このチュートリアルでは WebView2 に同梱されている **低レベル DOM ラッパー**（`webView.CoreWebView2` 経由）を使用します。

```csharp
private async void WebView_NavigationCompleted(
    object sender, CoreWebView2NavigationCompletedEventArgs e)
{
    // Step 1: Locate the heading element you want to style
    var heading = await webView.CoreWebView2
        .ExecuteScriptAsync("document.querySelector('h1');");

    // The script returns a JS object reference we can manipulate.
    // In practice we’ll call methods on it via ExecuteScriptAsync.
}
```

> **Why we do this:** 直接 DOM にアクセスすることで、大きな JavaScript ブロブを注入する必要がなくなります。これにより、**太字の適用方法** を WebView2 API で示すことができます。

---

## Step 4: 太字・斜体・組み合わせスタイルを適用

以下の 3 つのアプローチで見出しのスタイルを変更します。

1. **CSS `font-weight`** – 最も一般的な方法で、**見出しのフォントウェイトを設定** する要件を満たします。
2. **CSS `font-style`** – **斜体の適用方法** を示します。
3. **`WebFontStyle` フラグ** – 低レベルの代替手段で、**太字と斜体を同時に適用** できます。

```csharp
private async void StyleHeading()
{
    // 1️⃣ Apply a bold weight (700) – classic CSS method
    await webView.CoreWebView2.ExecuteScriptAsync(@"
        var h = document.querySelector('h1');
        h.style.fontWeight = '700';
    ");

    // 2️⃣ Apply italic style – fulfills “how to apply italic”
    await webView.CoreWebView2.ExecuteScriptAsync(@"
        var h = document.querySelector('h1');
        h.style.fontStyle = 'italic';
    ");

    // 3️⃣ Use the low‑level API to combine bold + italic flags
    // This requires the WebFontStyle enumeration from the WebView2 SDK.
    await webView.CoreWebView2.ExecuteScriptAsync(@"
        var h = document.querySelector('h1');
        // The following line mimics WebFontStyle usage in C#
        // Note: This is illustrative; actual flag usage happens in C#
        // h.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
    ");
}
```

> **Explanation:**  
> • `fontWeight = '700'` はブラウザーにテキストを **太字**（ウェイト 700）で描画させます。  
> • `fontStyle = 'italic'` は文字を傾け、**斜体の適用** に対応します。  
> • コメント行は、C# で `WebFontStyle` を設定できるラッパーがある場合の例です。実際のシナリオでは、`heading.Font.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;` のように呼び出します。

低レベル API を C# から呼び出すには COM インターフェイスのラッパーが必要です。以下は `Microsoft.Web.WebView2.Wpf` 名前空間への参照があることを前提とした最小例です。

```csharp
using Microsoft.Web.WebView2.WinForms;
using Microsoft.Web.WebView2.Core;
using System.Runtime.InteropServices;

private async void ApplyWebFontStyle()
{
    var script = @"
        (function() {
            var h = document.querySelector('h1');
            // Expose the element to C#
            return h;
        })();";

    var result = await webView.CoreWebView2.ExecuteScriptAsync(script);
    // The result is a JSON representation; you’d need a proper COM object to set flags.
    // For brevity, the example focuses on the CSS path which works everywhere.
}
```

> **Bottom line:** COM モデルに慣れていればフラグ方式で細かい制御が可能です。そうでなければ CSS ルートの方法で十分で、すべてのブラウザーで動作します。

---

## Step 5: すべてを統合 – 完全動作サンプル

以下は単一の `MainForm.cs` ファイルで、コンパイルして実行できます。HTML を読み込み、ナビゲーション完了時に見出しのスタイルを設定します。

```csharp
using System;
using System.Windows.Forms;
using Microsoft.Web.WebView2.Core;

namespace HeadingStyler
{
    public partial class MainForm : Form
    {
        public MainForm()
        {
            InitializeComponent();
            webView.NavigationCompleted += WebView_NavigationCompleted;
            InitializeAsync();
        }

        private async void InitializeAsync()
        {
            await webView.EnsureCoreWebView2Async();
            var htmlPath = System.IO.Path.Combine(
                AppDomain.CurrentDomain.BaseDirectory, "index.html");
            webView.CoreWebView2.Navigate($"file:///{htmlPath}");
        }

        private async void WebView_NavigationCompleted(
            object sender, CoreWebView2NavigationCompletedEventArgs e)
        {
            // Apply the three styling techniques
            await webView.CoreWebView2.ExecuteScriptAsync(@"
                var h = document.querySelector('h1');
                h.style.fontWeight = '700';   // bold
                h.style.fontStyle = 'italic'; // italic
                // For low‑level API, you’d use:
                // h.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
            ");
        }
    }
}
```

### 期待される出力

アプリを起動するとウィンドウに次のように表示されます。

- **“Dynamic Heading”** が **太字**（ウェイト 700）かつ **斜体** で描画されます。
- 周囲の段落は変更されません。
- 要素を検査すると（Ctrl + Shift + I）インラインスタイルが適用されていることが確認できます。

---

## よくある質問とエッジケース

### 1️⃣ *見出しにすでにクラスが付いている場合は？*  
`classList.add('my-bold-italic')` でクラスを追加し、スタイルシートに定義するか、今回のようにインラインスタイルを使い続けるか選べます。即座に一回だけ変更したい場合はインラインスタイルが便利です。

### 2️⃣ *すべてのブラウザーが `font-weight: 700` を尊重しますか？*  
はい。CSS 仕様では 700 が **Bold** に相当します。フォントファミリーに太字ウェイトが無い場合、ブラウザーは合成して表示しますが、若干ぼやけることがあります。そのため、Arial のように真の太字バリアントを持つフォントを使用することを推奨します。

### 3️⃣ *通常から太字への遷移をアニメーションさせられますか？*  
もちろんです。CSS トランジションを追加します。

```css
h1 {
    transition: font-weight 0.3s ease, font-style 0.3s ease;
}
```

C# からスタイルを切り替えるだけで、滑らかなアニメーションが確認できます。

### 4️⃣ *アクセシビリティはどうですか？*  
太字や斜体は視覚的な手がかりであり、意味的な情報ではありません。スクリーンリーダー向けには `aria-label` を付与したり、適切な見出し階層（`<h1>` → `<h2>`）を使用して重要度を伝えることが重要です。

---

## プロのコツと落とし穴

- **Pro tip:** CSS は別ファイルに分け、C# 側ではクラスの切り替えだけを行うと UI ロジックがすっきり保守しやすくなります。  
- **Watch out for:** ユーザーエージェントのデフォルトスタイルを上書きしないよう注意。例えば `<strong>` タグはデフォルトで `font-weight: bold` が付与されます。意図しない混在を避けるために、手動スタイルと組み合わせる際は意図を明確にしてください。  
- **Performance note:** インラインスタイルの変更はコストが低いですが、数十個以上の要素を同時に変更する場合は、1 回のスクリプト呼び出しにまとめてラウンドトリップ回数を削減しましょう。

---

## 結論

**見出しを太字にする方法** と **斜体の適用方法**、さらに **太字と斜体を同時に適用** するテクニック、そして C# から **見出しのフォントウェイトをプログラム的に設定** する方法をすべて網羅しました。小さな HTML ページ、WinForms の WebView2 ホスト、そして数行の `ExecuteScriptAsync` 呼び出しだけで実現できます。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}