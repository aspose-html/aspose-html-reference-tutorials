---
category: general
date: 2026-05-25
description: Aspose for Java kullanarak HTML'de nasıl arama yapılır. HTML'de metin
  aramayı, kelime bulmayı, eşleşmeleri saymayı ve aralıkları elde etmeyi birkaç kolay
  adımda öğrenin.
draft: false
keywords:
- how to search html
- search text in html
- find word in html
- how to count matches
- how to get ranges
language: tr
og_description: Aspose for Java kullanarak HTML'de nasıl arama yapılır. Bu öğreticide
  HTML'de metin nasıl aranır, bir kelime nasıl bulunur, eşleşmeler nasıl sayılır ve
  aralıklar nasıl alınır gösterilmektedir.
og_title: Aspose Java ile HTML'de Arama – Tam Rehber
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: How to search HTML using Aspose for Java. Learn to search text in HTML,
    find word in HTML, count matches, and get ranges in a few easy steps.
  headline: How to search HTML with Aspose Java – Complete Programming Guide
  type: TechArticle
tags:
- Java
- Aspose.HTML
- Text Search
- HTML Parsing
title: Aspose Java ile HTML Nasıl Aranır – Tam Programlama Rehberi
url: /tr/java/creating-managing-html-documents/how-to-search-html-with-aspose-java-complete-programming-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose Java ile HTML Arama – Tam Programlama Rehberi

Hiç **HTML içinde belirli bir kelimeyi** özel bir ayrıştırıcı yazmadan aramayı düşündünüz mü? Tek başınıza değilsiniz—geliştiriciler büyük HTML dosyalarında metin bulmak için güvenilir bir yola sürekli ihtiyaç duyuyor; ister veri çıkarma, içerik doğrulama, ister otomatik test olsun. İyi haber, Aspose.HTML for Java bu görevi neredeyse zahmetsiz hâle getiriyor.

Bu rehberde **HTML içinde metin arama**, **eşleşmeleri sayma** ve **her bir oluşum için aralıkları alma** konularını adım adım inceleyeceğiz. Sonunda, HTML içinde bir kelimeyi bulan, kaç kez geçtiğini yazdıran ve tam olarak hangi düğümlerin metni içerdiğini gösteren çalıştırılabilir bir Java programına sahip olacaksınız. Gizem yok, sadece net kod ve pratik ipuçları.

## Önkoşullar

Başlamadan önce şunların kurulu olduğundan emin olun:

* JDK 8 veya daha yeni bir sürüm.
* Bağımlılıkları yönetmek için Maven veya Gradle (örneklerde Maven kullanılacak).
* Aspose.HTML for Java lisansı (ücretsiz deneme sürümü öğrenme amaçlı yeterli).
* Java’dan referans alabileceğiniz bir konumda bulunan örnek HTML dosyası (`sample.html`).

Bu maddeler size yabancı geliyorsa panik yapmayın—bir sonraki bölümde hızlı kurulum adımlarını izleyin.

## HTML Arama – Ortamı Kurma

İlk iş olarak Aspose.HTML kütüphanesini projemize eklememiz gerekiyor. Maven kullanıyorsanız aşağıdaki snippet’i `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest version available -->
</dependency>
```

> **İpucu:** Sürüm numarasına dikkat edin; yeni sürümler genellikle metin arama performansında iyileştirmeler getirir.

Maven bağımlılığı çözüldükten sonra kodlamaya başlayabilirsiniz. Sevdiğiniz IDE’yi (IntelliJ, Eclipse, VS Code) açın ve `FindText` adında yeni bir Java sınıfı oluşturun.

## HTML’de Metin Arama – Belgeyi Yükleme

İlk mantıksal adım, **HTML belgesini** bir `HTMLDocument` nesnesine **yüklemektir**. Bu nesne bir DOM ağacı gibi davranır, sayfayı programatik olarak sorgulamamıza ve değiştirmemize olanak tanır.

```java
import com.aspose.html.dom.*;
import com.aspose.html.services.search.*;

public class FindText {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document from disk.
        // Replace "YOUR_DIRECTORY/sample.html" with the actual path.
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

Neden dosyayı sadece bir dize olarak okumak yerine tam bir `HTMLDocument` kullanıyoruz? Çünkü Aspose’un arama motoru DOM üzerinde çalışır, element sınırlarını gözetir ve `<script>` ya da `<style>` blokları içinde yanlış pozitif sonuçlar üretmez.

## HTML’de Kelime Bulma – Arama Seçeneklerini Yapılandırma

Belge belleğe yüklendiğine göre, motorun **ne** aradığını ve **nasıl** eşleyeceğini belirtmemiz gerekiyor. `TextSearchOptions` sınıfı, büyük/küçük harf duyarlılığı, tam kelime eşleşmesi ve kültüre özgü kurallar gibi ayarları ince ayar yapmamıza izin verir.

```java
        // Step 2: Set up text search options.
        TextSearchOptions searchOptions = new TextSearchOptions();
        // Make the search case‑insensitive (e.g., "Aspose" == "aspose").
        searchOptions.setCaseSensitive(false);
        // Restrict matches to whole words only, avoiding partial matches like "AsposeJS".
        searchOptions.setWholeWord(true);
```

Daha sonra bulanık bir arama yapmak isterseniz `setCaseSensitive(true)` yerine `false` yapabilir veya `setWholeWord(false)` ayarlayabilirsiniz. Varsayılan ayarlar, tahmin edilebilir sonuçlar elde etmeniz için kasıtlı olarak katıdır.

## Eşleşmeleri Sayma – Aramayı Gerçekleştirme

Belge ve seçenekler hazır olduğunda, **istenen kelimeyi arayabilir**iz. `searchText` metodu, hem sayıyı hem de bireysel aralıkları tutan bir `TextSearchResult` nesnesi döndürür.

```java
        // Step 3: Search for the word "Aspose" using the configured options.
        TextSearchResult searchResult = document.searchText("Aspose", searchOptions);
```

Bir sonraki satır **eşleşmeleri nasıl sayacağınızı** gösterir:

```java
        // Step 4: Output the total number of matches found.
        System.out.println("Found " + searchResult.getCount() + " matches.");
```

Arka planda Aspose DOM ağacını dolaşır, her metin düğümünü değerlendirir ve sonuçları toplar. `getCount()` çağrısı O(1)’dir çünkü motor arama sırasında sayıyı zaten hesaplamıştır.

## Aralıkları Alma – Sonuçları İşleme

Sayma faydalı olsa da, genellikle **her eşleşmenin nerede** olduğunu bilmek gerekir. İşte **aralıkları nasıl alacağınız** devreye girer. Her `TextRange` başlangıç ve bitiş düğümlerini, ayrıca karakter ofsetlerini verir.

```java
        // Step 5: Iterate through each match and display the node name where it occurs.
        for (TextRange range : searchResult.getRanges()) {
            // The start node is usually a Text node, but could be any node containing text.
            System.out.println("Match at node: " + range.getStartNode().getNodeName());
        }
```

Daha fazla detaya (örneğin tam satır numarası veya çevresindeki HTML) ihtiyacınız varsa `range.getStartOffset()` ve `range.getEndOffset()` çağırıp orijinal kaynaktan bir snippet çıkarabilirsiniz.

### Kenar Durumlarını Ele Alma

* **Boş belge:** `searchResult.getCount()` `0` dönecek; döngü çalışmayacaktır.
* **Aynı düğümde birden fazla oluşum:** Aspose her eşleşme için ayrı bir `TextRange` döndürür, bu yüzden aynı düğüm adı birden çok kez yazdırılabilir.
* **ASCII dışı karakterler:** Motor Unicode’u destekler, ancak kaynak dosyanızın UTF‑8 olarak kaydedildiğinden emin olun, aksi takdirde eşleşme hataları alabilirsiniz.

## Hepsini Bir Araya Getirme – Tam, Çalıştırılabilir Örnek

Aşağıda `FindText.java` adıyla bir dosyaya kopyalayıp yapıştırabileceğiniz eksiksiz program yer alıyor. `sample.html` yolunun doğru olduğundan emin olun, `javac` ile derleyin ve `java` ile çalıştırın.

```java
import com.aspose.html.dom.*;
import com.aspose.html.services.search.*;

public class FindText {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/sample.html");

        // Step 2: Set up text search options (case‑insensitive, whole‑word only)
        TextSearchOptions searchOptions = new TextSearchOptions();
        searchOptions.setCaseSensitive(false);
        searchOptions.setWholeWord(true);

        // Step 3: Search for the desired word in the document
        TextSearchResult searchResult = document.searchText("Aspose", searchOptions);

        // Step 4: Output the total number of matches found
        System.out.println("Found " + searchResult.getCount() + " matches.");

        // Step 5: Iterate through each match and display the node name where it occurs
        for (TextRange range : searchResult.getRanges()) {
            System.out.println("Match at node: " + range.getStartNode().getNodeName());
        }
    }
}
```

**Beklenen çıktı** (örnek `sample.html` dosyasında “Aspose” kelimesi üç kez geçiyorsa):

```
Found 3 matches.
Match at node: span
Match at node: p
Match at node: div
```

Sonucu, `sample.html` dosyasını açıp ilgili elementleri manuel olarak kontrol ederek doğrulayabilirsiniz.

## Sık Sorulan Sorular & Pratik İpuçları

* **Birden fazla kelimeyi aynı anda aramam gerekir mi?**  
  `searchText` metodunu bir döngü içinde çalıştırın veya bir düzenli ifade oluşturup `setWholeWord` özelliğini devre dışı bırakan özel bir `TextSearchOptions` kullanın.

* **Bulunan kelimeleri değiştirebilir miyim?**  
  Kesinlikle. Bir `TextRange` elde ettikten sonra `range.getStartNode().setNodeValue("yeni metin")` çağırabilir veya Aspose’un sağladığı `replaceText` servisini kullanabilirsiniz.

* **Arama çoklu iş parçacığı (thread‑safe) mi?**  
  `HTMLDocument` örneği thread‑safe değildir, ancak her iş parçacığı için ayrı bir belge oluşturursanız güvenle kullanabilirsiniz.

* **Performans nasıl ölçeklenir?**  
  Birkaç megabayt altındaki belgeler milisaniyeler içinde aranır. Daha büyük dosyalar için belgeyi akış (stream) olarak işlemek veya CSS seçicileriyle arama kapsamını daraltmak akıllıca olur.

## Sonuç

Aspose for Java kullanarak **HTML içinde nasıl arama yapılacağını**, dosyanın yüklenmesinden **HTML’de metin arama**, **HTML’de kelime bulma**, **eşleşmeleri sayma** ve **aralıkları alma** aşamalarına kadar ele aldık. Kod kısa, API sezgisel ve artık daha karmaşık metin‑işleme boru hatları oluşturmak için sağlam bir temele sahipsiniz.

Bir sonraki adım için hazır mısınız? Çevreleyen paragrafı çıkarın, sonuçları CSV’ye aktarın ya da eşleşmeleri oluşturulan bir PDF’de vurgulayın. Tüm bu görevler, yeni öğrendiğiniz kavramlar üzerine doğal olarak inşa edilebilir.

Sorularınız varsa yorumlarda buluşalım—mutlu kodlamalar!


## İlgili Eğitimler

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}