---
category: general
date: 2026-03-25
description: Aspose.HTML for Java ile sandbox kullanarak web sayfası ekran görüntüsü
  alma. HTML'yi PNG olarak kaydetmeyi, HTML'den görüntü dönüşümünü ve HTML'den PNG
  dönüşümünü dakikalar içinde öğrenin.
draft: false
keywords:
- how to use sandbox
- capture webpage screenshot
- save html as png
- html to image conversion
- html to png conversion
language: tr
og_description: Sandbox'ı kullanarak web sayfası ekran görüntüsü alma. Bu öğreticide
  HTML'yi PNG olarak kaydetme, HTML'den görüntü dönüşümü ve Aspose.HTML for Java ile
  HTML'den PNG dönüşümünü gösterir.
og_title: Sandbox'ı Kullanarak Web Sayfası Ekran Görüntüsü Nasıl Alınır
tags:
- Aspose.HTML
- Java
- Web Automation
title: Sandbox'ı Kullanarak Web Sayfasının Ekran Görüntüsünü Almak
url: /tr/java/conversion-html-to-various-image-formats/how-to-use-sandbox-to-capture-webpage-screenshot/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sandbox Kullanarak Web Sayfası Ekran Görüntüsü Alma

Sandbox kullanarak web sayfası ekran görüntüsü alma, duyarlı bir sayfanın piksel‑tam ön izlemesini gerektiğinde sıkça karşılaşılan bir gereksinimdir. Bu rehberde ayrıca Aspose.HTML for Java kullanarak **HTML’yi PNG olarak kaydetmeyi** gösterecek, *html to image conversion* ve *html to png conversion* süreçlerini tek, tekrarlanabilir bir örnekle ele alacağız.

Bir pazarlama açılış sayfasının telefonda, tablette ve masaüstünde farklı göründüğünü test ettiğinizi hayal edin. Üç ayrı tarayıcı açmak yerine bir sandbox oluşturup URL’ye yönlendirebilir ve gerçek bir cihazın render ettiğiyle aynı olan bir PNG elde edebilirsiniz. Bu öğreticinin sonunda, tam olarak bunu yapan çalıştırılabilir bir Java programına ve kendi projelerinizde yeniden kullanabileceğiniz birkaç pratik ipucuna sahip olacaksınız.

## Gerekenler

- **Aspose.HTML for Java** (v23.9 veya daha yeni). Kütüphane Maven Central üzerinden temin edilebilir, bu yüzden bağımlılığı eklemek çok kolay.
- Makinenizde **JDK 11+** yüklü.
- Tercih ettiğiniz bir IDE veya metin editörü (IntelliJ IDEA, VS Code, Eclipse… fark etmez).
- Örnek URL için internet erişimi (`https://example.com/responsive.html`) veya görüntüsünü almak istediğiniz herhangi bir sayfa.

Ek native ikili dosyalar veya headless tarayıcılar gerekmez—sandbox tamamen bellek içinde çalışır.

---

## Sandbox Kullanımı – Adım 1: Sanal Cihazı Tanımlama

İlk olarak sandbox’a hangi ekran boyutunu taklit etmesini istediğinizi söylemeniz gerekir. İşte bu aşamada anahtar kelime devreye girer: belirli bir viewport için *sandbox nasıl kullanılır*.

```java
// Step 1: Create a DeviceInfo that describes the virtual screen
DeviceInfo sandboxDevice = new DeviceInfo();
sandboxDevice.setWidth(800);               // width in pixels
sandboxDevice.setHeight(600);              // height in pixels
sandboxDevice.setDevicePixelRatio(1.0);    // 1 × for standard displays
sandboxDevice.setUserAgent("AsposeHTML/Java Sandbox");
```

**Neden önemli:**  
Genişlik ve yükseklik ayarlandığında, yerleşim motoru sayfayı 800×600 monitörde görüntüleniyormuş gibi işler. `devicePixelRatio` ise CSS‑tabanlı medya sorgularının (`@media (min‑device‑pixel‑ratio: ...)`) davranışını etkiler, böylece ekran görüntüsü gerçek dünyadaki deneyime uygun olur.

> **Pro tip:** Yüksek DPI bir ekran görüntüsü (Retina gibi) istiyorsanız `devicePixelRatio` değerini `2.0` yapın ve genişlik/yüksekliği buna göre artırın.

---

## Web Sayfası Ekran Görüntüsü Alma – Adım 2: Sayfayı Sandbox İçinde Yükleme

Şimdi Aspose.HTML’den uzaktaki HTML’yi alıp az önce tanımladığımız sandbox içinde render etmesini istiyoruz. Bu adım **capture webpage screenshot** işleminin kalbidir.

```java
// Step 2: Load the remote HTML page using the sandboxed environment
HTMLDocument document = new HTMLDocument(
        "https://example.com/responsive.html",
        new HTMLDocumentLoadOptions(new Sandbox(sandboxDevice)));
```

**Arka planda neler oluyor?**  
`HTMLDocumentLoadOptions`, `DeviceInfo` içeren bir `Sandbox` örneği alır. Kütüphane daha sonra viewport, user‑agent dizesi ve sayfanın çalıştırabileceği herhangi bir JavaScript’i göz önünde bulunduran headless bir render bağlamı oluşturur—*Chrome veya Firefox başlatmadan*.

Hedef sayfa kimlik doğrulama gerektiriyorsa, `HTMLDocumentLoadOptions` aracılığıyla çerezler veya özel başlıklar enjekte edebilirsiniz. Bu, intranet portalı gibi durumlarda kullanışlı bir kenar durumudur.

---

## HTML’yi PNG Olarak Kaydet – Adım 3: Render Edilen Belgeyi Görüntüye Dönüştürme

Sayfa render edildikten sonra son adım **HTML’yi PNG olarak kaydetmek**tir. Bu, gerçek *html to png conversion* adımıdır.

```java
// Step 3: Convert the rendered document to PNG and write it to disk
try (FileOutputStream out = new FileOutputStream("output/responsive_page.png")) {
    Converter.convertDocument(
            document,
            new ConversionOptions(ConversionFormat.PNG),
            out);
}
```

`Converter` tamamlandığında, `output` klasörü içinde `responsive_page.png` adlı bir dosya bulacaksınız. Açtığınızda, sayfanın 800×600 pikselde nasıl göründüğünü göreceksiniz—tarayıcı arayüzü, kaydırma çubukları yok, sadece saf render.

**Yaygın tuzaklar:**  
- **Dosya izin hataları:** Dizinin (`output/` örnekte) var olduğundan ve sürecin ona yazma iznine sahip olduğundan emin olun.  
- **Büyük sayfalar:** Çok uzun sayfalar devasa PNG dosyalarına yol açabilir; `DeviceInfo` içinde yüksekliği sınırlayabilir veya dönüşüm sonrası kırpma yapabilirsiniz.  
- **Dinamik içerik:** Sayfa, ilk yüklemeden sonra AJAX ile veri çekiyorsa, dönüşümden önce kısa bir gecikme (`Thread.sleep(2000)`) eklemeniz veya `HTMLDocumentLoadOptions.setWaitForResources(true)` kullanmanız gerekebilir.

---

### html to image conversion – Gelişmiş Seçenekler

Aspose.HTML, **html to image conversion** sürecini ince ayar yapmanız için çeşitli ayarlar sunar:

| Seçenek | Açıklama | Ne Zaman Kullanılır |
|--------|----------|---------------------|
| `ConversionOptions.setQuality(int)` | PNG sıkıştırma seviyesini (0‑100) ayarlar. | Web varlıkları için dosya boyutunu azaltmak. |
| `ConversionOptions.setBackgroundColor(Color)` | Arka plan rengini zorlar (varsayılan şeffaftır). | Sayfanın şeffaf bölümleri olduğunda faydalıdır. |
| `ConversionOptions.setPageSize(PageSize)` | Çıktı görüntüsü için sandbox boyutunu geçersiz kılar. | Farklı çözünürlükte küçük resimler oluşturmak. |

Aşağıda beyaz arka plan ve %90 kalite ayarlayan kısa bir snippet yer alıyor:

```java
ConversionOptions pngOptions = new ConversionOptions(ConversionFormat.PNG);
pngOptions.setBackgroundColor(java.awt.Color.WHITE);
pngOptions.setQuality(90);

try (FileOutputStream out = new FileOutputStream("output/white_bg_page.png")) {
    Converter.convertDocument(document, pngOptions, out);
}
```

---

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, `SandboxResponsiveExample.java` dosyasına kopyalayıp çalıştırabileceğiniz tam program aşağıdadır:

```java
import com.aspose.html.devices.DeviceInfo;
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.ConversionOptions;
import com.aspose.html.converters.ConversionFormat;
import com.aspose.html.render.HTMLDocument;
import com.aspose.html.render.HTMLDocumentLoadOptions;
import com.aspose.html.render.Sandbox;

import java.io.FileOutputStream;

public class SandboxResponsiveExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Define a sandbox with the desired viewport (800×600) and device pixel ratio
        DeviceInfo sandboxDevice = new DeviceInfo();
        sandboxDevice.setWidth(800);
        sandboxDevice.setHeight(600);
        sandboxDevice.setDevicePixelRatio(1.0);
        sandboxDevice.setUserAgent("AsposeHTML/Java Sandbox");

        // Step 2: Load the remote HTML page inside the sandboxed environment
        HTMLDocument document = new HTMLDocument(
                "https://example.com/responsive.html",
                new HTMLDocumentLoadOptions(new Sandbox(sandboxDevice)));

        // Step 3: Convert the document to PNG – the output reflects exactly how the page looks on the defined screen size
        try (FileOutputStream out = new FileOutputStream("output/responsive_page.png")) {
            Converter.convertDocument(
                    document,
                    new ConversionOptions(ConversionFormat.PNG),
                    out);
        }

        System.out.println("Screenshot saved to output/responsive_page.png");
    }
}
```

Programı çalıştırdığınızda bir onay satırı basılır ve PNG `output` klasörüne kaydedilir. Dosyayı açtığınızda, uzaktaki sayfanın belirttiğiniz tam boyutta sadık bir temsilini göreceksiniz.

---

## Sık Sorulan Sorular

**S: Yerel HTML dosyalarıyla da çalışır mı?**  
C: Kesinlikle. URL’yi `file://` URI’siyle değiştirin veya `HTMLDocument` yapıcısına bir `java.io.File` yolu geçin.

**S: PNG yerine PDF istersem ne yapmalıyım?**  
C: `ConversionFormat.PNG` yerine `ConversionFormat.PDF` kullanın. Kodun geri kalanı aynı kalır.

**S: Tam sayfa (kaydırmalı) ekran görüntüsü alabilir miyim?**  
C: Dönüşümden önce `DeviceInfo` yüksekliğini sayfanın kaydırma yüksekliğine (`document.getDocumentElement().getScrollHeight()`) ayarlayın veya tuvali genişletmek için `ConversionOptions.setPageSize` kullanın.

---

## Sonuç

Artık **sandbox nasıl kullanılır** sorusunun cevabını biliyorsunuz: bir web sayfasının ekran görüntüsünü alabilir, HTML’yi PNG olarak kaydedebilir ve Aspose.HTML for Java ile güvenilir html to image conversion gerçekleştirebilirsiniz. Yaklaşım hafif, tamamen programlanabilir ve geleneksel headless tarayıcıların getirdiği yükü ortadan kaldırıyor.

Sırada ne var? PNG çıktısını PDF’ye dönüştürmeyi deneyin, Retina ekranları taklit etmek için farklı device pixel ratio değerleriyle oynayın veya onlarca URL’nin toplu işlenmesini otomatikleştirin. Aynı sandbox tekniği, CI boru hatlarında, görsel regresyon testlerinde veya bir içerik yönetim sistemi için küçük resim üretiminde **html to png conversion** amacıyla da yeniden kullanılabilir.

Herhangi bir sorunla karşılaşırsanız yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}