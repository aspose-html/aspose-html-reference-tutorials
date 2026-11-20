---
category: general
date: 2026-04-03
description: Aspose.HTML Java'da sandbox'ı nasıl kullanarak kullanıcı ajanını ayarlayacağınızı,
  boyutu belirleyeceğinizi ve görünüm alanı (viewport) boyutunu anında alacağınızı
  öğrenin. Tam kod, açıklamalar ve ipuçları dahil.
draft: false
keywords:
- how to use sandbox
- set user agent
- get viewport size
- how to set size
- how to get viewport
language: tr
og_description: Aspose.HTML Java'da sandbox'ı nasıl kullanarak kullanıcı aracısını
  ayarlayacağınızı, boyutu belirleyeceğinizi ve görünüm alanı boyutunu anında alacağınızı
  öğrenin. Kod ve en iyi uygulamalarla tam rehber.
og_title: Sandbox Nasıl Kullanılır – Kullanıcı Aracısını Ayarla ve Görünüm Alanı Boyutunu
  Al
tags:
- AsposeHTML
- Java
- Sandbox
title: Sandbox Nasıl Kullanılır – Kullanıcı Aracısını Ayarla ve Görüntüleme Alanı
  Boyutunu Al
url: /tr/java/configuring-environment/how-to-use-sandbox-set-user-agent-get-viewport-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sandbox Nasıl Kullanılır – Kullanıcı Aracısını Ayarlama ve Görüntüleme Alanı Boyutunu Alma

HTML'i Aspose.HTML for Java ile işlerken **sandbox nasıl kullanılır** diye hiç merak ettiniz mi? Belki belirli bir ekran boyutunu taklit etmeye çalışırken takıldınız ya da sayfanın mobil bir tarayıcıdan ziyaret ediliyormuş gibi davranmasını sağlamak için bir kullanıcı‑aracısı (user‑agent) dizesi taklit etmeniz gerekiyor.  

İyi haber şu ki sandbox API'si tam da bunu yapmanıza izin veriyor ve sayfa yüklendikten sonra hesaplanan görüntüleme alanı (viewport) boyutunu da alabilirsiniz. Bu öğreticide bir sandbox oluşturmayı, boyutu ayarlamayı, özel bir kullanıcı aracısı belirlemeyi, uzaktan bir sayfa yüklemeyi ve sonunda viewport boyutlarını okumayı adım adım göstereceğiz. Sonunda **boyut nasıl ayarlanır**, **viewport nasıl alınır** ve bu adımların güvenilir başsız (headless) render için neden önemli olduğunu öğreneceksiniz.

> **Hızlı kazanç:** birkaç saniye içinde `Viewport: 1280×800` gibi bir şey yazdıran çalıştırılabilir bir Java sınıfına sahip olacaksınız.

---

## Gereksinimler

- **Aspose.HTML for Java** sürüm 24.6 veya daha yeni (kullandığımız API 24.5'te tanıtıldı).  
- Java 17+ geliştirme kiti (herhangi bir güncel JDK yeterli).  
- Bir IDE ya da basit bir metin editörü—özel eklentilere gerek yok.  
- `https://example.com` gibi harici bir URL yüklemek istiyorsanız internet erişimi.

Hepsi bu. Maven/Gradle sihirbazı zorunlu değil; isterseniz JAR'ları sınıf yoluna manuel olarak ekleyebilirsiniz.  

---

## Sandbox Nasıl Kullanılır – Genel Bakış

Sandbox, render motorunu ana işletim sisteminden izole eder, sanal bir ekran (genişlik, yükseklik, DPI) ve özel bir **kullanıcı aracısı** dizesi tanımlamanıza olanak tanır. Bunu tamamen bellekte çalışan mini bir tarayıcı penceresi gibi düşünün. Daha sonra `HTMLDocument`'in varsayılan görünümünü sorguladığınızda, motor sandbox ayarlarına dayanarak hesapladığı **viewport boyutunu** rapor eder.  

Aşağıda yüksek seviyeli bir akış şeması:

1. **Create** bir `DocumentSandbox` oluşturup genişlik, yükseklik, DPI ve user‑agent'i yapılandırın.  
2. **Load** bu sandbox içinde bir `HTMLDocument` yükleyin.  
3. **Query** belgenin varsayılan görünümünden viewport boyutunu alın.  

Şimdi her bir adıma dalalım.

---

## Adım 1: Sandbox Oluşturma ve Boyutu Ayarlama

İlk olarak bir sandbox başlatıp sanal ekranın ne kadar büyük olacağını söylüyoruz. İşte **boyut nasıl ayarlanır** sorusunun cevabı.

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.drawing.Size2D;

/* Step 1 – instantiate the sandbox */
DocumentSandbox sandbox = new DocumentSandbox();

/* Set the virtual screen width & height (in pixels) */
sandbox.setScreenWidth(1280);   // width in pixels
sandbox.setScreenHeight(800);   // height in pixels

/* DPI influences CSS pixel calculations – 96 is the CSS default */
sandbox.setDeviceDpi(96);

/* Optional: give the sandbox a friendly name for debugging */
sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");
```

> **İpucu:** Duyarlı (responsive) bir tasarımı test ediyorsanız, bir telefon taklit etmek için `360` gibi dar bir genişlik, masaüstü için `1920` gibi geniş bir değer deneyin. Sandbox, ayarladığınız DPI'yi de dikkate alır; bu yüzden yüksek yoğunluklu bir ekran (ör. 144 DPI) `device-pixel-ratio` kullanan medya sorgularını etkiler.

---

## Adım 2: Sandbox İçin Kullanıcı Aracısını Ayarlama

Özel bir **kullanıcı aracısı** (user agent) neden gerekli? Bazı siteler bildirilen tarayıcıya göre farklı işaretleme (markup) veya betikler sunar. `setUserAgent` metodunu çağırarak sayfayı Chrome, Firefox ya da bir mobil cihazdan ziyaret ediliyormuş gibi kandırabilirsiniz.

```java
/* Step 2 – customize the user‑agent string */
sandbox.setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                     "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                     "Version/15.0 Mobile/15E148 Safari/604.1");
```

Şimdi sayfa, iPhone üzerinden render ediliyormuş gibi davranacak. **Kullanıcı aracısını** varsayılan değere geri döndürmek isterseniz, önceki “AsposeHTML/24.6 …” dizesini yeniden kullanmanız yeterli.

---

## Adım 3: Sandbox İçinde Bir HTML Belgesi Yükleme

Sandbox hazır olduğunda, herhangi bir URL ya da yerel HTML dosyasını yükleyebiliriz. `HTMLDocument` yapıcı (constructor) ikinci parametre olarak sandbox'ı alır ve ikisini birbirine bağlar.

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – load the page using the configured sandbox */
try (HTMLDocument doc = new HTMLDocument("https://example.com", sandbox)) {
    // The document is now rendered inside the sandbox environment.
    // Any JavaScript or CSS will see the size and user‑agent we defined.
```

`try‑with‑resources` bloğu, belgeyi doğru şekilde serbest bırakır; böylece Aspose.HTML'nin altında gizli olarak ayırdığı yerel kaynaklar temizlenir.

---

## Adım 4: Belgeden Viewport Boyutunu Alma

Beklediğiniz an geldi: render motorunun hesapladığı **viewport boyutunu** almak. Bu, **viewport nasıl alınır** sorusunun cevabıdır, sayfa yerleşimi tamamlandıktan sonra.

```java
    /* Step 4 – fetch the viewport dimensions */
    Size2D viewport = doc.getDefaultView().getScreenSize();
    System.out.println("Viewport: " + viewport.getWidth() + "×" + viewport.getHeight());
}
```

Programı çalıştırdığınızda aşağıdaki gibi bir çıktı görmelisiniz:

```
Viewport: 1280×800
```

Eğer Adım 1'de sandbox boyutlarını değiştirdiyseniz, yazdırılan sayılar bu yeni değerlere göre olacaktır—duyarlı kırılma noktalarını (breakpoints) doğrulayan otomatik testler için mükemmel.

---

## Tam Çalışan Örnek

Aşağıda tüm parçaları bir araya getiren, doğrudan çalıştırılabilir sınıf yer alıyor. `SandboxExample.java` adlı bir dosyaya kopyalayıp Aspose.HTML JAR'larını sınıf yolunuza ekleyin, ardından `java SandboxExample` komutuyla çalıştırın.

```java
import com.aspose.html.*;
import com.aspose.html.drawing.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox with a custom screen size and DPI
        DocumentSandbox sandbox = new DocumentSandbox();
        sandbox.setScreenWidth(1280);          // width in pixels
        sandbox.setScreenHeight(800);          // height in pixels
        sandbox.setDeviceDpi(96);              // screen DPI
        sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");

        // Step 2: (Optional) Override the user agent if you need a mobile profile
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
            "Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 3: Load the HTML document inside the configured sandbox
        try (HTMLDocument htmlDocument = new HTMLDocument("https://example.com", sandbox)) {

            // Step 4: Retrieve and display the computed viewport size
            Size2D viewportSize = htmlDocument.getDefaultView().getScreenSize();
            System.out.println("Viewport: " + viewportSize.getWidth() + "×" + viewportSize.getHeight());
        }
    }
}
```

**Beklenen çıktı** (yukarıdaki sandbox ayarları varsayıldığında):

```
Viewport: 1280×800
```

Sandbox'ta farklı bir genişlik/yükseklik ayarlarsanız, çıktı da buna göre değişecektir—duyarlı tasarımları test ederken tam da ihtiyacınız olan şey.

---

## Kenar Durumları ve Yaygın Sorular

### Sayfa `window.innerWidth` yerine CSS medya sorguları kullanıyorsa ne olur?

Sandbox'ın sanal ekran boyutu hem CSS düzenini hem de JavaScript'in `window.innerWidth/innerHeight` değerlerini etkiler. Bu yüzden **viewport nasıl alınır** sorusunun JavaScript yanıtı da Java konsolunda gördüklerinizle aynı sayıları verir.

### Aynı anda birden fazla sandbox çalıştırabilir miyim?

Evet. Her `DocumentSandbox` örneği bağımsızdır; bir iş parçacığı havuzu (thread pool) oluşturup her iş parçacığına farklı boyutlarda kendi sandbox'ını vererek aynı anda onlarca sayfa render edebilirsiniz. JAR'ların çok iş parçacıklı (thread‑safe) olduğundan emin olun (oldukları gibi).

### DPI ayarı görüntü ölçeklendirmeyi etkiler mi?

Kesinlikle. Daha yüksek DPI, bir CSS pikselinin daha fazla cihaz pikseline karşılık gelmesini sağlar; bu da yüksek çözünürlüklü görsellerin daha keskin görünmesine yol açar. Retina‑stil varlıkları test ediyorsanız `sandbox.setDeviceDpi(144)` deneyin.

### Kendinden‑imzalı HTTPS sertifikalarını nasıl ele alırım?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}