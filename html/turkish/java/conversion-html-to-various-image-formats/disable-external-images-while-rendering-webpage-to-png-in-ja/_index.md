---
category: general
date: 2026-05-31
description: Aspose HTML kullanarak Java’da bir web sayfasını PNG’ye dönüştürürken
  harici görüntüleri devre dışı bırakın. Web sayfasını güvenli bir şekilde sandbox
  içinde yüklemeyi ve HTML belgesini PNG olarak kaydetmeyi öğrenin.
draft: false
keywords:
- disable external images
- render webpage to png
- load webpage in sandbox
- how to render html to image java
- save html document as png
language: tr
og_description: Java'da bir web sayfasını PNG olarak render ederken dış resimleri
  devre dışı bırakın. Bu adım adım rehber, bir web sayfasını sandbox içinde nasıl
  yükleyeceğinizi ve HTML belgesini PNG olarak nasıl kaydedeceğinizi gösterir.
og_title: Java'da Web Sayfasını PNG'ye Render Ederken Harici Görselleri Devre Dışı
  Bırak
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Disable external images when you render webpage to PNG in Java using
    Aspose HTML. Learn to load webpage in sandbox safely and save HTML document as
    PNG.
  headline: Disable External Images While Rendering Webpage to PNG in Java
  type: TechArticle
- questions:
  - answer: Yes. Inline `data:` URIs or base64‑encoded images are treated as part
      of the document and will appear in the PNG.
    question: Can I still display images that are bundled inside the HTML?
  - answer: The sandbox works as an all‑or‑nothing switch. For fine‑grained control,
      download the allowed images yourself, embed them as data URIs, and then render.
    question: What if I need to keep some external images but block others?
  - answer: Absolutely. Aspose.HTML is a pure‑Java library; it does not require a
      display server or browser engine.
    question: Does this approach work on headless servers?
  - answer: 'Selenium drives a real browser, which is heavyweight and harder to sandbox.
      Aspose.HTML renders HTML directly in memory, giving you deterministic performance
      and easier security controls like **disable external images**. --- ## Conclusion
      You now have a solid, end‑to‑end recipe for **disabling exter'
    question: How does this differ from using Selenium or Puppeteer?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- Image Rendering
title: Java'da Web Sayfasını PNG'ye Dönüştürürken Harici Görselleri Devre Dışı Bırak
url: /tr/java/conversion-html-to-various-image-formats/disable-external-images-while-rendering-webpage-to-png-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Web Sayfasını PNG Olarak Render Ederken Harici Görselleri Devre Dışı Bırakma Java’da

Hiç **harici görselleri devre dışı bırakmanız** gerektiğinde bir web sayfasını PNG’ye render ettiniz mi? Belki halka açık internetten izole bir thumbnail hizmeti oluşturuyorsunuzdur, ya da dönüşüm sırasında üçüncü‑taraf görsellerinin sızmasını kesin olarak önlemek istiyorsunuzdur. Hangi durumda olursanız olun, doğru yere geldiniz.

Bu öğreticide bir web sayfasını bir sandbox içinde yüklemeyi, harici görsel alımını kapatmayı ve sonunda HTML belgesini bir PNG dosyası olarak kaydetmeyi Aspose.HTML for Java ile adım adım göstereceğiz. Sonunda çalıştırmaya hazır bir örnek ve yaygın tuzaklardan kaçınmak için birkaç pratik ipucu elde edeceksiniz.

## Öğrenecekleriniz

- **HTML’yi Java’da görüntüye render etme** Aspose.HTML’in `Converter` sınıfı ile.
- **Sandbox içinde web sayfasını yükleme** için özel viewport ve DPI ayarları.
- Sayfayı render ederken **harici görselleri devre dışı bırakma** yapılandırması.
- **HTML belgesini PNG** (veya desteklenen diğer formatlarda) diske kaydetme.
- Kenar‑durumları yönetimi, performans ipuçları ve sorun giderme önerileri.

### Ön Koşullar

- Java 8 veya daha yeni bir sürüm yüklü (kod JDK 11+ ile de çalışır).
- Aspose.HTML for Java kütüphanesini çekmek için Maven veya Gradle.
- Java sözdizimi ve istisna yönetimi konusunda temel bilgi.
- İlk sayfa yüklemesi için bir internet bağlantısı (HTML’i yerel olarak sunmuyorsanız).

> **Pro tip:** Kurumsal bir proxy’nin arkasındaysanız, örneği çalıştırmadan önce JVM `http.proxyHost` ve `http.proxyPort` özelliklerini ayarlayın.

---

## Adım 1: Projenizi Kurun ve Aspose.HTML’i Ekleyin

İlk iş olarak Aspose.HTML bağımlılığını ekleyin. Maven kullanıyorsanız, `pom.xml` dosyanıza şunu ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Gradle için eşdeğeri:

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

Kütüphane sınıf yolunda olduğunda kodlamaya hazırsınız.

---

## Adım 2: **Harici Görselleri Devre Dışı Bırak** bir Sandbox Ortamı ile

Çözümün kalbi `DocumentSandbox`. *allowExternalImages* bayrağını `false` olarak geçirerek Aspose.HTML’e sandbox dışındaki URL’lere işaret eden `<img>` etiketlerini yok saymasını söylüyoruz. Bu, **harici görselleri devre dışı bırakmanın** tam mekanizmasıdır.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox that blocks external scripts and images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport size (width x height)
                96,                     // DPI – 96 is the screen default
                "MyApp/1.0",            // custom user‑agent string
                false,                  // allowExternalScripts = false
                false);                 // allowExternalImages = false  <-- disables external images
```

> **Neden önemli:** Sandbox olmadan renderlayıcı, sayfada referans verilen her görseli indirmeye çalışır; bu yavaş, güvenilir olmayan ve hatta bir güvenlik riski oluşturabilir. Bayrağı `false` yapmak, temiz ve kendi içinde tutarlı bir render geçişi garantiler.

---

## Adım 3: **Sandbox içinde Web Sayfasını Yükle**  

Şimdi Aspose.HTML’i yakalamak istediğimiz URL’ye yönlendiriyoruz. `HTMLDocument` yapıcı, az önce tanımladığımız kısıtlamaları otomatik olarak uygulayan sandbox örneğini kabul eder.

```java
        // 2️⃣ Load the target page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // replace with your target URL
                sandbox);
```

Sayfa, düzeni için dış script’lere çok bağımlıysa, script’leri de devre dışı bıraktığımız için eksik içerik görebilirsiniz. Bu durumda `allowExternalScripts` bayrağını `true` yapıp, `allowExternalImages` bayrağını `false` tutabilirsiniz.

---

## Adım 4: **Web Sayfasını PNG’ye Render Et**  

Belge yüklendikten sonra, `Converter.convert` kullanarak tek satırda bir görüntüye dönüştürülür. `ImageSaveOptions` nesnesi çıktı formatını seçmenizi sağlar; burada PNG seçiyoruz.

```java
        // 3️⃣ Render the document to a PNG image.
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png"; // ensure the folder exists

        Converter.convert(htmlDoc, saveOptions, outputPath);
        System.out.println("Image saved to: " + outputPath);
    }
}
```

Ortaya çıkan `sandboxed.png` dosyası, **herhangi bir harici görsel olmadan** sayfanın bir anlık görüntüsünü içerir—yalnızca satır içi SVG’ler veya base64‑kodlu grafikler kalır (varsa).

---

## Adım 5: Çıktıyı Doğrula ve Yaygın Sorunları Gider

Programı çalıştırdıktan sonra `sandboxed.png` dosyasını herhangi bir görüntü görüntüleyicide açın. Sayfa düzeni, metin ve CSS stillerini görmelisiniz, ancak tüm `<img src="http://…">` öğeleri boş (genellikle beyaz bir dikdörtgen olarak) ya da tamamen atlanmış olacaktır.

### Tipik sorunlar ve çözümleri

| Belirti | Muhtemel neden | Çözüm |
|---|---|---|
| Boş sayfa | Hedef URL isteği engelliyor (ör. Cloudflare) | Sandbox’ın user‑agent başlıklarını ekleyin veya bir proxy kullanın. |
| Eksik fontlar | Font dosyaları harici olarak barındırılıyor | Fontları yerel olarak kurun veya `@font-face` ile data URI olarak gömün. |
| Düzen kayması | CSS dış stil sayfalarına referans veriliyor ve bloklanıyor | CSS yüklemesi için sadece `allowExternalScripts`’i `true` yapın, ardından yeniden çalıştırın. |
| `java.lang.OutOfMemoryError` | Çok büyük bir sayfayı yüksek DPI’da renderlamak | Görüntü alanı boyutunu veya DPI’yı azaltın, ya da JVM heap’ini artırın (`-Xmx2g`). |

---

## Adım 6: Örneği Genişlet – Diğer Formatlarda Kaydet

Aynı kod JPEG, BMP ya da hatta PDF için de çalışır. Tek yapmanız gereken `SaveFormat` enum’unu değiştirmek:

```java
// Example: Save as JPEG with quality 80%
ImageSaveOptions jpegOptions = new ImageSaveOptions(SaveFormat.JPEG);
jpegOptions.setQuality(80);
Converter.convert(htmlDoc, jpegOptions, "output/sandboxed.jpg");
```

PDF ihtiyacınız varsa, `ImageSaveOptions` yerine `PdfSaveOptions` kullanın ve dosya uzantısını ona göre ayarlayın.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda **tam, çalıştırılabilir program** yer alıyor. Yeni bir Java sınıfı oluşturun, kodu yapıştırın, `output` klasörünün var olduğundan emin olun ve çalıştırın.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1 – Create a sandbox that disables external images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport width & height
                96,                     // DPI
                "MyApp/1.0",            // custom user‑agent
                false,                  // external scripts disabled
                false);                 // external images disabled (primary goal)

        // Step 2 – Load the page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // change to your URL
                sandbox);

        // Step 3 – Render to PNG.
        ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png";

        Converter.convert(htmlDoc, pngOptions, outputPath);
        System.out.println("PNG image saved to: " + outputPath);
    }
}
```

**Beklenen çıktı** (konsol):

```
PNG image saved to: output/sandboxed.png
```

`sandboxed.png` dosyasını açın – sayfanın **harici görseller olmadan** renderlandığını göreceksiniz.

---

## Sık Sorulan Sorular

**S: HTML içinde paketlenmiş görseller hâlâ gösterilebilir mi?**  
C: Evet. Satır içi `data:` URI’ları veya base64‑kodlu görseller belgeye dahil sayılır ve PNG’de görünür.

**S: Bazı harici görselleri tutup diğerlerini engellemek istiyorum, ne yapmalıyım?**  
C: Sandbox tamamen açık‑kapalı bir anahtardır. İnce ayar için izin verilen görselleri kendiniz indirin, data URI olarak gömün ve ardından renderlayın.

**S: Bu yöntem başsız (headless) sunucularda çalışır mı?**  
C: Kesinlikle. Aspose.HTML saf‑Java bir kütüphanedir; bir görüntü sunucusu ya da tarayıcı motoru gerektirmez.

**S: Selenium veya Puppeteer ile farkı nedir?**  
C: Selenium gerçek bir tarayıcıyı çalıştırır, bu da ağır ve sandbox’laması zor bir çözümdür. Aspose.HTML HTML’i doğrudan bellekte renderlar, belirli performans ve güvenlik kontrolleri (ör. **harici görselleri devre dışı bırakma**) sağlar.

---

## Sonuç

Artık **Java’da bir web sayfasını PNG’ye render ederken harici görselleri devre dışı bırakma** için sağlam, uçtan uca bir tarifiniz var. `DocumentSandbox` sayesinde dış kaynakların ne zaman izin verileceği üzerinde sıkı bir kontrol elde eder, güvenlik ve tekrarlanabilirliği sağlarsınız. Bundan sonra farklı viewport boyutları, DPI ayarları veya çıktı formatlarıyla deneyler yapabilir; her ayar size thumbnail, ön izleme ya da arşivleme anlık görüntüleri üretmek için yeni bir yol açar.

Bir sonraki meydan okumaya hazır mısınız? URL’leri paralel olarak batch halinde renderlayın ya da bu mantığı bir Spring Boot mikroservisine entegre edip talep üzerine PNG döndürün. Aspose.HTML’in esnekliği ile Java’nın eşzamanlılık araçlarını birleştirdiğinizde sınır yoktur.

Kodlamanın tadını çıkarın ve başarı hikayelerinizi yorumlarda paylaşmayı unutmayın!

## Sonraki Öğrenmeniz Gerekenler

- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [How to Render HTML to PNG with Aspose – Complete Guide](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)
- [How to Edit CSS - Advanced External CSS Editing with Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}