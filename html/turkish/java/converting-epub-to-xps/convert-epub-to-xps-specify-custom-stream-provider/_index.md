---
date: 2026-03-29
description: Aspose.HTML for Java kullanarak EPUB'u XPS'ye zahmetsizce nasıl dönüştüreceğinizi
  öğrenin. Sorunsuz bir dönüşüm süreci için bu adım adım kılavuzu izleyin.
linktitle: How to Convert EPUB to XPS with a Custom Stream Provider
second_title: Java HTML Processing with Aspose.HTML
title: Özel Bir Akış Sağlayıcı ile EPUB'u XPS'e Nasıl Dönüştürülür
url: /tr/java/converting-epub-to-xps/convert-epub-to-xps-specify-custom-stream-provider/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Özel Bir Akış Sağlayıcı ile EPUB'u XPS'ye Dönüştürme

Günümüz dijital yayıncılık dünyasında, **EPUB'u XPS'ye nasıl dönüştürülür** sorusu sıkça karşımıza çıkar—baskı, arşivleme veya Windows cihazları arasında paylaşım için sabit‑düzen bir temsil gerekebilir. Aspose.HTML for Java bu dönüşümü basitleştirir ve özel bir bellek akışı sağlayıcı kullanarak tüm süreci bellekte tutabilirsiniz; bu, bulut‑tabanlı veya yüksek‑performanslı senaryolar için mükemmeldir. Aşağıda, önkoşullardan tam çalışan bir örneğe kadar ihtiyacınız olan her şeyi bulacaksınız.

## Hızlı Yanıtlar
- **Dönüşüm ne üretiyor?** Düzeni ve yazı tiplerini koruyan bir XPS belgesi.  
- **Lisans gerekli mi?** Ücretsiz deneme sürümü test için çalışır; üretim için ticari lisans gereklidir.  
- **Bunu bir konteyner içinde çalıştırabilir miyim?** Evet—her şey bellekte tutulursa dosya sistemi yazımı gerekmez.  
- **Hangi Java sürümü destekleniyor?** Java 8 ve üzeri.  
- **Özel bir akış sağlayıcı zorunlu mu?** Hayır, ancak bellek kullanımı ve çıktı işleme üzerinde tam kontrol sağlar.

## EPUB'u XPS'ye Nasıl Dönüştürülür
Kodun içine dalmadan önce, dönüşümün gerçekte ne yaptığını ve neden her şeyi bellekte tutmak isteyebileceğinizi açıklayalım.

### “EPUB'u XPS'ye dönüştürmek” nedir?
Bir EPUB dosyasını XPS'ye dönüştürmek, yeniden akışlanabilir bir e‑kitap formatını sabit‑düzen, cihaz‑bağımsız bir belgeye çevirir. XPS (XML Paper Specification), Microsoft'un PDF'e karşılık gelen formatıdır; platformlar arasında değişmeyen görsel bir temsil gerektiğinde idealdir.

### Neden özel bir akış sağlayıcı kullanmalı?
Özel bir `MemoryStreamProvider`, dönüşüm sonucunu geçici bir dosyaya yazmak yerine RAM'de tutmanıza olanak tanır. Bu yaklaşım:
- I/O yükünü azaltır.  
- Sunucusuz veya mikro hizmet mimarilerinde performansı artırır.  
- Sonucu doğrudan bir istemciye, bulut depolamaya veya başka bir API'ye akıtma esnekliği sağlar.

## Önkoşullar

EPUB'u XPS'ye **başarıyla dönüştürmek** için aşağıdaki önkoşulları yerine getirdiğinizden emin olun:

### 1. Aspose.HTML for Java Kütüphanesi  

Java ortamınıza Aspose.HTML for Java kütüphanesini kurmuş ve yapılandırmış olmalısınız. Henüz yapmadıysanız, kütüphaneyi [indirme bağlantısı](https://releases.aspose.com/html/java/) üzerinden indirebilirsiniz.

### 2. Giriş EPUB Dosyası  

Dönüştürmek istediğiniz mevcut bir EPUB dosyanız olmalı. Bu dosyayı dönüşüm sürecine hazır bulundurun.

Şimdi tüm önkoşullara sahip olduğunuza göre, dönüşüm adımlarını adım adım inceleyelim.

## Paketleri İçe Aktar

Başlamadan önce, Aspose.HTML for Java'nın işlevlerini kullanabilmek için gerekli paketleri içe aktardığınızdan emin olun.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.XpsSaveOptions;
import com.aspose.html.saving.MemoryStreamProvider;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
```

## EPUB Dosyasını Aç

Mevcut EPUB dosyasını okumak için önce açmanız gerekir. Bu adımda, EPUB dosyasına erişmek için bir `FileInputStream` kullanıyoruz.

```java
try (FileInputStream fileInputStream = new FileInputStream("path/to/your/input.epub")) {
    // Your code for Step 1
}
```

## MemoryStreamProvider Oluştur

Sonra, `MemoryStreamProvider` örneğini oluşturun. Bu nesne, dönüşüm çıktısını bellek içinde tutacaktır.

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
    // Your code for Step 2
}
```

## EPUB'u XPS'ye Dönüştür

Şimdi, `Converter.convertEPUB` metodunu kullanarak EPUB dosyasını XPS'ye dönüştürün. `MemoryStreamProvider` hedef akışı sağlar.

```java
Converter.convertEPUB(
    fileInputStream,
    new XpsSaveOptions(),
    streamProvider.getStream().findFirst().get()
);
```

## Elde Edilen Veriyi Al

Dönüşüm tamamlandıktan sonra, XPS verisini içeren bellek akışını alın.

```java
InputStream inputStream = streamProvider.getStream().findFirst().get();
```

## Çıktıyı Kaydet (İsteğe Bağlı)

Fiziksel bir dosyaya ihtiyacınız varsa—belki hata ayıklama veya çevrimdışı inceleme için—bellek akışını diske yazın. Çoğu üretim senaryosunda bu adımı atlayıp veriyi doğrudan istemciye akıtabilirsiniz.

```java
try (FileOutputStream fileOutputStream = new FileOutputStream("path/to/your/output.xps")) {
    byte[] buffer = new byte[inputStream.available()];
    inputStream.read(buffer);
    fileOutputStream.write(buffer);
}
```

## Tam Kaynak Kodu

Aşağıda, tüm parçaları bir araya getiren tam, çalıştırılabilir örnek bulunmaktadır. Projenize kopyalayıp yapıştırabilir ve ihtiyacınıza göre uyarlayabilirsiniz.

```java
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of MemoryStreamProvider
            try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
                // Convert EPUB to XPS by using the MemoryStreamProvider
                com.aspose.html.converters.Converter.convertEPUB(
                        fileInputStream,
                        new com.aspose.html.saving.XpsSaveOptions(),
                        streamProvider.lStream
                );
                // Get access to the memory stream that contains the resulted data
                java.io.InputStream inputStream = streamProvider.lStream.stream().findFirst().get();
                // Flush the result data to the output file
                try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("output.xps"))) {
                    byte[] buffer = new byte[inputStream.available()];
                    inputStream.read(buffer);
                    fileOutputStream.write(buffer);
                }
            }
        }
```

## Yaygın Sorunlar ve Çözümler

| Sorun | Neden Oluşur | Çözüm |
|-------|----------------|-----|
| **`java.lang.OutOfMemoryError`** | Büyük EPUB dosyaları, tamamen bellek içinde tutulduğunda varsayılan yığın boyutunu aşabilir. | JVM yığın boyutunu (`-Xmx`) artırın veya mümkünse EPUB'u parçalara bölerek işleyin. |
| **Missing fonts in XPS** | EPUB içinde gömülü olmayan yazı tipleri, dönüşüm makinesinde mevcut değildir. | Gerekli yazı tiplerinin sunucuya yüklendiğinden emin olun veya EPUB içinde gömülü olduğundan emin olun. |
| **`UnsupportedOperationException` from `MemoryStreamProvider`** | Eski bir Aspose.HTML sürümü kullanılıyor. | En son Aspose.HTML for Java sürümüne güncelleyin. |

## Sıkça Sorulan Sorular

### 1. EPUB Nedir?
EPUB, Electronic Publication (Elektronik Yayın) kısaltmasıdır ve e‑kitaplar için yaygın kullanılan bir dosya formatıdır. e‑okuyucular, tabletler ve akıllı telefonlar gibi çeşitli cihazlarda kolayca okunabilir şekilde tasarlanmıştır.

### 2. XPS Nedir?
XPS, XML Paper Specification (XML Kağıt Spesifikasyonu) anlamına gelir ve Microsoft tarafından oluşturulan bir belge formatıdır. Tutarlı görünüm ve düzenle belgeleri paylaşmak ve arşivlemek için kullanılır.

### 3. Neden Aspose.HTML for Java Kullanmalı?
Aspose.HTML for Java, belge manipülasyonu, dönüşüm ve render işlemlerini basitleştiren güçlü bir kütüphanedir. Çeşitli belge formatları için kapsamlı özellikler ve destek sunar, bu da geliştiriciler için değerli bir araçtır.

### 4. Aspose.HTML for Java ile diğer belge formatlarını dönüştürebilir miyim?
Evet, Aspose.HTML for Java HTML, EPUB, XPS ve daha fazlası dahil olmak üzere çeşitli belge formatlarının dönüşümünü destekler. Belge yönetimi için çok yönlü bir araçtır.

### 5. Ek kaynakları ve desteği nereden bulabilirim?
Dokümantasyon ve destek için [Aspose.HTML for Java dokümantasyonu](https://reference.aspose.com/html/java/) ve [destek forumu](https://forum.aspose.com/) adreslerini ziyaret edin.

---

**Son Güncelleme:** 2026-03-29  
**Test Edilen:** Aspose.HTML for Java 24.12 (yazım anındaki en yeni sürüm)  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}