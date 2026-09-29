---
category: general
date: 2026-09-29
description: Java kullanarak bir HTML dosyasında JavaScript ile arka plan rengini
  değiştirin. Java’da HTML yüklemeyi, HTML içinde JavaScript çalıştırmayı ve yeni
  bir sayfa arka planı için Java ile HTML’yi değiştirmeyi öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change background color javascript
- load html in java
- run js in html
- modify html with java
- set page background
language: tr
lastmod: 2026-09-29
og_description: Java kullanarak bir HTML sayfasında arka plan rengini JavaScript ile
  değiştirin. Bu öğreticide, Java’da HTML nasıl yüklenir, HTML içinde JavaScript nasıl
  çalıştırılır ve sayfa arka planı programlı olarak nasıl ayarlanır gösterilmektedir.
og_image_alt: Screenshot of Java code that changes the page background color
og_title: Java ile JavaScript'te arka plan rengini değiştirme – adım adım rehber
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Change background color javascript in an HTML file using Java. Learn
    to load html in java, run js in html, and modify html with java for a new page
    background.
  headline: How to change background color javascript using Java
  type: TechArticle
tags:
- Java
- HTMLUnit
- JavaScript
- HTML manipulation
title: Java kullanarak JavaScript ile arka plan rengini nasıl değiştiririz
url: /tr/java/editing-html-documents/how-to-change-background-color-javascript-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java kullanarak background color javascript değiştirme

Mevcut bir HTML dosyasında **change background color javascript** değiştirmeniz gerekiyorsa, bunu tarayıcı açmadan tamamen Java üzerinden yapabilirsiniz. Bu öğreticide **load html in java**, küçük bir JavaScript kod parçasını çalıştırmayı ve ardından **modify html with java** sayesinde sayfanın arka planının güncellenmesini gösteriyoruz.  

Çözüm, gerçek bir tarayıcının yapabildiği gibi JavaScript'i değerlendirebilen başsız bir tarayıcı sağlayan açık kaynaklı **HTMLUnit** kütüphanesiyle çalışır. Bu kılavuzun sonunda, istediğiniz herhangi bir renge **sets page background** yapan yeniden kullanılabilir bir metoda sahip olacaksınız.

## Önkoşullar

| Gerekenler | Neden Önemli |
|---------------|----------------|
| Java 8 veya daha yeni | HTMLUnit en az Java 8 gerektirir. |
| Maven veya Gradle yapı aracı | HTMLUnit bağımlılığını otomatik olarak çekmek için. |
| Düzenlemek istediğiniz bir HTML dosyası (ör. `input.html`) | Yüklenip değiştirilecek kaynak belge. |

Projenize HTMLUnit ekleyin:

*Maven*  

```xml
<dependency>
    <groupId>net.sourceforge.htmlunit</groupId>
    <artifactId>htmlunit</artifactId>
    <version>2.71.0</version>
</dependency>
```

*Gradle*  

```gradle
implementation 'net.sourceforge.htmlunit:htmlunit:2.71.0'
```

> **Pro tip:** En doğru JavaScript motorunu elde etmek için HTMLUnit'in en son kararlı sürümünü kullanın.

## background color javascript – Java'da HTML yükleme

İlk adım, HTML belgesini bir `HTMLPage` nesnesine yüklemektir. Bu, size DOM benzeri bir API ve bir JavaScript yürütme bağlamı sağlar.

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;

public class BackgroundColorChanger {

    /**
     * Loads an HTML file from the given path.
     *
     * @param htmlPath absolute or relative path to the source HTML file
     * @return HtmlPage representing the loaded document
     * @throws IOException if the file cannot be read
     */
    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        // WebClient acts as a headless browser; disabling CSS speeds up loading.
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);

        // Convert the file path to a URL that HTMLUnit can understand.
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }
}
```

*Neden önemli*: `WebClient`, JavaScript'in çalışabileceği izole bir ortam oluşturur, böylece **run js in html**'i bir kullanıcının tarayıcısı gibi tam olarak çalıştırabilirsiniz.

## run js in html ile sayfa arka planını ayarla

Sayfa yüklendikten sonra, herhangi bir JavaScript ifadesini değerlendirebilirsiniz. Aşağıdaki kod parçacığı `<body>` öğesinin `backgroundColor` stilini değiştirir.

```java
/**
 * Executes JavaScript that changes the page background color.
 *
 * @param page   the HtmlPage loaded earlier
 * @param color  any valid CSS color string, e.g., "lightblue" or "#ffcc00"
 */
private static void changeBackground(HtmlPage page, String color) {
    // The eval method runs JavaScript in the page's context.
    String script = "document.body.style.backgroundColor = '" + color + "';";
    page.getEnclosingWindow().getScriptableObject().eval(script);
}
```

*Açıklama*:  
- `document.body.style.backgroundColor` sayfanın arka planı için standart DOM özelliğidir.  
- `eval` çağrısı ile gerçek bir tarayıcı penceresine ihtiyaç duymadan **run js in html** yapıyoruz.  
- Metod, herhangi bir renk için yeniden kullanılabilir ve **set page background** gereksinimini karşılar.

## modify html with java ve sonucu kaydet

Betik çalıştıktan sonra, DOM yeni stili yansıtır. Artık güncellenmiş HTML'i diske geri yazabilirsiniz.

```java
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Saves the modified HTML content to a new file.
 *
 * @param page          the HtmlPage that has been altered
 * @param outputPath    destination file path
 * @throws IOException  if writing fails
 */
private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
    // page.asXml() returns the current HTML markup, including the changed style.
    String updatedHtml = page.asXml();
    Files.write(Paths.get(outputPath), updatedHtml.getBytes());
}
```

Her şeyi bir araya getirdiğinizde tek bir çalıştırılabilir program elde edersiniz:

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class BackgroundColorChanger {

    public static void main(String[] args) {
        // Adjust these paths for your environment.
        String inputFile = "YOUR_DIRECTORY/input.html";
        String outputFile = "YOUR_DIRECTORY/js_modified.html";
        String newColor = "lightblue"; // Change to any CSS color you need.

        try {
            HtmlPage page = loadHtml(inputFile);
            changeBackground(page, newColor);
            saveModifiedHtml(page, outputFile);
            System.out.println("Background color changed to '" + newColor + "' and saved to " + outputFile);
        } catch (IOException e) {
            System.err.println("Error processing HTML file: " + e.getMessage());
        }
    }

    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }

    private static void changeBackground(HtmlPage page, String color) {
        String script = "document.body.style.backgroundColor = '" + color + "';";
        page.getEnclosingWindow().getScriptableObject().eval(script);
    }

    private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
        String updatedHtml = page.asXml();
        Files.write(Paths.get(outputPath), updatedHtml.getBytes());
    }
}
```

### Beklenen çıktı

Programı çalıştırmak şu çıktıyı verir:

```
Background color changed to 'lightblue' and saved to YOUR_DIRECTORY/js_modified.html
```

`js_modified.html` dosyasını herhangi bir tarayıcıda açtığınızda sayfa açık mavi bir arka planla gösterilir ve **change background color javascript** işleminin başarılı olduğu doğrulanır.

## Yaygın varyasyonlar ve uç durumlar

| Durum | Nasıl ele alınır |
|-----------|------------------|
| **Different color formats** | Herhangi bir CSS‑uyumlu değer (`"red"`, `"#ff0000"`, `"rgb(255,0,0)"`) geçirin. |
| **Missing `<body>` tag** | Betik sessizce başarısız olur; önce `page.getFirstByXPath("//body")` ile `<body>` öğesinin varlığını kontrol edebilirsiniz. |
| **Large HTML files** | CSS'i devre dışı bırakın (`setCssEnabled(false)`) ve yalnızca ihtiyacınız olan JavaScript özelliklerini etkinleştirerek bellek kullanımını azaltın. |
| **Running multiple scripts** | `changeBackground` metodunu tekrar tekrar çağırın veya bir JavaScript komut listesi kabul eden yardımcı bir metod oluşturun. |

## Sonuç

Artık bir HTML dosyasını Java'da **change background color javascript** yükleyerek, **run js in html** ve **modify html with java** ile istediğiniz herhangi bir renge **set page background** yapmayı biliyorsunuz. Yukarıdaki tam örnek, en son HTMLUnit kütüphanesiyle çalışır ve HTML raporlarını toplu işleme veya e‑posta şablonları hazırlama gibi daha büyük otomasyon hatlarına entegre edilebilir.

**Next steps**  
- Diğer DOM manipülasyonlarını keşfedin (ör. öğe ekleme, script kaldırma).  
- Bu yaklaşımı bir PDF renderlayıcı ile birleştirerek stillendirilmiş sayfaların PDF'lerini oluşturun.  
- Tam tarayıcı uyumluluğu gerekiyorsa Selenium WebDriver gibi farklı bir başsız motor kullanmayı deneyin.

İyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Computed Style Java – HTML'den Arka Plan Rengini Çıkar](/html/english/java/css-html-form-editing/get-computed-style-java-extract-background-color-from-html/)
- [HTML'yi Nasıl Yüklenir, Cihaz DPI'sı Ayarlanır ve Arka Plan Rengi Okunur](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Java'da JavaScript'ten HTML Oluşturma – Tam Adım Adım Kılavuz](/html/english/java/creating-managing-html-documents/generate-html-from-javascript-in-java-complete-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}