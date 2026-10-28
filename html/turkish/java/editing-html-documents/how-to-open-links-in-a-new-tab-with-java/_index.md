---
category: general
date: 2026-10-28
description: HTML'i Java'da ayrıştırarak dış bağlantıları bulup `target="_blank"`
  ekleyerek linklerin yeni sekmede açılmasını öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- open links new tab
- find external links
- add target blank
- parse html in java
- save modified html
language: tr
lastmod: 2026-10-28
og_description: 'Java kullanarak bağlantıları yeni sekmede aç: HTML''i ayrıştır, dış
  bağlantıları bul, target="_blank" ekle ve değiştirilmiş HTML''i kaydet.'
og_image_alt: Screenshot of Java code that parses HTML and updates external links
  to open in a new tab
og_title: Java ile bağlantıları yeni sekmede açma – adım adım rehber
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to open links in a new tab by parsing HTML in Java, finding
    external links and adding target blank.
  headline: How to open links in a new tab with Java
  type: TechArticle
tags:
- Java
- HTML parsing
- jsoup
- web automation
title: Java ile bağlantıları yeni sekmede nasıl açılır
url: /tr/java/editing-html-documents/how-to-open-links-in-a-new-tab-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java ile yeni sekmede linkleri nasıl açılır

Statik bir HTML dosyasından **linkleri yeni bir sekmede açmanız** gerekiyorsa, bu rehber tam olarak nasıl yapılacağını gösterir. **Java'da HTML ayrıştırmayı**, **dış linkleri bulmayı**, **target blank eklemeyi** ve **değiştirilmiş HTML'i kaydetmeyi** IDE'nizden çıkmadan öğreneceksiniz.

Dış linkleri yeni bir tarayıcı sekmesinde açmak, kullanıcı deneyimini iyileştirir ve ziyaretçileri orijinal sayfada tutar. Aşağıdaki çözüm herhangi bir HTML belgesiyle çalışır, sadece popüler jsoup kütüphanesini gerektirir ve Java 8 veya daha yeni sürümlerde çalışır.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* JDK 8 + yüklü  
* **jsoup** bağımlılığını çekebilecek bir yapı aracı (Maven veya Gradle)  
* `external` sınıfına sahip `<a>` etiketleri içeren bir HTML dosyası

Web sunucusuna veya ek framework'lere ihtiyacınız yoktur—jsoup her şeyi yerel olarak halleder.

## Adım 1: Projenizde jsoup'u kurun

jsoup'u bir bağımlılık olarak ekleyin. Maven kullanıyorsanız, bunu `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

Gradle için ise `build.gradle` dosyanıza aşağıdaki satırı ekleyin:

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Bu koordinatlar, (Ekim 2026 itibarıyla) en son kararlı sürümü çeker. Senkronizasyon sonrası Java kaynak dosyalarınızda `org.jsoup` sınıflarını içe aktarabilirsiniz.

## Adım 2: HTML belgesini ayrıştırın

Dosyayı ayrıştırmak, **linkleri yeni sekmede açma** hedefinin ilk adımıdır. `Jsoup.parse` yöntemi dosyayı değiştirilebilir bir DOM‑benzeri yapıya okur.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // Load the HTML document from disk
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");
        
        // Continue with link processing...
    }
}
```

*Bu neden önemli*: `Document`, CSS‑stil seçicileri sağlar; böylece ihtiyacınız olan öğeleri bulmak çok basit hâle gelir.

## Adım 3: Dış linkleri bulun

Şimdi `external` sınıfına sahip her `<a>` öğesini bulun. Bu, **dış linkleri bulma** gereksinimini karşılar.

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

// Inside main after parsing:
Elements externalLinks = doc.select("a.external");
```

`Elements`, eşleşen düğümlerin bir koleksiyonudur. Seçici boş bir küme döndürürse, HTML dosyanızda sınıf eksik ya da farklı bir adlandırma kullanılıyor demektir—seçiciyi buna göre ayarlayın.

## Adım 4: Her linke `target="_blank"` ekleyin

**Dış linkleri bulma** adımında elde edilen her düğüm için `target` özniteliğini `_blank` olarak ayarlayın. Bu, **target blank ekleme** adımını tamamlar ve tarayıcıların linki yeni bir sekmede açmasını sağlar.

```java
for (Element link : externalLinks) {
    link.attr("target", "_blank");
}
```

`attr` yöntemi mevcut `target` değerini üzerine yazar, böylece tüm dış bağlantılarda tutarlı davranış garantilenir.

## Adım 5: Değiştirilmiş HTML'i kaydedin

DOM güncellendikten sonra değişiklikleri bir dosyaya geri yazın. Bu, öğreticinin **değiştirilmiş html'i kaydet** kısmını tamamlar.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

// Still inside main:
Path output = Path.of("YOUR_DIRECTORY/updated.html");
Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
System.out.println("Updated file written to " + output);
```

`doc.outerHtml()` tüm belgeyi serileştirir, jsoup'un orijinal ayrıştırmasında korunan girinti ve biçimlendirmeyi korur.

## Tam çalışan örnek

Tüm adımları bir araya getiren, kopyalayıp yapıştırıp çalıştırabileceğiniz bağımsız bir program:

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

/**
 * Updates all external links so they open in a new tab.
 */
public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // 1️⃣ Parse the HTML file
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");

        // 2️⃣ Find external links (a.external)
        Elements externalLinks = doc.select("a.external");

        // 3️⃣ Add target="_blank" to each link
        for (Element link : externalLinks) {
            link.attr("target", "_blank");
        }

        // 4️⃣ Save the modified HTML
        Path output = Path.of("YOUR_DIRECTORY/updated.html");
        Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
        System.out.println("Updated file written to " + output);
    }
}
```

### Beklenen çıktı

`sample.html` dosyasının şu şekilde olduğunu varsayalım:

```html
<a href="https://example.com" class="external">Example</a>
<a href="/internal/page.html">Internal</a>
```

Programı çalıştırdıktan sonra `updated.html` şu içeriği taşıyacaktır:

```html
<a href="https://example.com" class="external" target="_blank">Example</a>
<a href="/internal/page.html">Internal</a>
```

Yalnızca dış link `target="_blank"` özniteliği almıştır; bu sayede tarayıcılar artık linki yeni bir sekmede açar.

## Profesyonel ipuçları ve yaygın tuzaklar

* **Pro ipucu:** CSS sınıfı olmadan `http://` veya `https://` ile başlayan linkleri dış link olarak kabul etmek isterseniz seçiciyi genişletin: `doc.select("a[href^=http]")`.
* **Köşe durumu:** Bazı sayfalarda zaten `target="_self"` belirtilmiş olabilir; `attr` çağrısı bunu üzerine yazar, tutarlı davranışı sağlar.
* **Performans:** Çok büyük HTML dosyaları için bellek kullanımını azaltmak amacıyla akış tabanlı ayrıştırma (`Jsoup.parse(File, String, String, Parser.htmlParser())`) düşünün.
* **Test:** Sonucu, `updated.html` dosyasını bir tarayıcıda açıp geliştirici araçlarıyla linki inceleyerek doğrulayın—`target` özniteliğinin varlığını kontrol edin.

## Sonuç

Artık **Java kullanarak linkleri yeni bir sekmede açma** için eksiksiz, çalıştırılabilir bir çözüme sahipsiniz. Bu öğreticide **java'da html ayrıştırma**, **dış linkleri bulma**, **target blank ekleme** ve **değiştirilmiş html'i kaydetme** konularını hafif jsoup kütüphanesiyle ele aldık.

Bundan sonra şunları yapabilirsiniz:

* Seçiciyi diğer link desenlerini (ör. `rel="external"`) kapsayacak şekilde genişletin.  
* Bu mantığı, projedeki tüm HTML dosyalarını işleyen bir yapı adımıyla birleştirin.  
* Kodu, daha büyük bir içerik‑yönetim boru hattına entegre edin.

Farklı seçiciler veya çıktı formatlarıyla denemeler yapmaktan çekinmeyin ve sonuçlarınızı toplulukla paylaşın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakın konuları kapsayan içerikler sunar. Her kaynak, adım adım açıklamalar ve tam çalışan kod örnekleri içerir; böylece ek API özelliklerini öğrenebilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [Java'da CSS Kullanımı – HTML Yükleme, Bağlantı Sayma ve XPath Değerlendirme](/html/english/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/)
- [Java'da HTML Ayrıştırma – HTML Makalelerinden Metin Çıkarma](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Java ile yeni HTML öğesi oluşturma – Tam Aspose.HTML Kılavuzu](/html/english/java/editing-html-documents/create-new-html-element-with-java-full-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}