---
date: 2026-01-09
description: Aspose.HTML for Java'ı kullanarak XPS kaydetme seçeneklerini nasıl belirleyeceğinizi
  ve EPUB'u verimli bir şekilde XPS'ye dönüştüreceğinizi öğrenin.
linktitle: Specifying XPS Save Options for EPUB to XPS
second_title: Java HTML Processing with Aspose.HTML
title: EPUB'tan XPS'ye Dönüştürme için Aspose HTML Kaydetme Seçeneklerini Belirleme
url: /tr/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# EPUB'tan XPS'ye Aspose HTML Kaydetme Seçeneklerini Belirleme

EPUB belgesini XPS'ye dönüştürmek, yayın akışının kullanışlı bir parçası olabilir ve **Aspose HTML Kaydetme Seçenekleri**, çıktıyı ince ayarlarla kontrol etmenizi sağlar. Bu öğreticide, Aspose.HTML for Java ile bu kaydetme seçeneklerini yapılandırmak ve yüksek kaliteli bir XPS dosyası üretmek için gereken adımları adım adım göstereceğiz.

## Hızlı Yanıtlar
- **Aspose HTML Kaydetme Seçenekleri ne işe yarar?** XPS gibi formatlara kaydederken sayfa boyutu, arka plan rengi ve diğer render ayarlarını özelleştirmenizi sağlar.  
- **Hangi kütüphane gereklidir?** Aspose.HTML for Java (en son sürüm).  
- **Lisans gerekir mi?** Değerlendirme için ücretsiz deneme sürümü çalışır; üretim için ticari bir lisans gereklidir.  
- **Sayfa boyutlarını değiştirebilir miyim?** Evet – `PageSetup` aracılığıyla istediğiniz genişlik ve yüksekliği ayarlayabilirsiniz.  
- **Dönüşüm hızlı mı?** Tipik EPUB dosyaları için dönüşüm, modern bir JVM üzerinde saniyeler içinde tamamlanır.

## Aspose HTML Kaydetme Seçenekleri Nedir?
Aspose HTML Kaydetme Seçenekleri, HTML, EPUB veya diğer web‑tabanlı belgelerin XPS, PDF veya görüntü dosyaları gibi hedef formatlara nasıl render edilip kaydedileceğini kontrol eden bir dizi özelliktir. Sayfa düzeni, arka plan renkleri, kenar boşlukları ve daha fazlasını tanımlamanıza olanak tanır; böylece ortaya çıkan dosya tasarım gereksinimlerinize tam olarak uyar.

## Neden Aspose.HTML for Java'ı EPUB'tan XPS'ye Dönüştürmek İçin Kullanmalısınız?
- **Yüksek doğruluk** – karmaşık düzenleri, yazı tiplerini ve vektör grafiklerini korur.  
- **Programatik kontrol** – Java uygulamaları içinde toplu dönüşümleri otomatikleştirin.  
- **Harici bağımlılık yok** – saf Java kütüphanesi, yerel bileşen gerektirmez.  
- **Özelleştirilebilir çıktı** – kaydetme seçenekleri sayesinde XPS'yi tam ihtiyacınıza göre şekillendirebilirsiniz.

## Önkoşullar

Kodlara geçmeden önce aşağıdakilerin kurulu olduğundan emin olun:

1. **Java Geliştirme Ortamı** – JDK 8 veya üzeri yüklü.  
2. **Aspose.HTML for Java Kütüphanesi** – [indirme bağlantısı](https://releases.aspose.com/html/java/) üzerinden indirin.  
3. **EPUB Dosyası** – dönüştürmek istediğiniz kaynak EPUB.

Bu öğeler hazır olduğunda adımları kesintisiz takip edebilirsiniz.

## Paketleri İçe Aktarın

İlk olarak gerekli sınıfları içe aktarın. İçe aktarmaları Java kaynak dosyanızın en üstüne yerleştirin:

```java
import java.io.FileInputStream;
import com.aspose.html.saving.XpsSaveOptions;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.drawing.Page;
import com.aspose.html.drawing.Size;
import com.aspose.html.drawing.Length;
import com.aspose.html.drawing.Color;
import com.aspose.html.converters.Converter;
import com.aspose.html.system.io.resources.Resources;
```

Bu importlar, dönüşüm motoruna ve ince ayar için gereken **Aspose HTML Kaydetme Seçenekleri**ne erişim sağlar.

## EPUB Dosyasını Açın

Sonra dönüştürmek istediğiniz EPUB dosyasını açın. `Resources.input` yardımcı metodu, demo kaynak klasöründen bir dosya yükler:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    // Your code for the EPUB file handling goes here.
}
```

`try‑with‑resources` bloğu, akışın otomatik olarak kapanmasını sağlar.

## XPS Kaydetme Seçeneklerini Oluşturun (Sayfa Boyutu ve Arka Planı Yapılandırma)

Şimdi bir `XpsSaveOptions` örneği oluşturup özelleştireceğiz. **Kaydetme seçenekleri** burada devreye girer:

```java
XpsSaveOptions options = new XpsSaveOptions();
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
anyPage.setSize(new Size(Length.fromPixels(3000), Length.fromPixels(1000)));
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **Sayfa boyutu** – bu örnekte 3000 × 1000 piksel olarak ayarlanmıştır; hedef kağıt boyutunuza göre ayarlayın.  
- **Arka plan rengi** – `AliceBlue`, tuval arka planını nasıl değiştirebileceğinizi gösterir; istediğiniz herhangi bir `Color` seçebilirsiniz.  

Bu ayarlar, nihai XPS belgesini etkileyen **Aspose HTML Kaydetme Seçenekleri**nin bir parçasıdır.

## EPUB'u XPS'ye Dönüştürün

Son olarak, akışı, yapılandırılmış seçenekleri ve çıktı yolunu belirterek dönüştürücüyü çalıştırın:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

Bu satır çalıştığında, Aspose.HTML EPUB'u okur, tanımladığınız sayfa ayarları ve arka plan rengini uygular ve tam uyumlu bir XPS dosyası yazar.

## Yaygın Sorunlar ve İpuçları

- **Yanlış sayfa boyutları** – boyutların piksel cinsinden (veya `Length.fromInches` kullanarak) ifade edildiğinden emin olun.  
- **Eksik yazı tipleri** – EPUB içinde gerekli yazı tiplerini gömün veya JVM ana bilgisayarına kurun; aksi takdirde yedek yazı tipine geçilir.  
- **Büyük dosyalar** – çok büyük EPUB'lar için JVM yığın alanını (`-Xmx`) artırarak `OutOfMemoryError` hatasını önleyin.  

## Sonuç

**Aspose HTML Kaydetme Seçenekleri**ni kullanarak, bir EPUB'un XPS'ye nasıl render edildiği üzerinde kesin kontrol elde edersiniz. Yukarıdaki adımlar, sayfa boyutu, arka plan rengi ayarlamayı ve sadece birkaç satır Java kodu ile dönüşümü nasıl gerçekleştireceğinizi gösterir. Bu deseni toplu işleme hatlarınızda kullanarak yayın görevlerini verimli bir şekilde otomatikleştirin.

## Sıkça Sorulan Sorular

**S: Aspose.HTML for Java nedir?**  
C: Geliştiricilerin tarayıcı gerektirmeden HTML, EPUB ve diğer web‑tabanlı belgeleri oluşturmasını, düzenlemesini, render etmesini ve dönüştürmesini sağlayan bir Java kütüphanesidir.

**S: Bunu ticari bir projede kullanabilir miyim?**  
C: Evet. Üretim ortamında geçerli bir lisansa ihtiyacınız vardır. Lisansı [satın alma sayfası](https://purchase.aspose.com/buy) üzerinden temin edebilirsiniz.

**S: Ücretsiz bir deneme sürümü mevcut mu?**  
C: Kesinlikle. [buradan](https://releases.aspose.com/) bir deneme sürümü indirebilirsiniz.

**S: Destek nereden alınır?**  
C: Aspose forumları üzerinden topluluk desteği ve resmi yardım [https://forum.aspose.com/](https://forum.aspose.com/) adresinde mevcuttur.

**S: Sistem gereksinimleri nelerdir?**  
C: Java Development Kit (JDK) 8+ ve Aspose çalışma zamanının desteklediği bir işletim sistemi. Önceden listelenen önkoşulları karşıladığınızdan emin olun.

---

**Son Güncelleme:** 2026-01-09  
**Test Edilen Versiyon:** Aspose.HTML for Java 24.12  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}