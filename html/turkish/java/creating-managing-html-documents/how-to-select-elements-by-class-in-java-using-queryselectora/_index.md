---
category: general
date: 2026-09-29
description: Sınıfa göre öğeleri seçmeyi, dosyadan HTML okumayı ve Java’da dış bağlantıları
  bulmayı öğrenin. Bu adım adım kılavuz, bir NodeList’i verimli bir şekilde yinelemeyi
  kapsar.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- select elements by class
- read html from file
- find external links
- iterate nodelist java
- use queryselectorall java
language: tr
lastmod: 2026-09-29
og_description: Sınıfa göre Java’da öğeleri seçin, dosyadan HTML okuyun ve querySelectorAll
  kullanarak dış bağlantıları bulun. NodeList’i yinelemek için tam örneği izleyin.
og_image_alt: Screenshot showing Java code that selects elements by class from an
  HTML file
og_title: Java'da sınıfa göre öğeleri seç – querySelectorAll ile tam rehber
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to select elements by class, read HTML from file, and find
    external links in Java. This step‑by‑step guide covers iterating a NodeList efficiently.
  headline: How to select elements by class in Java using querySelectorAll
  type: TechArticle
- questions:
  - answer: Yes. `Jsoup.parse` treats the input as a fragment and automatically adds
      missing root elements, allowing selectors to work on the fragment’s body.
    question: Does this work with HTML fragments that lack a `<html>` root?
  - answer: The standard Java DOM API (`org.w3c.dom`) does not include `querySelectorAll`.
      Libraries such as **HTMLUnit** or **jodd-lagarto** provide similar methods.
      The pattern shown here—load, select with CSS, iterate—remains the same.
    question: Can I use `querySelectorAll` without jsoup?
  - answer: 'After obtaining each `Element`, you can call `link.attr("href", "newUrl")`
      and then write the document back to disk with `Files.writeString`. ## Conclusion
      You now know how to **select elements by class**, **read HTML from file**, **find
      external links**, and **iterate a NodeList in Java** using `qu'
    question: What if I need to modify the links instead of just printing them?
  type: FAQPage
tags:
- Java
- HTML parsing
- DOM manipulation
title: Java'da querySelectorAll ile sınıfa göre öğeleri seçme
url: /tr/java/creating-managing-html-documents/how-to-select-elements-by-class-in-java-using-queryselectora/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da querySelectorAll kullanarak sınıfa göre öğeleri seçme

Java'da bir HTML dosyasını işlerken **sınıfa göre öğeleri seçmeniz** gerekiyorsa, bu kılavuz tam olarak nasıl yapılacağını gösterir. HTML'yi dosyadan okumayı, `querySelectorAll` kullanarak dış bağlantıları bulmayı ve ortaya çıkan `NodeList`'i güvenli bir şekilde yinelemeyi öğreneceksiniz.

Java'da HTML ile çalışmak genellikle ağır bir iş gibi hissettirebilir, ancak modern kütüphaneler size özlü, CSS‑seçici‑tabanlı bir API sunar. Aşağıdaki örnek **jsoup** (sürüm 1.17.2) kullanıyor çünkü `querySelectorAll`‑stilinde seçicileri uygular ve `NodeList` gibi davranan bir `Elements` koleksiyonu döndürür. Gerekirse aynı mantığı diğer DOM uygulamalarına da uyarlayabilirsiniz.

## Önkoşullar

* JDK 17 veya daha yeni bir sürüm yüklü.
* Bağımlılık yönetimi için Maven veya Gradle.
* Java akışları ve DOM modeli hakkında temel bilgi.

Projenize jsoup ekleyin:

```xml
<!-- Maven -->
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

```gradle
// Gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

## Adım 1: HTML'yi dosyadan okuyun

İlk görev, HTML belgesini diskteki dosyadan yüklemektir. `Jsoup.parse(Path, Charset)` dosyayı okur ve sorgulayabileceğiniz bir DOM ağacı oluşturur.

```java
import java.nio.file.Paths;
import java.nio.charset.StandardCharsets;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class HtmlLoader {
    /**
     * Loads an HTML file and returns a Jsoup Document.
     *
     * @param filePath absolute or relative path to the HTML file
     * @return parsed Document ready for DOM queries
     * @throws IOException if the file cannot be read
     */
    public static Document load(String filePath) throws IOException {
        return Jsoup.parse(Paths.get(filePath).toFile(),
                           StandardCharsets.UTF_8.name(),
                           "");
    }
}
```

*Neden önemli*: Dosyayı bir kez yüklemek, daha sonra öğeler üzerinde yineleme yaparken tekrarlanan I/O işlemlerinden kaçınmanızı sağlar. `Document` nesnesi tam DOM'u tutar ve hızlı seçici sorgularına olanak tanır.

## Adım 2: `querySelectorAll` kullanarak sınıfa göre öğeleri seçin

Belge belleğe yüklendiğine göre, bir CSS seçicisi kullanarak **sınıfa göre öğeleri seçebilirsiniz**. `"a.external"` seçicisi, `external` sınıfını taşıyan `<a>` etiketlerini eşleştirir—tam da **dış bağlantıları bulmak** için ihtiyacınız olan şey.

```java
import org.jsoup.select.Elements;
import org.jsoup.nodes.Element;

/**
 * Returns all anchor elements with the CSS class "external".
 *
 * @param doc the parsed HTML document
 * @return a collection of matching Elements
 */
public static Elements findExternalLinks(Document doc) {
    // querySelectorAll is simulated by the select() method in Jsoup
    return doc.select("a.external");
}
```

*Neden önemli*: Bir sınıf seçicisi kullanmak hem ifade gücüne sahiptir hem de performanslıdır. Kütüphane seçiciyi optimize edilmiş bir geçişe dönüştürür, böylece her düğüm için manuel döngüler yazmanıza gerek kalmaz.

## Adım 3: Java'da NodeList (Elements) üzerinde yineleme yapın

`Elements`, `Iterable<Element>` arayüzünü uygular, bu da standart bir `for‑each` döngüsü kullanarak **NodeList Java** nesnelerini **yineleyebileceğiniz** anlamına gelir. Aşağıdaki döngü her bağlantının `href` özniteliğini yazdırır.

```java
/**
 * Prints the href attribute of every external link.
 *
 * @param externalLinks collection returned by findExternalLinks()
 */
public static void printExternalLinks(Elements externalLinks) {
    for (Element link : externalLinks) {
        System.out.println("External link: " + link.attr("href"));
    }
}
```

*Neden önemli*: Doğrudan yineleme kodun okunabilirliğini korur ve sadece basit bir çıktı gerektiğinde koleksiyonu akıma dönüştürmenin getirdiği ek yükten kaçınır.

## Tam çalışan örnek

Üç adımı birleştirerek komut satırından çalıştırabileceğiniz bağımsız bir program elde edersiniz.

```java
import java.io.IOException;
import org.jsoup.nodes.Document;
import org.jsoup.select.Elements;

public class ExternalLinkExtractor {

    public static void main(String[] args) {
        // Validate input
        if (args.length != 1) {
            System.err.println("Usage: java ExternalLinkExtractor <input.html>");
            System.exit(1);
        }

        String inputPath = args[0];

        try {
            // Step 1: read HTML from file
            Document doc = HtmlLoader.load(inputPath);

            // Step 2: select elements by class (find external links)
            Elements externalLinks = findExternalLinks(doc);

            // Step 3: iterate NodeList Java and print hrefs
            printExternalLinks(externalLinks);
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
        }
    }

    // Reuse methods from previous sections
    private static Elements findExternalLinks(Document doc) {
        return doc.select("a.external");
    }

    private static void printExternalLinks(Elements externalLinks) {
        for (org.jsoup.nodes.Element link : externalLinks) {
            System.out.println("External link: " + link.attr("href"));
        }
    }
}
```

### Beklenen çıktı

`input.html` dosyasının şu içeriğe sahip olduğunu varsayalım:

```html
<a class="external" href="https://example.com">Example</a>
<a class="internal" href="/about">About</a>
<a class="external" href="https://openai.com">OpenAI</a>
```

Programı çalıştırdığınızda şu çıktı verir:

```
External link: https://example.com
External link: https://openai.com
```

## Profesyonel ipuçları ve yaygın tuzaklar

* **Kodlama önemlidir** – Dosyayı her zaman UTF‑8 (veya kaynağınıza uygun karakter seti) ile okuyun. Yanlış kodlama, öznitelik değerlerindeki karakterleri bozabilir.
* **Birden fazla sınıf** – Bir öğenin birden çok sınıfı varsa (ör. `class="btn external"`), `"a.external"` seçicisi yine de eşleşir çünkü CSS sınıf seçicileri tam dizeyi değil, token varlığını kontrol eder.
* **Performans ipucu** – Yalnızca `href` özniteliğine ihtiyacınız varsa, `doc.select("a.external[href]").eachAttr("href")` ile doğrudan isteyebilirsiniz. Bu, her eşleşme için tam `Element` nesneleri oluşturmayı önler.
* **Null güvenliği** – `link.attr("href")` öznitelik eksikse boş bir dize döndürür, bu yüzden yazdırmadan önce null kontrolüne gerek yoktur.

## Sıkça sorulan sorular

**S: Bu, `<html>` kökü olmayan HTML parçacıklarıyla çalışır mı?**  
C: Evet. `Jsoup.parse` girdiyi bir parça olarak ele alır ve eksik kök öğelerini otomatik olarak ekler, böylece seçiciler parçanın gövdesinde çalışabilir.

**S: `querySelectorAll`'ı jsoup olmadan kullanabilir miyim?**  
C: Standart Java DOM API'si (`org.w3c.dom`) `querySelectorAll` içermez. **HTMLUnit** veya **jodd-lagarto** gibi kütüphaneler benzer yöntemler sunar. Burada gösterilen desen—yükle, CSS ile seç, yinele—aynı kalır.

**S: Bağlantıları sadece yazdırmak yerine değiştirmem gerekirse ne yapmalıyım?**  
C: Her `Element` elde edildikten sonra `link.attr("href", "newUrl")` çağırabilir ve ardından belgeyi `Files.writeString` ile diske geri yazabilirsiniz.

## Sonuç

Artık **sınıfa göre öğeleri seçmeyi**, **HTML'yi dosyadan okumayı**, **dış bağlantıları bulmayı** ve `querySelectorAll`‑stilindeki seçicileri kullanarak **Java'da bir NodeList'i yinelemeyi** biliyorsunuz. Tam örnek, daha büyük kazıma veya dönüşüm hatlarına yerleştirebileceğiniz temiz, üretim‑hazır bir iş akışını gösterir.

Sonra **HTMLUnit ile dinamik içeriği ayrıştırma**, **değiştirilmiş HTML'yi diske geri yazma** veya **Java akışlarını kullanarak bağlantı URL'lerini bir listeye toplama** gibi ilgili konuları keşfedin. Bunların her biri burada gösterilen sınıf‑tabanlı seçme tekniği üzerine inşa edilmiştir. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Java'da HTML sorgulama – Öğeleri seçme, öznitelik ile filtreleme ve metin alma](/html/english/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/)
- [NodeList Java'yı yineleme – HTML oku ve Görsel src al](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [Aspose.HTML for Java'da Dosyadan HTML Belgeleri Yükleme](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}