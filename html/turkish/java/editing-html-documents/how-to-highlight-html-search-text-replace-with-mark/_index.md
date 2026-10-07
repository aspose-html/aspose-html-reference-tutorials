---
category: general
date: 2026-03-04
description: HTML içinde metin arayarak ve her eşleşmeyi <mark> etiketiyle sararak
  HTML'yi vurgulama. Metni <mark> öğeleriyle değiştirmek için adım adım Java rehberi.
draft: false
keywords:
- how to highlight html
- search text in html
- highlight word in html
- highlight occurrences of word
- replace text with mark
language: tr
og_description: HTML içinde metin arayarak ve eşleşmeleri <mark> etiketiyle sararak
  HTML'yi nasıl vurgularsınız. Metni <mark> etiketiyle değiştirmek için tam Java örneği.
og_title: HTML'i Vurgulama – Metni Ara ve <mark> ile Değiştir
tags:
- Aspose.HTML
- Java
- Text Processing
title: HTML'yi Vurgulama – Metni Ara ve <mark> ile Değiştir
url: /tr/java/editing-html-documents/how-to-highlight-html-search-text-replace-with-mark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML'yi Vurgulama – Metin Arama ve `<mark>` ile Değiştirme

Belirli bir kelime birden çok kez göründüğünde **HTML'yi nasıl vurgulayacağınızı** hiç merak ettiniz mi? Belki bir dokümantasyon sitesi, bir blog motoru oluşturuyorsunuz ya da sadece statik bir sayfada bir marka adını vurgulamanız gerekiyor. İyi haber? HTML'de metin aramayı ve sonuçları bir `<mark>` öğesiyle sarmalamayı öğrendiğinizde oldukça basit.

Bu öğreticide, bir HTML dosyasını yükleyen, hedef kelimeyi arayan, her oluşumu bir `<mark>` etiketiyle değiştiren ve sonunda vurgulanmış sürümü kaydeden tam bir Java çözümünü adım adım inceleyeceğiz. Sonuna geldiğinizde **HTML'de kelimeyi vurgulama**, **kelimenin oluşumlarını vurgulama** ve hatta **metni mark ile değiştirme** işlemlerini çevre işaretlemeyi bozmadan yapabileceksiniz.

> **İhtiyacınız olanlar**  
> • Java 17 veya daha yeni bir sürüm (kod daha eski sürümlerle de çalışır)  
> • Aspose.HTML for Java kütüphanesi (ücretsiz deneme veya lisanslı kopya)  
> • İşlemek istediğiniz basit bir HTML dosyası  

Bu temel gereksinimlere sahipseniz, başlayalım.  

![Vurgulanmış HTML çıktısını gösteren ekran görüntüsü – HTML nasıl vurgulanır](/images/highlight-html-example.png "HTML nasıl vurgulanır örneği")

## Adım 1 – HTML Belgesini Yükleme (HTML'yi Nasıl Vurgularsınız)

İlk olarak kaynak dosyayı belleğe almamız gerekiyor. Aspose.HTML’in `Document` sınıfı tüm ağır işleri yapar, işaretlemeyi DOM‑benzeri bir yapıya ayrıştırır ve sorgulayabilir hâle getirir.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Load the original HTML file
        Document document = new Document("YOUR_DIRECTORY/article.html");
```

**Neden önemli:** Belgeyi yüklemek, temiz bir nesne modeli sağlar; böylece etiketleri veya öznitelikleri bozma endişesi olmadan metin düğümlerini güvenle manipüle edebiliriz. Ayrıca boşlukları normalleştirir, bu da sonraki **HTML'de metin arama** adımını daha güvenilir kılar.

## Adım 2 – Hedef Kelime İçin HTML'de Metin Arama

Belge hazır olduğuna göre, vurgulamak istediğimiz kelimenin her oluşumunu arayacağız. `searchText` yöntemi, eşleşmenin DOM içinde nerede bulunduğunu açıklayan `TextMatch` nesnelerinin bir listesini döndürür.

```java
        // Define what we want to highlight
        String searchTerm = "Aspose";

        // Find all matches – this is the core of "search text in html"
        List<TextMatch> matches = document.searchText(searchTerm);
```

**İpucu:** Arama varsayılan olarak büyük/küçük harfe duyarlıdır. Büyük/küçük harfe duyarsız bir arama istiyorsanız, `searchText`i çağırmadan önce belge metnini ve `searchTerm`i aynı harfe dönüştürün ya da kütüphanenin sağladığı düzenli ifade tabanlı yaklaşımı kullanın.

## Adım 3 – Metni `<mark>` ile Değiştirme (HTML'de Kelimeyi Vurgulama)

Her eşleşme için, içeren düğümün metnini yeniden oluşturacağız ve tam kelimeyi bir `<mark>` öğesiyle saracağız. Bu, yalnızca hedef metni etkiler ve HTML’nin geri kalanını dokunulmaz bırakır.

```java
        // Iterate over each match and wrap it with <mark>
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();

            // Preserve text before and after the match
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;

            // Replace the node's content with the new fragment
            parentNode.setTextContent(highlightedFragment);
        }
```

**Açıklama:**  
- `getStartOffset`/`getEndOffset` bize eşleşmenin ebeveyn düğüm içindeki tam karakter konumlarını verir.  
- Orijinal metni (`textBefore` ve `textAfter`) dilimleyerek diğer her şeyi olduğu gibi tutarız.  
- Eşleşmeyi `<mark>` ile sarmak, **metni mark ile değiştirme** için kanonik yoldur ve ekstra CSS olmadan yerel tarayıcı vurgulaması sağlar.

### Kenar Durumları ve İpuçları

- **Aynı düğümde birden çok eşleşme:** Döngü her `TextMatch`i sırasıyla işler. Her seferinde tüm düğümün içeriğini değiştirdiğimiz için sonraki ofsetler kayar. Aspose.HTML eşleşmeleri belge sırasına göre döndürdüğü için basit değiştirme çoğu durumda çalışır. Çakışan eşleşmelerle karşılaşırsanız, önce tüm eşleşmeleri toplayıp düğümü tek bir geçişte yeniden oluşturmayı düşünün.  
- **Ham HTML içermeyen öğeler:** Ebeveyn düğüm bir `<script>` veya `<style>` bloğuysa, `<mark>` eklemek sayfayı bozabilir. Değiştirme öncesinde `parentNode.getNodeName()` kontrol ederek bu düğümleri atlayabilirsiniz.

## Adım 4 – Vurgulanan Belgeyi Kaydetme (Kelimenin Oluşumlarını Vurgulama)

Tüm değişiklikler tamamlandıktan sonra, değiştirilmiş DOM’u diske geri yazıyoruz. Çıktı dosyası, orijinal işaretlemenin yanı sıra yeni `<mark>` etiketlerini içerecek ve böylece **kelimenin oluşumlarını vurgulama** “Aspose” kelimesi etkili bir şekilde yapılmış olacak.

```java
        // Write the modified HTML back to a new file
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

Herhangi bir tarayıcıda `highlighted.html` dosyasını açın; her “Aspose” kelimesinin sarı‑msı bir arka planla ( `<mark>` için varsayılan stil) sarıldığını göreceksiniz. Özel bir görünüm isterseniz, küçük bir CSS kuralı ekleyin:

```html
<style>
    mark { background-color: #fffa8b; color: #000; }
</style>
```

## Yaygın Sorular (HTML'de Metin Arama – SSS)

**S: Kelime bir öznitelik değerinin içinde görünürse ne olur?**  
C: `searchText` yalnızca düğüm metin içeriğine bakar, öznitelik dizelerine bakmaz. Öznitelik değerlerini vurgulamak istiyorsanız, öğeler üzerinde döngü yapıp öznitelikleri manuel olarak incelemeniz gerekir.

**S: Tek seferde birden fazla farklı kelimeyi vurgulayabilir miyim?**  
C: Kesinlikle. Bir terim listesi oluşturun, her birini döngüye alın ve aynı değiştirme mantığını çalıştırın. Çakışan eşleşmelere karşı dikkatli olun.

**S: Bu, `<section>` veya `<article>` gibi yalnızca HTML5 etiketleriyle çalışır mı?**  
C: Evet. Aspose.HTML modern HTML5 öğelerini tam olarak destekler, bu yüzden DOM gezintisi etiket tipine bakılmaksızın çalışır.

## Tam Çalışan Örnek (Tüm Adımlar Birleştirildi)

Aşağıda, dosyayı yüklemekten vurgulanmış çıktıyı kaydetmeye kadar tüm iş akışını gösteren eksiksiz, çalıştırılabilir bir Java programı yer alıyor.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document
        Document document = new Document("YOUR_DIRECTORY/article.html");

        // Step 2: Search for the word "Aspose"
        String searchTerm = "Aspose";
        List<TextMatch> matches = document.searchText(searchTerm);

        // Step 3: Wrap each found occurrence with a <mark> element
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted HTML fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;
            parentNode.setTextContent(highlightedFragment);
        }

        // Step 4: Save the highlighted document
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

**Beklenen çıktı:** `highlighted.html` dosyasını açın ve “Aspose” kelimesinin her oluşumunun vurgulandığını görün. Sayfanın başka hiçbir bölümü değiştirilmez ve dosya geçerli bir HTML belgesi olarak kalır.

## Sonuç

**HTML'yi nasıl vurgulayacağınızı** programlı olarak **HTML'de metin arama**, her eşleşmeyi bir `<mark>` etiketiyle sarmalama ve sonunda değişiklikleri kalıcı hâle getirme yoluyla ele aldık. Bu yaklaşım, **HTML'de kelimeyi vurgulama**, **kelimenin oluşumlarını vurgulama** ve **metni mark ile değiştirme** işlemlerini kırılgan string‑manipülasyon kodu yazmadan yapmanızı sağlar.

Sonraki adımlar? Betiği şu şekilde genişletmeyi deneyin:  
- Arama terimini komut satırı argümanı olarak kabul edin.  
- Özel bir vurgulama rengi tanımlayan bir CSS dosyası oluşturun.  
- Bir klasördeki tüm HTML dosyalarını toplu olarak işleyin.  

Bu varyasyonlar, hem Aspose.HTML API'sini hem de genel metin‑işleme desenlerini daha derinlemesine anlamanızı sağlayacaktır.

Herhangi bir sorunla karşılaşırsanız veya daha fazla geliştirme fikriniz olursa, aşağıya bir yorum bırakın. İyi vurgulamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}