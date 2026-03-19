---
category: general
date: 2026-03-18
description: HTML'yi PDF'ye hızlı bir şekilde dönüştürmek için sabit iş parçacığı
  havuzu oluşturun. Toplu HTML'den PDF'ye dönüştürmeyi öğrenin, HTML'yi PDF olarak
  kaydedin ve Aspose.HTML ile birden fazla HTML dosyasını dönüştürün.
draft: false
keywords:
- create fixed thread pool
- convert html to pdf
- batch html to pdf
- save html as pdf
- convert multiple html files
language: tr
og_description: HTML'yi PDF'ye verimli bir şekilde dönüştürmek için sabit iş parçacığı
  havuzu oluşturun. Bu rehber, toplu HTML'den PDF'ye dönüştürme, HTML'yi PDF olarak
  kaydetme ve birden fazla dosyayla başa çıkma konularında size yol gösterir.
og_title: Paralel HTML‑to‑PDF Dönüşümü için Sabit İş Parçacığı Havuzu Oluştur
tags:
- Java
- Multithreading
- Aspose.HTML
- PDF conversion
title: Java'da Paralel HTML‑PDF Dönüştürme için Sabit İş Parçacığı Havuzu Oluştur
url: /tr/java/conversion-html-to-other-formats/create-fixed-thread-pool-for-parallel-html-to-pdf-conversion/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Paralel HTML‑to‑PDF Dönüşümü için Sabit İş Parçacığı Havuzu Oluşturma

Hiç **create fixed thread pool**'u nasıl **convert HTML to PDF**'yi yıldırım hızıyla yapabileceğini merak ettiniz mi? Tek başınıza değilsiniz—geliştiriciler, bir klasördeki raporların bir gecede PDF'ye dönüştürülmesi gerektiğinde sürekli bir engelle karşılaşıyor.  

İyi haber şu ki, bir işçi iş parçacığı havuzu oluşturabilir, her HTML dosyasını Aspose.HTML'ye verebilir ve JVM'nin ağır işi yapmasına izin verebilirsiniz. Bu öğreticide HTML'yi PDF'ye toplu olarak dönüştüreceğiz, HTML'yi PDF olarak kaydedeceğiz ve **convert multiple HTML files**'ı CPU'nuzu zorlamadan nasıl yapacağınızı göstereceğiz.

## İhtiyacınız Olanlar

- Java 17 veya daha yeni (kod herhangi bir yeni JDK'da çalışır)  
- Aspose.HTML for Java 23.9 (veya en son sürüm) – kullanacağımız `Converter` sınıfını içerir  
- PDF'ye dönüştürmek istediğiniz birkaç `.html` dosyası  
- Favori IDE'niz veya basit bir metin editörü  

Hepsi bu. Classpath'te Aspose.HTML JAR'ı dışında harici bir yapı aracı gerekmez.

## Adım 1: İşlemek İstediğiniz HTML Dosyalarını Listeleyin  

İlk olarak, bir kaynak dosya koleksiyonuna ihtiyacınız var. Bunu dönüşüm işiniz için bir “alışveriş listesi” olarak düşünün.

```java
// Step 1 – define the files that will be turned into PDFs
String[] htmlFileNames = {
        "YOUR_DIRECTORY/input1.html",
        "YOUR_DIRECTORY/input2.html",
        "YOUR_DIRECTORY/input3.html",
        "YOUR_DIRECTORY/input4.html"
};
```

Neden listeyi bir dizi içinde tutuyoruz? Basit, tip‑güvenli ve daha sonra temiz bir `for‑each` döngüsüyle yinelememizi sağlıyor. Eğer isimleri bir dizinden okumanız gerekirse, sadece diziyi `Files.list(Paths.get("YOUR_DIRECTORY"))…` ile değiştirin.

## Adım 2: **Create Fixed Thread Pool**'u CPU'nuzun Boyutuna Göre Oluşturun  

Şimdi gerçekten **create fixed thread pool**'u oluşturuyoruz. Havuz boyutu, mantıksal çekirdek sayısıyla eşleşir; bu genellikle işletim sistemini aç bırakmadan en iyi verimi sağlar.

```java
// Step 2 – spin up a fixed thread pool based on available processors
ExecutorService executor = Executors.newFixedThreadPool(
        Runtime.getRuntime().availableProcessors());
```

*Pro tip:* Dönüşümünüz I/O‑ağırlıklıysa (diskten büyük HTML dosyaları okuma), havuz boyutunu biraz artırabilirsiniz. Ancak CPU‑ağır renderleme için, çekirdek sayısıyla eşleşmek en ideal noktadır.

![Diagram of a fixed thread pool handling HTML‑to‑PDF tasks](/images/create-fixed-thread-pool-diagram.png "create fixed thread pool illustration")

*Alt text:* HTML dosyalarının PDF'ye paralel dönüşümünü gösteren create fixed thread pool diyagramı.

## Adım 3: Her Dosya İçin **Convert HTML to PDF** Görevi Gönderin  

Havuz hazır olduğunda, her HTML yolunu bir işçi iş parçacığına veririz. Lambda içinde Aspose.HTML’nin `Converter.convertDocument` metodunu çağırırız; bu, sayfayı render etme ve PDF yazma işini üstlenir.

```java
// Step 3 – enqueue a conversion job for every HTML file
for (String sourcePath : htmlFileNames) {
    executor.submit(() -> {
        String destinationPath = sourcePath.replace(".html", ".pdf");
        try {
            // Convert HTML to PDF using Aspose.HTML
            Converter.convertDocument(sourcePath, destinationPath, new PdfSaveOptions());
            System.out.println("Converted: " + sourcePath);
        } catch (Exception e) {
            // Wrap checked exceptions to avoid cluttering the lambda
            throw new RuntimeException(e);
        }
    });
}
```

Neden istisna sarmalıyoruz? Lambdalar, bir try‑catch olmadan denetimli istisnalar fırlatamaz ve `RuntimeException` olarak yeniden fırlatmak, kodu özlü tutar ve yine de hataları konsolda gösterir.

## Adım 4: Havuzu Zarifçe Kapatın ve **Convert Multiple HTML Files**  

Tüm işler kuyruğa alındıktan sonra, yürütücüye yeni iş kabul etmemesini ve her iş parçacığı bitene kadar beklemesini söyleriz. Bu, **batch HTML to PDF**'yi bırakılan iş parçacıkları olmadan temiz bir şekilde yapmanın yoludur.

```java
// Step 4 – stop accepting new tasks and wait for completion
executor.shutdown();
executor.awaitTermination(5, TimeUnit.MINUTES);
```

Zaman aşımı dolarsa, program bir uyarı ile çıkar—kontrolsüz bir süreç istemediğiniz CI boru hatları için mükemmeldir.

## Sonucu Doğrulama – **Save HTML as PDF**  

Program tamamlandığında, orijinal `.html` dosyalarının yanında bir dizi `.pdf` dosyası görmelisiniz. Herhangi birini açın; düzenin, CSS'in ve görsellerin korunduğunu fark edeceksiniz—modern bir renderleyiciyle **save HTML as PDF** yaptığınızda beklediğiniz tam olarak bu.

```text
$ ls YOUR_DIRECTORY
input1.html  input1.pdf  input2.html  input2.pdf  ...
```

Eğer bir PDF eksikse, istisna yığını izini görmek için konsol çıktısını kontrol edin. Yaygın tuzaklar şunlardır:

- Sunucuda eksik yazı tipleri (Aspose.HTML varsayılan bir yazı tipine geri döner, ancak görünüm değişebilir)  
- Çalışma dizininden çözülemeyen göreli görsel yolları  
- Son derece büyük HTML sayfaları için yetersiz bellek (JVM yığınını `-Xmx2g` ile artırın)

## Gerçek Dünya Kullanımı için İpuçları ve Püf Noktaları  

| Situation | Recommendation |
|-----------|----------------|
| **Büyük toplu işlem (1000+ dosya)** | `LinkedBlockingQueue` ile sınırlı bir kuyruk kullanın ve `OutOfMemoryError` oluşmasını önlemek için görevleri parçalar halinde gönderin. |
| **Farklı çıktı dizinleri** | `destinationPath`'i `Paths.get(outputDir, filename + ".pdf")` ile hesaplayın. |
| **Özel PDF ayarları** | Varsayılan yerine yapılandırılmış bir `PdfSaveOptions` (örneğin `setCompress(true)` ayarlayın) geçirin. |
| **`System.out` yerine logging** | Üretim seviyesinde loglar için SLF4J veya Log4j ekleyin. |
| **Hata yönetimi** | Başarısız dosyaları bir listede toplayın ve ana çalışmanın bitiminden sonra yeniden deneyin. |

Bu ayarlamalar, bir üretim ortamında **convert multiple HTML files**'ı güvenilir bir şekilde yapmanızı sağlar.

## Tam Çalışan Örnek  

Aşağıda eksiksiz, çalıştırmaya hazır Java sınıfı bulunuyor. `ParallelBatch.java` dosyasına kopyalayıp yapıştırın, classpath'inize Aspose.HTML JAR'ı ekleyin ve `java ParallelBatch` komutunu çalıştırın.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.PdfSaveOptions;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.TimeUnit;

public class ParallelBatch {
    public static void main(String[] args) throws Exception {

        // Step 1: List the HTML files to be converted
        String[] htmlFileNames = {
                "YOUR_DIRECTORY/input1.html",
                "YOUR_DIRECTORY/input2.html",
                "YOUR_DIRECTORY/input3.html",
                "YOUR_DIRECTORY/input4.html"
        };

        // Step 2: Create a fixed thread pool sized to the number of CPU cores
        ExecutorService executor = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());

        // Step 3: Submit a conversion task for each HTML file
        for (String sourcePath : htmlFileNames) {
            executor.submit(() -> {
                String destinationPath = sourcePath.replace(".html", ".pdf");
                try {
                    // Convert the HTML document to PDF using Aspose.HTML
                    Converter.convertDocument(sourcePath, destinationPath, new PdfSaveOptions());
                    System.out.println("Converted: " + sourcePath);
                } catch (Exception e) {
                    // Wrap any checked exception as an unchecked one for simplicity
                    throw new RuntimeException(e);
                }
            });
        }

        // Step 4: Shut down the pool and wait for all conversions to finish
        executor.shutdown();
        executor.awaitTermination(5, TimeUnit.MINUTES);
    }
}
```

Çalıştırın, ve konsolda her dosyanın onaylandığını göreceksiniz:

```
Converted: YOUR_DIRECTORY/input1.html
Converted: YOUR_DIRECTORY/input2.html
...
```

## Sonuç  

Size Java'da **create fixed thread pool**'u nasıl oluşturacağınızı ve bunu paralel olarak **convert HTML to PDF** yapmak için nasıl kullanacağınızı gösterdik. İşleri toplu hâle getirerek, **convert multiple HTML files**'ı verimli bir şekilde yapabilir, CPU'nuzu mutlu tutabilir ve sevk için hazır düzenli bir PDF seti elde edebilirsiniz.  

Sonra, daha gelişmiş Aspose.HTML özelliklerini keşfedebilirsiniz—örneğin yazı tiplerini gömmek, filigran eklemek veya oluşturulan PDF'leri tek bir raporda birleştirmek. Ya da ölçeklendirme konusunda meraklıysanız, yerel iş parçacığı havuzunu ForkJoinPool gibi dağıtık bir yürütücü veya bulut tabanlı bir iş kuyruğu ile değiştirebilirsiniz.  

Bir deneyin, havuz boyutunu ayarlayın ve uygulamanızın bir sonraki HTML rapor yığınıyla terlemeden başa çıkmasına izin verin. İyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}