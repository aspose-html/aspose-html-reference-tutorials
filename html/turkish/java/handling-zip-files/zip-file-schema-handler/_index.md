---
date: 2026-06-29
description: Aspose.HTML for Java kullanarak zip entry java nasıl okunur ve zip arşivlerinden
  dosyalar nasıl sunulur öğrenin. Bu kılavuz, java zip archive streaming ve java zip
  file response'ı özel bir schema handler ile gösterir.
keywords:
- read zip entry java
- serve files from zip
- java zip archive streaming
- custom schema handler
- Aspose.HTML for Java
linktitle: Aspose.HTML'de ZIP File Schema Handler
schemas:
- author: Aspose
  dateModified: '2026-06-29'
  description: Learn how to read zip entry java using Aspose.HTML for Java and serve
    files from zip archives. This guide shows java zip archive streaming and java
    zip file response with a custom schema handler.
  headline: Read ZIP Entry Java – ZIP Handler in Aspose.HTML
  type: TechArticle
- description: Learn how to read zip entry java using Aspose.HTML for Java and serve
    files from zip archives. This guide shows java zip archive streaming and java
    zip file response with a custom schema handler.
  name: Read ZIP Entry Java – ZIP Handler in Aspose.HTML
  steps:
  - name: '**Java Development Kit (JDK) 8+** installed.'
    text: '**Java Development Kit (JDK) 8+** installed.'
  - name: An IDE such as **IntelliJ IDEA**, **Eclipse**, or **NetBeans**.
    text: An IDE such as **IntelliJ IDEA**, **Eclipse**, or **NetBeans**.
  - name: '**Aspose.HTML for Java** library – download it **[here](https://releases.aspose.com/html/java/)**
      and add the JAR(s) to your project’s classpath.'
    text: '**Aspose.HTML for Java** library – download it **[here](https://releases.aspose.com/html/java/)**
      and add the JAR(s) to your project’s classpath.'
  - name: Basic familiarity with Java collections and exception handling.
    text: Basic familiarity with Java collections and exception handling.
  type: HowTo
- questions:
  - answer: The current implementation targets ZIP files only. You can adapt the logic
      by swapping `java.util.zip.ZipFile` with a library that supports RAR/TAR, but
      you’ll need to handle their specific entry‑lookup APIs.
    question: Can I use this handler for other archive formats like RAR or TAR?
  - answer: A corrupted archive triggers an `IOException` during `GetFile`. Catch
      the exception and return a 500 response with a diagnostic message to keep the
      application stable.
    question: What happens if the ZIP file is corrupted?
  - answer: No. This handler is read‑only; it streams entries to the client. For write‑back
      scenarios you would need a separate writer component that creates a new ZIP
      file.
    question: Is it possible to modify files within the ZIP archive using this handler?
  - answer: Implement HTTP range requests by checking the `Range` header and sending
      partial streams. This allows browsers to request file chunks, reducing perceived
      latency.
    question: How can I improve performance when serving very large files?
  - answer: Yes, provided each request creates its own `ZipFile` instance (as shown).
      Avoid sharing mutable state between threads.
    question: Can this handler be used safely in a multi‑threaded environment?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: ZIP Girişini Java ile Okuma – Aspose.HTML'de ZIP Handler
url: /tr/java/handling-zip-files/zip-file-schema-handler/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ZIP Girişi Java Okuma – Aspose.HTML'de ZIP İşleyicisi

## Giriş
Web uygulaması geliştirirken, paketlenmiş bir ZIP dosyasından doğrudan resim, betik veya stil sayfalarını çekmeniz gerektiğinde, arşivi önce geçici bir klasöre çıkarmak için zaman harcamak istemezsiniz. **Read zip entry java**, istenen girdiyi doğrudan HTTP yanıtına akıtmanıza olanak tanır, bellek kullanımını düşük tutar ve gecikmeyi en aza indirir. Aspose.HTML for Java'da bu, `ZIPFileSchemaMessageHandler` ile sağlanır; bu, `zip-file:` URI şemasını anlayan ve içeriği anında sunan özel bir şema işleyicisidir. Aşağıda tam uygulamayı adım adım inceleyecek, akışın neden önemli olduğunu tartışacak ve işleyiciyi üretim yükleri için yeterince sağlam hale getirmenin yollarını göstereceğiz.

## Hızlı Yanıtlar
- **İşleyici ne yapar?** Dosyaları, disk üzerine çıkarmadan doğrudan bir ZIP arşivinden akış yanıtı kullanarak sunar.  
- **Hangi URI şeması kullanılıyor?** `zip-file:` – Aspose.HTML'in ağ katmanına kaydedilmiş özel bir şema.  
- **Lisans gerekli mi?** Geliştirme için ücretsiz deneme çalışır; üretim kullanımı için ticari bir lisans gereklidir.  
- **Büyük dosyaları işleyebilir mi?** Evet – girdinin içeriğini akıtarak, yüzlerce megabaytlık varlıklar bile düşük bellek ayak iziyle işlenir.  
- **İş parçacığı güvenli mi?** İşleyici kendisi durumsuzdur; yalnızca temel ZIP dosyasının aynı anda değiştirilmediğinden emin olun.

## Read zip entry java nedir?
Java'da bir ZIP girdisini okumak, `.zip` konteyneri içinde belirli bir dosyayı bulmak ve verisini bir akış olarak elde etmek anlamına gelir. `java.util.zip.ZipFile` sınıfı rastgele erişimli okuma sağlar, böylece tüm arşivi yüklemeden tek bir girdiyi çıkarabilirsiniz. Aspose.HTML, bu mantığı özel bir şema işleyicisi aracılığıyla HTTP boru hattına entegre etmenizi sağlar ve basit bir `zip-file:` URL'sini tam nitelikli bir HTTP yanıtına dönüştürür.

## Neden java zip arşivi akışı kullanılır?
Bir ZIP girdisini akıtarak, tüm arşivin belleğe yüklenmesi önlenir; bu, yüksek trafikli uygulamalar veya yüksek çözünürlüklü resimler ya da video parçaları gibi büyük varlıklar için hayati öneme sahiptir. Aspose.HTML, **2 GB**'a kadar dosyaları sunabilir ve on binlerce girdi içeren arşivleri JVM yığını kullanımını düşük tutarak işleyebilir. ZIP formatının rastgele erişimi, yalnızca gerekli baytların okunmasını sağlar.

## Önkoşullar
Kodun içine dalmadan önce şunların yüklü olduğundan emin olun:

1. **Java Development Kit (JDK) 8+** yüklü.  
2. **IntelliJ IDEA**, **Eclipse**, veya **NetBeans** gibi bir IDE.  
3. **Aspose.HTML for Java** kütüphanesi – **[here](https://releases.aspose.com/html/java/)** adresinden indirin ve JAR(ları) projenizin sınıf yoluna ekleyin.  
4. Java koleksiyonları ve istisna yönetimi konusunda temel bilgi.

## Paketleri İçe Aktar
Aşağıdaki içe aktarmalar, Aspose.HTML ağ yardımcılarını, MIME işleme ve standart Java I/O sınıflarına erişim sağlar.

```java
import com.aspose.html.MimeType;
import com.aspose.html.net.INetworkOperationContext;
import com.aspose.html.net.ResponseMessage;
import com.aspose.html.net.StreamContent;
import com.aspose.html.utils.Stream;
```

## Adım 1: ZIP Dosya Şema İşleyici Sınıfını Oluşturun
`CustomSchemaMessageHandler` Aspose.HTML'in özel URI şemalarını işlemek için temel sınıfıdır. Bunu genişleterek `zip-file` şemasını kaydedebilir ve diskteki fiziksel bir ZIP arşivine yönlendirebiliriz.

**Definition anchor:** `ZIPFileSchemaMessageHandler` belirli bir ZIP dosyasındaki girdilere `zip-file:` URI'lerini eşleyen somut işleyicidir.  

Yapıcı, ZIP arşivinin mutlak yolunu saklar ve şemayı `MessageHandlerRegistry` ile kaydeder. Bu kayıt, işleyiciyi Aspose.HTML'in dahili istek yönlendiricisine global olarak kullanılabilir kılar.

```java
public class ZIPFileSchemaMessageHandler extends CustomSchemaMessageHandler {
    private final String archive;
    protected ZIPFileSchemaMessageHandler(String archive) {
        super("zip-file");
        this.archive = archive;
    }
}
```

## Adım 2: `invoke` Metodunu Geçersiz Kılın
`invoke` metodu, `zip-file:` şemasıyla eşleşen her istek için çağrılır. İstek URI'sinden göreli yolu çıkarır, ilgili girdiyi bulur ve girdinin verisini istemciye akıtan bir HTTP yanıtı oluşturur.

**Definition anchor:** `invoke`, Aspose.HTML'in özel‑şema isteği işlenmesi gerektiğinde çağırdığı giriş noktasıdır.  

İstenen girdi mevcut değilse, metod faydalı bir düz metin mesajı içeren 404 yanıtı döndürür. Aksi takdirde, bir `MessageResponse` nesnesi oluşturur, uygun MIME tipini ayarlar ve girdi akışını ekler.

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

## Adım 3: `GetFile` Metodunu Uygulayın
`GetFile`, arşiv içindeki girdiyi bulmak ve Aspose `Stream` olarak döndürmek için standart `java.util.zip.ZipFile` API'sını kullanır. **read zip entry java** işleminin gerçekleştiği yerdir.

**Definition anchor:** `GetFile`, ZIP arşivini açar, istek yoluyla eşleşen `ZipEntry`'yi bulur ve onun `InputStream`'ini bir Aspose `Stream` içinde sarar.  

Metod ayrıca dosya uzantısına göre doğru MIME tipini belirler, böylece tarayıcılar resimleri, betikleri veya stilleri doğru şekilde render eder.

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
|-------|----------------|-----|
| **`IOException` on large files** | Varsayılan tampon çok küçük olabilir. | Tampon boyutunu artırın veya akış için `java.nio` kanallarını kullanın. |
| **Incorrect MIME type** | `MimeType.fromFileExtension`, bilinmeyen uzantılar için `application/octet-stream` döndürebilir. | Bilinen içerik tiplerinize göre MIME tipini manuel olarak ayarlayın. |
| **Thread‑safety concerns** | Tek bir `ZipFile` örneğinin iş parçacıkları arasında paylaşılması `ZipException`'a neden olabilir. | `GetFile` içinde yeni bir `ZipFile` açın (gösterildiği gibi) böylece her istek kendi tutamacını alır. |
| **Missing entry returns 404** | Yol normalleştirme sorunları (ör. baştaki eğik çizgi). | `substring(1)` çağrısı baştaki eğik çizgiyi kaldırır; istek URI'sinin arşivin iç yapısıyla eşleştiğinden emin olun. |

### Performans İpuçları
- **Tamponları yeniden kullan:** 64 KB'lık yeniden kullanılabilir bir `byte[]` tahsis edin ve GC baskısını azaltmak için akış kopyalama döngüsüne geçirin.  
- **Tembel yüklemeyi etkinleştir:** 4 GB'den büyük arşivlerle çalışırken `ZipFile`'ın `useZip64` bayrağını `true` olarak ayarlayın.  
- **MIME eşlemelerini önbellekle:** Tekrarlanan aramaları önlemek için yaygın uzantıların MIME tiplerine static bir harita oluşturun.

## Sıkça Sorulan Sorular

**Q: Bu işleyiciyi RAR veya TAR gibi diğer arşiv formatları için kullanabilir miyim?**  
A: Mevcut uygulama yalnızca ZIP dosyalarını hedefler. `java.util.zip.ZipFile` yerine RAR/TAR destekleyen bir kütüphane ile değiştirerek mantığı uyarlayabilirsiniz, ancak onların özel giriş‑arama API'lerini yönetmeniz gerekir.

**Q: ZIP dosyası bozulmuş olursa ne olur?**  
A: Bozuk bir arşiv, `GetFile` sırasında bir `IOException` tetikler. İstisnayı yakalayın ve uygulamanın kararlı kalması için tanı mesajı içeren 500 yanıtı döndürün.

**Q: Bu işleyici ile ZIP arşivindeki dosyaları değiştirmek mümkün mü?**  
A: Hayır. Bu işleyici yalnızca okuma amaçlıdır; girdileri istemciye akıtır. Yazma‑geri senaryoları için yeni bir ZIP dosyası oluşturan ayrı bir yazar bileşenine ihtiyaç duyarsınız.

**Q: Çok büyük dosyalar sunarken performansı nasıl artırabilirim?**  
A: `Range` başlığını kontrol ederek HTTP aralık isteklerini uygulayın ve kısmi akışlar gönderin. Bu, tarayıcıların dosya parçalarını talep etmesini sağlar ve algılanan gecikmeyi azaltır.

**Q: Bu işleyici çok iş parçacıklı bir ortamda güvenli bir şekilde kullanılabilir mi?**  
A: Evet, her isteğin kendi `ZipFile` örneğini oluşturması koşuluyla (gösterildiği gibi). İş parçacıkları arasında değiştirilebilir durumu paylaşmaktan kaçının.

{{< blocks/products/products-backtop-button >}}

## İlgili Eğitimler

- [Aspose.HTML for Java'da ZIP Arşivi Mesaj İşleyicisi](/html/java/handling-zip-files/zip-archive-message-handler/)
- [Aspose.HTML for Java ile özel şema işleyicisi nasıl oluşturulur](/html/java/custom-schema-message-handling/custom-schema-message-handler/)
- [Aspose.HTML for Java'da Özel Şema Filtresi ve Mesaj İşleme](/html/java/custom-schema-message-handling/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}