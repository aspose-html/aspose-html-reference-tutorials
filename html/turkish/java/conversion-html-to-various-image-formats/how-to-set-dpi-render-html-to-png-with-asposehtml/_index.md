---
category: general
date: 2026-01-14
description: Bir URL'yi PNG'ye dönüştürürken DPI nasıl ayarlanır. HTML'yi PNG'ye render
  etmeyi, görünüm alanı boyutunu ayarlamayı ve Aspose.HTML'i Java'da kullanarak HTML'yi
  PNG olarak kaydetmeyi öğrenin.
draft: false
keywords:
- how to set dpi
- render html to png
- convert url to png
- set viewport size
- save html as png
language: tr
og_description: Bir URL'yi PNG'ye dönüştürürken DPI nasıl ayarlanır. HTML'yi PNG'ye
  render etme, görünüm alanı boyutunu kontrol etme ve Aspose.HTML kullanarak HTML'yi
  PNG olarak kaydetme adım adım rehberi.
og_title: dpi nasıl ayarlanır – AsposeHTML ile HTML'yi PNG'ye dönüştür
tags:
- AsposeHTML
- Java
- image rendering
title: dpi nasıl ayarlanır – AsposeHTML ile HTML'yi PNG'ye dönüştürme
url: /tr/java/conversion-html-to-various-image-formats/how-to-set-dpi-render-html-to-png-with-asposehtml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# dpi nasıl ayarlanır – AsposeHTML ile HTML'yi PNG'ye Render Etme

Web sayfasından oluşturulan ekran görüntüsü benzeri bir görüntünün **dpi nasıl ayarlanır** merak ettiniz mi? Belki baskı için 300 DPI PNG'ye, ya da mobil uygulama için düşük çözünürlüklü bir küçük resme ihtiyacınız var. Hangi durumda olursanız olun, püf noktası, render motoruna istediğiniz mantıksal DPI'yi söylemek ve ardından işin geri kalanını ona bırakmaktır.  

Bu öğreticide canlı bir URL alıp onu PNG dosyasına render edeceğiz, **görüntü alanı boyutunu ayarlayacağız**, DPI'yi değiştireceğiz ve sonunda **HTML'yi PNG olarak kaydedeceğiz**—hepsi Aspose.HTML for Java ile. Harici tarayıcılar yok, karmaşık komut satırı araçları yok—herhangi bir Maven ya da Gradle projesine ekleyebileceğiniz temiz Java kodu.

> **Pro ipucu:** Sadece hızlı bir küçük resim istiyorsanız DPI'yi 96 DPI (çoğu ekranın varsayılanı) olarak bırakabilirsiniz. Baskıya hazır varlıklar için DPI'yi 300 DPI ya da daha yüksek bir değere çıkarın.

![dpi ayarlama örneği](https://example.com/images/how-to-set-dpi.png "dpi ayarlama örneği")

## Gerekenler

- **Java 17** (veya daha yeni bir JDK).  
- **Aspose.HTML for Java** 24.10 veya daha yeni bir sürüm. Maven Central'dan alabilirsiniz:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.10</version>
</dependency>
```

- Hedef sayfayı indirmek için bir internet bağlantısı (örnek `httpsexample.com/sample.html` adresini kullanıyor).  
- Çıktı klasörüne yazma izni.

Hepsi bu—Selenium yok, headless Chrome yok. Aspose.HTML render işlemini süreç içinde yapar, yani JVM içinde kalırsınız ve bir tarayıcı başlatmanın getirdiği yükten kaçınırsınız.

## Adım 1 – URL'den HTML Belgesini Yükleme

İlk olarak yakalamak istediğimiz sayfayı işaret eden bir `HTMLDocument` örneği oluşturuyoruz. Yapıcı otomatik olarak HTML'i indirir, ayrıştırır ve DOM'u hazırlar.

```java
import com.aspose.html.HTMLDocument;
import java.nio.file.Paths;

// Load the remote page
HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");
```

*Bu neden önemli:* Belgeyi doğrudan yükleyerek ayrı bir HTTP istemcisine ihtiyaç duymamış olursunuz. Aspose.HTML yönlendirmeleri, çerezleri ve hatta URL içinde kimlik bilgileri gömülü ise temel kimlik doğrulamayı da destekler.

## Adım 2 – İstenen DPI ve Görüntü Alanı ile Sandbox Oluşturma

Bir **sandbox**, Aspose.HTML'in bir tarayıcı ortamını taklit etme şeklidir. Burada ona 1280 × 720 ekran olduğunu ve kritik olarak **cihaz DPI'sini** ayarladığımızı söylüyoruz. DPI'yi değiştirmek, mantıksal boyutu etkilemeden render edilen görüntünün piksel yoğunluğunu değiştirir.

```java
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;

// Create a sandbox that simulates a 1280×720 screen at 96 DPI
SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
        .setViewportSize(1280, 720)          // width, height in pixels
        .setDeviceDpi(96)                    // logical DPI (change to 300 for print)
        .setUserAgent("AsposeHTML/24.10")    // optional custom user‑agent
        .build();

// Apply the sandbox to the document
htmlDoc.setSandbox(sandbox);
```

*Bu değerleri neden ayarlayabilirsiniz:*  
- **Viewport size** CSS medya sorgularının (`@media (max-width: …)`) nasıl davranacağını kontrol eder.  
- **Device DPI** görüntünün baskı sırasında fiziksel boyutunu etkiler. 96 DPI bir görüntü ekranda iyi görünür; 300 DPI bir görüntü ise kağıtta keskinliğini korur.  

Kare bir küçük resme ihtiyacınız varsa sadece `setViewportSize(500, 500)` değiştirin ve DPI'yi düşük tutun.

## Adım 3 – Çıktı Formatı Olarak PNG Seçme

Aspose.HTML birkaç raster formatını destekler (PNG, JPEG, BMP, GIF). PNG kayıpsızdır, bu da her pikselin korunmasını istediğiniz ekran görüntüleri için mükemmeldir.

```java
import com.aspose.html.rendering.ImageSaveOptions;

// Prepare PNG save options
ImageSaveOptions pngOptions = new ImageSaveOptions();
pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);
```

Dosya boyutu konusunda endişeniz varsa sıkıştırma seviyesini (`pngOptions.setCompressionLevel(9)`) de ayarlayabilirsiniz.

## Adım 4 – Görüntüyü Render Et ve Kaydet

Şimdi belgeye kendisini bir görüntü olarak **kaydet**mesini söylüyoruz. `save` metodu bir dosya yolu ve önceden yapılandırılmış seçenekleri alır.

```java
// Define the output path (replace with your own directory)
String outputPath = "YOUR_DIRECTORY/sandboxed.png";

// Render the document to a PNG file
htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

System.out.println("Rendering completed.");
```

Program bittiğinde `YOUR_DIRECTORY/sandboxed.png` konumunda bir PNG dosyası bulacaksınız. Açın—DPI'yi 300 olarak ayarladıysanız, görüntü meta verileri bunu yansıtacak, piksel boyutları ise 1280 × 720 olarak kalacaktır.

## Adım 5 – DPI'yi Doğrulama (Opsiyonel ama Kullanışlı)

DPI'nin gerçekten uygulandığını iki kez kontrol etmek isterseniz, **metadata‑extractor** gibi hafif bir kütüphane ile PNG meta verilerini okuyabilirsiniz:

```java
import com.drew.imaging.ImageMetadataReader;
import com.drew.metadata.png.PngDirectory;

File pngFile = new File(outputPath);
var metadata = ImageMetadataReader.readMetadata(pngFile);
var pngDir = metadata.getFirstDirectoryOfType(PngDirectory.class);
int dpi = pngDir.getInt(PngDirectory.TAG_PIXELS_PER_UNIT_X);
System.out.println("DPI stored in PNG: " + dpi);
```

Konsolda `300` (veya ayarladığınız değer) yazdırıldığını görmelisiniz. Bu adım render için zorunlu değildir, ancak baskı iş akışı için varlıklar üretirken hızlı bir doğrulama sağlar.

## Yaygın Sorular ve Kenar Durumları

### “Sayfa içeriği yüklemek için JavaScript kullanıyorsa ne olur?”

Aspose.HTML **sınırlı bir alt küme** JavaScript çalıştırır. Çoğu statik site için kutudan çıkar çıkmaz çalışır. Sayfa, istemci tarafı framework'lerine (React, Angular, Vue) yoğun bir şekilde bağımlıysa, sayfayı önceden render etmeniz ya da bir headless tarayıcı kullanmanız gerekebilir. Ancak DOM hazır olduğunda DPI ayarı aynı şekilde çalışır.

### “PNG yerine PDF render edebilir miyim?”

Kesinlikle. `ImageSaveOptions` yerine `PdfSaveOptions` kullanın ve çıktı uzantısını `.pdf` olarak değiştirin. DPI ayarı, gömülü görüntülerin rasterleştirilmiş görünümünü hâlâ etkiler.

### “Retina ekranlar için yüksek çözünürlüklü ekran görüntüleri ne yapmalı?”

Viewport boyutlarını iki katına çıkarın ve DPI'yi 96 DPI tutun, ya da viewport'u aynı tutup DPI'yi 192'ye çıkarın. Ortaya çıkan PNG iki kat daha fazla piksel içerecek ve retina hissini sağlayacaktır.

### “Kaynakları temizlemem gerekiyor mu?”

`HTMLDocument` `AutoCloseable` uygular. Üretim uygulamasında bunu bir try‑with‑resources bloğuna sarın:

```java
try (HTMLDocument doc = new HTMLDocument(url)) {
    // configure sandbox, render, etc.
}
```

Bu, yerel kaynakların hızlı bir şekilde serbest bırakılmasını sağlar.

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda eksiksiz, çalıştırmaya hazır program yer alıyor. `YOUR_DIRECTORY` ifadesini makinenizdeki gerçek bir klasörle değiştirin.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.ImageSaveOptions;
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;
import java.nio.file.Paths;

public class RenderHtmlToPng {
    public static void main(String[] args) {
        // 1️⃣ Load the HTML document from a URL
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");

        // 2️⃣ Create a sandbox – set viewport size and DPI
        SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
                .setViewportSize(1280, 720)   // width × height in pixels
                .setDeviceDpi(96)             // change to 300 for print‑ready PNG
                .setUserAgent("AsposeHTML/24.10")
                .build();

        htmlDoc.setSandbox(sandbox); // apply sandbox to the document

        // 3️⃣ Prepare PNG save options
        ImageSaveOptions pngOptions = new ImageSaveOptions();
        pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);

        // 4️⃣ Render and save
        String outputPath = "YOUR_DIRECTORY/sandboxed.png";
        htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

        System.out.println("Rendering completed. Check: " + outputPath);
    }
}
```

Sınıfı çalıştırın, ve belirttiğiniz **dpi nasıl ayarlanır** ayarını koruyan bir PNG elde edeceksiniz.

## Sonuç

**dpi nasıl ayarlanır** konusunu **HTML'yi PNG'ye render ederken**, **görüntü alanı boyutunu ayarlama** adımını ele alarak ve Aspose.HTML for Java kullanarak **HTML'yi PNG olarak kaydetme** sürecini gösterdik. Özetle:

- DPI ve viewport kontrolü için bir **sandbox** kullanın.  
- Kayıpsız çıktı için doğru **ImageSaveOptions** seçin.  
- Baskı kalitesini garanti altına almak istiyorsanız DPI meta verisini doğrulayın.  

Buradan farklı DPI değerleri, daha büyük viewport'lar deneyebilir ya da URL listelerini toplu işleyebilirsiniz. Tüm bir web sitesini PNG küçük resimlerine dönüştürmek mi istiyorsunuz? URL dizisini döngüye alın ve aynı sandbox yapılandırmasını yeniden kullanın.

Keyifli renderlar, ve ekran görüntüleriniz her zaman piksel‑kusursuz olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}