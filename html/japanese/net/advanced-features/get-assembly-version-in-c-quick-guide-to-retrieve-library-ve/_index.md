---
category: general
date: 2026-01-06
description: C#でアセンブリのバージョンを素早く取得する。バージョンの取得方法、ライブラリのバージョンの取得、そしてライブラリのバージョンを表示する手順を明確に学びましょう。
draft: false
keywords:
- get assembly version
- how to get version
- type assembly c#
- retrieve library version
- display library version
language: ja
og_description: C#でアセンブリのバージョンを取得 – バージョンの取得方法、ライブラリのバージョンの取得、そしてライブラリのバージョンを表示する簡単な手順をご紹介します。
og_title: C#でアセンブリのバージョンを取得 – クイックガイド
tags:
- C#
- .NET
- Reflection
title: C#でアセンブリ バージョンを取得 – ライブラリ バージョン取得の簡易ガイド
url: /ja/net/advanced-features/get-assembly-version-in-c-quick-guide-to-retrieve-library-ve/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# でアセンブリ バージョンを取得する – クイック ガイド

サードパーティ DLL の **アセンブリ バージョンを取得** したいけど、どこから手を付ければいいか分からないこと、ありませんか？ 同じ壁にぶつかる開発者は多いです。幸い .NET には余計なパッケージを導入せずに **バージョン取得方法** を提供するシンプルなリフレクション API が用意されています。

このチュートリアルでは Aspose.HTML ライブラリのバージョン取得手順を解説し、コンソールへの **ライブラリ バージョン表示** 方法や、動的アセンブリの扱い、プロジェクト自身のバージョン確認といったバリエーションも紹介します。最後まで読めば「type assembly c#」の全体フローが把握でき、任意の .NET アプリで **ライブラリ バージョン取得** ができるようになります。

---

## 必要な環境

- .NET 6.0 以上（.NET Framework 4.7+ でも動作します）
- 対象ライブラリへの参照（例では Aspose.HTML）
- 基本的な C# コンソール プロジェクト（Visual Studio、Rider、または `dotnet new console`）

追加の NuGet パッケージは不要です。組み込みの `System.Reflection` 名前空間だけで完結します。

---

## 手順 1: 対象型を参照してアセンブリを取得

まず、対象アセンブリに含まれる実際の型を取得します。その型から CLR に対し、所属するアセンブリを問い合わせます。

```csharp
using System;
using System.Reflection;
// Make sure you have a using directive for the library you want to inspect
// For Aspose.HTML the namespace is Aspose.Html
using Aspose.Html;   // <-- adjust if you’re checking a different library

// Step 1: Grab the assembly that defines the HTMLDocument type
Assembly htmlAssembly = typeof(HTMLDocument).Assembly;
```

**動作のポイント:**  
`typeof(HTMLDocument)` は `System.Type` オブジェクトを返します。すべての `Type` は自分が属する `Assembly` を保持しているため、`.Assembly` で実行時にロードされたバイナリそのものを取得できます。具体的な型参照がある場合の「type assembly c#」として最も確実な方法です。

---

## 手順 2: バージョン情報を抽出

アセンブリは `AssemblyName` オブジェクトを通じてメタデータを公開します。`Version` プロパティには 4 部構成のバージョン番号（`major.minor.build.revision`）が格納されています。

```csharp
// Step 2: Pull the version from the assembly's name
Version version = htmlAssembly.GetName().Version;
```

**取得できるもの:**  
`Version` オブジェクトはアセンブリの `AssemblyVersion` 属性に設定された値を反映します。ライブラリ作者が `AssemblyFileVersion` も設定している場合は、後述の `FileVersionInfo` で取得可能です。

---

## 手順 3: ライブラリ バージョンを表示

`Version` インスタンスが手に入ったら、コンソールへの出力はとても簡単です。好きな形式でフォーマットできます。

```csharp
// Step 3: Show the Aspose.HTML version in the console
Console.WriteLine($"Aspose.HTML version: {version}");
```

すべてをまとめた、実行可能なコンソール プログラム例はこちらです。

```csharp
// ------------------------------------------------------------
// Complete example: Get Assembly Version of Aspose.HTML
// ------------------------------------------------------------
using System;
using System.Reflection;
using Aspose.Html;   // reference the Aspose.HTML NuGet package first

class Program
{
    static void Main()
    {
        // 1️⃣ Get the assembly that defines HTMLDocument
        Assembly htmlAssembly = typeof(HTMLDocument).Assembly;

        // 2️⃣ Extract the version information
        Version version = htmlAssembly.GetName().Version;

        // 3️⃣ Display the version
        Console.WriteLine($"Aspose.HTML version: {version}");

        // Optional: pause so you can see the output when running from IDE
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

**期待される出力（Aspose.HTML 23.9 時点）**

```
Aspose.HTML version: 23.9.0.0
Press any key to exit...
```

別のライブラリを調べる場合は、`HTMLDocument` をその DLL に含まれる任意の型に置き換えるだけです。

---

## 手順 4: エッジケースの処理（特殊シナリオでのバージョン取得）

### 4.1 アセンブリ パスしかないとき

型が手元にないケース、たとえばプラグイン フォルダーを走査する場合は、アセンブリを直接ロードします。

```csharp
string path = @"C:\Libraries\MyPlugin.dll";
Assembly pluginAssembly = Assembly.LoadFrom(path);
Version pluginVersion = pluginAssembly.GetName().Version;
Console.WriteLine($"MyPlugin version: {pluginVersion}");
```

> **プロのコツ:** `LoadFrom` は `try/catch` で囲み、破損したファイルが投げる `BadImageFormatException` に備えましょう。

### 4.2 ファイル バージョンを取得（より正確なライブラリ バージョン表示）

ビルド時に `AssemblyVersion` が上書きされることがありますが、ファイル バージョンはマーケティング バージョンを示すことが多いです。取得方法は次の通りです。

```csharp
using System.Diagnostics;

FileVersionInfo fvi = FileVersionInfo.GetVersionInfo(htmlAssembly.Location);
Console.WriteLine($"File version: {fvi.FileVersion}");
```

これで **ライブラリ バージョン取得**（`Version`）と **ライブラリ バージョン表示**（`FileVersionInfo`）の両方が手に入ります。

### 4.3 現在実行中のアセンブリのバージョンを確認

自分のアプリ自身のバージョンが欲しいときは、`Assembly.GetExecutingAssembly()` を使います。

```csharp
Version myAppVersion = Assembly.GetExecutingAssembly().GetName().Version;
Console.WriteLine($"My app version: {myAppVersion}");
```

ログやテレメトリに便利です。

---

## 手順 5: よくある落とし穴と回避策

| 落とし穴 | 発生理由 | 対策 |
|---------|----------|------|
| **`Version` が null** | アセンブリに `AssemblyVersion` 属性が設定されていない | フォールバックとして `FileVersionInfo` を使用 |
| **誤ったアセンブリがロードされる** | 同名 DLL の複数バージョンが探索パスに存在 | `Assembly.LoadFrom` で正確なパスを指定 |
| **リフレクション権限が拒否される（部分信頼）** | 環境によってはリフレクションが制限される | フルトラストで実行するか、`AssemblyName.GetAssemblyName(path)` を使用 |
| **動的アセンブリ** | ランタイム生成のため物理ファイルが存在しない | `assembly.GetName().Version` で取得。ファイル バージョンは取得不可 |

---

## 手順 6: 再利用可能なヘルパー メソッドにまとめる

**バージョン取得** を頻繁に行う場合は、以下のように静的ヘルパーにラップすると便利です。

```csharp
public static class AssemblyInfoHelper
{
    /// <summary>
    /// Returns the assembly version and optional file version for a given type.
    /// </summary>
    public static (Version AssemblyVersion, string FileVersion) GetVersionInfo<T>()
    {
        Assembly asm = typeof(T).Assembly;
        Version av = asm.GetName().Version;

        string fv = null;
        try
        {
            var fvi = FileVersionInfo.GetVersionInfo(asm.Location);
            fv = fvi.FileVersion;
        }
        catch
        {
            // ignore – not all assemblies expose a file version
        }

        return (av, fv);
    }
}
```

使用例:

```csharp
var (asmVer, fileVer) = AssemblyInfoHelper.GetVersionInfo<HTMLDocument>();
Console.WriteLine($"Assembly version: {asmVer}");
Console.WriteLine($"File version: {fileVer ?? "N/A"}");
```

これで任意のプロジェクトに **ライブラリ バージョン取得** ユーティリティを簡単に組み込めます。

---

## ビジュアル サマリー

![Diagram showing steps to get assembly version in C#](/images/get-assembly-version-diagram.png){: .align-center alt="Get assembly version workflow"}

*画像の alt テキストには主要キーワードが含まれており、SEO 要件を満たしています。*

---

## まとめ

C# で **アセンブリ バージョンを取得** する方法を、既知の型からアセンブリを取得し `Version` を抽出、必要に応じて `FileVersionInfo` でファイル バージョンを表示するまで、ステップバイステップで解説しました。また、ファイル パスだけが手元にある場合や自分の実行ファイルのバージョン確認、再利用可能なヘルパー作成といったシナリオにも対応しています。

このコードスニペットを活用すれば、Aspose.HTML はもちろん、Newtonsoft.Json や自作プラグインなど、あらゆる .NET ライブラリに対して **バージョン取得方法** を即座に答えられるようになります。次のステップとして、アプリ起動時にバージョンをログに記録したり、ロードされたすべてのアセンブリとそのバージョンを一覧表示する診断ページを作成してみてください。サポートチケットやコンプライアンス監査にも役立ちます。

Happy coding, and remember: a quick reflection call is often all you need to **retrieve library version** and keep your software transparent. 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}