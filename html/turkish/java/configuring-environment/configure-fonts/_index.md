---
date: 2026-02-04
description: Aspose.HTML'i kullanarak yazı tiplerini yapılandırmayı, özel CSS uygulamayı,
  geçici lisans kullanmayı ve Java’da HTML’den PDF oluşturmayı öğrenin.
linktitle: Configure Fonts in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Aspose.HTML'yi Kullanarak Java'da HTML'den PDF'ye Yazı Tiplerini Nasıl Yapılandırılır
url: /tr/java/configuring-environment/configure-fonts/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML ile Java’da HTML‑to‑PDF için Yazı Tiplerini Yapılandırma

## Giriş
Bu öğreticide **Aspose.HTML**'i nasıl kullanacağınızı keşfedecek ve Java’da HTML‑to‑PDF dönüşümü için yazı tiplerini yapılandıracaksınız. HTML belgeleriyle çalışırken doğru yazı tiplerini ayarlamak, oluşturulan PDF'nin orijinal web sayfası gibi görünmesini sağlar—marka renkleri, tipografi ve düzeni korur. Raporlar, faturalar veya herhangi bir belge‑oluşturma süreci oluşturuyor olun, doğru yazı tipi yapılandırması profesyonel görünümlü PDF'lerin anahtarıdır. Ortamı hazırlamaktan özel yazı tipleri ve CSS ile HTML'yi PDF'ye dönüştürmeye kadar tüm süreci adım adım inceleyelim.

## Hızlı Yanıtlar
- **Bu öğreticinin temel amacı nedir?** Aspose.HTML kullanarak Java’da HTML‑to‑PDF dönüşümü için yazı tiplerini yapılandırmak.  
- **Dönüşümü hangi kütüphane gerçekleştirir?** Aspose.HTML for Java (`Converter` sınıfı).  
- **Bir lisansa ihtiyacım var mı?** Geçici bir Aspose lisansı değerlendirme sınırlamalarını kaldırır; üretim için tam lisans gereklidir.  
- **Özel yazı tiplerim nerede bulunmalı?** `FontsLookupFolder` ile referans verilen bir klasörde, örneğin projenizin yanındaki bir `fonts` dizininde.  
- **PDF çıktısını özelleştirebilir miyim?** Evet—sayfa boyutu, kenar boşlukları ve daha fazlasını ayarlamak için `PdfSaveOptions` kullanın.

## Aspose.HTML ile Yazı Tipi Yapılandırması Nasıl Kullanılır
Aşağıda, yazı tipi işlemenin neden önemli olduğunu, özel CSS nasıl uygulanacağını ve çözümü test ederken tam işlevselliği açmak için **geçici lisans nasıl kullanılacağını** açıklayacağız.

## Ön Koşullar
Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:

1. **Java Development Kit (JDK) 1.8+** – kod herhangi bir modern JDK'da çalışır.  
2. **Aspose.HTML for Java** – en son JAR'ı [Aspose web sitesinden](https://releases.aspose.com/html/java/) indirin.  
3. **IDE** – IntelliJ IDEA, Eclipse veya herhangi bir Java uyumlu editör.  
4. **Temel Java bilgisi** – sınıflar, metodlar ve dosya G/Ç konusunda rahat olmalısınız.  
5. **Aspose.HTML lisansı** – bir [geçici lisans](https://purchase.aspose.com/temporary-license/) değerlendirme kısıtlamalarını kaldırır.

## Paketleri İçe Aktarma
İlk olarak, ihtiyacınız olan temel Java ve Aspose.HTML sınıflarını içe aktarın.  

```java
import java.io.IOException;
```

Bu içe aktarmalar, dosya işleme ve Aspose.HTML API'sine erişim sağlar.

## **html to pdf java** nedir ve Yazı Tipi Yapılandırması Neden Önemlidir?
**html to pdf java** süreci, bir HTML belgesini PDF sayfasına dönüştürür. Yazı tipleri, düzen, satır aralığı ve görsel doğruluk üzerinde etkili oldukları için render işleminin temel bir parçasıdır. Aspose.HTML'i özel bir yazı tipi klasörüne yönlendirerek, PDF'nin web sayfası için tasarladığınız tam tipografiyi kullandığından, yedek yazı tiplerini ortadan kaldırdığından ve marka tutarlılığını koruduğundan emin olursunuz.

## Adım‑Adım Kılavuz

### Adım 1: HTML İçeriği Oluşturma
İlk olarak, daha sonra PDF'ye dönüştüreceğimiz basit bir HTML dosyası oluşturacağız.

#### 1.1 HTML kodunu yazın
```java
String code = "<h1>FontsSettings property</h1>\r\n" +
    "<p>The FontsSettings property is used for configuration of fonts handling.</p>\r\n";
```

Bu snippet bir başlık ve bir paragraf tanımlar. Ek stilleri test etmeniz gerekiyorsa HTML'yi daha fazla öğe ile genişletmekten çekinmeyin.

#### 1.2 HTML'yi bir dosyaya kaydedin
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("user-agent-fontsetting.html")) {
    fileWriter.write(code);
}
```

`FileWriter`, dizeyi projenizin klasöründeki `user-agent-fontsetting.html` dosyasına yazar. Bu adımdan sonra işleme hazır bir fiziksel HTML dosyanız olacak.

### Adım 2: Aspose.HTML Ortamını Yapılandırma
Şimdi, HTML'nin nasıl render edildiğini kontrol etmemizi sağlayan Aspose.HTML `Configuration` nesnesini kuracağız.

#### 2.1 Configuration örneği oluşturun
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

`Configuration` nesnesi, yazı tipi işleme ve kullanıcı‑ajan davranışı gibi render seçeneklerini özelleştirmenin giriş noktasıdır.

#### 2.2 User Agent Servisine Erişin
```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

`IUserAgentService`, stil sayfalarını, yazı tiplerini ve diğer render detaylarını yönetir. Özel CSS enjekte etmek ve yazı tipi klasörümüzü göstermek için bunu kullanacağız.

### Adım 3: Özel Stiller ve Yazı Tipleri Uygulama
Ortam hazır olduğunda, CSS kurallarını ekleyebilir ve Aspose.HTML'e yazı tiplerimizin nerede olduğunu söyleyebiliriz.

#### 3.1 Özel CSS ayarlayın
```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; }\r\n" +
    "p { color:grey; }\r\n");
```

Bu CSS başlığı kahverengi ve paragrafı gri renklendirir. Buraya geçerli herhangi bir CSS kuralı ekleyebilirsiniz—Aspose.HTML tam CSS2.1 spesifikasyonunu ve birçok CSS3 özelliğini destekler. *(Bu, **apply custom css** örneğidir.)*

#### 3.2 Özel yazı tipi klasörünü gösterin
```java
userAgent.getFontsSettings().setFontsLookupFolder("fonts");
```

Kullanmak istediğiniz tüm `.ttf` veya `.otf` dosyalarını, projenizin kökünde bulunan `fonts` adlı klasöre yerleştirin. Aspose.HTML, render sırasında bu yazı tiplerini otomatik olarak yükleyecektir.

> **Pro ipucu:** Birden fazla yazı tipi ailesi varsa, bunları alt klasörlerde düzenli tutun ve her üst klasörü `FontsLookupFolder`'a noktalı virgül‑ayırıcı bir liste kullanarak ekleyin.

### Adım 4: HTML Belgesini Configuration ile Yükleyin
Şimdi, daha önce oluşturduğumuz HTML dosyasını, az önce oluşturduğumuz özel yapılandırmayı uygulayarak yüklüyoruz.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("user-agent-fontsetting.html", configuration);
```

`HTMLDocument` nesnesi artık dönüşüm için hazır stil verilen HTML'yi temsil ediyor.

### Adım 5: HTML'yi PDF'ye Dönüştürme
Son olarak, **aspose html pdf conversion** işlemini gerçekleştirerek özel yazı tiplerimizi ve stillerimizi koruyan bir PDF dosyası üretiriz.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.PdfSaveOptions(),
    "user-agent-fontsetting_out.pdf"
);
```

`PdfSaveOptions` nesnesi, sayfa boyutu, sıkıştırma ve meta veriler gibi çıktı ayarlarını ayarlamanıza olanak tanır. Temel bir dönüşüm için varsayılan seçenekler mükemmel çalışır.

### Adım 6: Kaynakları Temizleme
Doğru temizleme, özellikle uzun süren bir uygulamada birçok belge işlenirken bellek sızıntılarını önler.

#### 6.1 HTMLDocument'i serbest bırakın
```java
if (document != null) {
    document.dispose();
}
```

#### 6.2 Configuration'ı serbest bırakın
```java
if (configuration != null) {
    configuration.dispose();
}
```

Bu çağrılar, Aspose.HTML tarafından tahsis edilen yerel kaynakları serbest bırakır.

## Yaygın Sorunlar ve Çözümler
| Sorun | Çözüm |
|-------|----------|
| **Yazı tipleri görünmüyor** | `fonts` klasörünün doğru referans alındığını ve geçerli `.ttf`/`.otf` dosyaları içerdiğini doğrulayın. Klasör proje dizininin dışındaysa mutlak yollar kullanın. |
| **PDF boş görünüyor** | HTML dosya yolunun doğru ve dosyanın okunabilir olduğundan emin olun. `Configuration` nesnesinin `HTMLDocument` yapıcısına geçirildiğini kontrol edin. |
| **Lisans istisnası** | Herhangi bir Aspose API'si çağrılmadan önce geçici veya tam bir Aspose lisansı uygulayın. Lisans dosyasını sınıf yoluna yerleştirin ve `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` kodu ile yükleyin. |
| **Beklenmeyen CSS renderı** | Aspose.HTML çoğu CSS'i destekler ancak tüm modern özellikleri (ör. CSS Grid) desteklemez. Stilleri basitleştirin veya desteklenen CSS özelliklerini kullanın. |

## Sıkça Sorulan Sorular

**S: Aspose.HTML for Java ile herhangi bir yazı tipini kullanabilir miyim?**  
C: Evet, işletim sisteminizin desteklediği herhangi bir TrueType (`.ttf`) veya OpenType (`.otf`) yazı tipini kullanabilirsiniz. Dosyaları `FontsLookupFolder` ile belirttiğiniz klasöre yerleştirmeniz yeterlidir.

**S: Aspose.HTML for Java'ı kullanmak için bir lisansa ihtiyacım var mı?**  
C: Kütüphaneyi lisans olmadan değerlendirebilirsiniz, ancak bir [geçici Aspose lisansı](https://purchase.aspose.com/temporary-license/) değerlendirme sınırlamalarını kaldırır. Üretim için tam bir lisans gerekir.

**S: PDF çıktısını nasıl özelleştirebilirim?**  
C: `convertHTML` metoduna yapılandırılmış bir `PdfSaveOptions` örneği geçirin. Sayfa boyutu, kenar boşlukları, sıkıştırma seviyesi ve daha fazlasını ayarlayabilirsiniz.

**S: Daha karmaşık CSS stilleri uygulamak mümkün mü?**  
C: Evet, Aspose.HTML geniş bir CSS yelpazesini destekler. Karmaşık seçiciler, medya sorguları ve pseudo‑class'lar bir tarayıcıda olduğu gibi çalışır, ancak bazı çok yeni CSS3/4 özellikleri tam olarak desteklenmeyebilir.

**S: Daha fazla örnek ve belgeyi nerede bulabilirim?**  
C: Ayrıntılı API referansları ve ek kod örnekleri için resmi [Aspose.HTML for Java dokümantasyon sayfasını](https://reference.aspose.com/html/java/) ziyaret edin.

**S: Geçici Aspose lisansı dönüşümü nasıl etkiler?**  
C: Geçici lisans, değerlendirme modunda görülen 10‑sayfa sınırını ve filigranı kaldırır, böylece **aspose html pdf conversion** iş akışını tam olarak test edebilirsiniz.

---

**Son Güncelleme:** 2026-02-04  
**Test Edilen Versiyon:** Aspose.HTML for Java 24.12 (yazı zamanı itibarıyla en son)  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}