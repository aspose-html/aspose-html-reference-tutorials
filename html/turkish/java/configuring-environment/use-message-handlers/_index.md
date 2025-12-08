---
date: 2025-12-08
description: Aspose.HTML for Java ile HTML'yi PNG'ye dönüştürmeyi, kırık bağlantıları
  yönetmeyi ve özel mesaj işleyicileri kullanarak eksik kaynakları yakalamayı öğrenin.
language: tr
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Aspose.HTML for Java'da HTML'yi PNG'ye Dönüştürme ve Mesaj İşleyicilerini Kullanma
url: /java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML for Java ile HTML'yi PNG'ye Dönüştürme – Mesaj İşleyicileri Kullanarak

## Giriş  
Bu öğreticide **HTML'yi PNG'ye nasıl dönüştüreceğinizi** Aspose.HTML for Java kullanarak ve aynı zamanda **kırık linkleri** veya eksik kaynakları özel bir mesaj işleyicisiyle **nasıl ele alacağınızı** öğreneceksiniz. Basit bir HTML dosyası oluşturmayı, diske yazmayı, yüklemeyi ve ağ hatalarını yakalamayı adım adım göstereceğiz—üretim‑düzeyinde Java uygulamalarında güvenilir **html to image conversion** ihtiyacı olan geliştiriciler için mükemmel bir örnek.

## Hızlı Yanıtlar
- **Bu öğreticide ne anlatılıyor?** HTML'yi PNG'ye dönüştürme ve eksik kaynakları bir mesaj işleyicisiyle ele alma.  
- **Hangi kütüphane kullanılıyor?** Aspose.HTML for Java.  
- **Lisans gerekiyor mu?** Deneme sürümleri için geçici bir lisans önerilir.  
- **HTML dosyasını Java'dan yazabilir miyim?** Evet – “write html file java” adımına bakın.  
- **İşleyici kırık linkleri yakalar mı?** Kesinlikle; 200 olmayan yanıtları kaydeder.

## Aspose.HTML'de Mesaj İşleyicisi Nedir?  
Bir mesaj işleyicisi, ağ yığınına bir kanca ekleyerek **eksik kaynakları** (örneğin kırık bir resim URL'si) bir istisna fırlatmadan önce yakalamanızı sağlar. Yanıt durum kodunu inceleyerek isteği kaydedebilir, değiştirebilir veya yeniden deneyebilirsiniz—bu da ağ işlemleri üzerinde tam kontrol sağlar.

## Neden HTML'yi PNG'ye Dönüştürmek?  
HTML'yi bir görüntüye dönüştürmek, tam PDF dönüşümüne gerek kalmadan küçük resimler, e‑posta ön izlemeleri veya PDF benzeri anlık görüntüler oluşturmak için faydalıdır. Aspose.HTML, tarayıcı gerektirmeyen hızlı bir **html to image conversion** motoru sunar.

## Önkoşullar
1. **Java Development Kit (JDK)** – [Oracle web sitesinden](https://www.oracle.com/java/technologies/javase-downloads.html) indirin.  
2. **Aspose.HTML for Java** – en son JAR dosyalarını [Aspose sürüm sayfasından](https://releases.aspose.com/html/java/) edinin.  
3. **IDE** – IntelliJ IDEA, Eclipse veya NetBeans.  
4. **Temel Java bilgisi** – try‑with‑resources ve nesne temizleme konularına hâkim olmalısınız.  
5. **Geçici lisans** (isteğe bağlı) – deneme sınırlamalarından kaçınmak için bir [geçici lisans](https://purchase.aspose.com/temporary-license/) kullanın.

## Paketleri İçe Aktarma  
Başlamadan önce gerekli Java sınıflarını içe aktarın:

```java
import java.io.IOException;
```

Bu içe aktarmalar, dosya I/O ve Aspose.HTML ağ API'lerine erişim sağlar.

## Adım 1: HTML Dosyasını Yazma (write html file java)  
İlk olarak, **var olmayan** bir resmi referans alan küçük bir HTML snippet'i oluşturun. Bu, işleyiciyi test etmemizi sağlayacak.

```java
String code = "<img src='missing.jpg'>";
```

## Adım 2: HTML'yi Diske Kaydetme  
Snippet'i `document.html` adlı bir dosyaya kaydedin. Bu dosya daha sonra Aspose.HTML motoru ile yüklenecek.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Adım 3: Özel Bir Mesaj İşleyicisi Oluşturma (catch missing resource)  
Şimdi HTTP durum kodunu kontrol eden bir işleyici tanımlıyoruz. Kod `200` değilse dostça bir mesaj kaydediyoruz.

```java
com.aspose.html.net.MessageHandler handler = new com.aspose.html.net.MessageHandler() {
    @Override
    public void invoke(com.aspose.html.net.INetworkOperationContext context) {
        if (context.getResponse().getStatusCode() != 200) {
            System.out.println(String.format("File '%s' Not Found", context.getRequest().getRequestUri().toString()));
        }
        invoke(context);
    }
};
```

## Adım 4: İşleyiciyi Ağ Servisine Kaydetme  
Özel işleyiciyi Aspose.HTML'in ağ servisine ekleyerek her istekte yer almasını sağlıyoruz.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Adım 5: HTML Belgesini Yükleme (load html document java)  
Yapılandırma hazır olduğunda HTML dosyasını yükleyin. Eksik resim, az önce eklediğimiz işleyiciyi tetikleyecek.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Additional operations will go here
} finally {
    if (document != null) {
        document.dispose();
    }
}
```

## Adım 6: HTML'yi PNG'ye Dönüştürme (convert html to png)  
Son olarak, yüklenen belgeyi bir PNG görüntüsüne dönüştürün. Bu, tam **html to image conversion** iş akışını gösterir.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Adım 7: Kaynakları Temizleme  
Yerel kaynakları serbest bırakmak ve bellek sızıntılarını önlemek için `Configuration` nesnesini her zaman imha edin.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Yaygın Tuzaklar ve İpuçları
- **Recursive invoke çağrısı:** Özel işleyici, zinciri devam ettirmek için mantığınızdan *sonra* `invoke(context);` çağırmalıdır. Bunu unutmak diğer işleyicilerin çalışmasını engelleyebilir.  
- **Lisans eksikliği uyarıları:** Geçerli bir lisans olmadan dönüşüm su işareti ekleyebilir veya çıktı boyutunu sınırlayabilir.  
- **Yol sorunları:** `document.html` dosyasının çalışma dizinine yazıldığından emin olun veya mutlak bir yol sağlayın.  

## Sıkça Sorulan Sorular

**S: Aspose.HTML for Java nedir?**  
C: Tarayıcı gerektirmeden Java geliştiricilerinin HTML belgeleri oluşturmasına, manipüle etmesine ve dönüştürmesine olanak tanıyan sağlam bir kütüphanedir.

**S: Aspose.HTML for Java'da mesaj işleyicileri neden kullanılır?**  
C: **Kırık linkleri ele almanıza**, eksik kaynakları kaydetmenize veya istek/yanıtları anında değiştirmenize olanak tanır.

**S: Birden fazla mesaj işleyicisini zincirleyebilir miyim?**  
C: Evet—her işleyiciyi `network.getMessageHandlers()` listesine ekleyin; eklenme sırasına göre çalışırlar.

**S: Configuration ve HTMLDocument nesnelerinin imhası gerekli mi?**  
C: Kesinlikle; imha, yerel belleği serbest bırakır ve uzun süre çalışan uygulamalarda sızıntıları önler.

**S: Eksik görseller dışında, işleyiciler hangi hataları yönetebilir?**  
C: 200 olmayan tüm HTTP yanıtları—zaman aşımı, 404 sayfaları, kimlik doğrulama hataları vb.—yakalanıp işlenebilir.

## Sonuç  
Artık **HTML'yi PNG'ye dönüştürürken** **kırık linkleri** ve **eksik kaynakları yakalamayı** Aspose.HTML for Java ile gerçekleştiren tam, üretim‑hazır bir örneğe sahipsiniz. Bu deseni daha büyük projelere entegre ederek ağ işlemleri üzerinde ince ayar yapabilir ve HTML içeriğinizin güvenilir görüntü anlık görüntülerini oluşturabilirsiniz.

---

**Last Updated:** 2025-12-08  
**Tested With:** Aspose.HTML for Java 24.12 (latest)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}