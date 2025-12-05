---
date: 2025-12-05
description: Aspose.HTML for Java'da özel bir kullanıcı stil sayfası ayarlayarak HTML'den
  PDF oluşturmayı öğrenin ve Kullanıcı Aracısı Servisi ile HTML'yi PDF'ye kolayca
  dönüştürün.
language: tr
linktitle: Set User Style Sheet in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: HTML'den PDF Oluştur – Aspose.HTML for Java'da Kullanıcı Stil Sayfasını Ayarla
url: /java/configuring-environment/set-user-style-sheet/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML'den PDF Oluştur – Aspose.HTML for Java'da Kullanıcı Stil Sayfası Ayarla

## Giriş
Bu öğreticide, Aspose.HTML for Java kullanarak **HTML'den PDF oluşturmayı** ve özel bir kullanıcı stil sayfası uygulamayı öğreneceksiniz.  
HTML belgelerinizin görünümünü kendi benzersiz stilinizle ayarlamak istediğiniz zaman oldu mu? Bir web sayfası hazırladığınızı ve başlıkların belirli bir renkle öne çıkmasını ya da paragrafların cihazlar arasında tutarlı görünmesini istediğinizi hayal edin. İşte *kullanıcı stil sayfası* ve **Kullanıcı Aracısı Servisi** devreye giriyor. Basit bir HTML dosyası yazmaktan, kullanıcı aracısını yapılandırmaya, sonunda **HTML'yi PDF'ye dönüştürmeye** kadar her adımı adım adım göstereceğiz – böylece sonucu anında görebileceksiniz.

## Hızlı Yanıtlar
- **“HTML'den PDF oluştur” ne demektir?** Bir HTML belgesini (CSS, resimler, yazı tipleri vb. ile) işleyip görsel çıktıyı PDF dosyası olarak kaydetmek anlamına gelir.  
- **Hangi Aspose bileşeni gereklidir?** Aspose.HTML for Java kütüphanesi dönüşüm motorunu ve Kullanıcı Aracısı Servisini sağlar.  
- **Test için lisansa ihtiyacım var mı?** Geliştirme için ücretsiz deneme sürümü yeterlidir; üretim için ticari lisans gerekir.  
- **Harici bir CSS dosyası kullanabilir miyim?** Evet – normal bir tarayıcıda olduğu gibi harici stil sayfalarına bağlanabilirsiniz.  
- **Dönüşüm ne kadar sürer?** Bu kılavuzdaki basit belge için dönüşüm bir saniyenin altında tamamlanır.

## Önkoşullar
Kodlamaya başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:

1. **Aspose.HTML for Java** – en yeni JAR dosyasını [Aspose releases sayfasından](https://releases.aspose.com/html/java/) indirin.  
2. **Java Development Kit (JDK) 8+** – `java -version` komutu 8 veya üzeri bir sürüm gösteriyor olmalı.  
3. **IDE** – IntelliJ IDEA, Eclipse veya NetBeans kullanılabilir.  
4. **Temel HTML/CSS bilgisi** – faydalı ama zorunlu değil.

## Paketleri İçe Aktar
Başlamak için gerekli Java sınıflarını içe aktarın. Bu örnek için tek açık içe aktarma `java.io.IOException` sınıfıdır; Aspose sınıfları daha sonra tam nitelikli adlarıyla referans verilecektir.

```java
import java.io.IOException;
```

## Adım 1: Basit Bir HTML Belgesi Oluştur
İlk olarak, PDF dönüşümümüzün kaynağı olacak minimal bir HTML dosyası (`document.html`) yazacağız.

```java
String code = "<h1>User Agent Service</h1>\r\n" +
        "<p>The User Agent Service allows you to specify a custom user stylesheet, a primary character set for the document, language, and fonts settings.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Pro ipucu:** HTML dosyasını Java kaynağınızla aynı dizinde tutun, böylece yol ile ilgili sorunlardan kaçınabilirsiniz.

## Adım 2: Aspose.HTML Yapılandırmasını Ayarla
Bir `Configuration` nesnesi oluşturun. Bu nesne, daha sonra kullanacağınız tüm servisleri (Kullanıcı Aracısı Servisi dahil) içeren bir kapsayıcı görevi görür.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Adım 3: Kullanıcı Aracısı Servisine Eriş
**Kullanıcı Aracısı Servisi**, özel bir stil sayfası eklemenize, varsayılan karakter kümesini ayarlamanıza ve diğer render seçeneklerini kontrol etmenize olanak tanır.

```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

## Adım 4: Kullanıcı Stil Sayfasını Tanımla ve Uygula
Şimdi, HTML render edildiğinde uygulanacak CSS kurallarını sağlayacağız. İşte burada **kullanıcı aracısı servisini** kullanarak stil sayfasını ayarlıyoruz.

```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; font-size:2em; }\r\n" +
        "p { background-color:GhostWhite; color:SlateGrey; font-size:1.2em; }\r\n");
```

> **Neden önemli:** Stil sayfasını kullanıcı‑aracısı seviyesinde uygulayarak, orijinal HTML bir CSS dosyasına referans vermese bile stillerin saygı görmesini sağlarsınız.

## Adım 5: Özel Yapılandırmayla HTML Belgesini Yükle
Dosya yolunu ve `Configuration` örneğini `HTMLDocument` yapıcısına aktarın. Bu, kullanıcı stil sayfasını belgeye bağlar.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```

## Adım 6: HTML'yi PDF'ye Dönüştür
Belge tamamen stil almışken, statik `convertHTML` metodunu çağırarak **HTML'yi PDF'ye dönüştürün**. `PdfSaveOptions` nesnesi, çıktı (ör. sayfa boyutu, sıkıştırma) üzerinde ince ayar yapmanıza olanak tanır.

```java
com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.PdfSaveOptions(),
        "user-agent-stylesheet_out.pdf"
);
```

> **Sonuç:** `user-agent-stylesheet_out.pdf` dosyası, başlığı kahverengi ve paragrafı GhostWhite arka planıyla, stil sayfasında tanımlandığı gibi içerecek.

## Adım 7: Kaynakları Temizle
Yerel belleği serbest bırakmak için Aspose nesnelerini her zaman dispose edin.

```java
if (document != null) {
    document.dispose();
}
if (configuration != null) {
    configuration.dispose();
}
```

## Yaygın Sorunlar ve Çözümler
| Sorun | Sebep | Çözüm |
|-------|-------|------|
| **Boş PDF çıktısı** | Stil sayfası uygulanmamış veya belge yapılandırma ile yüklenmemiş. | `configuration` nesnesinin `HTMLDocument`'e geçirildiğini ve `setUserStyleSheet` metodunun yüklemeden önce çağrıldığını doğrulayın. |
| **Desteklenmeyen CSS özelliği uyarısı** | Aspose.HTML bazı gelişmiş CSS özelliklerini desteklemiyor. | Sadece Aspose.HTML belgelerinde listelenen CSS özelliklerini kullanın veya daha basit stillere geri dönün. |
| **FileNotFoundException** | `document.html` dosyasının yolu yanlış. | Mutlak bir yol kullanın veya HTML dosyasını proje köküne yerleştirin. |

## Sık Sorulan Sorular

**S: Farklı HTML öğeleri için farklı stiller uygulayabilir miyim?**  
C: Kesinlikle! Kullanıcı stil sayfası içinde ihtiyacınız kadar CSS kuralı tanımlayabilirsiniz.

**S: Stil sayfasını dinamik olarak değiştirmem gerekirse?**  
C: Yeni bir `HTMLDocument` örneği oluşturmadan önce `setUserStyleSheet` metodunu tekrar çağırın; yeni stiller bir sonraki dönüşümde uygulanır.

**S: Aspose.HTML for Java ile harici CSS dosyaları kullanabilir miyim?**  
C: Evet – HTML içinde harici bir stil sayfasına bağlayabilir veya içeriğini okuyup `setUserStyleSheet` metoduna geçirebilirsiniz.

**S: Aspose.HTML desteklenmeyen CSS özelliklerini nasıl ele alıyor?**  
C: Desteklenmeyen özellikler yok sayılır, böylece stil sayfasının geri kalan kısmı hatasız olarak render edilir.

**S: HTML'yi PDF dışındaki formatlara dönüştürebilir miyim?**  
C: Evet, Aspose.HTML uygun `SaveOptions` sınıflarıyla XPS, TIFF, PNG, JPEG ve daha fazlasına dönüşümü destekler.

## Sonuç
Artık Aspose.HTML for Java ile özel bir kullanıcı stil sayfası ayarlayarak **HTML'den PDF oluşturmayı** gördünüz. Bu iş akışı, oluşturulan PDF'nin görsel görünümünü tam kontrol etmenizi sağlar ve otomatik rapor oluşturma, fatura üretimi veya tutarlı stilin kritik olduğu herhangi bir senaryo için idealdir. Daha karmaşık CSS, harici yazı tipleri veya ek dönüşüm formatlarıyla denemeler yaparak bu temeli genişletmekten çekinmeyin.

---

**Son Güncelleme:** 2025-12-05  
**Test Edilen Sürüm:** Aspose.HTML for Java 24.11 (yazım anındaki en yeni sürüm)  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}