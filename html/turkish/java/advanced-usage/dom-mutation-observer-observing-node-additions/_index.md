---
title: Java için Aspose.HTML ile DOM Mutasyon Gözlemcisi
linktitle: DOM Mutasyon Gözlemcisi - Düğüm Eklemelerini Gözlemleme
second_title: Aspose.HTML ile Java HTML İşleme
description: Bu adım adım kılavuzda DOM Mutation Observer'ı uygulamak için Aspose.HTML for Java'yı nasıl kullanacağınızı öğrenin. DOM değişikliklerini etkili bir şekilde izleyin ve bunlara tepki verin.
type: docs
weight: 11
url: /tr/java/advanced-usage/dom-mutation-observer-observing-node-additions/
---

Bir HTML belgesinin Belge Nesne Modeli'ndeki (DOM) değişiklikleri gözlemlemek ve bunlara tepki vermek isteyen bir Java geliştiricisi misiniz? Java için Aspose.HTML bu görev için güçlü bir çözüm sunar. Bu adım adım kılavuzda, bir HTML belgesi oluşturmak ve Mutation Observer ile düğüm eklemelerini gözlemlemek için Java için Aspose.HTML'i nasıl kullanacağınızı keşfedeceğiz. Bu eğitim, her örneği birden fazla adıma bölerek sizi süreçte yönlendirecektir. Sonunda, Java projelerinizde DOM Mutation Observer'ları kolaylıkla uygulayabileceksiniz.

## Ön koşullar

Java için Aspose.HTML'i kullanmaya başlamadan önce, gerekli ön koşulların mevcut olduğundan emin olalım:

1. Java Geliştirme Ortamı: Sisteminizde Java Geliştirme Kiti'nin (JDK) yüklü olduğundan emin olun.

2.  Java için Aspose.HTML: Java için Aspose.HTML'i indirip yüklemeniz gerekecektir. İndirme bağlantısını bulabilirsiniz[Burada](https://releases.aspose.com/html/java/).

3. IDE (Bütünleşik Geliştirme Ortamı): Java kodu yazmak ve çalıştırmak için IntelliJ IDEA veya Eclipse gibi tercih ettiğiniz Java IDE'sini kullanın.

## Paketleri İçe Aktar

Java için Aspose.HTML'i kullanmaya başlamak için gerekli paketleri Java kodunuza aktarmanız gerekir. Bunu şu şekilde yapabilirsiniz:

```java
// Gerekli paketleri içe aktarın
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

Artık gerekli paketleri içe aktardığımıza göre, Java'da DOM Mutation Observer'ı uygulamaya yönelik adım adım kılavuza geçelim.

## Adım 1: Mutasyon Gözlemcisi Örneği Oluşturun

Öncelikle bir Mutation Observer örneği oluşturmanız gerekir. Bu gözlemci DOM'daki değişiklikleri izleyecek ve mutasyonlar meydana geldiğinde bir geri çağırma işlevini yürütecektir.

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

Bu adımda, DOM'a düğümler eklendiğinde bir mesaj yazdıran bir geri çağırma işlevine sahip bir gözlemci oluşturuyoruz.

## Adım 2: Gözlemciyi Yapılandırın

Şimdi, gözlemciyi istenilen seçeneklerle yapılandıralım. Çocuk listesi değişikliklerini ve alt ağaç değişikliklerini ve karakter verilerindeki değişiklikleri gözlemlemek istiyoruz.

```java
MutationObserverInit config = new MutationObserverInit();
config.setChildList(true);
config.setSubtree(true);
config.setCharacterData(true);

// Belirtilen yapılandırmayla gözlemlemek için hedef düğümü geçirin
observer.observe(document.getBody(), config);
```

 Burada, şunu ayarladık:`config` nesne, çocuk listesini, alt ağacı ve karakter veri değişikliklerini gözlemlemeyi etkinleştirir. Daha sonra hedef düğümü (bu durumda, belgenin`<body>`) ve yapılandırmayı gözlemciye iletir.

## Adım 3: DOM'u değiştirin

Şimdi, gözlemciyi tetiklemek için DOM'da bazı değişiklikler yapacağız. Bir paragraf öğesi oluşturacağız ve bunu belgenin gövdesine ekleyeceğiz.

```java
// Bir paragraf öğesi oluşturun ve bunu belge gövdesine ekleyin
Element p = document.createElement("p");
document.getBody().appendChild(p);

// Bir metin oluşturun ve onu paragrafa ekleyin
Text text = document.createTextNode("Hello World");
p.appendChild(text);
```

Bu adımda bir HTML paragraf öğesi oluşturup bunu belgenin gövdesine ekliyoruz. Daha sonra, "Hello World" içeriğine sahip bir metin düğümü oluşturup bunu paragrafa ekliyoruz.

## Adım 4: Gözlemleri Bekleyin (Eşzamansız)

Mutasyonlar eş zamanlı olarak gözlemlendiğinden, gözlemcinin değişiklikleri yakalamasına izin vermek için bir an beklememiz gerekir.`synchronized` Ve`wait` Bu amaçla aşağıda gösterildiği gibi.

```java
// Mutasyonlar asenkron modda çalıştığı için birkaç saniye bekleyin
synchronized (this) {
    wait(5000);
}
```

Burada gözlemcinin herhangi bir mutasyonu yakalama şansına sahip olduğundan emin olmak için 5 saniye bekliyoruz.

## Adım 5: Gözlemlemeyi bırakın

Son olarak, gözlemlemeyi bitirdiğinizde kaynakları serbest bırakmak için gözlemcinin bağlantısını kesmeniz önemlidir.

```java
// Gözlemlemeyi bırak
observer.disconnect();
```

Bu adımla gözlemi tamamlamış olursunuz ve kaynakları temizleyebilirsiniz.

## Çözüm

Bu eğitimde, Java için Aspose.HTML'i kullanarak bir DOM Mutation Observer uygulama sürecini ele aldık. Bir gözlemci oluşturmayı, yapılandırmayı, DOM'da değişiklikler yapmayı, gözlemleri beklemeyi ve gözlemlemeyi durdurmayı öğrendiniz. Artık, HTML belgelerinin DOM'undaki değişiklikleri etkili bir şekilde izlemek ve bunlara tepki vermek için Java projelerinizde DOM Mutation Observer'ları uygulama becerisine sahipsiniz.

Herhangi bir sorunuz varsa veya sorunla karşılaşırsanız, yardım istemekten çekinmeyin.[Aspose.HTML forumu](https://forum.aspose.com/) Ek olarak, şunlara erişebilirsiniz:[belgeleme](https://reference.aspose.com/html/java/) Java için Aspose.HTML hakkında detaylı bilgi için.

## SSS

### S1: DOM Mutasyon Gözlemcisi nedir?

A1: DOM Mutation Observer, bir HTML belgesinin Belge Nesne Modeli'ndeki (DOM) değişiklikleri izlemenize olanak tanıyan bir JavaScript özelliğidir. DOM düğümlerinin eklenmesine, silinmesine veya değiştirilmesine gerçek zamanlı olarak tepki vermenin bir yolunu sağlar.

### S2: Ticari projelerimde Aspose.HTML for Java'yı kullanabilir miyim?

 A2: Evet, ticari projelerde Java için Aspose.HTML kullanabilirsiniz. Lisanslama ve satın alma bilgilerini bulabilirsiniz[Burada](https://purchase.aspose.com/buy).

### S3: Aspose.HTML for Java için ücretsiz deneme sürümü mevcut mu?

 A3: Evet, Java için Aspose.HTML'nin ücretsiz deneme sürümünü edinebilirsiniz[Burada](https://releases.aspose.com/). Bu, satın alma işlemi yapmadan önce özelliklerini ve yeteneklerini keşfetmenizi sağlar.

### S4: Mutation Observer ile karakter verilerindeki değişiklikleri gözlemlemenin faydası nedir?

A4: Karakter verisi değişikliklerini gözlemlemek, HTML öğelerinin metin içeriğindeki değişiklikleri izlemek ve bunlara tepki vermek istediğiniz senaryolar için yararlıdır. Örneğin, bunu web formlarındaki kullanıcı girdisini izlemek ve bunlara yanıt vermek için kullanabilirsiniz.

### S5: Java için Aspose.HTML kullanırken kaynakları nasıl imha edebilirim?

 A5: İşiniz bittiğinde kaynakları serbest bırakmak önemlidir. Örneğimizde,`document.dispose()` HTML belgesiyle ilişkili kaynakları temizlemek için. Bellek sızıntılarını önlemek için oluşturduğunuz tüm nesneleri ve kaynakları elden çıkardığınızdan emin olun.