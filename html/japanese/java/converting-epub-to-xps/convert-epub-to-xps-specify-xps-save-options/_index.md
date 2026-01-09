---
date: 2026-01-09
description: Aspose.HTML for Java を使用して XPS の保存オプションを指定し、EPUB を XPS に効率的に変換する方法を学びましょう。
linktitle: Specifying XPS Save Options for EPUB to XPS
second_title: Java HTML Processing with Aspose.HTML
title: EPUB から XPS への変換のための Aspose HTML 保存オプションの指定
url: /ja/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# EPUB から XPS への Aspose HTML 保存オプションの指定

EPUB ドキュメントを XPS に変換することは、出版ワークフローで便利な工程となり得ます。**Aspose HTML Save Options** を使用すると、出力を細かく制御できます。このチュートリアルでは、Aspose.HTML for Java を使って保存オプションを設定し、高品質な XPS ファイルを生成する手順を詳しく解説します。

## クイック回答
- **Aspose HTML Save Options は何をするものですか？** XPS などの形式で保存する際に、ページサイズや背景色、その他のレンダリング設定をカスタマイズできます。  
- **必要なライブラリはどれですか？** Aspose.HTML for Java（最新バージョン）。  
- **ライセンスは必要ですか？** 評価用の無料トライアルで動作しますが、商用利用には正式なライセンスが必要です。  
- **ページサイズは変更できますか？** はい、`PageSetup` を使用して任意の幅と高さを設定できます。  
- **変換は高速ですか？** 一般的な EPUB ファイルであれば、最新の JVM 上で数秒で変換が完了します。

## Aspose HTML Save Options とは？
Aspose HTML Save Options は、HTML、EPUB、その他の Web ベースドキュメントを XPS、PDF、画像ファイルなどのターゲット形式にレンダリングして保存する際の動作を制御するプロパティ群です。ページレイアウト、背景色、余白などを定義でき、生成されるファイルがデザイン要件に合致するようにします。

## なぜ Aspose.HTML for Java を使って EPUB を XPS に変換するのか？
- **高忠実度** – 複雑なレイアウト、フォント、ベクターグラフィックを正確に保持します。  
- **プログラム制御** – Java アプリケーション内でバッチ変換を自動化できます。  
- **外部依存なし** – 純粋な Java ライブラリで、ネイティブコンポーネントが不要です。  
- **出力カスタマイズ** – 保存オプションにより、XPS を細部まで調整可能です。

## 前提条件

コードに取り掛かる前に、以下を用意してください。

1. **Java 開発環境** – JDK 8 以上がインストールされていること。  
2. **Aspose.HTML for Java ライブラリ** – [download link](https://releases.aspose.com/html/java/) からダウンロード。  
3. **EPUB ファイル** – 変換したい元の EPUB。

これらが揃っていれば、途中で中断されることなく手順を進められます。

## パッケージのインポート

まず、必要なクラスをインポートします。インポート文は Java ソースファイルの先頭に配置してください。

```java
import java.io.FileInputStream;
import com.aspose.html.saving.XpsSaveOptions;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.drawing.Page;
import com.aspose.html.drawing.Size;
import com.aspose.html.drawing.Length;
import com.aspose.html.drawing.Color;
import com.aspose.html.converters.Converter;
import com.aspose.html.system.io.resources.Resources;
```

これらのインポートにより、変換エンジンと **Aspose HTML Save Options** にアクセスできるようになります。

## EPUB ファイルを開く

次に、変換対象の EPUB を開きます。`Resources.input` ヘルパーはデモリソースフォルダーからファイルを読み込みます。

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    // Your code for the EPUB file handling goes here.
}
```

try‑with‑resources ブロックを使用することで、ストリームが自動的にクローズされます。

## XPS 保存オプションの作成（ページサイズと背景の設定）

ここで `XpsSaveOptions` インスタンスを作成し、カスタマイズします。**保存オプション** が本領を発揮するポイントです。

```java
XpsSaveOptions options = new XpsSaveOptions();
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
anyPage.setSize(new Size(Length.fromPixels(3000), Length.fromPixels(1000)));
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **ページサイズ** – 本例では 3000 × 1000 ピクセルに設定しています。目的の用紙サイズに合わせて調整してください。  
- **背景色** – `AliceBlue` はキャンバスの背景色変更例です。任意の `Color` を指定できます。

これらの設定は最終的な XPS ドキュメントに影響を与える **Aspose HTML Save Options** の一部です。

## EPUB を XPS に変換

最後に、ストリーム、設定済みオプション、出力パスを指定してコンバータを呼び出します。

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

この行が実行されると、Aspose.HTML が EPUB を読み込み、設定したページレイアウトと背景色を適用し、完全に準拠した XPS ファイルを書き出します。

## よくある問題とヒント

- **ページサイズが正しくない** – ピクセル単位で指定しているか確認してください（または `Length.fromInches` を使用）。  
- **フォントが欠落している** – 必要なフォントを EPUB に埋め込むか、JVM ホストにインストールしてフォールバックを防止してください。  
- **ファイルが大きすぎる** – 非常に大きな EPUB の場合、JVM ヒープ (`-Xmx`) を増やして `OutOfMemoryError` を回避します。  

## 結論

**Aspose HTML Save Options** を活用することで、EPUB を XPS にレンダリングする際の細部まで制御できます。上記の手順に従えば、ページサイズや背景色の設定、変換処理を数行の Java コードで実現できます。このパターンをバッチ処理パイプラインに組み込めば、出版タスクの自動化が効率的に行えます。

## FAQ（よくある質問）

**Q: Aspose.HTML for Java とは何ですか？**  
A: ブラウザーを必要とせずに、開発者が HTML、EPUB、その他の Web ベースドキュメントを作成、編集、レンダリング、変換できる Java ライブラリです。

**Q: 商用プロジェクトで使用できますか？**  
A: はい。製品版の使用には有効なライセンスが必要です。ライセンスは [purchase page](https://purchase.aspose.com/buy) から購入できます。

**Q: 無料トライアルはありますか？**  
A: もちろんです。トライアル版は [here](https://releases.aspose.com/) からダウンロードできます。

**Q: サポートはどこで受けられますか？**  
A: Aspose フォーラム（[https://forum.aspose.com/](https://forum.aspose.com/)）でコミュニティサポートと公式サポートが利用できます。

**Q: システム要件は何ですか？**  
A: JDK 8 以上と、Aspose ランタイムがサポートする OS が必要です。前述の前提条件を満たしていることを確認してください。

**最終更新日:** 2026-01-09  
**テスト環境:** Aspose.HTML for Java 24.12  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}