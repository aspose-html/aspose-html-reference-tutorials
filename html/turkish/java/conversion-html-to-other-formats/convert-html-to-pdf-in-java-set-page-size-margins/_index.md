---
category: general
date: 2026-04-26
description: Aspose.HTML ile Java’da HTML’yi PDF’ye dönüştürün – PDF sayfa boyutunu
  nasıl ayarlayacağınızı, PDF kenar boşluklarını nasıl ekleyeceğinizi ve HTML’yi birkaç
  satırda PDF olarak dışa aktaracağınızı öğrenin.
draft: false
keywords:
- convert html to pdf
- set pdf page size
- add pdf margins
- export html as pdf
- how to set margins
language: tr
og_description: Aspose.HTML ile Java’da HTML’yi PDF’ye dönüştürün. Bu kılavuz, PDF
  sayfa boyutunu nasıl ayarlayacağınızı, PDF kenar boşluklarını nasıl ekleyeceğinizi
  ve HTML’yi hızlı bir şekilde PDF olarak dışa aktaracağınızı gösterir.
og_title: Java'da HTML'yi PDF'ye Dönüştür – Sayfa Boyutunu ve Kenar Boşluklarını Ayarla
tags:
- Java
- Aspose.HTML
- PDF conversion
title: Java'da HTML'yi PDF'ye Dönüştür – Sayfa Boyutu ve Kenar Boşluklarını Ayarla
url: /tr/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-set-page-size-margins/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML'yi Java’da PDF’ye Dönüştür – Sayfa Boyutu ve Kenar Boşluklarını Ayarla

**Java’da HTML'yi PDF’ye dönüştürmek** mi istiyorsunuz? **PDF sayfa boyutunu ayarlama** ya da **PDF kenar boşlukları ekleme** konusunda zorlanıyor musunuz? Yalnız değilsiniz. Birçok projede nihai PDF, kurumsal kimliğe uymalı ve bu da kesin sayfa ölçüleri ve düzenli kenar boşlukları anlamına geliyor.  

Bu öğreticide, Aspose.HTML kütüphanesini kullanarak **html'yi pdf olarak dışa aktaran** tam, çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz. Sonunda *kenar boşluklarını nasıl ayarlayacağınızı* ve PDF‑A‑1b uyumluluğunun arşivleme için neden bir cankurtaran olduğunu öğreneceksiniz. Belirsiz referanslar yok—kopyalayıp yapıştırıp çalıştırabileceğiniz kodlar var.

## Gereksinimler

- **Java 17** (veya herhangi bir güncel JDK) – API Java 8+ ile çalışır ancak yeni sürümler daha iyi performans sağlar.  
- **Aspose.HTML for Java** JAR dosyaları – bunları Maven Central deposundan ya da Aspose web sitesinden alabilirsiniz.  
- PDF’ye dönüştürmek istediğiniz basit bir **input.html** dosyası.  
- Çıktı dosyası için biraz disk alanı (PDF birkaç yüz kilobayt olacaktır).  

Hepsi bu. Ek bir framework, dış hizmet yok. Bu parçalar elinizdeyse, başlayabiliriz.

## HTML'yi PDF’ye Dönüştür – Adım‑Adım Genel Bakış

Aşağıda izleyeceğimiz yüksek‑seviye akış yer alıyor:

1. **HTML kaynağını belirtin** – yerel dosya, uzak URL ya da bir `InputStream`.  
2. **PDF kaydetme seçeneklerini yapılandırın** – sayfa boyutu, kenar boşlukları ve PDF‑A uyumluluğunu ayarlayın.  
3. **Dönüştürmeyi çalıştırın** – Aspose işi halleder.  

Bu adımlar kendi bölümlerinde ayrılmıştır, böylece ihtiyacınız olan kısımları seçip kullanabilirsiniz.

## Adım 1: HTML Kaynağını Belirtin

Dönüştürücünün ilk ihtiyacı, PDF’ye dönüştürmek istediğiniz HTML’e bir referans. Aspose.HTML esnek: bir yol, bir URL ya da HTML bellekte ise bir akış verebilirsiniz.

```java
// Step 1 – Define where the HTML comes from
String htmlPath = "YOUR_DIRECTORY/input.html"; // replace with your actual file
```

> **Neden önemli:** Basit bir dize kullanmak örneği sade tutar, ancak gerçek dünyada HTML’i bir web servisinden ya da veritabanından alabilirsiniz. API `java.net.URL` ya da `java.io.InputStream` kabul eder; bu da geçici bir dosya yazmak istemediğinizde işe yarar.

## Adım 2: PDF Sayfa Boyutunu Ayarlayın

Çoğu PDF varsayılan olarak **Letter** boyutundadır; izleyiciniz **A4** bekliyorsa bu garip görünebilir. Sayfa boyutunu `PdfSaveOptions` ile tek satırda değiştirebilirsiniz.

```java
// Step 2 – Create PDF options and set the page size to A4
PdfSaveOptions pdfOptions = new PdfSaveOptions();
pdfOptions.setPageSize(PdfPageSize.A4); // this is the “set pdf page size” step
```

> **İpucu:** Özel bir boyut (örneğin bir fiş formatı) gerekiyorsa, Aspose size tam genişlik ve yüksekliği puan cinsinden belirten bir `SizeF` nesnesi geçirmenize izin verir.

## Adım 3: PDF Kenar Boşluklarını Ekleyin

Kenar boşlukları, içeriğin sayfa kenarına yapışmasını önler. Puan cinsinden ölçülür (1 mm ≈ 2.8346 pt), ancak Aspose milimetreyi doğrudan kabul eden kullanışlı bir `Margin` sınıfı sunar.

```java
// Step 3 – Define 20 mm margins on all sides (how to set margins)
pdfOptions.setMargins(new Margin(20, 20, 20, 20));
```

> **Neden umursamalısınız:** Kenar boşlukları olmazsa, başlıklar yazdırıldığında kesilebilir ve altbilgiler yazıcının basılamayan alanına kayabilir. Tutarlı kenar boşlukları PDF’nin profesyonel görünmesini sağlar.

## Adım 4: PDF‑A‑1b Uyumluluğunu Etkinleştirin (Opsiyonel ama Tavsiye Edilir)

Belgeyi yasal ya da düzenleyici nedenlerle arşivliyorsanız, PDF‑A‑1b dosyanın kendine yeterli ve geleceğe dayanıklı olmasını sağlar.

```java
// Step 4 – Make the PDF archival‑ready
pdfOptions.setPdfACompliance(PdfACompliance.PdfA1b);
```

> **Kısa not:** PDF‑A uyumluluğu, fontların gömülmesi nedeniyle dosya boyutunu biraz artırabilir. Uzun vadeli okunabilirlik için ödenmesi gereken küçük bir bedeldir.

## Adım 5: Dönüştürmeyi Gerçekleştirin

Her şey yapılandırıldıktan sonra, gerçek dönüşüm tek bir statik çağrı ile yapılır. Aspose, render motoru, CSS, JavaScript (etkinleştirildiyse) ve resim gömme işlemlerini arka planda halleder.

```java
// Step 5 – Convert the HTML to PDF using the configured options
Converter.convertHtmlToPdf(htmlPath, "YOUR_DIRECTORY/output.pdf", pdfOptions);
```

İşte tüm program! Tüm parçacıkları bir araya koyduğunuzda çalıştırılabilir bir sınıf elde edersiniz.

## Tam Çalışan Örnek

Aşağıda `ConvertHtmlToPdfCustom.java` dosyasına kopyalayabileceğiniz eksiksiz Java programı yer alıyor. Yer tutucu yolları makinenizdeki gerçek konumlarla değiştirin.

```java
import com.aspose.html.*;
import com.aspose.html.converters.*;
import com.aspose.html.saving.*;

public class ConvertHtmlToPdfCustom {
    public static void main(String[] args) throws Exception {

        // Step 1: Specify the source HTML file (local file, URL, or stream)
        String htmlPath = "YOUR_DIRECTORY/input.html";

        // Step 2: Configure PDF output options
        //   • A4 page size
        //   • 20 mm margins on all sides
        //   • PDF‑A‑1b compliance for archival
        PdfSaveOptions pdfOptions = new PdfSaveOptions();
        pdfOptions.setPageSize(PdfPageSize.A4);
        pdfOptions.setMargins(new Margin(20, 20, 20, 20));
        pdfOptions.setPdfACompliance(PdfACompliance.PdfA1b);

        // Step 3: Convert the HTML to PDF using the configured options
        Converter.convertHtmlToPdf(htmlPath, "YOUR_DIRECTORY/output.pdf", pdfOptions);
    }
}
```

### Beklenen Sonuç

Programı çalıştırdığınızda `output.pdf` şu özelliklere sahip olur:

- **A4** (210 mm × 297 mm).  
- Sol, sağ, üst ve alt tarafta **20 mm** kenar boşlukları.  
- **PDF‑A‑1b** uyumlu, yani tüm fontlar gömülmüş ve dosya kendine yeterli.  
- `input.html` dosyasının düzenini eksiksiz yansıtır (görseller, tablolar ve CSS stilleri korunur).

PDF’yi herhangi bir görüntüleyicide (Adobe Acrobat, Foxit ya da Chrome) açabilirsiniz; içerik etrafında rahat bir beyaz kenarla temiz bir sayfa görmelisiniz.

![html'yi pdf'ye dönüştür çıktı önizlemesi](/images/convert-html-to-pdf.png)

*Şekil: Dönüştürmeden sonra oluşturulan PDF’ye hızlı bir bakış.*

## Yaygın Sorular ve Kenar Durumları

### HTML'im dış CSS ya da görseller içeriyorsa ne olur?

Aspose.HTML, tarayıcıların kullandığı aynı kuralları izler. URL’ler erişilebilir olduğu sürece (mutlak ya da HTML dosyasının klasörüne göre göreceli), dönüştürücü onları çeker. Kodunuzu internete erişimi olmayan bir sunucuda çalıştırıyorsanız, kaynakları **data‑URI** dizgileri olarak gömmeyi ya da bir `MemoryStream` içine önceden yüklemeyi düşünün.

### **URL** yerine bir **dosya** dönüştürmek istiyorum, nasıl yaparım?

`htmlPath` dizesini bir URL ile değiştirin:

```java
String htmlPath = "https://example.com/report.html";
```

Aynı `Converter.convertHtmlToPdf` aşırı yüklemesi sayfayı indirip render edecektir.

### Kenar boşluğu birimlerini inç ya da puan olarak değiştirebilir miyim?

Evet. `Margin` yapıcı ayrıca **puan** cinsinden `float left, float top, float right, float bottom` parametrelerini kabul eder. İnç tercih ediyorsanız, 72 ile çarpın (1 inç = 72 pt). Örneğin, 0.5 inç kenar boşluğu `new Margin(36, 36, 36, 36)` olur.

### **Farklı bir sayfa yönlendirmesi** (landscape) ihtiyacım var ise?

`setPageSize` çağrısından önce `PageOrientation` özelliğini ayarlayın:

```java
pdfOptions.setPageOrientation(PageOrientation.Landscape);
pdfOptions.setPageSize(PdfPageSize.A4);
```

### Otomatik **başlık/altbilgi** eklemenin bir yolu var mı?

Aspose.HTML, `PdfPageTemplate` sınıfı aracılığıyla başlık ya da altbilgi olarak davranan HTML parçacıkları enjekte etmenize izin verir. Küçük bir HTML fragmenti oluşturup `pdfOptions.getPageTemplate().setHeaderHtml(...)` (veya `.setFooterHtml(...)`) ile atarsınız. Bu kendi içinde ayrı bir konu, ancak temel çıkarım: başlık/altbilgileri normal HTML gibi ele alabilirsiniz.

## Üretim‑Hazır Kod İçin İpuçları

- **Kütüphaneyi lisanslayın** – ücretsiz

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}