---
date: 2026-01-07
description: Aspose.HTML for Java kullanarak EPUB'u XPS'ye zahmetsizce dönüştürün.
  Sorunsuz bir dönüşüm süreci için bu adım adım kılavuzu izleyin.
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

Günümüz dijital yayıncılık dünyasında **convert EPUB to XPS** yaygın bir gereksinimdir—ister baskı, arşivleme ya da Windows cihazları arasında paylaşım için sabit‑düzen bir temsil ihtiyacınız olsun. Aspose.HTML for Java bu dönüşümü sorunsuz bir şekilde gerçekleştirir ve özel bir bellek akışı sağlayıcı kullanarak tüm süreci bellekte tutabilirsiniz; bu, bulut‑tabanlı veya yüksek‑performanslı senaryolar için mükemmeldir. Aşağıda, ön koşullardan tam çalışan bir örneğe kadar ihtiyacınız olan her şeyi bulacaksınız.

## Hızlı Yanıtlar
- **Dönüşüm ne üretir?** Düzeni ve yazı tiplerini koruyan bir XPS belgesi.  
- **Lisans gerekli mi?** Test için ücretsiz deneme yeterlidir; üretim için ticari lisans gerekir.  
- **Bunu bir konteyner içinde çalıştırabilir miyim?** Evet—her şeyi bellekte tutarsanız dosya sistemi yazımı gerekmez.  
- **Hangi Java sürümü destekleniyor?** Java 8 ve üzeri.  
- **Özel bir akış sağlayıcı zorunlu mu?** Hayır, ancak bellek kullanımı ve çıktı yönetimi üzerinde tam kontrol sağlar.

## “convert EPUB to XPS” nedir?
Bir EPUB dosyasını XPS'ye dönüştürmek, yeniden akışlanabilir e‑kitap formatını sabit‑düzen, cihaz‑bağımsız bir belgeye çevirir. XPS (XML Paper Specification), Microsoft'un PDF'e karşılığıdır ve platformlar arasında değişmeyen görsel bir temsil gerektiğinde idealdir.

## Neden özel bir akış sağlayıcı kullanmalı?
Özel bir `MemoryStreamProvider`, dönüşüm sonucunu geçici bir dosyaya yazmak yerine RAM'de tutmanıza olanak tanır. Bu yaklaşım:
- G/Ç yükünü azaltır.
- Sunucusuz veya mikro‑servis mimarilerinde performansı artırır.
- Sonucu doğrudan bir istemciye, bulut depolamaya veya başka bir API'ye akıtma esnekliği sağlar.

## Ön Koşullar

**convert EPUB to XPS** işlemini sorunsuz bir şekilde gerçekleştirmek için aşağıdaki ön koşulları sağlayın:

### 1. Aspose.HTML for Java Kütüphanesi  

Aspose.HTML for Java kütüphanesinin Java ortamınıza kurulu ve yapılandırılmış olması gerekir. Henüz indirmediyseniz, kütüphaneyi [download link](https://releases.aspose.com/html/java/) adresinden edinebilirsiniz.

### 2. Giriş EPUB Dosyası  

Dönüştürmek istediğiniz mevcut bir EPUB dosyasına ihtiyacınız var. Dönüşüm sürecine başlamadan bu dosyanın hazır olduğundan emin olun.

Tüm ön koşulları tamamladığınıza göre, dönüşüm adımlarını adım adım inceleyelim.

## Paketleri İçe Aktarma

Başlamadan önce, Aspose.HTML for Java işlevlerini kullanabilmek için gerekli paketleri içe aktarın.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.XpsSaveOptions;
import com.aspose.html.saving.MemoryStreamProvider;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
```

## EPUB Dosyasını Açma

Mevcut EPUB dosyasını okuma amaçlı açmanız gerekir. Bu adımda `FileInputStream` kullanarak EPUB dosyasına erişiyoruz.

```java
try (FileInputStream fileInputStream = new FileInputStream("path/to/your/input.epub")) {
    // Your code for Step 1
}
```

## MemoryStreamProvider Oluşturma

Sonra bir `MemoryStreamProvider` örneği oluşturun. Bu nesne dönüşüm çıktısını bellek içinde tutacaktır.

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
    // Your code for Step 2
}
```

## EPUB'u XPS'ye Dönüştürme

Şimdi `Converter.convertEPUB` metodunu kullanarak EPUB dosyasını XPS'ye dönüştürün. `MemoryStreamProvider` hedef akışı sağlar.

```java
Converter.convertEPUB(
    fileInputStream,
    new XpsSaveOptions(),
    streamProvider.getStream().findFirst().get()
);
```

## Sonuç Verisini Alma

Dönüşüm tamamlandıktan sonra XPS verisini içeren bellek akışını alın.

```java
InputStream inputStream = streamProvider.getStream().findFirst().get();
```

## Çıktıyı Kaydetme (İsteğe Bağlı)

Fiziksel bir dosyaya ihtiyaç duyarsanız—örneğin hata ayıklama veya çevrimdışı inceleme için—bellek akışını diske yazabilirsiniz. Çoğu üretim senaryosunda bu adımı atlayıp veriyi doğrudan istemciye akıtabilirsiniz.

```java
try (FileOutputStream fileOutputStream = new FileOutputStream("path/to/your/output.xps")) {
    byte[] buffer = new byte[inputStream.available()];
    inputStream.read(buffer);
    fileOutputStream.write(buffer);
}
```

## Tam Kaynak Kodu

Aşağıda tüm parçaları bir araya getiren, çalıştırılabilir tam örnek yer almaktadır. Kopyalayıp projenize uyarlamaktan çekinmeyin.

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
|-------|--------------|------|
| **`java.lang.OutOfMemoryError`** | Büyük EPUB dosyaları, tamamen bellek içinde tutulduğunda varsayılan yığın boyutunu aşabilir. | JVM yığın boyutunu (`-Xmx`) artırın veya mümkünse EPUB'u parçalara bölerek işleyin. |
| **XPS'te eksik yazı tipleri** | EPUB içinde gömülü olmayan yazı tipleri dönüşüm makinesinde mevcut değildir. | Gerekli yazı tiplerinin sunucuda kurulu olduğundan emin olun veya EPUB'a gömün. |
| **`MemoryStreamProvider`'dan `UnsupportedOperationException`** | Eski bir Aspose.HTML sürümü kullanılıyor. | Aspose.HTML for Java'nın en son sürümüne güncelleyin. |

## Sık Sorulan Sorular

### 1. EPUB nedir?

EPUB, Electronic Publication (Elektronik Yayın) kısaltmasıdır ve e‑kitaplar için yaygın olarak kullanılan bir dosya formatıdır. Çeşitli cihazlarda—e‑okuyucular, tabletler, akıllı telefonlar—kolayca okunacak şekilde tasarlanmıştır.

### 2. XPS nedir?

XPS, XML Paper Specification (XML Kağıt Spesifikasyonu) anlamına gelir ve Microsoft tarafından oluşturulmuş bir belge formatıdır. Tutarlı görünüm ve düzenle belge paylaşımı ve arşivleme için kullanılır.

### 3. Neden Aspose.HTML for Java kullanılmalı?

Aspose.HTML for Java, belge manipülasyonu, dönüşüm ve render işlemlerini basitleştiren güçlü bir kütüphanedir. Çok çeşitli belge formatları için kapsamlı özellikler ve destek sunar; bu da geliştiriciler için değerli bir araçtır.

### 4. Aspose.HTML for Java ile başka belge formatları da dönüştürülebilir mi?

Evet, Aspose.HTML for Java HTML, EPUB, XPS ve daha fazlası dahil olmak üzere çeşitli belge formatlarının dönüşümünü destekler. Belgelerin yönetimi için çok yönlü bir araçtır.

### 5. Ek kaynaklar ve destek nereden bulunabilir?

Dokümantasyon ve destek için [Aspose.HTML for Java documentation](https://reference.aspose.com/html/java/) ve [support forum](https://forum.aspose.com/) adreslerini ziyaret edin.

---

**Son Güncelleme:** 2026-01-07  
**Test Edilen Sürüm:** Aspose.HTML for Java 24.12 (yazım anındaki en yeni sürüm)  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}