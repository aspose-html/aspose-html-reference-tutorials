---
title: Aspose.HTML for Java を使用した DOM Mutation Observer
linktitle: DOM Mutation Observer - ノード追加の監視
second_title: Aspose.HTML を使用した Java HTML 処理
description: このステップバイステップ ガイドでは、Aspose.HTML for Java を使用して DOM Mutation Observer を実装する方法を学びます。 DOM の変更を効果的に監視し、それに対応します。
type: docs
weight: 11
url: /ja/java/advanced-usage/dom-mutation-observer-observing-node-additions/
---

あなたは Java 開発者で、HTML ドキュメントのドキュメント オブジェクト モデル (DOM) の変更を観察して対応したいと考えていますか? Aspose.HTML for Java は、このタスクに対する強力なソリューションを提供します。このステップバイステップのガイドでは、Aspose.HTML for Java を使用して HTML ドキュメントを作成し、Mutation Observer でノードの追加を観察する方法を説明します。このチュートリアルでは、各例を複数のステップに分けてプロセスを説明します。最終的には、Java プロジェクトに DOM Mutation Observer を簡単に実装できるようになります。

## 前提条件

Aspose.HTML for Java の使用に入る前に、必要な前提条件が整っていることを確認してください。

1. Java 開発環境: システムに Java Development Kit (JDK) がインストールされていることを確認してください。

2.  Aspose.HTML for Java: Aspose.HTML for Java をダウンロードしてインストールする必要があります。ダウンロードリンクが見つかります[ここ](https://releases.aspose.com/html/java/).

3. IDE (統合開発環境): Java コードの作成と実行には、IntelliJ IDEA や Eclipse などの好みの Java IDE を使用します。

## パッケージのインポート

Aspose.HTML for Java の使用を開始するには、必要なパッケージを Java コードにインポートする必要があります。その方法は次のとおりです。

```java
//必要なパッケージをインポートする
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.mutations.MutationObserver;
import com.aspose.html.dom.mutations.MutationCallback;
import com.aspose.html.dom.mutations.MutationRecord;
import com.aspose.html.dom.mutations.MutationObserverInit;
import com.aspose.html.dom.Element;
import com.aspose.html.dom.Text;
import com.aspose.html.generic.IGenericList;

//空の HTML ドキュメントを作成する
HTMLDocument document = new HTMLDocument();
```

必要なパッケージをインポートしたので、Java で DOM Mutation Observer を実装するためのステップバイステップ ガイドに進みましょう。

## ステップ 1: Mutation Observer インスタンスを作成する

まず、Mutation Observer インスタンスを作成する必要があります。このオブザーバーは DOM 内の変更を監視し、突然変異が発生した場合にコールバック関数を実行します。

```java
MutationObserver observer = new MutationObserver(new MutationCallback() {
    @Override
    public void invoke(IGenericList<MutationRecord> mutations, MutationObserver mutationObserver) {
        mutations.forEach(mutationRecord -> {
            mutationRecord.getAddedNodes().forEach(node -> {
                synchronized (this) {
                    System.out.println("The '" + node + "' node was added to the document.");
                    notifyAll();
                }
            });
        });
    }
});
```

このステップでは、ノードが DOM に追加されたときにメッセージを出力するコールバック関数を備えたオブザーバーを作成します。

## ステップ 2: オブザーバーを構成する

次に、必要なオプションを使用してオブザーバーを構成しましょう。子リストの変更とサブツリーの変更、および文字データの変更を観察したいと考えています。

```java
MutationObserverInit config = new MutationObserverInit();
config.setChildList(true);
config.setSubtree(true);
config.setCharacterData(true);

//指定された構成で観察するターゲット ノードを渡します
observer.observe(document.getBody(), config);
```

ここで設定するのは、`config`オブジェクトを使用して、子リスト、サブツリー、および文字データの変更を監視できるようにします。次に、ターゲット ノード (この場合、ドキュメントのノード) を渡します。`<body>`) とオブザーバーへの設定。

## ステップ 3: DOM を変更する

ここで、DOM にいくつかの変更を加えて、オブザーバーをトリガーします。段落要素を作成し、ドキュメントの本文に追加します。

```java
//段落要素を作成し、文書本文に追加します。
Element p = document.createElement("p");
document.getBody().appendChild(p);

//テキストを作成して段落に追加します
Text text = document.createTextNode("Hello World");
p.appendChild(text);
```

このステップでは、HTML 段落要素を作成し、それをドキュメントの本文に追加します。次に、「Hello World」という内容のテキスト ノードを作成し、段落に追加します。

## ステップ 4: 観測を待つ (非同期)

突然変異は非同期的に観察されるため、観察者が変化を捕捉できるようになるまで少し待つ必要があります。使用します`synchronized`そして`wait`この目的のために、以下に示すように。

```java
//ミューテーションは非同期モードで動作しているため、数秒待ちます
synchronized (this) {
    wait(5000);
}
```

ここでは、観察者が突然変異を捕捉する機会を確実に得るために 5 秒間待機します。

## ステップ 5: 観察をやめる

最後に、観察が終了したら、オブザーバーを切断してリソースを解放することが重要です。

```java
//観察をやめる
observer.disconnect();
```

この手順により、観察が完了し、リソースをクリーンアップできるようになります。

## 結論

このチュートリアルでは、Aspose.HTML for Java を使用して DOM Mutation Observer を実装するプロセスを説明しました。オブザーバーの作成、構成、DOM への変更、監視の待機、監視の停止の方法を学習しました。これで、Java プロジェクトに DOM Mutation Observer を適用して、HTML ドキュメントの DOM の変更を効果的に監視し、それに対応するスキルが得られました。

ご質問がある場合や問題が発生した場合は、お気軽にサポートを求めてください。[Aspose.HTML フォーラム](https://forum.aspose.com/)。さらに、次の場所にアクセスできます。[ドキュメンテーション](https://reference.aspose.com/html/java/)Aspose.HTML for Java の詳細については、「Aspose.HTML for Java」を参照してください。

## よくある質問

### Q1: DOM ミューテーション オブザーバーとは何ですか?

A1: DOM Mutation Observer は、HTML ドキュメントのドキュメント オブジェクト モデル (DOM) の変更を監視できる JavaScript 機能です。これは、DOM ノードの追加、削除、変更にリアルタイムで対応する方法を提供します。

### Q2: 商用プロジェクトで Aspose.HTML for Java を使用できますか?

 A2: はい、商用プロジェクトで Aspose.HTML for Java を使用できます。ライセンスと購入に関する情報を見つけることができます[ここ](https://purchase.aspose.com/buy).

### Q3: Aspose.HTML for Java の無料トライアルはありますか?

A3: はい、Aspose.HTML for Java の無料トライアルを入手できます。[ここ](https://releases.aspose.com/)。これにより、購入する前にその機能と機能を調べることができます。

### Q4: Mutation Observer でキャラクター データの変化を観察する利点は何ですか?

A4: 文字データの変更の監視は、HTML 要素のテキスト コンテンツの変更を監視して対応する必要があるシナリオに役立ちます。たとえば、これを使用して、Web フォームでのユーザー入力を追跡し、応答することができます。

### Q5: Aspose.HTML for Java を使用するときにリソースを破棄するにはどうすればよいですか?

 A5: 完了したらリソースを解放することが重要です。この例では、`document.dispose()` HTML ドキュメントに関連付けられたリソースをクリーンアップします。メモリ リークを避けるために、作成したオブジェクトとリソースは必ず破棄してください。