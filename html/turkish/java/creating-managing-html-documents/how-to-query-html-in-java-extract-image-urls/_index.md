---
category: general
date: 2026-03-05
description: 'Java’da HTML sorgulama: bir HTML dosyasını okuyup resimleri çıkarmak.
  Java ile HTML dosyasını okuma, Java ile resim URL’lerini elde etme ve Java ile NodeList
  üzerinde yineleme öğrenin.'
draft: false
keywords:
- how to query html
- read html file java
- how to extract images
- iterate over nodelist java
- get image urls java
language: tr
og_description: Java'da HTML sorgulama ve resim URL'lerini alma. Bu rehber, Java'da
  HTML dosyasını okuma, resimleri bulma ve NodeList üzerinde yineleme yapma yöntemlerini
  gösterir.
og_title: Java'da HTML Sorgulama – Görsel URL'lerini Çıkarma
tags:
- html parsing
- java
- aspose-html
- xpath
- css selector
title: Java’da HTML Sorgulama – Görsel URL’lerini Çıkarma
url: /tr/java/creating-managing-html-documents/how-to-query-html-in-java-extract-image-urls/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da HTML Sorgulama – Görüntü URL’lerini Çıkarma

Hiç **Java’da HTML nasıl sorgulanır** diye merak ettiniz mi ve bir sayfadaki tüm resimleri çekmek istediniz mi? Tek başınıza değilsiniz—geliştiriciler sürekli HTML dosyalarını okumak, resimleri kazımak ve ardından URL’lerle bir şeyler yapmak zorunda kalıyor. Bu öğreticide, **Java’da HTML nasıl sorgulanır** gösteren pratik bir örnek üzerinden ilerleyecek, Java tarzında bir HTML dosyasını okuyacak ve Java‑civarıyla resim URL’lerini elde edeceğiz.

Aspose.HTML for Java'ı kullanacağız, ancak kavramlar—XPath, CSS seçicileri ve bir `NodeList` üzerinde yineleme—herhangi bir DOM kütüphanesine uygulanabilir. Bu rehberin sonunda **görselleri nasıl çıkaracağınızı** rahatça yapabilecek, **NodeList Java üzerinde nasıl yineleme yapılacağını** bilecek ve projenize ekleyebileceğiniz hazır‑kod parçacığına sahip olacaksınız.

![Java’da HTML sorgulama örneği](https://example.com/placeholder.png "Java’da HTML sorgulama")

---

## Öğrenecekleriniz

- Diskten bir HTML belgesi yükleyin (read HTML file Java)
- XPath ve CSS seçicileriyle `<img>` etiketlerini bulun (how to extract images)
- Ortaya çıkan `NodeList`i döngüye alın (iterate over NodeList Java)
- Her resmin `src` özniteliğini yazdırın (get image URLs Java)

Harici hizmetler yok, karmaşık yapı araçları yok—sadece saf Java ve tek bir Maven bağımlılığı.

---

## Önkoşullar

- Java 8 veya daha yeni bir sürüm yüklü
- Bağımlılık yönetimi için Maven veya Gradle
- HTML yapısına temel aşinalık
- Opsiyonel ama faydalı: bazı `<figure><img …></figure>` öğeleri içeren basit bir HTML dosyası (`sample.html`)

Eğer bunlara sahipseniz, hemen başlayabiliriz.

---

## Adım 1: HTML Dosyasını Java’da Oku – Belgeyi Yükle

İlk iş olarak, HTML’i belleğe getirmemiz gerekiyor. Aspose.HTML’in `HTMLDocument` sınıfı bu işi yapıyor. Bunu, istediğiniz sayfaya geçebileceğiniz bir kitabı açmak gibi düşünün.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.NodeList;
import com.aspose.html.dom.Element;

/**
 * Demonstrates how to query HTML in Java and extract image URLs.
 */
public class QueryExample {
    public static void main(String[] args) throws Exception {

        // ① Load the HTML document from a local file.
        // Replace "YOUR_DIRECTORY/sample.html" with the actual path.
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

**Neden önemli:** Dosyayı yüklemek, sorgulayabileceğiniz bir DOM ağacı sağlar. Yol yanlışsa `FileNotFoundException` alırsınız, bu yüzden çalıştırmadan önce konumu iki kez kontrol edin.

---

## Adım 2: Görselleri XPath ile Bul – Görselleri Nasıl Çıkarırsınız

XPath, düğümleri lazer hassasiyetiyle hedeflemenizi sağlayan güçlü bir sorgu dilidir. Burada, `alt` özniteliğine sahip bir `<figure>` içindeki her `<img>` öğesini istiyoruz.

```java
        // ② Use XPath to find <img> elements that have an "alt" attribute.
        NodeList xpathImages = document.evaluateXPath("//figure/img[@alt]");
        System.out.println("XPath found " + xpathImages.getLength() + " images.");
```

**Neden XPath?** Kısadır ve HTML dağınık olsa bile çalışır. `//figure/img[@alt]` ifadesi şu anlama gelir: “`alt` özniteliği taşıyan bir `<figure>` altındaki herhangi bir `<img>`”. Başka özniteliklere göre filtrelemeniz gerekiyorsa, köşeli parantezleri değiştirmeniz yeterlidir.

---

## Adım 3: Görselleri CSS Seçicisi ile Bul – Görselleri Çıkarma İçin Alternatif Yöntem

Bazen CSS sözdizimini tercih edersiniz çünkü stil sayfalarında yazdığınızla aynıdır. `querySelectorAll`, tarayıcıda kullanacağınız aynı seçiciyi kabul eder.

```java
        // ③ Same query using a CSS selector.
        NodeList cssImages = document.querySelectorAll("figure img[alt]");
        System.out.println("CSS selector found " + cssImages.getLength() + " images.");
```

**Neden her ikisi?** İkisini de göstermek, sizin en rahat olduğunuz aracı seçebileceğinizi gösterir. Pratikte birine bağlı kalırsınız, ancak her iki örnek de öğreticiyi daha eksiksiz kılar.

---

## Adım 4: NodeList Java Üzerinde Yineleme – Görsel URL’lerini Al Java

Şimdi bir koleksiyonumuz olduğuna göre, üzerinde dolaşmamız gerekiyor. İşte **NodeList Java üzerinde yineleme** burada devreye giriyor. Her resmin `src` özniteliğini alıp yazdıracağız.

```java
        // ④ Loop through the NodeList returned by the CSS query.
        for (int i = 0; i < cssImages.getLength(); i++) {
            Element imageElement = (Element) cssImages.item(i);
            // Extract the "src" attribute – that’s the image URL.
            System.out.println("Image src: " + imageElement.getAttribute("src"));
        }
    }
}
```

**Neden klasik `for` döngüsü?** Aspose `NodeList` `Iterable` arayüzünü uygulamaz, bu yüzden geliştirilmiş `for‑each` sözdizimi derlenmez. Bir indeks döngüsü kullanmak, **NodeList Java üzerinde yineleme** yapmanın güvenilir yoludur.

---

## Beklenen Çıktı

Running the program against a sample HTML like:

```html
<figure>
    <img src="images/pic1.jpg" alt="First picture">
</figure>
<figure>
    <img src="images/pic2.png" alt="Second picture">
</figure>
```

Will produce something similar to:

```
XPath found 2 images.
CSS selector found 2 images.
Image src: images/pic1.jpg
Image src: images/pic2.png
```

Eğer dosyanız kriterlere uyan daha fazla `<img>` etiketi içeriyorsa, sayılar buna göre artacaktır.

---

## Yaygın Tuzaklar ve Profesyonel İpuçları

- **Dosya yolu sorunları:** Mutlak bir yol kullanın veya `sample.html` dosyasını projenizin çalışma dizinine göre göreli bir konuma yerleştirin.  
- **Eksik `alt` özniteliği:** XPath/CSS sorgularımız `[@alt]` üzerine filtre uygular. *Tüm* görselleri istiyorsanız, öznitelik filtresini kaldırın (`//figure/img` veya `figure img`).  
- **Performans:** Çok büyük belgeler için akış (streaming) ayrıştırıcıları düşünün, ancak çoğu web‑kazıma görevi için DOM yaklaşımı yeterlidir.  
- **Kodlama sorunları:** Aspose.HTML, HTML’de bildirilen karakter setine saygı gösterir. Bozuk karakterler görürseniz, dosyanın UTF‑8 olarak kaydedildiğinden emin olun.  

---

## Örneği Genişletmek

Artık **Görsel URL’lerini Java’da alabilirsiniz**, şu eklemeleri yapmak isteyebilirsiniz:

1. `java.net.URL` ve `Files.copy` kullanarak **görselleri indirin**.  
2. **URL’leri bir veritabanına kaydedin** ilerideki işlemler için.  
3. **Dosya uzantısına göre filtreleyin** (`src.endsWith(".png")`).  

Bunların hepsi Adım 4’te gösterilen döngünün basit uzantılarıdır.

---

## Sonuç

Bu rehberde, Java’da **HTML nasıl sorgulanır** konusunu baştan sona ele aldık: dosyayı yükleme, hem XPath hem de CSS seçicileriyle görselleri bulma ve **NodeList Java üzerinde yineleme** yaparak her resmin `src` özniteliğini yazdırma. Artık **görselleri nasıl çıkaracağınız** konusunda sağlam bir temele sahipsiniz ve Aspose.HTML kullanarak **Java’da HTML dosyası nasıl okunur** konusunda tam bilgi sahibisiniz.

Kodu kendi kazıma ihtiyaçlarınıza göre uyarlamaktan çekinmeyin—ister başka öznitelikler çekmek, `<a>` etiketlerini işlemek, ister URL’leri bir indiriciye beslemek olsun. Desen aynı kalır: yükle, sorgula, yinele ve uygula.

Sorularınız mı var ya da ilginç bir kullanım senaryosu paylaşmak mı istiyorsunuz? Aşağıya bir yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}