---
category: general
date: 2026-03-26
description: Aspose.HTML for Java kullanarak HTML'den özel boyutlu PDF oluşturun.
  HTML'yi PDF'ye dönüştürmeyi ve PDF sayfa boyutunu sadece birkaç adımda ayarlamayı
  öğrenin.
draft: false
keywords:
- create pdf custom size
- convert html to pdf
- change pdf page size
- generate pdf from html
- set pdf page size
language: tr
og_description: Aspose ile HTML'den özel boyutta PDF oluşturun. Bu kılavuz, HTML'yi
  PDF'ye dönüştürmeyi, PDF sayfa boyutunu değiştirmeyi ve PDF sayfa boyutunu zahmetsizce
  ayarlamayı gösterir.
og_title: PDF Özel Boyut Oluştur – HTML'yi PDF'ye Dönüştürme Hızlı Rehberi
tags:
- aspose
- java
- pdf
- html
title: Özel Boyutta PDF Oluştur – Aspose ile HTML'yi PDF'ye Dönüştür
url: /tr/java/conversion-html-to-other-formats/create-pdf-custom-size-convert-html-to-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF Özel Boyut Oluşturma – HTML'yi Aspose ile PDF'ye Dönüştürme

Hiç **HTML dosyasından PDF özel boyut** oluşturmanız gerekti mi? Bu öğreticide **HTML'yi PDF'ye dönüştürme** ve PDF sayfa boyutunu Aspose.HTML for Java kullanarak ayarlama adımlarını göstereceğiz.  

Faturalar, raporlar veya e‑kitaplar oluşturuyorsanız, tam sayfa boyutları çok önemlidir—aksi takdirde düzeniniz ortalanmamış ya da kesilmiş görünür.  

Kaynak HTML'yi yüklemekten kenar boşluklarını ayarlamaya kadar her adımı adım adım anlatacağız ve sonunda kullanıma hazır bir PDF elde edeceksiniz. Belirsiz referanslar yok, sadece bugün kopyalayıp yapıştırabileceğiniz tam, çalıştırılabilir bir örnek.

## Gereksinimler

- **Java 17** (veya herhangi bir güncel JDK).  
- **Aspose.HTML for Java** JAR'ları – en son sürümü Maven deposundan ya da Aspose web sitesinden alabilirsiniz.  
- Kontrol ettiğiniz bir klasörde bulunan basit bir `input.html` dosyası.  
- Tercih ettiğiniz bir IDE veya metin düzenleyici; ben genellikle IntelliJ IDEA kullanıyorum, Eclipse de gayet iyi çalışır.

Bu ön koşullara sahip olmak, “class not found” hatalarıyla yarı yolda takılmamanızı sağlar.  

Şimdi başlayalım.

![PDF özel boyut oluşturma örneği](/images/create-pdf-custom-size.png "Özel sayfa boyutu ve kenar boşluklarıyla oluşturulmuş bir PDF'nin ekran görüntüsü – pdf özel boyut oluşturma")

## PDF Özel Boyut Oluşturma – Temel Adımlar

Aşağıda elde edeceğiniz tam Java programı yer alıyor. `ConvertHtmlToPdfCustomPage.java` adlı bir dosyaya kopyalayıp, proje bağımlılıklarını ekledikten sonra çalıştırabilirsiniz.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.PdfConversionOptions;
import com.aspose.html.saving.PageSize;
import com.aspose.html.saving.Margin;

public class ConvertHtmlToPdfCustomPage {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the source HTML document
        HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/input.html");

        // Step 2: Set up PDF conversion options
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setPageSize(PageSize.A4); // Choose page size (A4, Letter, etc.)
        pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Portrait); // Portrait or Landscape
        pdfOptions.setMargins(new Margin(20, 20, 20, 20)); // Margins: left, top, right, bottom (points)

        // Step 3: Convert the HTML document to a PDF file with the custom settings
        Converter.convertHTML(htmlDoc, "YOUR_DIRECTORY/custom_page.pdf", pdfOptions);

        // Step 4: Inform the user that the PDF has been created
        System.out.println("PDF generated with custom page size and margins.");
    }
}
```

### Adım 1 – HTML'yi PDF'ye Dönüştürme: Belgeyi Yükleme

İlk olarak **PDF'ye dönüştürmek istediğimiz HTML'yi** yüklüyoruz.  
`HTMLDocument` dosyayı okur, göreli bağlantıları çözer ve Aspose'un render edebileceği bir DOM oluşturur.  

> **Neden önemli:** HTML, CSS veya resimlere referans veriyorsa, Aspose bu kaynakları dosya yoluna göre alır. Mutlak bir yol (`YOUR_DIRECTORY/input.html`) kullanmak “dosya bulunamadı” sürprizlerini önler.

### Adım 2 – PDF Sayfa Boyutunu Değiştirme: Seçenekleri Yapılandırma

Burada bir `PdfConversionOptions` nesnesi oluşturuyoruz.  
- `setPageSize(PageSize.A4)` Aspose'a standart A4 boyutlarını (210 × 297 mm) kullanmasını söyler.  
- `setPageOrientation(...)` sayfayı yatay (landscape) yapmak için yönü değiştirir.  
- `setMargins(new Margin(20, 20, 20, 20))` her kenara 20 point kenar boşluğu ekler.

`PageSize.A4` yerine `PageSize.LETTER` ya da **özel bir boyut** için bir `SizeF` nesnesi geçirebilirsiniz, örneğin:

```java
pdfOptions.setPageSize(new SizeF(500, 800)); // width, height in points
```

> **İpucu:** Bir point, 1/72 inçtir. Milimetre cinsinden düşünüyorsanız, point değerini elde etmek için 2.83465 ile çarpın.

### Adım 3 – HTML'den PDF Oluşturma: Dönüşümü Çalıştırma

`Converter.convertHTML` işi halleder. Yüklenmiş `HTMLDocument`, çıktı yolu ve az önce yapılandırdığımız seçenekleri alır.  

PDF sayfa boyutunu içeriğe göre dinamik olarak ayarlamak isterseniz, bu adımdan önce gerekli boyutları hesaplayıp `pdfOptions` nesnesini buna göre güncelleyebilirsiniz.

### Adım 4 – Sonucu Doğrulama

`System.out.println` satırı isteğe bağlıdır, ancak programı bir konsoldan çalıştırdığınızda hızlı bir geri bildirim sağlar. Çalıştırdıktan sonra `custom_page.pdf` dosyasını açın – A4 dikey (portrait) bir PDF, her tarafta 20 point eşit kenar boşluğu, tam olarak belirttiğimiz gibi olmalıdır.

## HTML'yi PDF'ye Dönüştürme – Yaygın Varyasyonlar

### Dosya Yolu Yerine Akış (Stream) Kullanma

Bazen fiziksel bir dosyanız olmayabilir; HTML bir veritabanından ya da API'den geliyor olabilir. Bu durumda string'i bir `ByteArrayInputStream` içine sarın:

```java
String htmlContent = "<html><body><h1>Hello, PDF!</h1></body></html>";
HTMLDocument htmlDoc = new HTMLDocument(
        new ByteArrayInputStream(htmlContent.getBytes(StandardCharsets.UTF_8)),
        "http://example.com/");
```

İkinci argüman, göreli kaynakları çözmek için temel URL'dir.

### Sayfa Yönünü Değiştirme

Raporunuz genişse, yatay (landscape) moda geçin:

```java
pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Landscape);
```

### Kenar Boşluklarını İnce Ayarlama

Kenar boşlukları ondalıklı değerler kabul eder, bu yüzden 0.5 pt gibi çok ince bir sınır ayarlayabilirsiniz:

```java
pdfOptions.setMargins(new Margin(5.5, 10.2, 5.5, 10.2));
```

### Büyük HTML Dosyalarını İşleme

Devasa belgeler için **bellek‑verimli akış** etkinleştirmeyi düşünün:

```java
pdfOptions.setUseMemoryCache(true);
```

Bu, Aspose'un ara verileri RAM yerine geçici dosyalara yazmasını sağlar.

## PDF Sayfa Boyutu Ayarlama – Kenar Durumları ve Tuzaklar

- **Eksik Yazı Tipleri:** HTML'niz sunucuda yüklü olmayan özel bir yazı tipi kullanıyorsa, PDF varsayılan bir yazı tipine geri döner. `pdfOptions.getFontEmbeddingMode().setEmbeddingMode(EmbeddingMode.Always);` ile yazı tipini gömün.  
- **Resim Ölçekleme:** Yüksek çözünürlüklü resimler PDF'yi şişirebilir. `pdfOptions.setImageResolution(150);` ile kaliteyi koruyarak çözünürlüğü düşürün.  
- **CSS Uyumluluğu:** Tüm CSS özellikleri tam desteklenmez. Standart düzen tekniklerini (flexbox çalışır, grid bazı sorunlar çıkarabilir) kullanın.  
- **Yol İzinleri:** İşlemin `YOUR_DIRECTORY` içine yazma izni olduğundan emin olun. Aksi takdirde `IOException` fırlatılır.

## Beklenen Çıktı

Programı çalıştırdığınızda aşağıdaki gibi bir PDF elde edersiniz (kavramsal gösterim):

```
+---------------------------------------------------+
|                     Header                        |
|                                                   |
|   (HTML rendered content goes here)               |
|                                                   |
|                     Footer                        |
+---------------------------------------------------+
```

- Sayfa boyutu: **A4** (210 × 297 mm).  
- Yönlendirme: **Dikey**.  
- Kenar boşlukları: **20 pt** her iki tarafta.  

Dosyayı herhangi bir PDF görüntüleyici (Adobe Reader, Chrome vb.) ile açarak doğrulayın.

## Özet

Artık Aspose.HTML for Java kullanarak bir HTML kaynağından **PDF özel boyut** oluşturmayı biliyorsunuz. Öğreticide **HTML'yi PDF'ye dönüştürme**, **PDF sayfa boyutunu değiştirme**, **PDF sayfa boyutunu ayarlama** ve **özel kenar boşluklarıyla PDF oluşturma** adımlarını baştan sona gördünüz.  

Deney yapmaktan çekinmeyin—`PageSize.LETTER` yerine legal boyut kullanın, kenar boşluklarını ayarlayın ya da kendi yazı tiplerinizi gömün. Sonraki adım olarak **filigran ekleme**, **PDF şifreleme** veya **birden çok HTML dosyasını toplu işleme** konularını keşfedebilirsiniz. Tüm bu konular, az önce ele aldığımız temel kavramlar üzerine inşa edilir.

Belirli bir kenar durumu hakkında sorunuz mu var? Aşağıya yorum bırakın, size yardımcı olayım. Kodlamanın tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}