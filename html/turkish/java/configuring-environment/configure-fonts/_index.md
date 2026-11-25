---
date: 2026-04-05
description: HTML'den PDF oluşturmayı, yazı tiplerini yapılandırmayı, özel CSS uygulamayı,
  geçici bir lisans kullanmayı ve Aspose.HTML ile Java'da HTML'yi PDF'ye dönüştürmeyi
  öğrenin.
keywords:
- generate pdf from html
- convert html pdf java
- add custom fonts pdf
- fonts not showing pdf
linktitle: Aspose.HTML'de Yazı Tiplerini Yapılandır
second_title: Java HTML Processing with Aspose.HTML
title: 'HTML''den PDF Oluşturma: Aspose.HTML for Java ile Yazı Tiplerini Yapılandırma'
url: /tr/java/configuring-environment/configure-fonts/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML‑to‑PDF Java için Aspose.HTML ile Yazı Tiplerini Yapılandırma

## Giriş
Bu öğreticide, Aspose.HTML kullanarak **generate PDF from HTML** işlemini nasıl gerçekleştireceğinizi ve Java'da HTML‑to‑PDF dönüşümü için yazı tiplerini nasıl yapılandıracağınızı keşfedeceksiniz. HTML belgeleriyle çalışırken doğru yazı tiplerini ayarlamak, oluşturulan PDF'nin orijinal web sayfası gibi görünmesini sağlar—marka renklerini, tipografiyi ve düzeni korur. Raporlar, faturalar veya herhangi bir belge‑oluşturma hattı oluşturuyor olun, doğru yazı tipi yapılandırması profesyonel görünümlü PDF'lerin anahtarıdır. Ortamı hazırlamaktan HTML'yi özel yazı tipleri ve CSS ile PDF'ye dönüştürmeye kadar tüm süreci adım adım inceleyelim.

## Hızlı Yanıtlar
- **Bu öğreticinin temel amacı nedir?** Java kullanarak Aspose.HTML ile HTML‑to‑PDF dönüşümü için yazı tiplerini yapılandırmak.  
- **Hangi kütüphane dönüşümü gerçekleştirir?** Aspose.HTML for Java (`Converter` sınıfı).  
- **Lisans almam gerekiyor mu?** Geçici bir Aspose lisansı değerlendirme sınırlamalarını kaldırır; üretim için tam lisans gereklidir.  
- **Özel yazı tiplerim nerede bulunmalı?** `FontsLookupFolder` tarafından referans verilen bir klasörde, örneğin projenizin yanındaki bir `fonts` dizininde.  
- **PDF çıktısını özelleştirebilir miyim?** Evet—`PdfSaveOptions` kullanarak sayfa boyutu, kenar boşlukları ve daha fazlasını ayarlayabilirsiniz.

## **generate PDF from HTML** Nedir ve Yazı Tipi Yapılandırması Neden Önemlidir?
**generate PDF from HTML** süreci, bir HTML belgesini PDF sayfasına dönüştürür. Yazı tipleri, düzen, satır aralığı ve görsel doğruluk açısından kritik bir rol oynar. Aspose.HTML'i özel bir yazı tipi klasörüne yönlendirerek, PDF'nin web sayfası için tasarladığınız tam tipografiyi kullanmasını sağlarsınız; bu da yedek yazı tiplerini ortadan kaldırır ve marka tutarlılığını korur.

## Yazı Tipi Yapılandırması İçin Aspose.HTML Neden Kullanılmalı?
- **Doğru renderleme:** CSS2.1 ve birçok CSS3 özelliğini destekler, böylece HTML'niz PDF'de aynı görünür.  
- **Çapraz‑platform:** Java 1.8+ çalıştırabilen herhangi bir işletim sisteminde çalışır.  
- **Lisans esnekliği:** Geçici bir lisansla test edin, ardından üretim için tam lisansa geçin.  
- **Performans:** Karmaşık sayfalarda bile hızlı dönüşüm.

## Önkoşullar
Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:

1. **Java Development Kit (JDK) 1.8+** – kod, modern bir JDK üzerinde çalışır.  
2. **Aspose.HTML for Java** – en son JAR dosyasını [Aspose web sitesinden](https://releases.aspose.com/html/java/) indirin.  
3. **IDE** – IntelliJ IDEA, Eclipse veya herhangi bir Java‑uyumlu editör.  
4. **Temel Java bilgisi** – sınıflar, metodlar ve dosya I/O konusunda rahat olmalısınız.  
5. **Aspose.HTML lisansı** – bir [geçici lisans](https://purchase.aspose.com/temporary-license/) değerlendirme kısıtlamalarını kaldırır.

## Paketleri İçe Aktarma
İlk olarak, ihtiyacınız olacak temel Java ve Aspose.HTML sınıflarını içe aktarın.  

```java
import java.io.IOException;
```

Bu importlar, dosya işlemleri ve Aspose.HTML API'sine erişim sağlar.

## Özel Yazı Tipleri PDF Oluşturma Nasıl Eklenir
Aşağıda, yazı tipi işleme neden önemli, özel CSS nasıl uygulanır ve **geçici bir lisans** nasıl kullanılacağı açıklanacaktır.

## Adım‑Adım Kılavuz

### Adım 1: HTML İçeriğini Oluşturun
HTML'yi PDF'ye dönüştürmek için önce basit bir HTML dosyası oluşturacağız.

#### 1.1 HTML kodunu yazın
```java
String code = "<h1>FontsSettings property</h1>\r\n" +
    "<p>The FontsSettings property is used for configuration of fonts handling.</p>\r\n";
```

Bu snippet bir başlık ve bir paragraf tanımlar. Daha fazla stil test etmek isterseniz HTML'yi ek elemanlarla genişletebilirsiniz.

#### 1.2 HTML'yi bir dosyaya kaydedin
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("user-agent-fontsetting.html")) {
    fileWriter.write(code);
}
```

`FileWriter`, dizeyi projenizin klasöründeki `user-agent-fontsetting.html` dosyasına yazar. Bu adımın ardından işleme hazır bir fiziksel HTML dosyanız olur.

### Adım 2: Aspose.HTML Ortamını Yapılandırın
Şimdi, HTML'nin nasıl render edileceğini kontrol etmemizi sağlayan Aspose.HTML `Configuration` nesnesini ayarlayacağız.

#### 2.1 Configuration örneği oluşturun
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

`Configuration` nesnesi, yazı tipi yönetimi ve kullanıcı‑aracısı davranışı gibi render seçeneklerini özelleştirmenin giriş noktasıdır.

#### 2.2 Kullanıcı Aracısı Servisine Erişin
```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

`IUserAgentService`, stil sayfalarını, yazı tiplerini ve diğer render detaylarını yönetir. Özel CSS enjekte etmek ve yazı tipi klasörümüzü göstermek için bunu kullanacağız.

### Adım 3: Özel Stil ve Yazı Tiplerini Uygulayın
Ortam hazır olduğunda, CSS kurallarını ekleyebilir ve Aspose.HTML'e yazı tiplerimizin nerede olduğunu söyleyebiliriz.

#### 3.1 Özel CSS ayarla
```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; }\r\n" +
    "p { color:grey; }\r\n");
```

Bu CSS başlığı kahverengi, paragrafı gri renklendirir. Buraya geçerli herhangi bir CSS kuralı ekleyebilirsiniz—Aspose.HTML tam CSS2.1 spesifikasyonunu ve birçok CSS3 özelliğini destekler. *(Bu, **apply custom css** örneğidir.)*

#### 3.2 Özel yazı tipi klasörüne işaret edin
```java
userAgent.getFontsSettings().setFontsLookupFolder("fonts");
```

Kullanmak istediğiniz `.ttf` veya `.otf` dosyalarını, projenizin kökünde bulunan `fonts` adlı klasöre yerleştirin. Aspose.HTML render sırasında bu yazı tiplerini otomatik olarak yükleyecektir.

> **Pro ipucu:** Birden fazla yazı tipi ailesi varsa, alt klasörlerde düzenli tutun ve her üst klasörü `FontsLookupFolder` listesine noktalı‑virgül ile ayrılmış bir dize olarak ekleyin.

### Adım 4: HTML Belgesini Yapılandırma ile Yükleyin
Şimdi, daha önce oluşturduğumuz HTML dosyasını yükleyerek az önce oluşturduğumuz özel yapılandırmayı uygularız.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("user-agent-fontsetting.html", configuration);
```

`HTMLDocument` nesnesi artık stil verilmiş HTML'yi temsil eder ve dönüşüm için hazırdır.

### Adım 5: HTML'yi PDF'ye Dönüştürün
Son olarak, **aspose html pdf conversion** işlemini gerçekleştirerek özel yazı tipleri ve stillerimizi koruyan bir PDF dosyası üretiriz.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.PdfSaveOptions(),
    "user-agent-fontsetting_out.pdf"
);
```

`PdfSaveOptions` nesnesi, sayfa boyutu, sıkıştırma ve meta veriler gibi çıktı ayarlarını ayarlamanıza olanak tanır. Temel bir dönüşüm için varsayılan seçenekler mükemmel çalışır.

### Adım 6: Kaynakları Temizleyin
Özellikle uzun süren bir uygulamada birçok belge işliyorsanız, doğru temizleme bellek sızıntılarını önler.

#### 6.1 HTMLDocument'i Serbest Bırakın
```java
if (document != null) {
    document.dispose();
}
```

#### 6.2 Configuration'ı Serbest Bırakın
```java
if (configuration != null) {
    configuration.dispose();
}
```

Bu çağrılar, Aspose.HTML tarafından tahsis edilen yerel kaynakları serbest bırakır.

## Yaygın Sorunlar ve Çözümler
| Sorun | Çözüm |
|-------|----------|
| **Yazı tipleri görünmüyor** | `fonts` klasörünün doğru referans edildiğini ve geçerli `.ttf`/`.otf` dosyaları içerdiğini doğrulayın. Klasör proje dışındaysa mutlak yollar kullanın. |
| **PDF boş görünüyor** | HTML dosya yolunun doğru ve dosyanın okunabilir olduğundan emin olun. `Configuration` nesnesinin `HTMLDocument` yapıcıya geçirildiğini kontrol edin. |
| **Lisans istisnası** | Aspose API'lerini çağırmadan önce geçici ya da tam bir Aspose lisansı uygulayın. Lisans dosyasını sınıf yoluna (classpath) yerleştirin ve `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` kodu ile yükleyin. |
| **Beklenmeyen CSS renderı** | Aspose.HTML çoğu CSS'i destekler ancak tüm modern özellikleri (ör. CSS Grid) desteklemez. Stilleri sadeleştirin veya desteklenen CSS özelliklerini kullanın. |

## Sıkça Sorulan Sorular

**S: Aspose.HTML for Java ile herhangi bir yazı tipini kullanabilir miyim?**  
C: Evet, işletim sisteminizin desteklediği herhangi bir TrueType (`.ttf`) veya OpenType (`.otf`) yazı tipini kullanabilirsiniz. Dosyaları `FontsLookupFolder` ile belirttiğiniz klasöre yerleştirmeniz yeterlidir.

**S: Aspose.HTML for Java kullanmak için lisansa ihtiyacım var mı?**  
C: Kütüphaneyi lisans olmadan değerlendirebilirsiniz, ancak bir [geçici Aspose lisansı](https://purchase.aspose.com/temporary-license/) değerlendirme sınırlamalarını kaldırır. Üretim ortamı için tam lisans gereklidir.

**S: PDF çıktısını nasıl özelleştirebilirim?**  
C: `convertHTML` metoduna yapılandırılmış bir `PdfSaveOptions` örneği geçin. Sayfa boyutu, kenar boşlukları, sıkıştırma seviyesi vb. ayarları burada belirtebilirsiniz.

**S: Daha karmaşık CSS stilleri uygulamak mümkün mü?**  
C: Evet, Aspose.HTML geniş bir CSS yelpazesini destekler. Karmaşık seçiciler, medya sorguları ve pseudo‑class'lar tarayıcıdaki gibi çalışır; ancak çok yeni CSS3/4 özelliklerinin bazıları tam olarak desteklenmeyebilir.

**S: Daha fazla örnek ve dokümantasyona nereden ulaşabilirim?**  
C: Ayrıntılı API referansları ve ek kod örnekleri için resmi [Aspose.HTML for Java dokümantasyon sayfasını](https://reference.aspose.com/html/java/) ziyaret edin.

**S: Geçici Aspose lisansı dönüşümü nasıl etkiler?**  
C: Geçici lisans, değerlendirme modunda görülen 10‑sayfa sınırını ve filigranı kaldırır; böylece **aspose html pdf conversion** iş akışını tam olarak test edebilirsiniz.

---

**Son Güncelleme:** 2026-04-05  
**Test Edilen Sürüm:** Aspose.HTML for Java 24.12 (yazım anındaki en yeni sürüm)  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}