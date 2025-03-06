---
title: Aspose.HTML for Java で HTML ドキュメントをファイルに保存する
linktitle: Aspose.HTML for Java で HTML ドキュメントをファイルに保存する
second_title: Aspose.HTML を使用した Java HTML 処理
description: 複数のリンクされたリソースを簡単に処理するのに最適な Aspose.HTML for Java を使用して HTML ドキュメントをファイルに保存する方法を学習します。
weight: 11
url: /ja/java/saving-html-documents/save-html-to-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML for Java で HTML ドキュメントをファイルに保存する

## 導入
このチュートリアルでは、リンクされたリソースを管理しながら HTML ドキュメントをファイルに保存する方法を説明します。これは、複数の HTML ファイルを含むプロジェクトで作業している場合に特に便利です。これは、他の Web ページを参照する Web ページのようなものだと考えてください。このガイドの最後まで読めば、Aspose.HTML for Java を使用して HTML ドキュメントを柔軟かつ効率的に管理できるようになります。
## 前提条件
始める前に、いくつか準備しておく必要があります。
1.  Java開発キット（JDK）：マシンにJDKがインストールされていることを確認してください。バージョン8以上が推奨されます。ダウンロードできます。[ここ](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html).
2.  Aspose.HTML for Java ライブラリ: Aspose.HTML ライブラリをダウンロードする必要があります。リリース ページから入手できます。[ここ](https://releases.aspose.com/html/java/).
3. IDE またはテキストエディタ: Java 開発には、任意の IDE またはテキストエディタを使用できます。IntelliJ IDEA、Eclipse、またはメモ帳のようなシンプルなエディタでもかまいません。++大丈夫です。
4. Java の基礎知識: Java プログラミングの基礎知識があると役立ちます。ファイルの操作方法や例外の処理方法を理解する必要があります。
すべての準備が完了したら、楽しい部分であるコーディングに進みましょう。
## パッケージのインポート
Aspose.HTML を使用するには、必要なパッケージを Java プロジェクトにインポートする必要があります。手順は次のとおりです。
### Aspose 依存関係を含める
Mavenを使用している場合は、Aspose.HTMLの依存関係を`pom.xml`ファイル。Maven 構文は次のとおりです。
```xml
<dependency>
   <groupId>com.aspose</groupId>
   <artifactId>aspose-html</artifactId>
   <version>{latest_version}</version>
</dependency>
```
必ず交換してください`{latest_version}`実際のバージョン番号は Aspose のダウンロード ページから入手できます。
### Java ファイル内のインポート文
また、Java ファイルの先頭に関連するインポート ステートメントを含める必要があります。
```java
import java.io.IOException;
```

## ステップ1: 出力パスの準備
まず、ドキュメントを保存する場所を指定する必要があります。これは、コード内でファイル パスを定義することで実行できます。
```java
String documentPath = "save-with-linked-file.html";
```
ここでは、メインのHTMLドキュメントに名前を付けます`save-with-linked-file.html`.
## ステップ2: メインHTMLファイルの作成
次に、別のドキュメントにリンクするメインの HTML ファイルを作成します。ここで HTML コンテンツを記述します。
```java
java.nio.file.Files.write(java.nio.file.Paths.get(documentPath), "<p>Hello World!</p><a href='linked.html'>linked file</a>".getBytes());
```
このステップでは、段落と別のHTMLドキュメントへのリンクを含む単純なHTML構造を作成します。`linked.html`.
## ステップ3: リンクされたHTMLファイルの作成
ここで、前の手順で説明したリンクされた HTML ファイルも作成しましょう。
```java
java.nio.file.Files.write(java.nio.file.Paths.get("linked.html"), "<p>Hello linked file!</p>".getBytes());
```
これにより、メイン ドキュメントからリンクをクリックしたときに表示される HTML ファイルが作成されます。
## ステップ4: HTMLドキュメントをメモリに読み込む
両方のファイルが作成されたら、次のステップはメインの HTML ドキュメントをメモリに読み込み、プログラムで操作することです。
```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument(documentPath);
```
このコマンドでは、`HTMLDocument`次の手順で操作できるオブジェクトです。
## ステップ5: 保存オプションの作成
ドキュメントを保存する前に、保存方法を設定することが重要です。これには、`HTMLSaveOptions`.
```java
com.aspose.html.saving.HTMLSaveOptions options = new com.aspose.html.saving.HTMLSaveOptions();
```
## ステップ6: リソース処理オプションの構成
リンクされたファイルがある場合、この部分は重要です。出力にそれらを含めるか除外するかを決定する必要があります。 
```java
options.getResourceHandlingOptions().setMaxHandlingDepth(1);
```
設定`MaxHandlingDepth`に`1`リンクされたドキュメントがメイン ドキュメントと一緒に保存されないようにします。必要に応じて、リンクされた HTML ファイルを含めるようにこの値を変更します。
## ステップ7: ドキュメントを保存する
最後に、設定したオプションを使用してドキュメントを保存します。
```java
document.save("save-with-linked-file_out.html", options);
```
ここではメイン文書を次のように保存します。`save-with-linked-file_out.html`指定したオプションを保存プロセスに適用します。
## 結論
これで完了です。Aspose.HTML for Java を使用して、リンクされたリソースを含む HTML ドキュメントを保存できるようになりました。この API は強力なだけでなく、プロジェクトに簡単に統合できるため、HTML の処理が簡単になります。初心者でも経験豊富な開発者でも、Aspose.HTML for Java にはワークフローを大幅に強化できる機能が備わっています。
## よくある質問
### Aspose.HTML とは何ですか?  
Aspose.HTML は、HTML の操作、変換、レンダリングに使用される強力な API です。これにより、開発者は HTML ドキュメントをシームレスに操作できるようになります。
### HTML ファイルに画像やその他のリソースを含めることはできますか?  
はい。Aspose.HTML は、画像、スタイル、スクリプトなど、さまざまなリソース タイプをサポートしており、包括的なドキュメント処理が可能です。
### Aspose.HTML の無料試用版はありますか?  
もちろんです！Aspose.HTMLの無料トライアルをご利用ください[ここ](https://releases.aspose.com/).
### Aspose.HTML のテクニカル サポートを受けるにはどうすればよいですか?  
Asposeサポートフォーラムをご覧ください[ここ](https://forum.aspose.com/c/html/29)ご質問やご不明な点がございましたら、お気軽にお問い合わせください。
### Aspose.HTML を商用プロジェクトに使用できますか?  
はい、Aspose.HTMLは商用プロジェクトでも使用できますが、ライセンスを購入する必要があります。ライセンスオプションについては、[ここ](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
