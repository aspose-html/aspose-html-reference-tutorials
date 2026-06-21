---
category: general
date: 2026-04-02
description: Aspose.HTML Sandbox'ta DPI ayarlamayı, görünüm alanı boyutunu ve kullanıcı
  ajanını nasıl ayarlayacağınızı öğrenin. Tam kod ve ipuçlarıyla adım adım Java örneği.
draft: false
keywords:
- how to set dpi
- set viewport size
- set user agent
- Aspose.HTML sandbox
- Java rendering settings
language: tr
og_description: Aspose.HTML Sandbox'ta DPI, viewport boyutunu ve kullanıcı aracısını
  ayarlamayı eksiksiz bir Java örneğiyle öğrenin.
og_title: Aspose.HTML Sandbox'ta DPI Nasıl Ayarlanır – Java Öğreticisi
tags:
- Aspose.HTML
- Java
- Rendering
- Sandbox
title: Aspose.HTML Sandbox'ta DPI Nasıl Ayarlanır – Tam Java Rehberi
url: /tr/java/configuring-environment/how-to-set-dpi-in-aspose-html-sandbox-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML Sandbox'ta DPI Nasıl Ayarlanır – Tam Java Rehberi

Aspose.HTML ile bir web sayfasını render ederken **DPI nasıl ayarlanır** diye hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok test senaryosunda düzenin belirli bir ekran yoğunluğuna uyması gerekir—baskıya hazır PDF'ler ya da yüksek çözünürlüklü ekran görüntüleri gibi. İyi haber şu ki, Aspose.HTML sandbox DPI, viewport boyutu ve hatta user‑agent dizesini tek bir paket içinde kontrol etmenizi sağlıyor.

Bu öğreticide, **DPI ayarlayan**, **viewport boyutunu ayarlayan** ve **user‑agent'ı ayarlayan** pratik bir Java örneği üzerinden ilerleyeceğiz. Sonunda çalıştırılabilir bir programınız olacak, her ayarın neden önemli olduğunu anlayacaksınız ve sandbox'ı kendi projeleriniz için özelleştirmeye hazır olacaksınız.

---

## Gereksinimler

- **Java 17** (veya herhangi bir güncel JDK; API Java 8+ ile uyumludur)
- **Aspose.HTML for Java** kütüphanesi (sürüm 23.12 veya daha yeni)
- Bir IDE veya basit bir metin editörü + komut satırı derlemesi
- Örnek URL için internet erişimi (`https://example.com`)

Harici bir derleme aracı gerekmez; kod `javac` ile derlenir ve `java` ile çalıştırılır. Maven ya da Gradle tercih ederseniz sadece Aspose.HTML bağımlılığını ekleyin—başka bir şey yapmanıza gerek yok.

---

## Adım 1: Rendering Ortamını Tanımlayan Bir Sandbox Oluşturun

Sandbox, Aspose.HTML'e “hangi ekranı” taklit ettiğinizi söylediğiniz yerdir. Burada **1024 × 768 viewport**, **96 DPI** ve özel bir **user‑agent dizesi** ayarlıyoruz.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Define the sandbox – this is the core of how to set dpi, viewport, and user agent.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent
```

**Neden önemli:**  
- **DPI**, CSS `pt` birimlerinin piksellere nasıl dönüştüğünü etkiler; daha yüksek DPI daha keskin render sağlar.  
- **Viewport boyutu**, responsive CSS'in tetiklediği layout kırılma noktalarını belirler.  
- **User‑agent**, sunucu tarafı içerik varyasyonlarını (mobil vs masaüstü) tetikleyebilir.

> **Pro ipucu:** Daha sonra PDF oluşturacaksanız, DPI'yi hedef baskı çözünürlüğüne (ör. yüksek kalite baskılar için 300 dpi) eşleştirin.

---

## Adım 2: Sandbox İçinde Bir Web Sayfası Yükleyin

Şimdi sandbox'ı bir URL'ye yönlendiriyoruz. `HTMLDocument` yapıcı metodu sandbox'ı kabul eder, böylece layout motoru tanımladığımız ayarları dikkate alır.

```java
        // Load the page using the sandbox we just configured.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {
```

**Arka planda ne oluyor?**  
Aspose.HTML, tam bir Chromium örneğinin ağırlığı olmadan, başsız bir tarayıcıya benzer izole bir render bağlamı oluşturur. Bu, işlemi hızlı ve bellek‑hafif hâle getirir—toplu işleme için mükemmeldir.

---

## Adım 3: DOM ile Etkileşim – Sayfa Başlığını Okuyun

Gösterim amaçlı başlığı alıp ekrana yazdıracağız. Gerçek bir senaryoda ekran görüntüsü alabilir, PDF'ye dışa aktarabilir ya da veri kazıyabilirsiniz.

```java
            // Simple DOM interaction – fetch and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());
        }
    }
}
```

**Beklenen çıktı** (`https://example.com` erişilebilir olduğunda):

```
Title inside sandbox: Example Domain
```

Site farklı bir başlık döndürürse, onu göreceksiniz—başka bir değişiklik yapmanıza gerek yok.

---

## Adım 4: Ayarları Doğrulama (İsteğe Bağlı Hata Ayıklama)

Bazen sandbox'ın DPI ve viewport ayarlarını gerçekten uyguladığını iki kez kontrol etmek istersiniz. Aspose.HTML bu değerleri doğrudan sunmaz, ancak öğe boyutlarını ölçerek çıkarım yapabilirsiniz.

```java
        // Example: measure a known element's width in pixels.
        int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
        System.out.println("Measured width (px): " + elementWidth);
```

CSS'de öğenin `width: 200pt;` olarak tanımlandığını biliyorsanız, **96 dpi**'de `200pt * (96/72) ≈ 267px` görmelisiniz. DPI'yi değiştirip yeniden çalıştırın; sayının değiştiğini göreceksiniz—**DPI nasıl ayarlanır** sorusunun gerçekten çalıştığının kanıtı.

---

## Tek Bir Blokta Tam Kaynak Kodu

Aşağıdakileri `SandboxExample.java` dosyasına kopyalayıp yapıştırın. Olduğu gibi derlenir; sadece Aspose.HTML JAR dosyasının sınıf yolunuzda olduğundan emin olun.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox that defines the rendering environment
        // (viewport size 1024×768 and 96 dpi) and a custom user‑agent string.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent

        // Step 2: Load a web page inside the sandbox so layout respects the settings.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {

            // Step 3: Interact with the DOM – here we simply read and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());

            // Optional: verify DPI effect by measuring an element (if you know its CSS size).
            // int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
            // System.out.println("Measured width (px): " + elementWidth);
        }
    }
}
```

Derleyin ve çalıştırın:

```bash
javac -cp "aspose-html-23.12.jar" SandboxExample.java
java -cp ".:aspose-html-23.12.jar" SandboxExample
```

Başlık ekrana yazdırılacak, sandbox'ın **ayarlanmış DPI**, **ayarlanmış viewport boyutu** ve **ayarlanmış user‑agent** ile çalıştığını onaylayacaksınız.

---

## Yaygın Sorular ve Kenar Durumları

### Farklı bir DPI'ye ihtiyacım olursa?

`DocumentSandbox`'ın ikinci argümanını değiştirmeniz yeterlidir. Baskıya hazır PDF'ler için `300` kullanabilirsiniz:

```java
new DocumentSandbox(new Size(1024, 768), 300, "MyCustomUserAgent/1.0");
```

Daha yüksek DPI, aynı CSS puanları için daha büyük piksel boyutları üretir; raster kalitesini artırır ancak daha fazla bellek tüketir.

### URL yerine yerel bir HTML dosyası yükleyebilir miyim?

Elbette. URL'yi bir dosya yolu ile değiştirin:

```java
HTMLDocument webDoc = new HTMLDocument("file:///C:/myfolder/page.html", renderingSandbox);
```

Yolun mutlak olduğundan ve `file:///` şemasını kullandığından emin olun.

### Sandbox oluşturulduktan sonra user‑agent'ı nasıl değiştiririm?

Sandbox değiştirilemez—`HTMLDocument`'e geçirdiğiniz anda ayarlar kilitlenir. Farklı bir user‑agent kullanmak için istediğiniz dizeyle yeni bir `DocumentSandbox` örneği oluşturmanız gerekir.

### Aspose.HTML JavaScript yürütmeyi destekliyor mu?

Evet, motor çoğu istemci‑tarafı betiği çalıştırır. Bir betik yüklemeden sonra DOM'u değiştiriyorsa, biraz bekleyebilirsiniz:

```java
webDoc.waitForLoad();
```

Ya da öğeleri sorgulamadan önce sayfa içinde `setTimeout` benzeri bir mantık kullanın.

---

## Görsel Doğrulama (Resim)

Aşağıda başarılı çalıştırmayı gösteren bir konsol ekran görüntüsü yer alıyor. Başlık çıktısının sayfayla eşleştiğine dikkat edin; sandbox ayarlarımızın uygulandığını doğruluyor.

![Aspose.HTML Sandbox'ta DPI ayarlama, viewport boyutu ayarlama ve user agent ayarlama gösteren konsol çıktısı](/images/console-output.png)

*Alt text:* *Aspose.HTML Sandbox'ta DPI ayarlama, viewport boyutu ayarlama ve user‑agent ayarlama gösteren konsol çıktısı.*

---

## Özet ve Sonraki Adımlar

**DPI nasıl ayarlanır** (örnekte 96 dpi), **viewport boyutu nasıl ayarlanır** (1024 × 768) ve **user‑agent nasıl ayarlanır** (özel dize) konularını Aspose.HTML sandbox API'siyle ele aldık. Tam, çalıştırılabilir Java programı, bu ayarların sadece teorik olmadığını, doğrudan render ve DOM etkileşimini etkilediğini kanıtlıyor.

Daha fazlasına hazır mısınız?

- **PDF Olarak Dışa Aktar:** Sayfayı yükledikten sonra `webDoc.save("output.pdf", SaveFormat.PDF);` çağrısını yaparak ayarladığınız DPI'yi yansıtan yüksek çözünürlüklü bir PDF oluşturabilirsiniz.  
- **Ekran Görüntüsü Al:** `webDoc.renderToBitmap("screenshot.png");` ile piksel‑tam görüntüler elde edin.  
- **Responsive Layout'larla Oynayın:** Gerçek bir cihaz olmadan mobil kırılma noktalarını test etmek için viewport boyutlarını değiştirin.  

Farklı DPI değerleri, viewport kombinasyonları ve user‑agent'larla deney yapın; sunucuların ve CSS'in nasıl tepki verdiğini görün. Sandbox, tam tarayıcıları çalıştırmadan size hafif bir oyun alanı sunar.

---

### Keşfetmeye Devam Et

- **Aspose.HTML Documentation** – `DocumentSandbox` seçeneklerine derinlemesine bakın.  
- **Advanced CSS Media Queries** – viewport boyutunun farklı stilleri nasıl tetiklediğini öğrenin.  
- **User‑Agent Spoofing** – bazı sitelerin user‑agent dizesine göre alternatif işaretleme sunduğunu keşfedin.

Sorularınız veya zor bir durumunuz mu var? Bir yorum bırakın, birlikte sorunları çözelim. Mutlu kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}