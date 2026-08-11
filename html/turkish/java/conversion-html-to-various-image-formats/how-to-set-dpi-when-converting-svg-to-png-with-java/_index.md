---
category: general
date: 2026-02-14
description: Java kullanarak SVG'den PNG'ye dönüşümde DPI nasıl ayarlanır. Yüksek
  çözünürlüklü PNG dışa aktar, SVG'yi PNG'ye dönüştürmeyi öğren ve bir Java görüntü
  dönüşüm kütüphanesi kullan.
draft: false
keywords:
- how to set dpi
- convert svg to png
- export high resolution png
- how to convert svg
- java image conversion library
language: tr
og_description: Java kullanarak SVG'den PNG'ye dönüşüm için DPI nasıl ayarlanır. Bu
  kılavuz, yüksek çözünürlüklü PNG nasıl dışa aktarılacağını ve bir Java görüntü dönüştürme
  kütüphanesinin nasıl kullanılacağını gösterir.
og_title: Java ile SVG'yi PNG'ye Dönüştürürken DPI Nasıl Ayarlanır
tags:
- java
- image-conversion
- svg
- png
title: Java ile SVG'yi PNG'ye Dönüştürürken DPI Nasıl Ayarlanır
url: /tr/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-with-java/
---

terms unchanged.

Let's do it.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SVG'yi PNG'ye Java ile Dönüştürürken DPI Nasıl Ayarlanır

Bir SVG‑to‑PNG dönüşümünde sonucun baskıya hazır bir posterde net görünmesi için **DPI nasıl ayarlanır** diye hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok projede—pazarlama broşürleri, UI mock‑up'ları veya teknik diyagramlar gibi—SVG'den yüksek çözünürlüklü PNG elde etmek tartışmasız bir gerekliliktir.  

Bu öğreticide **SVG'yi PNG'ye dönüştürme**, **yüksek çözünürlüklü PNG dışa aktarma** adımlarını ve en önemlisi Aspose.HTML for Java kütüphanesini kullanarak DPI kontrolünü adım adım göstereceğiz. Sonunda, ister masaüstü aracı ister arka uç servisi geliştirin, herhangi bir Java uygulamasına ekleyebileceğiniz yeniden kullanılabilir bir kod parçacığına sahip olacaksınız.

## Gereksinimler

- **Java 8+** (kod, herhangi bir güncel JDK ile derlenebilir)
- **Aspose.HTML for Java** JAR'ları (Maven Central ya da Aspose web sitesinden temin edilebilir)
- Rasterleştirmek istediğiniz bir SVG dosyası  
- Bir tutam merak—başka bir şey gerekmez.

Maven kullanıyorsanız bir sonraki bölümde gösterilen bağımlılığı ekleyin; aksi takdirde JAR'ları manuel olarak indirip sınıf yolunuza ekleyin.

## Adım 1: Java Görüntü Dönüştürme Kütüphanesini Ekleyin

İlk olarak—projenizin **java image conversion library**'ye ihtiyacı var; bu kütüphane SVG'yi okuyup PNG'ye yazabilir. Aspose.HTML, CSS, font ve karmaşık vektör özelliklerini kutudan çıkar çıkmaz desteklediği için sağlam bir seçimdir.

**Maven kullanıcıları** aşağıdakini `pom.xml` dosyanıza yapıştırabilir:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- use the latest stable version -->
</dependency>
```

**Gradle kullanıcıları** ise şu satırı ekleyebilir:

```gradle
implementation 'com.aspose:aspose-html:23.12'
```

Manuel yolu tercih ediyorsanız, Aspose indirme sayfasından JAR'ı indirin ve `libs/` klasörüne koyun, ardından IDE'nizin derleme yoluna ekleyin.

> **Pro ipucu:** Sürüm numarasına dikkat edin; yeni sürümler genellikle DPI işleme iyileştirmeleri ve kenar‑durum hatalarını düzeltir.

## Adım 2: Dönüşüm Seçeneklerini Oluşturun ve İstenen DPI'yi Ayarlayın

Kütüphane artık projede olduğuna göre, çıktının PNG olarak nasıl görünmesi gerektiğini ona söylememiz gerekiyor. İşte **DPI nasıl ayarlanır** sorusunun devreye girdiği yer. `ImageConversionOptions` sınıfı, yatay (`dpiX`) ve dikey (`dpiY`) çözünürlük üzerinde ayrıntılı kontrol sağlar.

```java
import com.aspose.html.converters.ImageConversionOptions;

// Step 2: Build the options object and set DPI
ImageConversionOptions conversionOptions = new ImageConversionOptions();
conversionOptions.setDpiX(300); // 300 DPI horizontally
conversionOptions.setDpiY(300); // 300 DPI vertically
```

Neden 300 DPI? Çoğu baskı iş akışında 300 dots‑per‑inch “baskı kalitesi” olarak kabul edilir. Sadece web amaçlı varlıklar hedefliyorsanız, dosya boyutlarını hafif tutmak için bunu 72 veya 96 DPI'ye düşürebilirsiniz.

> **Farklı bir DPI değeri genişlik ve yükseklik için gerekirse ne yapmalıyım?**  
> `setDpiX` ve `setDpiY` değerlerini bağımsız olarak değiştirin. Kütüphane, eşit olmayan değerleri destekler; bu, anamorfik görüntüler için kullanışlıdır.

## Adım 3: SVG‑den PNG‑ye Dönüşümü Gerçekleştirin

Seçenekler hazır olduğunda, gerçek dönüşüm tek bir statik çağrı ile yapılır. Platform bağımsızlığı sağlamak için `java.nio.file.Paths` kullanacağız.

```java
import com.aspose.html.converters.Converter;
import java.nio.file.Paths;

public class SvgToPng {
    public static void main(String[] args) throws Exception {
        // Paths to input SVG and output PNG
        var inputSvg  = Paths.get("YOUR_DIRECTORY/input.svg").toUri();
        var outputPng = Paths.get("YOUR_DIRECTORY/output.png").toUri();

        // Convert using the DPI settings we defined earlier
        Converter.convert(inputSvg, outputPng, conversionOptions);
    }
}
```

Hepsi bu—`main` metodunu çalıştırın ve `YOUR_DIRECTORY` içinde net, 300 DPI bir PNG bulacaksınız. Kütüphane, belirttiğiniz DPI'ye göre vektör grafiği otomatik olarak ölçeklendirir, en boy oranını ve metin netliğini korur.

## Adım 4: Sonucu Doğrulayın (İsteğe Bağlı ama Tavsiye Edilir)

Hızlı bir tutarlılık kontrolü, ileride baş ağrısını önleyebilir. DPI meta verisini gösteren bir görüntü görüntüleyicide (ör. Photoshop, GIMP veya Windows Explorer’ın “Details” sekmesi) oluşturulan PNG'yi açın. Yatay ve dikey çözünürlük altında **300 DPI** görmelisiniz.

Dosya bulanıksa, şu noktaları kontrol edin:

1. Orijinal SVG zaten düşük çözünürlüklü değil mi? (Vektör dosyaları çözünürlükten bağımsızdır, ancak içindeki gömülü raster görüntüler kaliteyi sınırlayabilir.)  
2. DPI'yi ayarladıktan sonra dosyayı gerçekten kaydettiniz mi? IDE'ler bazen eski derlemeleri önbelleğe alabilir.  
3. Dönüşüm seçenekleri kodunuzun başka bir yerinde üzerine yazıldı mı?

## DPI Neden Önemlidir? (Yüksek Çözünürlüklü PNG Dışa Aktarma)

“DPI ile ne işim var? PNG zaten piksel değil mi?” diye sorabilirsiniz. Gerçekte DPI, aşağı akış uygulamalarına (özellikle baskı odaklı olanlara) bir inç fiziksel alana kaç piksel denk geldiğini söyleyen bir *metadata* etiketidir. 1200 × 800 bir PNG'yi DPI bilgisi olmadan bir yazıcıya verirseniz, yazıcı genellikle varsayılan (çoğunlukla 72 DPI) bir değeri kabul eder ve görüntüyü büyütür; bu da bulanık bir çıktı ile sonuçlanır.

DPI'yi doğru ayarlamak aynı zamanda bir performans avantajıdır: Daha sonra raster görüntüleri büyütme ihtiyacını ortadan kaldırır, bu da hem işlem gücünden tasarruf sağlar hem de kalite kaybını önler.

## Kenar Durumları ve Yaygın Tuzaklar

| Durum | Dikkat Edilmesi Gereken | Çözüm |
|-----------|-------------------|------------|
| **SVG içinde gömülü bitmap görüntüler** | Gömülü bitmap düşük çözünürlüklü olabilir, bu da yüksek DPI'de bile son PNG'nin pikselli görünmesine neden olur. | Bitmap'i daha yüksek çözünürlüklü bir versiyonla değiştirin veya SVG'yi harici bir görüntüye referans verecek şekilde düzenleyin. |
| **Çok yüksek DPI değerleri (ör. 1200 DPI)** | Bellek tüketimi artar; `OutOfMemoryError` alabilirsiniz. | JVM heap boyutunu artırın (`-Xmx2g`) veya DPI'yi kullanım senaryonuza uygun mantıklı bir maksimuma sınırlayın. |
| **Kare olmayan pikseller** | Bazı ekranlar DPI'yi farklı yorumlayarak görüntünün uzamasına yol açabilir. | `setDpiX` ile `setDpiY` değerlerini eşitleyin, aksi takdirde özel bir sebebiniz olmadıkça. |
| **Eksik fontlar** | SVG'deki metin, varsayılan bir fonta geri dönebilir ve düzen bozulur. | Fontları SVG'ye gömün veya çalışma zamanındaki makinede gerekli fontları kurun. |

## Tek Cümlelik Özet

SVG‑den PNG‑ye dönüşümde **DPI nasıl ayarlanır** sorusunun cevabı, bir `ImageConversionOptions` nesnesi oluşturup `dpiX`/`dpiY` değerlerini ayarlamak ve ardından Aspose.HTML Java kütüphanesinin `Converter.convert` metodunu çağırmaktır.

## Sonraki Adımlar ve İlgili Konular

- **Toplu işleme:** Bir klasördeki SVG dosyalarını döngüye alıp aynı DPI ayarlarını uygulayın.  
- **Dinamik DPI:** Çalışma zamanında bir yapılandırma dosyası ya da komut satırı argümanı okuyarak DPI'yi ayarlayın.  
- **Alternatif kütüphaneler:** Aspose kullanamıyorsanız **Batik** (Apache) veya **SVG Salamander** gibi seçenekleri değerlendirin; ancak DPI yönetimi için ekstra kod gerekebilir.  
- **Android varlıkları için yüksek çözünürlüklü PNG dışa aktarma:** Bu tekniği Android’in `drawable‑hdpi`, `xhdpi` vb. klasörleriyle birleştirin.

Denemeler yapmaktan çekinmeyin—web küçük resimleri için 72 DPI, büyük format baskılar için 600 DPI ya da orta bir çözünürlük için 150 DPI kullanabilirsiniz. Kod aynı kalır; sadece sayılar değişir.

---

![dpi ayarlama](placeholder-image.png "Java dönüşüm iş akışında DPI ayarlama illüstrasyonu")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}