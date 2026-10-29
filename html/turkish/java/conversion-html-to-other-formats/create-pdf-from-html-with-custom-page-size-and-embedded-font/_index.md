---
category: general
date: 2026-03-05
description: Aspose.HTML kullanarak HTML'den hızlıca PDF oluşturun – özel bir PDF
  sayfa boyutu ayarlayın, yazı tiplerini gömün ve tam kodla HTML'yi PDF'ye nasıl dönüştüreceğinizi
  öğrenin.
draft: false
keywords:
- create pdf from html
- convert html to pdf
- html to pdf conversion
- custom pdf page size
- embed fonts pdf
language: tr
og_description: Aspose.HTML ile HTML'den PDF oluşturun. Bu kılavuz, özel bir PDF sayfa
  boyutu ayarlamayı, PDF'ye yazı tipleri eklemeyi ve HTML'den PDF'ye dönüşümü nasıl
  yapacağınızı gösterir.
og_title: HTML'den PDF Oluştur – Özel Sayfa Boyutu ve Gömülü Yazı Tipleri
tags:
- Java
- PDF
- Aspose.HTML
title: HTML'den Özel Sayfa Boyutu ve Gömülü Yazı Tipleriyle PDF Oluştur
url: /tr/java/conversion-html-to-other-formats/create-pdf-from-html-with-custom-page-size-and-embedded-font/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML'den PDF Oluşturma: Özel Sayfa Boyutu ve Gömülü Yazı Tipleri

Hiç **HTML'den PDF oluşturma** ihtiyacı hissettiniz mi ama stil aşamasında takıldınız mı? Tek başınıza değilsiniz. İster bir pazarlama açılış sayfasını basılabilir bir broşüre dönüştürmek, ister bir web uygulamasında oluşturulan faturaları arşivlemek isteyin, muhtemelen markanızın tam boyutlarına uyan ve tüm yazı tiplerinin keskin göründüğü bir PDF istiyorsunuz.  

Bu öğreticide, Aspose.HTML for Java kullanarak **HTML'yi PDF'ye dönüştürme**, **özel PDF sayfa boyutu** ayarlama ve **embed fonts PDF** özelliğini etkinleştirerek çıktının herhangi bir makinede aynı görünmesini sağlayan, tamamen çalışır bir örnek üzerinden adım adım ilerleyeceğiz. Sonunda projenize ekleyebileceğiniz tek bir Java sınıfına sahip olacaksınız ve anında PDF üretmeye başlayabileceksiniz.

## Öğrenecekleriniz

* Maven veya Gradle projesine Aspose.HTML kütüphanesini nasıl ekleyeceğiniz.  
* **PdfConversionOptions** ile **özel pdf sayfa boyutu** (bu örnekte 8.5 × 11 inç) nasıl yapılandırılır.  
* Hedef sistemde orijinal yazı tipleri bulunmasa bile metnin doğru render edilmesi için **embed fonts pdf** nasıl açılır.  
* **HTML'den PDF'ye dönüşümü** nasıl çalıştırır ve oluşan sayfa sayısını nasıl okursunuz.  

Süsleme yok, sadece kopyala‑yapıştır yapabileceğiniz pratik, uçtan uca bir çözüm.

## Ön Koşullar

Başlamadan önce şunların kurulu olduğundan emin olun:

* Java 17 veya daha yeni bir sürüm (API Java 8+ ile çalışır, ancak daha yeni JDK'lar daha iyi performans sağlar).  
* Maven ya da Gradle – Aspose.HTML JAR'ını Maven Central deposundan çekmek için bir yapı aracı.  
* PDF'ye dönüştürmek istediğiniz bir HTML dosyası (`sample.html`).  
* PDF sayfa düzeni hakkında biraz merak – bunu kod içinde ele alacağız.

> **Pro tip:** Eğer bir HTML dosyanız yoksa, sadece bir `<h1>` ve bir paragraf içeren basit bir dosya oluşturun; dönüşüm aynı şekilde çalışır.

## Adım 1: Aspose.HTML'i Projenize Ekleyin (Convert HTML to PDF)

**Maven** kullanıyorsanız, aşağıdaki bağımlılığı `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- latest at time of writing -->
</dependency>
```

**Gradle** için ise bu satırı `build.gradle` dosyanıza ekleyin:

```gradle
implementation 'com.aspose:aspose-html:23.12'
```

Bu tek satır, **html to pdf conversion** için ihtiyacınız olan her şeyi—`Converter`, seçenek sınıfları ve çizim yardımcılarını—sağlar.

## Adım 2: Özel PDF Sayfa Boyutu Ayarlayın (Custom PDF Page Size)

Kütüphane sınıf yolunda olduğuna göre çıktıyı şekillendirmeye başlayabiliriz. `PdfConversionOptions` nesnesi, sayfa boyutları, kenar boşlukları ve yazı tiplerinin gömülüp gömülmeyeceği gibi ayarları belirlemenizi sağlar. Aşağıdaki kod, her kenarda yarım inç kenar boşluğu ile 8.5 × 11 inç **custom pdf page size** ayarlar:

```java
// Step 2: Create PDF conversion options and configure page size, margins, and font embedding
PdfConversionOptions pdfOptions = new PdfConversionOptions();

// Set a custom PDF page size – 8.5 × 11 inches (Letter)
pdfOptions.setPageSize(new SizeF(Unit.inch(8.5), Unit.inch(11)));

// Margins are also expressed in inches; here we use 0.5 in on each side
pdfOptions.setMargins(0.5, 0.5, 0.5, 0.5); // left, top, right, bottom

// Enable font embedding so the PDF looks the same everywhere
pdfOptions.setEmbedFonts(true);
```

`setEmbedFonts(true)` çağrısına dikkat edin. Bu bayrak, Aspose.HTML'in **embed fonts PDF** dosyaları oluşturmasını sağlar ve farklı bir bilgisayarda PDF açtığınızda “yazı tipi eksik” sorununu ortadan kaldırır.

## Adım 3: HTML'den PDF'ye Dönüşümü Gerçekleştirin

Seçenekler hazır olduğunda, gerçek dönüşüm tek satırda yapılır. `Converter`'ı kaynak HTML dosyasına ve hedef PDF dosyasına yönlendirir, ardından az önce oluşturduğumuz seçenekleri veririz:

```java
// Step 3: Convert the HTML file to PDF using the configured options
String htmlPath = "YOUR_DIRECTORY/sample.html";
String pdfPath  = "YOUR_DIRECTORY/custom.pdf";

PdfConversionResult conversionResult = Converter.convertHTML(htmlPath, pdfPath, pdfOptions);
```

Her şey sorunsuz çalışırsa, `conversionResult` oluşturulan PDF hakkında, örneğin sayfa sayısı gibi meta verileri içerir.

## Adım 4: Çıktıyı Doğrulayın – Sayfa Sayısını Kontrol Edin

Dönüşümün başarılı olduğunu teyit etmek her zaman iyidir. `PdfConversionResult`, sayfa sayısını hızlıca okumanızı sağlar:

```java
// Step 4: Output the number of pages in the generated PDF
System.out.println("Custom PDF created, pages: " + conversionResult.getPageCount());
```

Programı çalıştırdığınızda aşağıdaki gibi bir çıktı görmelisiniz:

```
Custom PDF created, pages: 1
```

Bu satır, **html to pdf conversion** işleminin tek sayfalık bir PDF ürettiğini ve tanımladığınız **custom pdf page size** ile eşleştiğini gösterir. Kaynak HTML daha uzun ise, sayfa sayısı otomatik olarak artacaktır.

## Tam Çalışan Örnek

Aşağıda, `ConvertHtmlToPdfWithOptions.java` adlı bir dosyaya kopyalayabileceğiniz tam Java sınıfı yer alıyor. `YOUR_DIRECTORY` kısmını `sample.html` dosyanızın bulunduğu gerçek klasörle değiştirin.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.pdf.PdfConversionOptions;
import com.aspose.html.converters.pdf.PdfConversionResult;
import com.aspose.html.drawing.SizeF;
import com.aspose.html.drawing.Unit;

public class ConvertHtmlToPdfWithOptions {
    public static void main(String[] args) throws Exception {

        // Step 1: Create PDF conversion options and configure page size, margins, and font embedding
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setPageSize(new SizeF(Unit.inch(8.5), Unit.inch(11)));
        pdfOptions.setMargins(0.5, 0.5, 0.5, 0.5);   // left, top, right, bottom (in inches)
        pdfOptions.setEmbedFonts(true);            // embed fonts PDF for consistent rendering

        // Step 2: Convert the HTML file to PDF using the configured options
        String htmlPath = "YOUR_DIRECTORY/sample.html";
        String pdfPath  = "YOUR_DIRECTORY/custom.pdf";
        PdfConversionResult conversionResult = Converter.convertHTML(htmlPath, pdfPath, pdfOptions);

        // Step 3: Output the number of pages in the generated PDF
        System.out.println("Custom PDF created, pages: " + conversionResult.getPageCount());
    }
}
```

### Beklenen Sonuç

Sınıfı derleyip (`javac ConvertHtmlToPdfWithOptions.java`) çalıştırdıktan (`java ConvertHtmlToPdfWithOptions`) aynı klasörde `custom.pdf` dosyasını bulacaksınız. Herhangi bir PDF görüntüleyicide açtığınızda, **custom pdf page size** üzerinde tüm yazı tiplerinin doğru şekilde gömülmüş olduğunu göreceksiniz. Eksik karakter uyarısı, düzen kayması gibi bir sorun olmayacak.

![HTML'den PDF oluşturma örneği, oluşturulan PDF önizlemesi](/images/create-pdf-from-html-preview.png "html'den pdf önizleme")

## Sık Sorulan Sorular & Özel Durumlar

**HTML'im dış CSS veya resimlere referans veriyorsa ne olur?**  
Aspose.HTML, bir tarayıcı gibi aynı kuralları izler. Yollar mutlak ya da HTML dosyasının konumuna göre göreceli ise, dönüştürücü bunları çeker. Uzaktaki URL'ler için, dönüşümün gerçekleştiği makinenin internet erişimi olduğundan emin olun.

**Sayfa yönünü yatay (landscape) yapmak mümkün mü?**  
Elbette. `setPageSize` çağrısında genişlik ve yükseklik değerlerini değiştirmeniz yeterlidir:

```java
pdfOptions.setPageSize(new SizeF(Unit.inch(11), Unit.inch(8.5)));
```

**Üretim ortamında Aspose.HTML'i lisanslamam gerekiyor mu?**  
Kütüphane değerlendirme modunda çalışır, ancak PDF'e bir filigran ekler. Ticari projeler için geçerli bir lisans dosyasına ihtiyacınız var—programın başında şu şekilde yükleyin: `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`.

**Unicode yazı tipleriyle ne olacak?**  
HTML'inizde Latin dışı karakterler varsa, gömeceğiniz yazı tiplerinin bu kod noktalarını desteklediğinden emin olun. `setEmbedFonts(true)` tüm yazı tipi dosyasını gömer, böylece PDF herhangi bir cihazda Unicode karakterleri doğru şekilde render eder.

## Sonuç

Artık **HTML'den PDF oluşturma** sürecinde **custom pdf page size** kontrolünü nasıl sağlayacağınızı ve son belgenin **embed fonts PDF** özelliği sayesinde platformlar arası kusursuz render alacağını biliyorsunuz. Örnek, **html to pdf conversion** sürecinin tüm aşamalarını—bağımlılık kurulumundan seçenek yapılandırmasına, çıktının doğrulanmasına—kapsıyor.

Daha ileri gitmek ister misiniz? Şunları deneyin:

* Tek bir belgede **birden fazla sayfa boyutu** (her dönüşüm için farklı seçenekler).  
* Aspose.HTML'in `PdfPageSettings` sınıfını kullanarak **başlık/altbilgi şablonları**.  
* **Şifre koruması** gibi güvenlik özellikleri (`PdfEncryptionOptions`).  

Bu konular, az önce inşa ettiğimiz temelin üzerine kuruludur; böylece sorunsuz bir şekilde ilerleyebilirsiniz.

İyi kodlamalar ve web sayfalarınızı kusursuz biçimlendirilmiş PDF'lere dönüştürmenin tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}