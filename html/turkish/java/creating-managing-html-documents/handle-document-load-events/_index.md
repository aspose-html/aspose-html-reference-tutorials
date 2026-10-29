---
date: 2026-04-23
description: Bu adım adım rehberde Aspose.HTML for Java kullanarak dış HTML'yi nasıl
  alacağınızı ve belge yüklenmesini nasıl bekleyeceğinizi öğrenin.
keywords:
- get outer html
- wait for document load
- java html processing
- navigate html document
- aspose html example
linktitle: Aspose.HTML'de Belge Yükleme Olaylarını İşleyin
second_title: Java HTML Processing with Aspose.HTML
title: Aspose.HTML for Java'da Dış HTML'yi Al ve Yükleme Olaylarını İşleyin
url: /tr/java/creating-managing-html-documents/handle-document-load-events/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dış HTML Al ve Aspose.HTML for Java'da Yükleme Olaylarını İşle

## Giriş
Uzak bir sayfadan **dış html** almanız ve belge yüklenmeyi tamamladığında hemen tepki vermeniz gerektiğinde, belge yükleme olaylarını yönetmek çok önemlidir. Java'da Aspose.HTML, bir URL'ye gitmek ve `OnLoad` olayını dinlemek için temiz bir API sunar; böylece HTML hazır olduğunda güvenli bir şekilde erişebilirsiniz. Bu öğretici, ortamı kurmaktan yüklenmiş bir sayfanın dış HTML'ini yazdırmaya kadar tüm süreci adım adım gösterir; böylece bunu herhangi bir web‑odaklı Java uygulamasına entegre edebilirsiniz.

## Hızlı Yanıtlar
- **“dış html al” ne anlama geliyor?** Belgenin kök öğesinin tam HTML işaretlemesini döndürür.  
- **Hangi kütüphane yükleme olaylarını yönetir?** Aspose.HTML for Java `OnLoad` olayını sağlar.  
- **Test için lisansa ihtiyacım var mı?** Ücretsiz bir deneme sürümü mevcuttur; üretim için ticari lisans gereklidir.  
- **Belgenin yüklenmesini nasıl bekleyebilirim?** Demo amaçlı `OnLoad` işleyicisini veya basit bir uyku (sleep) komutunu kullanın.  
- **Bu yaklaşım asenkron güvenli mi?** Evet, olay belge yüklenmeyi tamamladıktan sonra tetiklenir ve HTML'in hazır olduğunu garanti eder.

## “Dış html al” nedir?
`document.getDocumentElement().getOuterHTML()` belge kök öğesinin tam HTML dizesini, açılış ve kapanış etiketleri dahil, döndürür. Bu, ham işaretlemeyi daha fazla işleme, depolama veya dönüşüm için gerektiğinde faydalıdır.

## Neden Aspose.HTML for Java kullanmalısınız?
- **Sağlam HTML ayrıştırma** bir tarayıcı motoruna ihtiyaç duymadan.  
- **Olay‑tabanlı model** belge hazır olduğunda tam olarak tepki vermenizi sağlar.  
- **Çapraz‑platform** Windows, Linux ve macOS desteği.  
- **Zengin API** gezinme, manipülasyon ve PDF, görüntü vb. dönüşümler için.

## Önkoşullar
Koda geçmeden önce aşağıdakilere sahip olduğunuzdan emin olun:

1. **Java Development Kit (JDK)** – [Oracle'ın web sitesinden](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html) yükleyin.  
2. **Aspose.HTML for Java** – En son JAR dosyasını [Aspose sürüm sayfasından](https://releases.aspose.com/html/java/) indirin.  
3. **IDE** – IntelliJ IDEA, Eclipse veya tercih ettiğiniz herhangi bir editör.  
4. **Temel Java bilgisi** – Sınıflar, metodlar ve olay yönetimini anlama.  
5. **İnternet bağlantısı** – Örnek çevrimiçi bir HTML sayfası yükler.

Her şey hazır olduğunda, kodlamaya başlamaya hazırsınız!

## Adım‑Adım Kılavuz

### Adım 1: Bir HTML Belgesi Başlatın
İlk olarak bir `HTMLDocument` örneği oluşturun. Ayrıca yükleme durumunu izlemek için bir `AtomicBoolean` ayarlarız.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument();
java.util.concurrent.atomic.AtomicBoolean isLoading = new java.util.concurrent.atomic.AtomicBoolean(false);
```

### Adım 2: **OnLoad** Olayına Abone Olun
`isLoading` bayrağını belge yüklenmeyi tamamladığında değiştiren bir işleyici ekleyin. İşte **dış html al** çağrısının güvenli olduğunu bileceğimiz yer.

```java
document.OnLoad.add(new DOMEventHandler() {
    @Override
    public void invoke(Object o, Event event) {
        isLoading.set(true);
    }
});
```

### Adım 3: Belgeye Git (url'den html yükle)
`HTMLDocument`'e hangi sayfayı alacağını söyleyin. Bu örnekte bir public Aspose dokümantasyon sayfasını yüklüyoruz.

```java
document.navigate("https://docs.aspose.com/html/net/creating-a-document/document.html");
```

### Adım 4: Belgenin Yüklenmesini Bekleyin
Uzak bir sayfanın yüklenmesi asenkrondur. Demonstrasyon için birkaç saniye boyunca iş parçacığını duraklatıyoruz; üretimde `OnLoad` bayrağına veya daha gelişmiş bir senkronizasyon tekniğine güvenirsiniz.

```java
Thread.sleep(5000);
```

### Adım 5: Yüklenen Belgeye Erişin ve **Dış HTML Al**
`isLoading` artık true olduğuna göre, belgenin kök öğesinin tam işaretlemesini alın.

```java
System.out.println("outerHTML = " + document.getDocumentElement().getOuterHTML());
```

Konsolda yüklenen sayfanın tam HTML'ini görmelisiniz.

## Yaygın Sorunlar ve Çözümler
| Sorun | Sebep | Çözüm |
|-------|--------|-----|
| **`isLoading` asla true olmuyor** | `OnLoad` işleyicisi `navigate()` çağrılmadan önce eklenmemişti | İşleyiciyi `navigate()` çağırmadan **önce** ekleyin. |
| **`getDocumentElement()` üzerinde `NullPointerException`** | Belge erişildiğinde tam olarak yüklenmemişti | Uygun bir bekleme mekanizması kullanın (ör. `isLoading.get()` üzerinde döngü veya bir `CountDownLatch`). |
| **HTTPS URL'leri yüklerken SSLHandshakeException** | Güvenilen sertifikalar eksik | Uygun sertifikayı Java keystore'unuza ekleyin veya `-Djsse.enableSNIExtension=false` kullanın. |
| **Yavaş yükleme zaman aşımına neden oluyor** | Büyük sayfa veya ağ gecikmesi | Uyku süresini artırın veya zaman aşımı farkında bir dinleyici uygulayın. |

## Sıkça Sorulan Sorular

**Q: Aspose.HTML for Java nedir?**  
A: Aspose.HTML for Java, geliştiricilerin Java uygulamalarında HTML belgeleri oluşturmasına, manipüle etmesine ve dönüştürmesine olanak tanıyan bir kütüphanedir.

**Q: Aspose.HTML for Java nasıl indirilir?**  
A: Bunu [Aspose sürüm sayfasından](https://releases.aspose.com/html/java/) indirebilirsiniz.

**Q: Aspose.HTML'i ücretsiz kullanabilir miyim?**  
A: Evet, [Aspose web sitesinden](https://releases.aspose.com/) bir deneme sürümü indirerek Aspose.HTML'i ücretsiz deneyebilirsiniz.

**Q: Aspose.HTML için destek mevcut mu?**  
A: Evet, [Aspose forumunda](https://forum.aspose.com/c/html/29) destek bulabilir ve sorular sorabilirsiniz.

**Q: Aspose.HTML için geçici lisans nasıl alınır?**  
A: [Aspose geçici lisans sayfasını](https://purchase.aspose.com/temporary-license/) ziyaret ederek geçici bir lisans talep edebilirsiniz.

---

**Son Güncelleme:** 2026-04-23  
**Test Edildi:** Aspose.HTML for Java 24.11  
**Yazar:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}