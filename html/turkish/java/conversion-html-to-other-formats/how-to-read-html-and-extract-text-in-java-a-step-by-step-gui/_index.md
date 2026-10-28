---
category: general
date: 2026-10-28
description: Java'da HTML nasıl okunur ve HTML dosyalarından metin nasıl çıkarılır.
  Jsoup ile HTML'yi metne dönüştürmeyi öğrenin; dosyadan HTML okuma ve Java'da HTML'den
  metne dönüşüm tekniklerini kapsar.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to read html
- extract text from html
- convert html to text
- html to text java
- read html from file
language: tr
lastmod: 2026-10-28
og_description: Java’da HTML nasıl okunur ve HTML dosyalarından metin nasıl çıkarılır.
  Bu öğreticide Jsoup kullanarak HTML’yi metne dönüştürmek için tam bir çözüm gösterilmektedir.
og_image_alt: Diagram showing how to read HTML and extract text in Java
og_title: HTML'yi okuma ve Java'da metin çıkarma – hızlı rehber
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  headline: How to read HTML and extract text in Java – a step‑by‑step guide
  type: TechArticle
- description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  name: How to read HTML and extract text in Java – a step‑by‑step guide
  steps:
  - name: Maven
    text: '```xml <dependency> <groupId>org.jsoup</groupId> <artifactId>jsoup</artifactId>
      <version>1.17.2</version> </dependency> ```'
  - name: Gradle
    text: '```gradle implementation ''org.jsoup:jsoup:1.17.2'' ```'
  - name: Expected output
    text: 'Assuming `input.html` contains:'
  - name: Running the program
    text: '```bash javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java java -cp .:jsoup-1.17.2.jar
      HtmlToTextDemo ```'
  type: HowTo
tags:
- Java
- HTML parsing
- Text extraction
title: Java'da HTML'yi okuma ve metin çıkarma – adım adım rehber
url: /tr/java/conversion-html-to-other-formats/how-to-read-html-and-extract-text-in-java-a-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da HTML okuma ve metin çıkarma – adım adım kılavuz

Yerel bir dosyadan **how to read html** yapmanız gerekiyorsa, bu kılavuz eksiksiz bir çözüm sunar. Bir HTML belgesini nasıl yükleyeceğinizi, düz metni nasıl çıkaracağınızı ve isteğe bağlı olarak HTML'yi ince ayarlı kontrolle metne nasıl dönüştüreceğinizi öğreneceksiniz. Eğitim sonunda örnek kodu çalıştırabilir ve çıkarılan metnin konsola yazdırıldığını görebilirsiniz.

HTML dosyalarını okumak, web kazıma verilerini işleme, rapor oluşturma veya kullanıcı tarafından oluşturulan içeriği temizleme gibi durumlarda yaygın bir görevdir. Aşağıdaki adımlar, gerekli kütüphaneyi eklemekten bozuk işaretleme ya da karakter kodlaması sorunları gibi uç durumları ele almaya kadar ihtiyacınız olan her şeyi kapsar.

## İhtiyacınız olanlar

- Java 17 veya daha yeni (kod daha eski sürümlerle de derlenebilir)
- Bağımlılık yönetimi için Maven veya Gradle, ya da Jsoup JAR'ı manuel olarak ekleyerek
- Projenin `src/main/resources` dizinine yerleştirilmiş `input.html` adlı bir HTML dosyası (yolu daha sonra değiştirebilirsiniz)

## Jsoup kütüphanesini kurun

Jsoup, HTML'yi DOM benzeri bir yapıya ayrıştıran hafif ve iyi belgelenmiş bir kütüphanedir. Bozuk HTML'yi sorunsuz bir şekilde işler, bu da **extract text from html** görevleri için ideal kılar.

### Maven

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

### Gradle

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Manuel indirmeyi tercih ederseniz, JAR dosyasını sınıf yolunuza yerleştirin ve kaynak dosyanızda `org.jsoup.*` paketini içe aktarın.

## Dosyadan HTML yükleme

İlk programatik adım, dosyayı bir `Document` nesnesine okumaktır. Jsoup, bir `File` ve karakter seti adını kabul eden statik bir `parse` yöntemi sunar.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Path to the HTML file – adjust if your file lives elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Parse the file using UTF‑8 encoding
            Document doc = Jsoup.parse(input, "UTF-8");
            // Continue with text extraction…
        } catch (IOException e) {
            System.err.println("Failed to read the HTML file: " + e.getMessage());
        }
    }
}
```

**Neden önemli:** `Jsoup.parse(File, String)` ham baytları okur, verilen karakter setine göre çözer ve temiz bir DOM oluşturur. Bu yaklaşım, dosyayı kendiniz bir dizeye okumanıza göre daha güvenlidir; çünkü Jsoup satır sonlarını normalleştirir ve yaygın işaretleme hatalarını otomatik olarak düzeltir.

## HTML'den düz metin çıkarma

Bir `Document` elde ettiğinizde, görünen metni almak tek bir yöntem çağrısıdır. `text()` yöntemi, tüm öğelerin metinsel içeriğini birleştirirken etiketleri, script ve stil bölümlerini atar.

```java
// Inside the try block from the previous snippet
String plainText = doc.body().text();
System.out.println("Extracted text:");
System.out.println(plainText);
```

`body()` çağrısı, çıkarımı `<body>` öğesiyle sınırlar; bu, içerik analizi için **read html from file** yaparken tipik hedeftir. Ortaya çıkan dize, boşlukları tek bir boşluğa çökertir ve bir tarayıcının metni nasıl render edeceğine benzer bir biçimde sunar.

### Beklenen çıktı

`input.html` dosyası şu içeriğe sahipse:

```html
<!DOCTYPE html>
<html>
<head><title>Sample</title></head>
<body>
  <h1>Hello World</h1>
  <p>This is a <strong>demo</strong> page.</p>
</body>
</html>
```

Program çalıştırıldığında şu çıktı verir:

```
Extracted text:
Hello World This is a demo page.
```

## HTML'yi ek seçeneklerle metne dönüştürme

Bazen `text()` metodunun sunduğundan daha fazla kontrol gerekir—örneğin satır sonlarını korumak, liste numaralandırmasını tutmak ya da belirli etiketleri yok saymak. Jsoup’un `NodeTraversor` sınıfı ile özel bir `NodeVisitor` birleştirildiğinde bu esnekliği elde edersiniz.

```java
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

public class HtmlToTextDemo {

    // ... (main method unchanged)

    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();
        NodeVisitor visitor = new NodeVisitor() {
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Preserve line breaks for block elements
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }
            public void tail(Node node, int depth) {
                // No action needed on exit
            }
        };
        NodeTraversor.traverse(visitor, doc.body());
        // Collapse multiple newlines into a single one
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

Basit `doc.body().text()` çağrısını şu kodla değiştirin:

```java
String detailedText = convertHtmlToText(doc);
System.out.println("Detailed conversion:");
System.out.println(detailedText);
```

**Neden çalışıyor:** Ziyaretçi, DOM'u derinlemesine dolaşarak her blok‑seviye öğeden (ör. `<p>`, `<div>`, `<h1>`) önce bir yeni satır ekler. Bu, paragraf ayrımlarını korur ve **convert html to text** işlemlerinde okunabilirliği ya da sonraki NLP boru hatlarını iyileştirir.

## Yaygın tuzaklar ve en iyi uygulamalar

| Sorun | Neden oluşur | Önerilen çözüm |
|-------|---------------|-----------------|
| Yanlış karakter seti | Dosyalar ISO‑8859‑1 olarak kaydedilip UTF‑8 olarak ayrıştırıldığında bozuk karakterler oluşur. | Dosyanın meta etiketinden (`<meta charset="...">`) karakter setini algılayın veya `Jsoup.parse` metoduna doğru adı geçirin. |
| Büyük dosyalar | Çok büyük bir HTML dosyasını belleğe yüklemek `OutOfMemoryError` hatasına yol açabilir. | `Jsoup.parse(File, String, String baseUri)` ile dosyayı akış olarak işleyin ve düğümleri kademeli olarak işleyin, ya da JVM yığın boyutunu artırın. |
| İstenmeyen script/style metni | `text()` script ve stil içeriğini kaldırır, ancak özel ziyaretçiler bunları yanlışlıkla dahil edebilir. | Ziyaretçinin `head` metodunda etiket adı `script` veya `style` olan düğümleri atlayın. |
| Boşlukların korunması | Boşlukların çökertilmesi, markdown dönüşümü için gerekli biçimlendirmeyi kaybettirebilir. | Ham metin düğümleri için `Element.wholeText()` kullanın, ardından boşlukları manuel olarak işleyin. |

Bu konulara dikkat etmek, **html to text java** çözümünüzün çeşitli girdilerde güvenilir çalışmasını sağlar.

## Tam çalıştırılabilir örnek

Aşağıda, bağımlılık kurulumundan çıktı doğrulamaya kadar tüm iş akışını gösteren bağımsız bir program yer almaktadır. Kodu `HtmlToTextDemo.java` adlı bir dosyaya kopyalayın, yanına bir `input.html` dosyası koyun ve gösterildiği gibi `javac && java` komutlarını çalıştırın.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Adjust the path if your HTML file is located elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Load and parse the HTML file using UTF‑8
            Document doc = Jsoup.parse(input, "UTF-8");

            // Simple extraction – suitable for most cases
            String plain = doc.body().text();
            System.out.println("=== Simple extraction ===");
            System.out.println(plain);
            System.out.println();

            // Detailed conversion – keeps line breaks for readability
            String detailed = convertHtmlToText(doc);
            System.out.println("=== Detailed conversion ===");
            System.out.println(detailed);
        } catch (IOException e) {
            System.err.println("Error reading HTML file: " + e.getMessage());
        }
    }

    /**
     * Walks the DOM and builds a text representation that preserves
     * line breaks for block‑level elements.
     *
     * @param doc the parsed HTML document
     * @return a readable plain‑text version of the HTML body
     */
    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();

        NodeVisitor visitor = new NodeVisitor() {
            @Override
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Add a newline before block elements (e.g., <p>, <div>, <h1>)
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }

            @Override
            public void tail(Node node, int depth) {
                // No operation needed when exiting a node
            }
        };

        NodeTraversor.traverse(visitor, doc.body());

        // Collapse consecutive newlines and trim leading/trailing whitespace
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

### Programı çalıştırma

```bash
javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java
java -cp .:jsoup-1.17.2.jar HtmlToTextDemo
```

Konsol, hem basit çıkarımı hem de detaylı ...

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanıza ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalarla tam çalışan kod örnekleri içerir.

- [Java’da XPath Kullanımı – HTML Okuma ve Metin Çıkarma](/html/english/java/creating-managing-html-documents/how-to-use-xpath-in-java-read-html-and-extract-text/)
- [Java’da HTML Ayrıştırma – HTML Makalelerinden Metin Çıkarma](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Java ile HTML’den Metin Çıkarma – Tam Adım Adım Kılavuz](/html/english/java/creating-managing-html-documents/extract-text-from-html-with-java-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}