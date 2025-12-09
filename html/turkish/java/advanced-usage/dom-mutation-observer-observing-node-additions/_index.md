---
date: 2025-11-30
description: Aspose.HTML'in Mutation Observer'ını kullanarak Java'da gövdeye öğe eklemeyi
  ve DOM değişikliklerini izlemeyi öğrenin. HTML belgesi oluşturma adımlarını ve mutation
  observer'ı devre dışı bırakmayı içerir.
linktitle: Append Element to Body - Observing Node Additions
second_title: Java HTML Processing with Aspose.HTML
title: Aspose.HTML for Java ile DOM Mutasyon Gözlemcisi Kullanarak Gövdeye Eleman
  Ekle
url: /tr/java/advanced-usage/dom-mutation-observer-observing-node-additions/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML for Java ile DOM Mutation Observer Kullanarak Gövdeye Eleman Ekleme

Eğer DOM'da gerçekleşen her değişikliği gözlemleyerek **append element to body** yapmanız gereken bir Java geliştiricisiyseniz, doğru yerdesiniz. Aspose.HTML for Java, **create HTML document Java** nesnelerini oluşturmayı, bir Mutation Observer eklemeyi ve düğümler eklendiğinde, kaldırıldığında veya değiştirildiğinde anında tepki vermeyi kolaylaştırır. Bu adım‑adım öğreticide, belgeyi kurmaktan **disconnect mutation observer**'ı temiz bir şekilde yapmaya kadar tüm süreci ele alacağız; böylece Java uygulamalarınızda DOM değişikliklerini güvenle izleyebilirsiniz.

## Hızlı Yanıtlar
- **Mutation Observer ne yapar?** DOM ağacını izler ve düğüm eklemeleri, kaldırmaları veya özellik değişiklikleri hakkında sizi bilgilendirir.  
- **Java'da bunu sağlayan kütüphane hangisidir?** Aspose.HTML for Java, tam özellikli bir Mutation Observer API'si içerir.  
- **Üretim için lisansa ihtiyacım var mı?** Evet, ticari kullanım için geçerli bir Aspose.HTML lisansı gereklidir.  
- **Metin düğümlerindeki değişiklikleri izleyebilir miyim?** Kesinlikle—observer yapılandırmasında `characterData`'yı `true` olarak ayarlayın.  
- **Observer'ı nasıl durdururum?** `observer.disconnect()` metodunu, izlemeyi bitirdiğinizde çağırın.

## Aspose.HTML bağlamında “append element to body” nedir?
Bir elemanı `<body>` etiketine eklemek, programlı olarak belgenin ana içerik alanına yeni bir düğüm (örneğin bir `<p>` veya `<div>`) eklemek anlamına gelir. Mutation Observer ile birleştirildiğinde, bu eklemeyi anında tespit edebilir ve özel mantığı tetikleyebilirsiniz—dinamik HTML üretimi, test veya sunucu‑tarafı render senaryoları için mükemmeldir.

## Java'da Mutation Observer Neden Kullanılır?
- **Gerçek zamanlı izleme:** DOM değişiklikleri gerçekleşir gerçekleşmez tepki verin.  
- **Daha temiz kod:** Manuel sorgulama veya karmaşık olay işleme gerekmez.  
- **Çapraz platform tutarlılığı:** HTML'i bir tarayıcıda ya da sunucuda render etseniz aynı şekilde çalışır.  
- **Performans:** Observer'lar verimlidir ve asenkron çalışır, ana iş parçacığınızı serbest tutar.

## Önkoşullar
1. **Java Development Kit (JDK)** – 8 veya üzeri.  
2. **Aspose.HTML for Java** – resmi siteden en son sürümü indirin.  
3. **IDE** – IntelliJ IDEA, Eclipse veya herhangi bir Java‑uyumlu editör.  

Aspose.HTML for Java'yi indirme sayfasından [burada](https://releases.aspose.com/html/java/) edinebilirsiniz.

## Paketleri İçe Aktarma
İlk olarak, ihtiyacınız olan sınıfları içe aktarın. Bu aynı zamanda daha sonra dolduracağımız boş bir HTML belgesi oluşturur.

```java
// Import necessary packages
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.mutations.MutationObserver;
import com.aspose.html.dom.mutations.MutationCallback;
import com.aspose.html.dom.mutations.MutationRecord;
import com.aspose.html.dom.mutations.MutationObserverInit;
import com.aspose.html.dom.Element;
import com.aspose.html.dom.Text;
import com.aspose.html.generic.IGenericList;

// Create an empty HTML document
HTMLDocument document = new HTMLDocument();
```

## Adım 1: Mutation Observer Örneği Oluşturma (mutation observer java)
Bir **Mutation Observer**, bir mutasyon gerçekleştiğinde çağrılacak bir geri çağırma (callback) gerektirir. Geri çağırmamızda, eklenen her düğüm için sadece bir mesaj yazdırıyoruz.

```java
MutationObserver observer = new MutationObserver(new MutationCallback() {
    @Override
    public void invoke(IGenericList<MutationRecord> mutations, MutationObserver mutationObserver) {
        mutations.forEach(mutationRecord -> {
            mutationRecord.getAddedNodes().forEach(node -> {
                synchronized (this) {
                    System.out.println("The '" + node + "' node was added to the document.");
                    notifyAll();
                }
            });
        });
    }
});
```

## Adım 2: Observer'ı Yapılandırma (monitor dom changes java)
Observer'a **neyi** izleyeceğini söylüyoruz—çocuk liste değişiklikleri, alt ağaç (subtree) değişiklikleri ve karakter verisi güncellemeleri.

```java
MutationObserverInit config = new MutationObserverInit();
config.setChildList(true);
config.setSubtree(true);
config.setCharacterData(true);

// Pass in the target node to observe with the specified configuration
observer.observe(document.getBody(), config);
```

## Adım 3: Gövdeye Eleman Ekleme ve Observer'ı Tetikleme
Şimdi gerçekten **append element to body** yapıyoruz. Bir metin düğümü içeren `<p>` elemanını eklemek, daha önce kurduğumuz observer'ı tetikleyecek.

```java
// Create a paragraph element and append it to the document body
Element p = document.createElement("p");
document.getBody().appendChild(p);

// Create a text and append it to the paragraph
Text text = document.createTextNode("Hello World");
p.appendChild(text);
```

## Adım 4: Gözlemler İçin Bekleme (asynchronous handling)
Mutasyonlar asenkron olarak raporlanır, bu yüzden observer'ın değişikliği işlemesi için kısa bir süre bekliyoruz.

```java
// Since mutations are working in async mode, wait for a few seconds
synchronized (this) {
    wait(5000);
}
```

## Adım 5: Observer'ı Bağlantısını Kesme (disconnect mutation observer)
İzlemeyi bitirdiğinizde, her zaman **disconnect mutation observer** yaparak kaynakları serbest bırakın.

```java
// Stop observing
observer.disconnect();
```

## Yaygın Tuzaklar ve İpuçları
- **Never forget to disconnect** – observer'ların çalışır halde bırakılması bellek sızıntılarına yol açabilir.  
- **Thread safety:** Geri çağırma arka plan iş parçacığında çalışır; paylaşılan veriyi değiştiriyorsanız uygun senkronizasyon kullanın.  
- **Observe the right node:** `document.getBody()`'ı izlemek çoğu UI değişikliğini yakalar, ancak daha ince izleme için herhangi bir elementi hedefleyebilirsiniz.  
- **Pro tip:** Özellik değişikliklerini de izlemek istiyorsanız `config.setAttributes(true)` kullanın.

## Sıkça Sorulan Sorular

**Q: DOM Mutation Observer nedir?**  
A: DOM ağacını düğüm eklemeleri, kaldırmaları veya özellik güncellemeleri gibi değişiklikler için izleyen bir API'dir; bu olayları bir geri çağırma aracılığıyla iletir.

**Q: Aspose.HTML for Java'yi ticari projelerde kullanabilir miyim?**  
A: Evet, geçerli bir Aspose.HTML lisansı ile. Satın alma detayları [burada](https://purchase.aspose.com/buy) mevcuttur.

**Q: Aspose.HTML for Java için ücretsiz deneme sürümü var mı?**  
A: Kesinlikle—deneme sürümünü [release sayfasından](https://releases.aspose.com/) indirebilirsiniz.

**Q: Karakter verisi değişikliklerini nasıl izlerim?**  
A: Observer yapılandırmasında, Adım 2'de gösterildiği gibi `config.setCharacterData(true)` ayarlayın.

**Q: Gözlemeyi bitirdikten sonra ne yapmalıyım?**  
A: `observer.disconnect()` (Adım 5) çağırın ve bir `HTMLDocument` oluşturduysanız, yerel kaynakları serbest bırakmak için `document.dispose()` ile yok edin.

## Sonuç
Artık **append element to body**, bir **mutation observer java** kurma ve Aspose.HTML for Java kullanarak **monitor DOM changes java** yapmayı öğrendiniz. Bu adımları izleyerek sunucu‑tarafı Java uygulamalarınızda herhangi bir DOM mutasyonunu güvenilir bir şekilde tespit edip tepki verebilirsiniz. Farklı düğüm tipleri, özellik izlemeleri veya daha karmaşık senaryolar için birden fazla observer ile denemeler yapmaktan çekinmeyin.

Herhangi bir sorunla karşılaşırsanız, topluluk [Aspose.HTML forumunda](https://forum.aspose.com/) size yardımcı olmaya hazırdır. Daha derin API detayları için resmi [Aspose.HTML for Java belgelerine](https://reference.aspose.com/html/java/) bakın.

---

**Son Güncelleme:** 2025-11-30  
**Test Edilen Versiyon:** Aspose.HTML for Java 24.11  
**Yazar:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}