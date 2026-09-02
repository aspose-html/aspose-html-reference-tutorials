---
category: general
date: 2026-01-07
description: Java'da Aspose HTML kullanarak bir web sayfasının ekran görüntüsünü nasıl
  alabilirsiniz. HTML'yi görüntüye dönüştürmeyi, görünüm alanı boyutunu ayarlamayı
  ve web sayfasını PNG olarak kaydetmeyi öğrenin.
draft: false
keywords:
- how to capture screenshot
- convert html to image
- set viewport size
- save webpage as png
- how to convert html
language: tr
og_description: Aspose HTML Java ile bir web sayfasının ekran görüntüsünü nasıl alabilirsiniz.
  HTML'yi görüntüye dönüştürme, görünüm alanı boyutunu ayarlama ve PNG olarak kaydetme
  adım adım rehberi.
og_title: Bir web sayfasının ekran görüntüsünü nasıl alırsınız – Java öğreticisi
tags:
- Aspose HTML
- Java
- Web automation
title: Aspose HTML ile bir web sayfasının ekran görüntüsünü nasıl alabilirsiniz –
  Java rehberi
url: /tr/java/conversion-html-to-various-image-formats/how-to-capture-screenshot-of-a-webpage-with-aspose-html-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose HTML – Java ile bir web sayfasının ekran görüntüsünü nasıl yakalarız

Dinamik bir web sayfasının **ekran görüntüsünü nasıl yakalarız** diye hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok projede—test, izleme veya içerik arşivleme—HTML'yi bir bitmap dosyasına dönüştürmenin güvenilir bir yoluna ihtiyacınız var. İyi haber? Aspose.HTML for Java bunu çocuk oyuncağı haline getiriyor.

Bu öğreticide tüm süreci adım adım inceleyeceğiz: bir sandbox yapılandırma, viewport boyutunu ayarlama, canlı bir URL'yi yükleme ve sonunda **convert html to image** ve **save webpage as png**. Sonunda tam olarak bunu yapan çalıştırılmaya hazır bir Java programına sahip olacaksınız.

## Gerekenler

* Java 17 (veya herhangi bir güncel JDK) yüklü.  
* Bağımlılıkları yönetmek için Maven veya Gradle.  
* Aspose.HTML for Java lisansı (ücretsiz değerlendirme testi için yeterli).  
* Java'ya temel aşinalık—gelişmiş hileler gerekmez.  

> **Pro ipucu:** Maven kullanıyorsanız, Aspose.HTML bağımlılığını `pom.xml` dosyanıza ekleyin. Tek bir satırdır ve her şeyi düzenli tutar.

## 1. Adım – Sandbox oluşturma ve **set viewport size**

Sandbox, render işlemini ana makinenizden izole eder ve ekran görüntüsünün ortamlar arasında tutarlı olmasını sağlar. Bu sırada, `setViewportSize` ile mantıksal ekran boyutlarını tanımlayabilirsiniz. Bu, bir fotoğraf çekmeden önce tarayıcı penceresini yeniden boyutlandırmaya eşdeğerdir.

```java
import com.aspose.html.*;

public class ScreenshotDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a sandbox with high‑resolution settings
        Sandbox renderingSandbox = new Sandbox();
        // Set the logical viewport to 1024×768 pixels – perfect for most desktop pages
        renderingSandbox.setViewportSize(1024, 768);
        // Optional: increase DPI for sharper output (useful for print‑ready PNGs)
        renderingSandbox.setDeviceDpi(300);
```

**set viewport size** neden önemlidir? Bir sayfayı 800×600 boyutunda render ederseniz, normalde o satırın altında görünecek tüm öğeler kırpılır. Viewport'u tasarım genişliğine eşleştirerek tüm düzeni tek seferde yakalarsınız.

## 2. Adım – Hedef sayfayı sandbox içinde yükleme

Sandbox hazır olduğuna göre, yakalamak istediğiniz URL'ye yönlendirin. Aspose.HTML HTML'yi alır, CSS'i işler, JavaScript'i çalıştırır ve gerçek bir tarayıcı gibi bir DOM oluşturur.

```java
        // 2️⃣ Load the web page you wish to screenshot
        // Replace the URL with any page you need to capture
        HtmlDocument webPage = new HtmlDocument("https://example.com", renderingSandbox);
```

> **Sayfa kimlik doğrulama gerektiriyorsa ne olur?**  
> Çerezleri veya özel başlıkları `HtmlDocument` yapıcısına geçirin. API, bir `RequestHeaders` nesnesi eklemenize izin verir—intranet siteleri için harika.

## 3. Adım – **convert html to image** ve **save webpage as png**

Belge tam olarak render edildikten sonra dönüşüm adımı basittir. `Converter` sınıfı rasterleştirmeyi yönetir ve `ImageConversionOptions` aracılığıyla çıktı seçeneklerini (piksel formatı, kalite vb.) ayarlayabilirsiniz.

```java
        // 3️⃣ Convert the rendered HTML to a PNG file
        ImageConversionOptions options = new ImageConversionOptions();
        // You can force a specific pixel format, e.g., PNG24 or PNG32
        options.setPixelFormat(PixelFormat.Format32bppArgb);
        // Perform the conversion
        Converter.convert(webPage, "output/screenshot.png", options);

        System.out.println("Screenshot saved to output/screenshot.png");
    }
}
```

Programı çalıştırdığınızda `output` klasöründe `screenshot.png` oluşturulur. Açtığınızda canlı sayfanın CSS stilleri, yazı tipleri ve hatta çalıştırılmış istemci‑tarafı scriptleriyle tam bir bitmap görüntüsünü göreceksiniz.

### Tam Çalışan Örnek

Aşağıda, kopyala‑yapıştır hazır tam kod bulunmaktadır. İçe aktarmalar, sandbox yapılandırması, sayfa yükleme ve dönüşüm içerir. Gizli parçalar yok, “belgelere bak” kısayolları da yok.

```java
import com.aspose.html.*;

public class ScreenshotDemo {
    public static void main(String[] args) throws Exception {
        // Create and configure the sandbox
        Sandbox renderingSandbox = new Sandbox();
        renderingSandbox.setViewportSize(1024, 768);
        renderingSandbox.setDeviceDpi(300);

        // Load the target URL
        HtmlDocument webPage = new HtmlDocument("https://example.com", renderingSandbox);

        // Set conversion options (optional but recommended for quality)
        ImageConversionOptions options = new ImageConversionOptions();
        options.setPixelFormat(PixelFormat.Format32bppArgb);

        // Convert to PNG and save
        Converter.convert(webPage, "output/screenshot.png", options);

        System.out.println("Screenshot saved to output/screenshot.png");
    }
}
```

**Beklenen çıktı:** Tam olarak 1024 × 768 piksel (veya viewport'un ötesine genişleyen sayfa düzeni varsa daha büyük) bir PNG dosyası. 300 DPI ayarı sayesinde görüntü net olacaktır.

## Yaygın Tuzaklar ve Kenar Durumları

| Durum | Neden Olur | Nasıl Düzeltilir |
|-----------|----------------|------------|
| **Boş görüntü** | Sandbox DPI'si ayarlanmamış veya sayfa yüklenmeyi tamamlamamış. | `webPage.waitForLoad()` metodunu dönüşümden önce çağırın veya `DeviceDpi` değerini artırın. |
| **Kırpılmış içerik** | Viewport, sayfa genişliğinden daha küçük. | Sayfanın tasarım genişliğine uygun boyutlarla `setViewportSize` kullanın. |
| **Eksik yazı tipleri** | Yazı tipi ana makinede yüklü değil. | CSS `@font-face` ile web fontlarını gömün veya gerekli fontları sunucuya kurun. |
| **Kimlik doğrulama gerekli** | Sayfa giriş sayfasına yönlendiriyor. | `HtmlLoadOptions` aracılığıyla çerezleri veya özel başlıkları sağlayın. |
| **Büyük sayfalar OOM hatasına neden oluyor** | Düşük bellekli ortamlarda çok büyük sayfaların render edilmesi. | Java heap boyutunu artırın (`-Xmx2g`) veya daha düşük DPI ile render edin. |

Bu ipuçları, hedef site basit bir statik sayfa olmasa bile **how to convert html** işlemini güvenilir bir şekilde yapmanıza yardımcı olur.

## Bonus: Tek Çalıştırmada Birden Fazla Sayfa Yakalama

Birden fazla ekran görüntüsü gerekiyorsa, URL listesi üzerinde döngü oluşturun. Sandbox yeniden kullanılabilir, bu da işleme süresini hızlandırır.

```java
String[] urls = {"https://example.com", "https://example.org/about", "https://example.net/contact"};
for (String url : urls) {
    HtmlDocument doc = new HtmlDocument(url, renderingSandbox);
    String fileName = "output/" + url.replaceAll("[^a-zA-Z0-9]", "_") + ".png";
    Converter.convert(doc, fileName, options);
    System.out.println("Saved: " + fileName);
}
```

## Sonuç

Artık Aspose.HTML for Java kullanarak herhangi bir web sayfasının **how to capture screenshot** işlemi için sağlam, uçtan uca bir çözümünüz var. **set viewport size**, **convert html to image** ve **save webpage as png** konularını birkaç kısa adımda ele aldık.  

Denemekten çekinmeyin: baskı kalitesinde varlıklar için DPI'yi değiştirin, dosya boyutu önemliyse PNG'yi JPEG ile değiştirin veya bu kodu otomatik UI regresyon testleri için bir CI boru hattına entegre edin.  

**how to convert html** hakkında başka ortamlarla ilgili sorularınız varsa ya da kimlik doğrulama ipuçlarıyla ilgili yardıma ihtiyacınız varsa, aşağıya bir yorum bırakın, iyi kodlamalar!  

![Aspose HTML Java kullanarak bir web sayfasının ekran görüntüsünü yakalama](https://example.com/assets/screenshot-demo.png "Aspose HTML Java kullanarak bir web sayfasının ekran görüntüsünü yakalama")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}