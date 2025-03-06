---
title: Aspose.HTML for Java を使用した DOM ミューテーション オブザーバー
linktitle: DOM ミューテーション オブザーバー - ノード追加の監視
second_title: Aspose.HTML を使用した Java HTML 処理
description: このステップバイステップ ガイドでは、Aspose.HTML for Java を使用して DOM Mutation Observer を実装する方法を学習します。DOM の変更を効果的に監視して対応します。
weight: 11
url: /ja/java/advanced-usage/dom-mutation-observer-observing-node-additions/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML for Java を使用した DOM ミューテーション オブザーバー


HTML ドキュメントのドキュメント オブジェクト モデル (DOM) の変更を監視して対応したいと考えている Java 開発者ですか? Aspose.HTML for Java は、このタスクのための強力なソリューションを提供します。このステップ バイ ステップ ガイドでは、Aspose.HTML for Java を使用して HTML ドキュメントを作成し、Mutation Observer を使用してノードの追加を監視する方法について説明します。このチュートリアルでは、各例を複数のステップに分割して、プロセスを順を追って説明します。最後には、Java プロジェクトに DOM Mutation Observer を簡単に実装できるようになります。

## 前提条件

Aspose.HTML for Java の使用を開始する前に、必要な前提条件が満たされていることを確認しましょう。

1. Java 開発環境: システムに Java 開発キット (JDK) がインストールされていることを確認してください。

2.  Aspose.HTML for Java: Aspose.HTML for Javaをダウンロードしてインストールする必要があります。ダウンロードリンクは[ここ](https://releases.aspose.com/html/java/).

3. IDE (統合開発環境): Java コードの記述と実行には、IntelliJ IDEA や Eclipse などの好みの Java IDE を使用します。

## パッケージのインポート

Aspose.HTML for Java を使い始めるには、必要なパッケージを Java コードにインポートする必要があります。手順は次のとおりです。

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

//空のHTMLドキュメントを作成する
HTMLDocument document = new HTMLDocument();
```

必要なパッケージをインポートしたので、Java で DOM Mutation Observer を実装するためのステップバイステップ ガイドに進みましょう。

## ステップ1: Mutation Observerインスタンスを作成する

まず、Mutation Observer インスタンスを作成する必要があります。このオブザーバーは DOM の変更を監視し、変更が発生したときにコールバック関数を実行します。

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

このステップでは、ノードが DOM に追加されたときにメッセージを出力するコールバック関数を持つオブザーバーを作成します。

## ステップ2: オブザーバーを構成する

次に、必要なオプションを使用してオブザーバーを構成します。子リストの変更とサブツリーの変更、および文字データの変更を監視します。

```java
MutationObserverInit config = new MutationObserverInit();
config.setChildList(true);
config.setSubtree(true);
config.setCharacterData(true);

//指定された構成で監視するターゲットノードを渡します
observer.observe(document.getBody(), config);
```

ここでは、`config`オブジェクトを使用して、子リスト、サブツリー、文字データの変更を監視できるようにします。次に、ターゲットノード（この場合はドキュメントの`<body>`と構成をオブザーバーに通知します。

## ステップ3: DOMを変更する

ここで、オブザーバーをトリガーするために DOM にいくつか変更を加えます。段落要素を作成し、それをドキュメントの本文に追加します。

```java
//段落要素を作成し、それを文書本体に追加する
Element p = document.createElement("p");
document.getBody().appendChild(p);

//テキストを作成し、段落に追加します
Text text = document.createTextNode("Hello World");
p.appendChild(text);
```

このステップでは、HTML 段落要素を作成し、それをドキュメントの本文に追加します。次に、「Hello World」というコンテンツを含むテキスト ノードを作成し、それを段落に追加します。

## ステップ 4: 観測を待つ (非同期)

変化は非同期的に観察されるため、観察者が変化を捉えられるまで少し待つ必要があります。`synchronized`そして`wait`この目的のために、以下に示すようにします。

```java
//ミューテーションは非同期モードで動作しているので、数秒待ってください
synchronized (this) {
    wait(5000);
}
```

ここでは、観察者が突然変異を捕捉する機会を確保するために 5 秒間待機します。

## ステップ5: 観察をやめる

最後に、観察が終わったら、リソースを解放するためにオブザーバーを切断することが重要です。

```java
//観察をやめる
observer.disconnect();
```

この手順で、観察が完了し、リソースをクリーンアップできます。

## 結論

このチュートリアルでは、Aspose.HTML for Java を使用して DOM Mutation Observer を実装するプロセスを説明しました。オブザーバーの作成、構成、DOM の変更、監視の待機、監視の停止の方法を学びました。これで、Java プロジェクトに DOM Mutation Observer を適用して、HTML ドキュメントの DOM の変更を効果的に監視し、対応するためのスキルを習得しました。

ご質問や問題がある場合は、お気軽にお問い合わせください。[Aspose.HTML フォーラム](https://forum.aspose.com/)さらに、[ドキュメント](https://reference.aspose.com/html/java/)Aspose.HTML for Java の詳細については、こちらをご覧ください。

## よくある質問

### Q1: DOM Mutation Observer とは何ですか?

A1: DOM Mutation Observer は、HTML ドキュメントのドキュメント オブジェクト モデル (DOM) の変更を監視できる JavaScript 機能です。DOM ノードの追加、削除、または変更にリアルタイムで反応する方法を提供します。

### Q2: Aspose.HTML for Java を商用プロジェクトで使用できますか?

 A2: はい、Aspose.HTML for Javaは商用プロジェクトでも使用できます。ライセンスと購入に関する情報は、[ここ](https://purchase.aspose.com/buy).

### Q3: Aspose.HTML for Java の無料試用版はありますか?

 A3: はい、Aspose.HTML for Javaの無料トライアルをご利用いただけます。[ここ](https://releases.aspose.com/)これにより、購入前にその機能や性能を調べることができます。

### Q4: Mutation Observer を使用して文字データの変更を観察する利点は何ですか?

A4: 文字データの変更を観察することは、HTML 要素のテキスト コンテンツの変更を監視して対応したいシナリオで役立ちます。たとえば、Web フォームでのユーザー入力を追跡して応答するために使用できます。

### Q5: Aspose.HTML for Java を使用するときにリソースを破棄するにはどうすればよいですか?

 A5: 作業が終わったらリソースを解放することが重要です。この例では、`document.dispose()` HTML ドキュメントに関連付けられたリソースをクリーンアップします。メモリ リークを回避するために、作成したオブジェクトとリソースを必ず破棄してください。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
