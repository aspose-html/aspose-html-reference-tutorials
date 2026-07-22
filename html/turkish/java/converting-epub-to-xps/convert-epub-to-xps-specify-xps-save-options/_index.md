---
date: 2026-03-29
description: Aspose.HTML for Java'ı XPS kaydetme seçeneklerini belirtmek, EPUB'u XPS'ye
  dönüştürmek ve lisanslamayı yönetmek için nasıl kullanacağınızı öğrenin.
linktitle: Specifying XPS Save Options for EPUB to XPS
second_title: Java HTML Processing with Aspose.HTML
title: Aspose HTML Kaydetme Seçeneklerini EPUB'tan XPS'ye Nasıl Kullanılır
url: /tr/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# EPUB'tan XPS'ye Aspose HTML Kaydetme Seçeneklerini Nasıl Kullanılır

Bu rehberde **how to use Aspose** HTML Kaydetme Seçeneklerini kullanarak bir EPUB belgesini XPS'ye dönüştürmeyi, sayfa boyutları, arka plan rengi ve lisanslama hususları üzerinde tam kontrol sağlamayı göstereceğiz. İster toplu‑işleme hattı ister tek seferlik bir dönüşüm aracı oluşturuyor olun, bu adımlar güvenilir sonuçları hızlı bir şekilde almanıza yardımcı olacaktır.

## Hızlı Yanıtlar
- **Aspose HTML Kaydetme Seçenekleri ne yapar?** XPS gibi formatlara kaydederken sayfa boyutunu, arka plan rengini ve diğer render ayarlarını özelleştirmenizi sağlar.  
- **Hangi kütüphane gereklidir?** Aspose.HTML for Java (en son sürüm).  
- **Bir lisansa ihtiyacım var mı?** Değerlendirme için ücretsiz deneme sürümü çalışır; üretim için ticari bir lisans gereklidir.  
- **Sayfa boyutlarını değiştirebilir miyim?** Evet – `PageSetup` aracılığıyla istediğiniz genişlik ve yüksekliği ayarlayabilirsiniz.  
- **Dönüşüm hızlı mı?** Tipik EPUB dosyaları için dönüşüm modern bir JVM'de saniyeler içinde tamamlanır.

## Bu Bağlamda “how to use aspose” Ne Anlama Geliyor?
“**how to use Aspose**” ifadesi, Aspose.HTML kütüphanesini web‑tabanlı belgeleri manipüle etmek ve dönüştürmek için kullanmanın pratik adımlarını ifade eder. Bu öğreticide, **aspose html save options** üzerine odaklanıyoruz; bu seçenekler **convert EPUB to XPS**'i yaparken çıktıyı ince ayar yapmanıza olanak tanır.

## Neden Aspose.HTML for Java'i EPUB'tan XPS'ye Dönüştürmek İçin Kullanmalısınız?
- **Yüksek doğruluk** – karmaşık düzenleri, yazı tiplerini ve vektör grafikleri korur.  
- **Programatik kontrol** – Java uygulamaları içinde toplu dönüşümleri otomatikleştirir.  
- **Harici bağımlılık yok** – saf Java kütüphanesi, yerel bileşen yok.  
- **Özelleştirilebilir çıktı** – kaydetme seçenekleri sayesinde XPS'yi tam ihtiyaçlarınıza göre şekillendirebilirsiniz; örneğin **sayfa boyutlarını belirtmek** veya özel bir arka plan ayarlamak gibi.  

## Ön Koşullar

Koda geçmeden önce aşağıdakilere sahip olduğunuzdan emin olun:

1. **Java Geliştirme Ortamı** – JDK 8 veya daha yüksek bir sürüm yüklü.  
2. **Aspose.HTML for Java Kütüphanesi** – bunu [download link](https://releases.aspose.com/html/java/) adresinden indirin.  
3. **EPUB Dosyası** – **convert EPUB to XPS** yapmak istediğiniz kaynak EPUB.  

Bu gereksinimler hazır olduğunda adımları kesintisiz takip edebilirsiniz.

## Paketleri İçe Aktar

İlk olarak, gerekli sınıfları içe aktarın. İçe aktarmaları Java kaynak dosyanızın en üstüne yerleştirin:

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

Bu içe aktarmalar, dönüşüm motoruna ve ince ayar için gereken **Aspose HTML Save Options**'a erişim sağlar.

## EPUB Dosyasını Aç

Sonra, dönüştürmek istediğiniz EPUB dosyasını açın. `Resources.input` yardımcı işlevi, demo kaynak klasöründen bir dosya yükler:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    // Your code for the EPUB file handling goes here.
}
```

Bir try‑with‑resources bloğu kullanmak, akışın otomatik olarak kapatılmasını sağlar.

## XPS Kaydetme Seçeneklerini Oluştur (Sayfa Boyutu ve Arka Planı Yapılandır)

Şimdi bir `XpsSaveOptions` örneği oluşturup özelleştiriyoruz. **save options**'ın gerçekten parladığı yer burası:

```java
XpsSaveOptions options = new XpsSaveOptions();
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
anyPage.setSize(new Size(Length.fromPixels(3000), Length.fromPixels(1000)));
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **Sayfa boyutu** – bu örnekte 3000 × 1000 piksel olarak ayarlanmıştır; hedef kağıt boyutunuza göre ayarlayın veya inç cinsinden **sayfa boyutlarını belirtmek** için `Length.fromInches` kullanın.  
- **Arka plan rengi** – `AliceBlue`, tuval arka planını nasıl değiştireceğinizi gösterir; istediğiniz herhangi bir `Color` seçebilirsiniz.  

Bu ayarlar, final XPS belgesini etkileyen **aspose html save options**'ın bir parçasıdır.

## EPUB'u XPS'ye Dönüştür

Son olarak, dönüştürücüyü akış, yapılandırılmış seçenekler ve bir çıktı yolu ile çağırın:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

Bu satır çalıştığında, Aspose.HTML EPUB'u okur, tanımladığınız sayfa ayarını ve arka plan rengini uygular ve tam uyumlu bir XPS dosyası yazar.

## Yaygın Sorunlar ve İpuçları

- **Yanlış sayfa boyutları** – boyutların piksel cinsinden ifade edildiğinden emin olun (veya `Length.fromInches` kullanın).  
- **Eksik yazı tipleri** – gerekli yazı tiplerini EPUB içinde gömün veya geri dönüşümden kaçınmak için JVM ana bilgisayarına kurun.  
- **Büyük dosyalar** – çok büyük EPUB'lar için JVM yığınını (`-Xmx`) artırarak **OutOfMemoryError** oluşmasını önleyin.  
- **Aspose HTML lisanslaması** – dönüşümden önce geçerli bir lisans yüklendiğinden emin olun; aksi takdirde deneme filigranı görünecektir.

## Sonuç

**Aspose HTML Save Options**'ı kullanarak, bir EPUB'un XPS'ye nasıl render edildiği üzerinde kesin kontrol elde edersiniz. Yukarıdaki adımlar, **how to convert EPUB**'i nasıl yapacağınızı, **sayfa boyutlarını** ayarlamayı, arka planı değiştirmeyi ve dönüşümü sadece birkaç Java kod satırıyla gerçekleştirmeyi gösterir. Bu deseni toplu işleme hatlarınıza entegre ederek yayın görevlerini verimli bir şekilde otomatikleştirebilirsiniz.

## Sıkça Sorulan Sorular

**Q: Aspose.HTML for Java nedir?**  
A: Geliştiricilerin bir tarayıcıya ihtiyaç duymadan HTML, EPUB ve diğer web‑tabanlı belgeleri oluşturmasını, düzenlemesini, render etmesini ve dönüştürmesini sağlayan bir Java kütüphanesidir.

**Q: Bunu ticari bir projede kullanabilir miyim?**  
A: Evet. Üretim ortamında kullanmak için geçerli bir lisansa ihtiyacınız var. Lisansı [purchase page](https://purchase.aspose.com/buy) adresinden satın alabilirsiniz.

**Q: Ücretsiz bir deneme sürümü mevcut mu?**  
A: Kesinlikle. [here](https://releases.aspose.com/) adresinden bir deneme sürümü indirebilirsiniz.

**Q: Destek nereden alabilirim?**  
A: Aspose forumları üzerinden topluluk desteği ve resmi yardım [https://forum.aspose.com/](https://forum.aspose.com/) adresinde mevcuttur.

**Q: Sistem gereksinimleri nelerdir?**  
A: Java Development Kit (JDK) 8+ ve Aspose çalışma zamanı tarafından desteklenen bir işletim sistemi. Ortamınızın daha önce listelenen ön koşulları karşıladığından emin olun.

---

**Son Güncelleme:** 2026-03-29  
**Test Edilen Versiyon:** Aspose.HTML for Java 24.12  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}