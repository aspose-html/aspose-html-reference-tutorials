---
date: 2026-02-04
description: Aspose.HTML for Java'da özel bir kullanıcı stil sayfası ayarlayarak HTML'den
  PDF oluşturmayı öğrenin ve Kullanıcı Aracısı Servisi ile HTML'yi PDF'ye kolayca
  dönüştürün.
linktitle: Set User Style Sheet in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: HTML'den PDF Oluştur – Aspose.HTML for Java'da Kullanıcı Stil Sayfasını Ayarlama
url: /tr/java/configuring-environment/set-user-style-sheet/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML'den PDF Oluştur – Aspose.HTML for Java'da Kullanıcı Stil Sayfası Ayarlama

## Giriiş
Bu öğreticide, Aspose.HTML for Java kullanarak **HTML'den PDF oluşturmayı** ve özel bir kullanıcı stil sayfası uygulama listesi.
Kendi benzersiz stilinizde HTML belgelerinizin görünümünü ayarlamak istediğiniz bir an oldu mu? Bir web sayfasını hazırlamanızı ve başlıkların belirli bir renkle öne çıkmasını ya da paragrafların tüm özelliklerinin görünmesini istediğinizi hayal edin. İşte *user stylesheet* ve **User Agent Service** burada devreye giriyor. Basit bir HTML dosyası yazmaktan, kullanıcı aracını kontrolya, son olarak **HTML'yi PDF'ye dönüştürmeye** kadar her adımı adım adım göstereceğiz—böylece sonucunu anında görebileceksiniz.

## Hızlı Yanıtlar
- **HTML'den PDF oluşturmak** ne anlama geliyor? Bir HTML belgesini (CSS, resimler, yazı türleri vb. ile) işleyip görsel olarak çıkartıp PDF dosyasının kaydedilmesini sağlar gelir.
- **Hangi Aspose uzmanı gereklidir?** Dönüştürme motoru ve User Agent Service'i sağlayan Aspose.HTML for Java kütüphanesi.
- **Test için lisansa ihtiyaç var mı?** Geliştirme için ücretsiz deneme sürümü yeterlidir; üretim için ticari lisans gerekir.
- **Harici bir CSS dosyası kullanabilir miyim?** Evet – normal bir tarayıcıda olduğu gibi harici stil sayfalarına bağlanabilirsiniz.
- **Dönüştürme ne kadar sürer?** Bu kılavuzdaki basit belge için dönüşüm bir saniyenin altında tamamlanır.

## Önkoşullar
Kodlara başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:

1. **Aspose.HTML for Java** – en yeni JAR kopyası [Aspose sürümler sayfası](https://releases.aspose.com/html/java/) adresinden indirin.
2. **Java Development Kit (JDK) 8+** – `java -version` komutu 8 veya daha yüksek bir sürüm gösterildiğinden emin olun.
3. **IDE** – IntelliJ IDEA, Eclipse veya NetBeans mevcuttur.
4. **Temel HTML/CSS bilgisi** – faydalı ancak zorunlu değil.

## Paketleri İçe Aktar
Başlamak için gerekli Java sınıflarını içeri aktarın. Bu örnek için tek açık içe aktarma `java.io.IOException` sınıfıdır; Aspose sınıfları daha sonra tam kapsamlı adlarıyla kullanılacaktır.

```java
import java.io.IOException;
```

## Adım 1: Basit Bir HTML Belgesi Oluşturun
İlk olarak, PDF dönüşümümüzün kaynağı olacak minimal bir HTML dosyası (`document.html`) oluşturacağız.

```java
String code = "<h1>User Agent Service</h1>\r\n" +
        "<p>The User Agent Service allows you to specify a custom user stylesheet, a primary character set for the document, language, and fonts settings.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Pro tip:** HTML dosyasını Java kaynağınızla aynı dizinde tutarak yol‑ile ilgili sorunların önüne geçin.

## Adım 2: Aspose.HTML Yapılandırmasını Ayarlayın
Bir `Configuration` nesnesi oluşturun. Bu nesne, daha sonra kullanacağınız tüm servisleri (User Agent Service dahil) içeren bir kapsayıcı görevi görür.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Kullanıcı Aracısı Servisini Neden Kullanmalısınız?
**User Agent Service**, varsayılan karakter seti, dil, yazı tipleri ve bu öğreticinin odak noktası olan özel bir kullanıcı stil sayfası gibi düşük seviyeli render seçenekleri üzerinde kontrol sağlar. Stilleri bu seviyede uygulayarak, orijinal HTML'nin kendi CSS'i olmasa bile tutarlı bir görsel çıktı elde edersiniz.

## Adım 3: Kullanıcı Aracısı Servisine Erişin
**User Agent Service**, özel bir stil sayfası eklemenize, varsayılan karakter setini ayarlamanıza ve diğer render seçeneklerini kontrol etmenize olanak tanır.

```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

## Adım 4: Kullanıcı Stil Sayfasını Tanımlayın ve Uygulayın  
Şimdi, HTML render edildiğinde uygulanacak CSS kurallarını tanımlıyoruz. İşte **user agent service** kullanarak stil sayfasını ayarladığımız yer.

```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; font-size:2em; }\r\n" +
        "p { background-color:GhostWhite; color:SlateGrey; font-size:1.2em; }\r\n");
```

> **Why this matters:** Stil sayfasını kullanıcı‑ajan seviyesinde uygulayarak, orijinal HTML bir CSS dosyasına referans vermese bile stillerin uygulanmasını garantilersiniz.

## Adım 5: Özel Yapılandırmayla HTML Belgesini Yükleyin 
Dosya yolunu ve `Configuration` örneğini `HTMLDocument` yapıcısına aktarın. Bu, kullanıcı stil sayfasını belgeye bağlar.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```

## Adım 6: HTML'yi PDF'ye Dönüştürme  
Belge tamamen stil almışken, statik `convertHTML` metodunu çağırarak **HTML'den PDF'ye dönüşümü** gerçekleştirin. `PdfSaveOptions` nesnesi, çıktı (sayfa boyutu, sıkıştırma vb.) üzerinde ince ayar yapmanıza izin verir.

```java
com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.PdfSaveOptions(),
        "user-agent-stylesheet_out.pdf"
);
```

> **Result:** `user-agent-stylesheet_out.pdf` dosyası, başlığı kahverengi ve paragrafı GhostWhite arka plan rengiyle, stil sayfasında tanımlandığı gibi içerecektir.

## Adım 7: Kaynakları Temizleme  
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
| Sorun | Neden | Çözüm |
|----------|----------|-----|
| **Boş PDF çıktısı** | Stil sayfası uygulanmadı veya belge ayarları ile yüklenmedi. | `configuration` nesnesinin `HTMLDocument`a geçirilmesi ve `setUserStyleSheet`in yüklenmesinden önce çağrıldığını doğrulayın. |
| **Desteklenmeyen CSS özelliği uyarısı** | Aspose.HTML bazı gelişmiş CSS özelliklerini desteklemiyor. | Aspose.HTML belgelerinde CSS özelliklerini kullanın veya daha basit stillere geçin. |
| **FileNotFoundException** | `document.html`in kopyalarının yolu yanlış. | Mutlak bir yol kullanın veya HTML miktarını proje köküne ekleyin. |

## Sıkça Sorulan Sorular

**S: Farklı HTML bileşenleri için farklı stiller uygulayabilir miyim?**
C: elbette! Kullanıcı stil sayfası içinde ihtiyacınız kadar CSS kural tanımlayabilirsiniz.

**S: Stili dinamik olarak değiştirmem gerekirse ne yapmalıyım?**
C: Yeni bir `HTMLDocument` örnek oluşturmadan önce `setUserStyleSheet` yöntemini tekrar çağırın; yeni stiler bir sonraki dönüşümde uygulanacaktır.

**S: Aspose.HTML for Java ile harici CSS dosyalarını kullanmak mümkün mü?**
C: Evet – HTML içinde harici bir stil sayfasını bağlayabilir veya gerçekleştirmediğiniz `setUserStyleSheet` yöntemini çalıştırabilirsiniz.

**S: Aspose.HTML desteklenmeyen CSS özellikleri nasıl ele alıyor?**
C: Desteklenmeyen özellikler yok sayılır, bu şekilde hala devam eden geri kalan kısmı incelemez olarak işlenir.

**S: PDF dışındaki formatlara da HTML'ye dönüştürülebilir mi?**
C: Evet, Aspose.HTML'ye uygun `SaveOptions` sınıflarıyla XPS, TIFF, PNG, JPEG ve daha fazlasına saklanması.

## Çözüm
Artık Aspose.HTML for Java ile özel bir kullanıcı stil sayfasını ayarlayarak **HTML'den PDF oluşturmayı** gördünüz. Bu iş sistemleri, yazılım PDF'nin görsel görünümünü tam kontrol etmenizi sağlar; otomatik rapor oluşturma, fatura üretimi veya stilin kritik olduğu herhangi bir senaryo için idealdir. Daha karmaşık CSS, harici yazı türleri veya ek dönüşüm formatlarıyla deneyler yaparak bu temeli genişletmeden ortaya çıkar.

---

**Son Güncelleme:** 2026-02-04
**Test Edilenler:** Aspose.HTML for Java 24.11 (yazım sırasındaki en son sürüm)
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}