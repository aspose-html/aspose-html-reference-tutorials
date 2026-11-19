---
category: general
date: 2026-04-19
description: Java を使用して MHTML から HTML を迅速に抽出します。MHTML を HTML に変換する方法、メール本文を抽出する方法、文字列をファイルに書き込む方法、MHT
  変換の処理方法を学びましょう。
draft: false
keywords:
- extract html from mhtml
- convert mhtml to html
- extract email body
- write string to file
- convert mht to html
language: ja
og_description: JavaでMHTMLからHTMLを抽出する。このガイドでは、MHTMLをHTMLに変換し、メール本文を抽出し、文字列をファイルに書き込む方法を示します。
og_title: MHTMLからHTMLを抽出 – Javaステップバイステップ
tags:
- Java
- Aspose.HTML
- Email Processing
title: MHTMLからHTMLを抽出 – 完全なJavaガイド
url: /ja/java/creating-managing-html-documents/extract-html-from-mhtml-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# MHTMLからHTMLを抽出 – 完全なJavaガイド

**MHTMLからHTMLを抽出**したいことはありませんか？でも、どこから始めればいいか分からない…という方もいるでしょう。たとえば、アーカイブされたメール（`.mht`）を受け取り、Webプレビュー用にクリーンな本文が欲しい場合や、レガシーなアーカイブを最新のHTMLページに変換するマイグレーションスクリプトを作成している場合です。どちらの場合も問題は同じです。単一ファイルのウェブアーカイブがあり、そこから生のHTMLマークアップを取り出す必要があります。

朗報です！数行のJavaコードと Aspose.HTML ライブラリさえあれば、**MHTMLをHTMLに変換**し、メール本文を取得し、さらにその文字列をファイルに書き出すことができます――IDEを離れる必要はありません。このチュートリアルでは、全工程を順を追って解説し、各ステップの重要性を説明するとともに、リソースが欠落している場合や非UTF‑8エンコーディングなどの一般的なエッジケースの対処方法も紹介します。

> **クイックリキャップ:** 本ガイドの最後までに、**メール本文の抽出**、**MHTMLからHTMLへの変換**、そして**文字列をファイルに書き込む**ことができる、どんな `.mht` や `.mhtml` に対しても使えるクリーンで再利用可能なスニペットが手に入ります。

---

## 必要なもの

作業を始める前に、以下を用意してください。

- **Java 17+**（コードは try‑with‑resources パターンを使用しています。このパターンは Java 7 以降で利用可能ですが、現在の LTS は Java 17 です）。
- **Aspose.HTML for Java** の JAR をクラスパスに配置します。入手は [Aspose のウェブサイト](https://products.aspose.com/html/java/) から、または Maven を利用してください。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

- 処理対象となるサンプルの **`.mht` または `.mhtml`** ファイル。デモでは `email.mht` という名前で `YOUR_DIRECTORY` に置くことにします。

以上です――余計なフレームワークや重いパーサは不要です。純粋な Java と、ドキュメントが充実した単一ライブラリだけで完結します。

---

## Step 1 – MHTML ファイルをストリームとして開く

最初に行うのは、アーカイブされたメールを `InputStream` として開くことです。ストリームを使用することで、特に埋め込み画像や CSS を含む大きな `.mht` ファイルでもメモリ使用量を抑えることができます。

```java
// Step 1: Open the MHTML file as a stream
try (InputStream mhtmlStream = new FileInputStream("YOUR_DIRECTORY/email.mht")) {
    // Subsequent steps go inside this block
}
```

**なぜストリームか？**  
ストリームは `MhtmlDocument` がデータをオンザフライで読み取れるようにし、アーカイブが数メガバイトでも `OutOfMemoryError` が発生しません。また、後でデータベースから `ByteArrayInputStream` を渡すなど、他のソースから読み込む柔軟性も確保できます。

---

## Step 2 – ストリームから MHTML ドキュメントをロード

次に、Aspose の `MhtmlDocument` クラスにストリームを渡します。このクラスは MIME エンコードされたアーカイブを解析し、埋め込まれた HTML の DOM ライクな表現を構築します。

```java
// Step 2: Load the MHTML document from the stream
MhtmlDocument mhtmlDoc = new MhtmlDocument(mhtmlStream);
```

**内部で何が起きているか:**  
Aspose は各 MIME パート（HTML、画像、CSS）を抽出し、内部で再構築します。そのため、後で HTML 部分だけを取得しても、埋め込みリソースの処理を気にする必要がありません。

---

## Step 3 – メインの HTML コンテンツを取得

ドキュメントがロードされたら、HTML を取得するのはワンライナーです。`getHtmlContent()` メソッドは本文を `String` として返し、元のマークアップをそのまま保持します。

```java
// Step 3: Retrieve the main HTML content as a string
String htmlContent = mhtmlDoc.getHtmlContent();
```

**取得できるもの:**  
`htmlContent` には `<head>` と `<body>` タグを含む完全な HTML ページが格納されます。表示部分だけが欲しい場合は、後で Jsoup などで `<head>` を除去すれば OK です。

---

## Step 4 – 抽出した HTML を別ファイルに書き込む

文字列をディスクに保存するのは `java.nio.file` API を使えば簡単です。このステップは、**文字列をファイルに書き込む** パターンを示しており、どのプラットフォームでも動作します。

```java
// Step 4: Save the extracted HTML to a separate file
Files.writeString(Path.of("YOUR_DIRECTORY/email_body.html"), htmlContent);
```

**Tip:**  
特定の文字セットが必要な場合は `Files.writeString(Path, CharSequence, Charset)` を使用してください。デフォルトは UTF‑8 で、ほとんどのモダンメールに適しています。

---

## Step 5 – 抽出結果を確認

簡単な `System.out.println` で例外が発生せずに処理が完了したことを確認できます。本番環境では適切なロギングに置き換えるのがベストです。

```java
// Step 5: Indicate successful extraction
System.out.println("HTML extracted.");
```

プログラムを実行するとコンソールに `HTML extracted.` と表示され、`email_body.html` が `YOUR_DIRECTORY` に作成されます。

---

## 完全に実行可能なサンプルコード

全体をまとめた、自己完結型の Java クラスです。IDE にコピペして **Run** すればすぐに動作します。

```java
import com.aspose.html.MhtmlDocument;
import java.io.FileInputStream;
import java.io.InputStream;
import java.nio.file.Files;
import java.nio.file.Path;

public class MhtmlToHtmlConverter {

    public static void main(String[] args) {
        // Adjust the path to point to your .mht/.mhtml file
        String sourcePath = "YOUR_DIRECTORY/email.mht";
        String targetPath = "YOUR_DIRECTORY/email_body.html";

        // Try-with-resources ensures the stream is closed automatically
        try (InputStream mhtmlStream = new FileInputStream(sourcePath)) {

            // Load the MHTML document
            MhtmlDocument mhtmlDoc = new MhtmlDocument(mhtmlStream);

            // Extract the HTML content
            String htmlContent = mhtmlDoc.getHtmlContent();

            // Write the HTML string to a new file
            Files.writeString(Path.of(targetPath), htmlContent);

            // Simple confirmation output
            System.out.println("HTML extracted to " + targetPath);
        } catch (Exception e) {
            // In real code you might want to log this instead of printing
            System.err.println("Failed to extract HTML: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### 期待される出力

プログラム実行時のコンソール出力例:

```
HTML extracted to YOUR_DIRECTORY/email_body.html
```

そして `email_body.html` には元メールのフル HTML ソースが保存されます。ブラウザで開くと、アーカイブされた元メッセージと同じビジュアルが表示されます（ただし、バンドルされていない外部リソースは除外されます）。

---

## 一般的なエッジケースの対処法

### 1. 埋め込みリソースが欠落している場合

MHTML が外部画像への参照だけを保持していることがあります。その場合でも `getHtmlContent()` は `<img src="...">` タグを返しますが、URL は元のウェブ位置を指します。完全に自己完結型の HTML が必要なら、以下のいずれかを実施してください。

- `MhtmlDocument.save(Path, SaveFormat.HTML)` を使用して、Aspose にすべてのリソースをフォルダーに抽出させる。  
- **Jsoup** などのライブラリで HTML を後処理し、リモート URL を Base64 エンコードされたデータ URI に置き換える。

### 2. 非 UTF‑8 エンコーディング

メールが `windows-1252` など別の文字セットで保存されている場合、取得した文字列が文字化けすることがあります。書き込み時に明示的に文字セットを指定すると解決できます。

```java
Files.writeString(
    Path.of(targetPath),
    htmlContent,
    StandardCharsets.ISO_8859_1
);
```

### 3. 大容量ファイル

数百メガバイトを超えるアーカイブの場合、文字列全体をメモリに保持せずに `BufferedWriter` へ直接ストリーミングして書き出すことを検討してください。Aspose には `save` メソッドがあり、途中の `String` を経由せずに直接ファイルへ書き込むことができます。

---

## プロのコツ & ベストプラクティス

- **`MhtmlDocument` オブジェクトを再利用** すれば、CSS や画像など複数のパーツを抽出する際にアーカイブの解析を一度だけ行えます。  
- **出力を検証** する際は HTML バリデータ（W3C バリデータや `jsoup.isValid()`）を使用し、次のシステムへ渡す前に問題がないか確認してください。  
- **本番環境ではログを使用** し、`System.out.println` はやめましょう。SLF4J などのロギングフレームワークに置き換えて、タイムスタンプや重要度を記録します。  
- **依存関係はバージョン管理** してください。Aspose は頻繁に更新されるため、`pom.xml` でバージョンを固定し、予期せぬ破壊的変更を防ぎます。

---

## 結論

ここまでで、**MHTML から HTML を抽出**する実用的かつエンドツーエンドな解決策を Java で実装しました。アーカイブをストリームとして開き、Aspose.HTML でロードし、HTML 文字列を取得し、**文字列をファイルに書き込む**という流れを習得したことで、**MHTML から HTML への変換**、**メール本文の抽出**、さらには **MHT から HTML への変換** を安定して行えるようになりました。

スニペットは自由にカスタマイズできます。たとえば、データベースに保存されたアーカイブを処理する場合は `FileInputStream` を `ByteArrayInputStream` に置き換えるだけですし、数十件のメールを一括処理するバッチジョブに組み込むことも可能です。基本的な考え方は変わりません――専用ライブラリに重い処理を任せ、取得したプレーンテキストを必要に応じて扱うだけです。

**次に試すべきこと:**

- Jsoup を使って **抽出した HTML をクリーンアップ**（トラッキングピクセルやインライン CSS の除去など）する。  
- ディレクトリ内の `.mht` ファイルをループ処理して **一括変換** を自動化する。  
- **Apache POI** と組み合わせて、クリーンアップした HTML を Word や PDF に埋め込む。

特定のエッジケースについて質問がある場合や、拡張した実装を共有したい場合はコメントで教えてください。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}