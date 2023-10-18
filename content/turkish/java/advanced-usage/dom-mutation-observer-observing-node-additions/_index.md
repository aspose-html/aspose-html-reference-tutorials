---
title: Aspose.HTML for Java ile DOM Mutasyon Gözlemcisi
linktitle: DOM Mutation Observer - Düğüm Eklemelerini Gözlemleme
second_title: Aspose.HTML ile Java HTML İşleme
description: Bu adım adım kılavuzda DOM Mutation Observer'ı uygulamak için Aspose.HTML for Java'yı nasıl kullanacağınızı öğrenin. DOM değişikliklerini etkili bir şekilde izleyin ve bunlara tepki verin.
type: docs
weight: 11
url: /tr/java/advanced-usage/dom-mutation-observer-observing-node-additions/
---

Bir HTML belgesinin Belge Nesne Modelindeki (DOM) değişiklikleri gözlemlemek ve bunlara tepki vermek isteyen bir Java geliştiricisi misiniz? Aspose.HTML for Java bu görev için güçlü bir çözüm sunar. Bu adım adım kılavuzda, bir HTML belgesi oluşturmak ve Mutation Observer ile düğüm eklemelerini gözlemlemek için Aspose.HTML for Java'nın nasıl kullanılacağını keşfedeceğiz. Bu eğitim, her örneği birden fazla adıma ayırarak süreç boyunca size yol gösterecektir. Sonunda, DOM Mutation Observers'ı Java projelerinize kolaylıkla uygulayabileceksiniz.

## Önkoşullar

Aspose.HTML for Java kullanımına geçmeden önce gerekli önkoşulların mevcut olduğundan emin olalım:

1. Java Geliştirme Ortamı: Sisteminizde Java Geliştirme Kitinin (JDK) kurulu olduğundan emin olun.

2.  Aspose.HTML for Java: Aspose.HTML for Java'yı indirip yüklemeniz gerekecek. İndirme linkini bulabilirsiniz[Burada](https://releases.aspose.com/html/java/).

3. IDE (Entegre Geliştirme Ortamı): Java kodunu yazmak ve çalıştırmak için IntelliJ IDEA veya Eclipse gibi tercih ettiğiniz Java IDE'yi kullanın.

## Paketleri İçe Aktar

Aspose.HTML for Java'yı kullanmaya başlamak için gerekli paketleri Java kodunuza aktarmanız gerekir. Bunu nasıl yapabileceğiniz aşağıda açıklanmıştır:

```java
// Gerekli paketleri içe aktar
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.mutations.MutationObserver;
import com.aspose.html.dom.mutations.MutationCallback;
import com.aspose.html.dom.mutations.MutationRecord;
import com.aspose.html.dom.mutations.MutationObserverInit;
import com.aspose.html.dom.Element;
import com.aspose.html.dom.Text;
import com.aspose.html.generic.IGenericList;

// Boş bir HTML belgesi oluşturun
HTMLDocument document = new HTMLDocument();
```

Artık gerekli paketleri içe aktardığınıza göre, Java'da DOM Mutation Observer'ı uygulamaya yönelik adım adım kılavuza geçelim.

## Adım 1: Mutasyon Gözlemcisi Örneği Oluşturun

Öncelikle bir Mutation Observer örneği oluşturmanız gerekir. Bu gözlemci DOM'daki değişiklikleri izleyecek ve mutasyonlar meydana geldiğinde bir geri arama işlevi yürütecektir.

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

Bu adımda, DOM'a düğümler eklendiğinde mesaj yazdıran geri çağırma işlevine sahip bir gözlemci oluşturuyoruz.

## Adım 2: Observer'ı yapılandırın

Şimdi gözlemciyi istenilen seçeneklerle yapılandıralım. Karakter verilerindeki değişikliklerin yanı sıra alt liste değişikliklerini ve alt ağaç değişikliklerini de gözlemlemek istiyoruz.

```java
MutationObserverInit config = new MutationObserverInit();
config.setChildList(true);
config.setSubtree(true);
config.setCharacterData(true);

// Belirtilen konfigürasyonla gözlemlemek için hedef düğüme geçin
observer.observe(document.getBody(), config);
```

 Burada ayarları yapıyoruz`config` Alt liste, alt ağaç ve karakter verisi değişikliklerinin gözlemlenmesini sağlayan nesne. Daha sonra hedef düğüme geçeriz (bu durumda belgenin`<body>`) ve gözlemciye konfigürasyon.

## 3. Adım: DOM'yi değiştirin

Şimdi gözlemciyi tetiklemek için DOM'da bazı değişiklikler yapacağız. Bir paragraf öğesi oluşturacağız ve onu belgenin gövdesine ekleyeceğiz.

```java
// Bir paragraf öğesi oluşturun ve bunu belge gövdesine ekleyin
Element p = document.createElement("p");
document.getBody().appendChild(p);

// Bir metin oluşturun ve onu paragrafa ekleyin
Text text = document.createTextNode("Hello World");
p.appendChild(text);
```

Bu adımda bir HTML paragraf öğesi oluşturup onu belgenin gövdesine ekliyoruz. Daha sonra "Merhaba Dünya" içeriğine sahip bir metin düğümü oluşturup onu paragrafa ekliyoruz.

## Adım 4: Gözlemleri Bekleyin (Eşzamansız)

Mutasyonlar eş zamanlı olarak gözlemlenmediğinden gözlemcinin değişiklikleri yakalaması için bir süre beklememiz gerekir. kullanacağız`synchronized` Ve`wait` bu amaçla aşağıda gösterildiği gibi.

```java
// Mutasyonlar eşzamansız modda çalıştığından birkaç saniye bekleyin
synchronized (this) {
    wait(5000);
}
```

Burada gözlemcinin herhangi bir mutasyonu yakalama şansına sahip olmasını sağlamak için 5 saniye bekliyoruz.

## Adım 5: Gözlemlemeyi Durdurun

Son olarak, gözlemlemeyi bitirdiğinizde, kaynakları serbest bırakmak için gözlemcinin bağlantısını kesmek önemlidir.

```java
// Gözlemlemeyi bırak
observer.disconnect();
```

Bu adımla gözlemi tamamladınız ve kaynakları temizleyebilirsiniz.

## Çözüm

Bu eğitimde, DOM Mutation Observer'ı uygulamak için Aspose.HTML for Java kullanma sürecini anlattık. Bir gözlemci oluşturmayı, onu yapılandırmayı, DOM'da değişiklik yapmayı, gözlemleri beklemeyi ve gözlemlemeyi nasıl durduracağınızı öğrendiniz. Artık, HTML belgelerinin DOM'undaki değişiklikleri etkili bir şekilde izlemek ve bunlara tepki vermek için Java projelerinizde DOM Mutasyon Gözlemcilerini uygulama becerisine sahipsiniz.

Herhangi bir sorunuz varsa veya sorunla karşılaşırsanız, yardım istemekten çekinmeyin.[Aspose.HTML forumu](https://forum.aspose.com/) . Ek olarak, şuraya erişebilirsiniz:[dokümantasyon](https://reference.aspose.com/html/java/) Aspose.HTML for Java hakkında ayrıntılı bilgi için.

## SSS'ler

### S1: DOM Mutasyon Gözlemcisi nedir?

Cevap1: DOM Mutasyon Gözlemcisi, bir HTML belgesinin Belge Nesne Modelindeki (DOM) değişiklikleri izlemenize olanak tanıyan bir JavaScript özelliğidir. DOM düğümlerinin eklenmesine, silinmesine veya değiştirilmesine gerçek zamanlı olarak tepki vermenin bir yolunu sağlar.

### S2: Aspose.HTML for Java'yı ticari projelerimde kullanabilir miyim?

 Cevap2: Evet, Aspose.HTML for Java'yı ticari projelerde kullanabilirsiniz. Lisanslama ve satın alma bilgilerini bulabilirsiniz[Burada](https://purchase.aspose.com/buy).

### S3: Aspose.HTML for Java'nın ücretsiz deneme sürümü mevcut mu?

 Cevap3: Evet, Aspose.HTML for Java'nın ücretsiz deneme sürümünü edinebilirsiniz[Burada](https://releases.aspose.com/). Bu, satın alma işlemi yapmadan önce özelliklerini ve yeteneklerini keşfetmenizi sağlar.

### S4: Karakter verisi değişikliklerini Mutation Observer ile gözlemlemenin faydası nedir?

Cevap4: Karakter verisi değişikliklerini gözlemlemek, HTML öğelerinin metin içeriğindeki değişiklikleri izlemek ve bunlara tepki vermek istediğiniz senaryolar için kullanışlıdır. Örneğin, bunu web formlarındaki kullanıcı girişini izlemek ve yanıtlamak için kullanabilirsiniz.

### S5: Aspose.HTML for Java'yı kullanırken kaynakları nasıl elden çıkarabilirim?

 C5: İşiniz bittiğinde kaynakları serbest bırakmak önemlidir. Örneğimizde kullandık`document.dispose()` HTML belgesiyle ilişkili kaynakları temizlemek için. Bellek sızıntılarını önlemek için oluşturduğunuz tüm nesneleri ve kaynakları attığınızdan emin olun.