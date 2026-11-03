---
category: general
date: 2026-05-31
description: HTML kaynak yüklemesini kontrol etmek için ResourceHandlingOptions örneği
  oluşturun. Kaynak derinliğini nasıl sınırlayacağınızı ve özel seçeneklerle bir HTMLDocument'i
  nasıl yükleyeceğinizi öğrenin.
draft: false
keywords:
- create resourcehandlingoptions instance
- limit resource depth
- HTMLDocument options
- resource loading configuration
- python html parsing
language: tr
og_description: HTML kaynak yüklemesini kontrol etmek için ResourceHandlingOptions
  örneği oluşturun. Bu kılavuz, maksimum işleme derinliğini nasıl ayarlayacağınızı
  ve özel seçeneklerle bir HTMLDocument'i nasıl yükleyeceğinizi gösterir.
og_title: HTML Yükleme için ResourceHandlingOptions Örneği Oluştur
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create ResourceHandlingOptions instance to control HTML resource loading.
    Learn how to limit resource depth and load an HTMLDocument with custom options.
  headline: Create ResourceHandlingOptions Instance for HTML Loading
  type: TechArticle
tags:
- Python
- HTML parsing
- Resource handling
title: HTML Yükleme için ResourceHandlingOptions Örneği Oluştur
url: /tr/python/general/create-resourcehandlingoptions-instance-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML Yükleme için ResourceHandlingOptions Örneği Oluşturma

Büyük bir HTML sayfasının ayrıştırıcınızı bozmasını önlemek için **ResourceHandlingOptions örneği oluşturmanın** nasıl olduğunu hiç merak ettiniz mi? Tek başınıza değilsiniz—iç içe scriptler, çerçeveler veya eklemeler içeren büyük belgeler, basit bir kazıma işlemini bir kabusa dönüştürebilir.  

Bu öğreticide, bir `ResourceHandlingOptions` nesnesi oluşturmak, iç içeleme seviyesini sınırlamak ve bunu bir `HTMLDocument`'e beslemek için tam adımları göstereceğiz. Sonunda, **resource loading configuration** için temiz ve tekrarlanabilir bir desen elde edeceksiniz; bu, dünyanın herhangi bir boyutundaki HTML dosyasıyla çalışır.

## Öğrenecekleriniz

- `ResourceHandlingOptions` örneğinin büyük sayfaları ayrıştırırken neden önemli olduğunu.
- **resource depth** sınırlamasının sonsuz özyinelemeyi önlemek için nasıl kullanılacağını.
- Özel seçeneklerinizle bir `HTMLDocument` yüklemek için tam sözdizimini.
- Bugün projenize ekleyebileceğiniz tam, çalıştırılabilir bir örnek.

**Önkoşullar:** Python 3.8+, `HTMLDocument` ve `ResourceHandlingOptions` sağlayan `htmlparser` kütüphanesi. Başka bir bağımlılık gerekmez.

---

## Adım 1: ResourceHandlingOptions Örneği Oluşturma

İhtiyacınız olan ilk şey yeni bir `ResourceHandlingOptions` nesnesidir. Bunu, ayrıştırıcının karşılaşabileceği her dış kaynağın (scriptler, görüntüler, iframe'ler, ne isterseniz) kontrol paneli olarak düşünün.

```python
# Step 1: Initialize the options object
options = ResourceHandlingOptions()
```

> **Neden önemli:** Açık bir örnek olmadan ayrıştırıcı varsayılanlarına geri döner; bu genellikle “her şeyi yükle” anlamına gelir. Büyük sayfalarda bu varsayılan, gigabaytlarca bellek tüketebilir ve betiğinizi durdurabilir.

---

## Adım 2: Resource Depth'i Sınırlama

Sonra, seçeneklere ne kadar derine gitmek istediğimizi söylüyoruz. Örneğin `max_handling_depth` değerini 5 olarak ayarlamak, ayrıştırıcıyı iç içe beş seviye kaynak sonrası durdurur. Sayıyı kullanım durumunuza göre ayarlayın.

```python
# Step 2: Cap the nesting depth (e.g., stop after 5 levels)
options.max_handling_depth = 5
```

> **Pro ipucu:** Yalnızca üst seviye içeriğe ilgi duyuyorsanız, 1 veya 2 derinlik genellikle yeterlidir ve işlemi büyük ölçüde hızlandırır.

---

## Adım 3: Seçeneklerle HTML Belgesini Yükleme

Şimdi yapılandırılmış `options` nesnesini `HTMLDocument`'e veriyoruz. Yapıcı, dosya yolunu (veya URL'yi) ve seçenek nesnesini kabul eder; bu da neyin yükleneceği üzerinde ayrıntılı kontrol sağlar.

```python
# Step 3: Parse the HTML file using the configured options
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", options)
```

> **Gördükleriniz:** Ayrıştırıcı `big_page.html` dosyasını okuyacak, ancak derinliği 5'i aşacak herhangi bir kaynak sessizce yok sayılacak. Bu, kontrol dışı özyinelemeyi önler ve bellek kullanımını öngörülebilir tutar.

---

## Adım 4: Sonucu Doğrulama (İsteğe Bağlı ama Faydalı)

Belgenin beklendiği gibi yüklendiğini kontrol etmek iyi bir alışkanlıktır. Aşağıda, başarılı bir şekilde işlenen kaynakların sayısını yazdıran hızlı bir doğrulama örneği bulunmaktadır.

```python
# Step 4: Quick verification
print(f"Handled resources: {len(doc.resources)}")
print(f"Document title: {doc.title}")
```

**Beklenen çıktı** (girdi dosyasına bağlı olarak sayılarınız farklı olacaktır):

```
Handled resources: 12
Document title: Example Large Page
```

Eğer sayı beklediğinizden çok düşükse, `max_handling_depth` değerini artırmanız veya diğer `ResourceHandlingOptions` özelliklerini ayarlamanız gerekebilir.

---

## Yaygın Varyasyonlar ve Kenar Durumları

| Durum | Ayar |
|-----------|------------|
| **Sadece görüntüleri yok saymanız gerekiyor** | `options.ignore_images = True` olarak ayarlayın. |
| **Scriptler zaman aşımına neden oluyor** | `options.max_script_execution_time = 2` (saniye) kullanın. |
| **Bir dosya yerine uzak bir URL ayrıştırıyorsanız** | URL dizesini `HTMLDocument`'e dosya yolu gibi geçirin. |
| **Özel bir logger istiyorsunuz** | Yüklemeden önce `options.logger = my_logger` atayın. |

Bu ayarlamalar, **HTMLDocument options** araç setinin bir parçasıdır ve ayrıştırıcınızı yeniden yazmadan **resource loading configuration**'ı ince ayar yapmanızı sağlar.

---

## Tam Çalışan Örnek

Hepsini bir araya getirerek, şu anda çalıştırabileceğiniz bağımsız bir betik burada. `parse_big_page.py` olarak kaydedin ve `python parse_big_page.py` komutuyla çalıştırın.

```python
# parse_big_page.py
from htmlparser import HTMLDocument, ResourceHandlingOptions

def main():
    # 1️⃣ Create the options instance
    options = ResourceHandlingOptions()
    
    # 2️⃣ Limit how deep we go into nested resources
    options.max_handling_depth = 5
    
    # Optional: ignore images to speed things up
    # options.ignore_images = True
    
    # 3️⃣ Load the document with our custom options
    doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", options)
    
    # 4️⃣ Verify the load
    print(f"Handled resources: {len(doc.resources)}")
    print(f"Document title: {doc.title}")

if __name__ == "__main__":
    main()
```

Çalıştırdığınızda, kaynak sayısını ve başlığı yazdırdığını göreceksiniz; bu, **resourcehandlingoptions örneği oluşturduğunuzu** ve uyguladığınızı doğrular.

---

## Sonuç

Size **ResourceHandlingOptions örneği oluşturmanın**, iç içeleme seviyesini sınırlamanın ve bunu bir `HTMLDocument`'e vermenin nasıl yapılacağını gösterdik. Bu desen, herhangi bir büyük HTML dosyası için güvenilir **resource loading configuration** sağlar; Python HTML ayrıştırmanızı hızlı ve bellek‑dostu tutar.

Bir sonraki adıma hazır mısınız? Derinlik limitini değiştirin, `ignore_images`'ı açıp kapatın veya özel bir logger entegre edin—her ayar, **HTMLDocument options** ve veri hattınızla nasıl etkileşime girdiği konusunda size daha fazla şey öğretecek.  

Bu rehberi faydalı bulduysanız, paylaşmaktan, depoya yıldız vermekten veya kendi ipuçlarınızı yorum olarak bırakmaktan çekinmeyin. İyi ayrıştırmalar!

## Sonra Ne Öğrenmelisiniz?

- [C#'ta Dizeden HTML Oluşturma – Özel Kaynak İşleyici Kılavuzu](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [C#'ta HTML Kaydetme – Özel Kaynak İşleyici Kullanarak Tam Kılavuz](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [.NET'te Aspose.HTML ile Stream Provider Oluşturma](/html/english/net/advanced-features/create-stream-provider/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}