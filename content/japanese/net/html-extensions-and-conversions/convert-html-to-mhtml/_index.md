---
title: Aspose.HTML を使用して .NET で HTML を MHTML に変換する
linktitle: .NET で HTML を MHTML に変換する
second_title: Aspose.HTML .NET HTML 操作 API
description: Aspose.HTML を使用して .NET で HTML を MHTML に変換する - 効率的な Web コンテンツのアーカイブ化のためのステップバイステップ ガイド。Aspose.HTML for .NET を使用して MHTML アーカイブを作成する方法を学習します。
type: docs
weight: 19
url: /ja/net/html-extensions-and-conversions/convert-html-to-mhtml/
---

Web 開発の世界では、効率的なドキュメント変換が重要です。Aspose.HTML for .NET ライブラリは、HTML ドキュメントを MHTML などのさまざまな形式に変換することを簡素化する強力なツールです。MHTML (「MIME HTML」の略) は、Web ページとそのリソースを 1 つのファイルに保存できる Web ページ アーカイブ形式です。このステップ バイ ステップ ガイドでは、Aspose.HTML for .NET を使用して HTML ドキュメントを MHTML に変換するプロセスについて説明します。

## 前提条件

変換プロセスに進む前に、次の前提条件が満たされていることを確認してください。

### 1. Aspose.HTML for .NET ライブラリ

 Aspose.HTML for .NETライブラリをインストールする必要があります。まだインストールしていない場合は、Webサイトからダウンロードできます。[ここ](https://releases.aspose.com/html/net/)ウェブサイトに記載されているインストール手順に従ってください。

### 2. サンプル HTML ドキュメント

変換を実行するには、作業に使用するHTML文書が必要です。サンプルHTMLファイルを用意してください。独自のHTML文書を使用することも、サンプルをダウンロードすることもできます。[Aspose.HTML ドキュメント](https://reference.aspose.com/html/net/).

前提条件が整ったので、変換を進めましょう。

## 名前空間のインポート

まず、必要な名前空間を C# コードにインポートする必要があります。これは、Aspose.HTML ライブラリによって提供されるクラスとメソッドにアクセスするために不可欠です。

### 必要な名前空間をインポートする

```csharp
using Aspose.Html;
```

必要な名前空間をインポートしたので、実際の変換プロセスに進むことができます。

わかりやすくするために、HTML ドキュメントから MHTML への変換をいくつかのステップに分けて説明します。

## HTMLドキュメントを読み込む

```csharp
string dataDir = "Your Data Directory"; //データディレクトリを指定する
HTMLDocument htmlDocument = new HTMLDocument(dataDir + "input.html"); //HTMLドキュメントを読み込む
```

この手順では、HTML ドキュメントへのパスを指定します。Aspose.HTML は HTML ファイルを読み込み、変換の準備を整えます。

## MHTMLSaveOptions を初期化する

```csharp
MHTMLSaveOptions options = new MHTMLSaveOptions();
```

ここで、`MHTMLSaveOptions` MHTML 変換のオプションを提供するクラス。

## リソース処理ルールを設定する

```csharp
options.ResourceHandlingOptions.MaxHandlingDepth = 1;
```

要件に応じてリソース処理ルールを設定できます。この例では、最大処理深度を 1 に制限しています。つまり、メインの HTML ドキュメントとその直接のリソースのみが MHTML ファイルに含まれることになります。

## 出力パスを指定する

```csharp
string outputMHTML = dataDir + "HTMLtoMHTML_Output.mht"; //出力ファイルのパスを指定する
```

この手順では、結果の MHTML ファイルのパスを指定します。これは、変換された MHTML ドキュメントが保存される場所です。

## 変換を実行する

```csharp
Converter.ConvertHTML(htmlDocument, options, outputMHTML);
```

さて、HTML文書をMHTMLに変換します。`ConvertHTML`メソッドは、読み込まれた HTML ドキュメント、設定したオプション、および出力ファイル パスをパラメーターとして受け取ります。

おめでとうございます! Aspose.HTML for .NET を使用して HTML ドキュメントを MHTML に正常に変換しました。これで、指定した出力パスで MHTML ファイルにアクセスできるようになりました。

## 結論

HTML ドキュメントを MHTML 形式に効率的に変換することは、Web 開発者やコンテンツ作成者にとって貴重なスキルです。Aspose.HTML for .NET は、このプロセスを簡素化し、アクセスしやすくユーザーフレンドリーにします。上記のステップ バイ ステップ ガイドに従うことで、Web コンテンツの MHTML アーカイブを簡単に作成できます。

ここで、このトピックについてさらに明確にするために、よくある質問 (FAQ) をいくつか取り上げてみましょう。

## よくある質問

### MHTML とは何ですか? また、なぜ使用されるのですか?

MHTML は「MIME HTML」の略で、Web ページとそのリソースを 1 つのファイルに保存できる Web ページ アーカイブ形式です。Web コンテンツをアーカイブしたり、Web ページを 1 つのファイルとして共有したり、異なるサーバーでホストされている場合でもすべてのリソース (画像、スタイルシートなど) が含まれるようにしたりする場合によく使用されます。

### MHTML に変換するときにリソース処理をカスタマイズできますか?

はい、できます。例に示すように、`ResourceHandlingOptions`の`MHTMLSaveOptions`クラス。MHTML ファイルに含まれるリソースの深さを制御できます。

### Aspose.HTML for .NET のその他のリソースやドキュメントはどこで入手できますか?

探索することができます[Aspose.HTML ドキュメント](https://reference.aspose.com/html/net/)詳細情報、チュートリアル、APIリファレンスについては、[Aspose.HTML フォーラム](https://forum.aspose.com/)は、助けを求めたり、問題や疑問を話し合ったりするのに最適な場所です。

### Aspose.HTML for .NET の無料試用版はありますか?

はい、Aspose.HTML for .NETの無料トライアルは、次のサイトから入手できます。[このリンク](https://releases.aspose.com/)試用版では、購入前にライブラリの機能を試すことができます。

### Aspose.HTML for .NET の一時ライセンスを取得するにはどうすればよいですか?

臨時免許証が必要な場合は、[Aspose.Purchase ウェブサイト](https://purchase.aspose.com/temporary-license/)この一時ライセンスにより、限られた期間、ライブラリの全機能にアクセスできるようになります。

