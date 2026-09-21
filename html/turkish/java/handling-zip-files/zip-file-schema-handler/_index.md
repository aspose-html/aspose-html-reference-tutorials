---
date: 2026-02-15
description: Aspose.HTML for Java kullanarak zip girişini nasıl okuyacağınızı öğrenin.
  Bu kılavuz, Java zip arşivi akışını ve özel bir şema işleyicisiyle Java zip dosyası
  yanıtını gösterir.
linktitle: ZIP File Schema Handler in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: ZIP Girişini Okuma Java – Aspose.HTML'de ZIP İşleyicisi
url: /tr/java/handling-zip-files/zip-file-schema-handler/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ZIP Girişi Java Okuma – Aspose.HTML'de ZIP İşleyicisi

## Giriş
Karmaşık HTML belgeleri veya web uygulamalarıyla çalışırken, ZIP arşivlerinin içinde bulunan kaynakları sunmak için **read zip entry java** yapmanız gerekebilir. Görselleri, betikleri veya stil sayfalarını doğrudan paketlenmiş bir ZIP dosyasından yükleyip normal bir web yanıtının parçası olarak sunmayı hayal edin—ekstra bir çıkarma adımına gerek yok. Aspose.HTML for Java'daki `ZIPFileSchemaMessageHandler` tam da bunu sağlar. Bu öğreticide, **java zip archive streaming** sağlayan ve `zip-file:` şemasını hedefleyen herhangi bir istek için uygun bir **java zip file response** döndüren özel bir şema işleyicisinin oluşturulmasını adım adım inceleyeceğiz.

## Hızlı Yanıtlar
- **Handler ne yapar?** Dosyaları disk üzerine çıkarmadan doğrudan bir ZIP arşivinden sunar.  
- **Hangi şema kullanılır?** `zip-file:` – Aspose.HTML ile kayıtlı özel bir URI şeması.  
- **Lisans gerekli mi?** Geliştirme için ücretsiz deneme çalışır; üretim için ticari bir lisans gereklidir.  
- **Büyük dosyaları işleyebilir mi?** Evet, giriş içeriğini akış olarak gönderir, bellek kullanımını en aza indirir.  
- **İş parçacığı güvenli mi?** İşleyici kendisi durum içermez; yalnızca temel ZIP dosyasının aynı anda değiştirilmediğinden emin olun.

## **read zip entry java** nedir?
Java'da bir ZIP girişini okumak, `.zip` konteyneri içinde belirli bir dosyayı bulmak ve verisini bir akış olarak elde etmek anlamına gelir. Standart `java.util.zip.ZipFile` sınıfı bu işlemi basitleştirir ve Aspose.HTML, bu mantığı özel bir şema işleyicisi aracılığıyla HTTP boru hattına eklemenizi sağlar.

## Neden **java zip archive streaming** kullanmalı?
Bir ZIP girişini akış olarak sunmak, tüm arşivin belleğe yüklenmesini önler; bu, yüksek trafikli web uygulamaları veya büyük varlıkların (ör. yüksek çözünürlüklü görseller veya video parçaları) sunulması için kritik öneme sahiptir. Bu yaklaşım ayrıca ZIP formatının bireysel girişlere rastgele erişimi desteklemesi sayesinde I/O yükünü azaltır.

## Önkoşullar
1. **Java Development Kit (JDK) 8+** yüklü.  
2. **IntelliJ IDEA**, **Eclipse** veya **NetBeans** gibi bir IDE.  
3. **Aspose.HTML for Java** kütüphanesi – **[buradan](https://releases.aspose.com/html/java/)** indirin ve JAR(ları) projenizin sınıf yoluna ekleyin.  
4. Java koleksiyonları ve istisna yönetimi konusunda temel bilgi.

## Paketleri İçe Aktarma
Aşağıdaki içe aktarmalar, Aspose.HTML ağ araçları, MIME işleme ve standart Java I/O sınıflarına erişim sağlar.

```java
import com.aspose.html.MimeType;
import com.aspose.html.net.INetworkOperationContext;
import com.aspose.html.net.ResponseMessage;
import com.aspose.html.net.StreamContent;
import com.aspose.html.utils.Stream;
```

## Adım 1: ZIP Dosyası Şema İşleyici Sınıfını Oluşturma
`CustomSchemaMessageHandler` sınıfını genişleterek başlarız. Yapıcı, özel `zip-file` şemasını kaydeder ve sunmak istediğimiz ZIP arşivinin yolunu saklar.

```java
public class ZIPFileSchemaMessageHandler extends CustomSchemaMessageHandler {
    private final String archive;
    protected ZIPFileSchemaMessageHandler(String archive) {
        super("zip-file");
        this.archive = archive;
    }
}
```

## Adım 2: `invoke` Metodunu Geçersiz Kılma
`invoke` metodu, `zip-file:` şemasını kullanan her isteği yakalar. İstenen yolu ayıklar, ilgili girişi bir akış olarak alır ve bir **java zip file response** oluşturur. Giriş bulunamazsa 404 yanıtı döndürülür.

```java
@Override
public void invoke(INetworkOperationContext context) {
    String pathInsideArchive = context.getRequest().getRequestUri().getPathname().substring(1).replaceAll("\\\\", "/");
    Stream stream = GetFile(pathInsideArchive);
    if (stream != null) {
        // If the file is found, return it as a response
        ResponseMessage response = new ResponseMessage(200);
        response.setContent(new StreamContent(stream));
        response.getHeaders().getContentType().setMediaType(MimeType.fromFileExtension(context.getRequest().getRequestUri().getPathname()));
        context.setResponse(response);
    } else {
        // If the file is not found, return a 404 error
        context.setResponse(new ResponseMessage(404));
    }
    // Invoke the next handler in the chain
    invoke(context);
}
```

## Adım 3: `GetFile` Metodunu Uygulama
`GetFile`, arşiv içindeki girişi bulmak ve Aspose `Stream` olarak döndürmek için standart `java.util.zip.ZipFile` API'sini kullanır. **read zip entry java** işleminin gerçekleştiği yerdir.

```java
Stream GetFile(String path) {
    try (ZipFile zipFile = new ZipFile(archive)) {
        ZipEntry entry = zipFile.getEntry(path);
        if (entry != null) {
            InputStream inputStream = zipFile.getInputStream(entry);
            return new Stream(inputStream);
        }
    } catch (IOException e) {
        e.printStackTrace();
    }
    return null;
}
```

## Yaygın Sorunlar ve Çözümler
| Sorun | Neden Oluşur | Çözüm |
|-------|--------------|-------|
| **Büyük dosyalarda `IOException`** | Varsayılan tampon çok küçük olabilir. | Tampon boyutunu artırın veya akış için `java.nio` kanallarını kullanın. |
| **Yanlış MIME türü** | `MimeType.fromFileExtension` bilinmeyen uzantılar için `application/octet-stream` döndürebilir. | Bilinen içerik türlerinize göre MIME tipini manuel olarak ayarlayın. |
| **İş parçacığı güvenliği endişeleri** | Tek bir `ZipFile` örneğinin birden çok iş parçacığı arasında paylaşılması `ZipException`a neden olabilir. | `GetFile` içinde yeni bir `ZipFile` açın (gösterildiği gibi) böylece her istek kendi tutamacını alır. |
| **Eksik giriş 404 döndürür** | Yol normalleştirme sorunları (ör. baştaki eğik çizgi). | `substring(1)` çağrısı baştaki eğik çizgiyi kaldırır; istek URI'sinin arşivin iç yapısıyla eşleştiğinden emin olun. |

## Sıkça Sorulan Sorular

### Bu işleyiciyi RAR veya TAR gibi diğer arşiv formatları için kullanabilir miyim?
Şu anda işleyici yalnızca ZIP dosyaları için tasarlanmıştır. Ancak, bazı değişikliklerle diğer arşiv formatlarını da işleyebilecek şekilde uyarlanabilir.

### ZIP dosyası bozuk olursa ne olur?
ZIP dosyası bozuksa, işleyici dosyaları alamaz ve muhtemelen bir `IOException` ile karşılaşırsınız. Uygulamanızın kararlı kalmasını sağlamak için bu tür istisnaları ele almanız gerekir.

### Bu işleyiciyle ZIP arşivindeki dosyaları değiştirmek mümkün mü?
Hayır, bu işleyici yalnızca ZIP arşivindeki dosyaları okumak için tasarlanmıştır, değiştirmek için değil.

### Büyük dosyaları sunma performansını nasıl artırabilirim?
Büyük dosyalar için bellek kullanımını azaltmak ve performansı artırmak amacıyla dosya parçalama veya akış tekniklerini uygulamayı düşünün.

### Bu işleyici çok iş parçacıklı bir ortamda kullanılabilir mi?
Evet, ancak özellikle ZIP dosyası gibi paylaşılan kaynaklarla çalışırken iş parçacığı güvenliğini sağlamalısınız.

---

**Son Güncelleme:** 2026-02-15  
**Test Edilen:** Aspose.HTML for Java 24.11 (yazım anındaki en yeni sürüm)  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}