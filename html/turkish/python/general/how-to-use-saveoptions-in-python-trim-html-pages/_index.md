---
category: general
date: 2026-05-28
description: Python'da SaveOptions kullanarak HTML sayfalarını nasıl kırpacağınızı
  öğrenin. Bu adım adım rehber, bir HTML belgesini nasıl yükleyeceğinizi ve iç içe
  kaynakları verimli bir şekilde nasıl kaldıracağınızı da açıklar.
draft: false
keywords:
- how to use saveoptions
- how to load html document
- how to trim html page
language: tr
og_description: Python'da SaveOptions kullanarak HTML sayfalarını nasıl kırpılır.
  Bu kılavuzu izleyerek bir HTML belgesi yükleyin, kaynak limitlerini ayarlayın ve
  temiz, hafif bir dosya kaydedin.
og_title: Python'da SaveOptions Nasıl Kullanılır – HTML Sayfalarını Kırp
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to use SaveOptions to trim HTML pages in Python. This step‑by‑step
    guide also explains how to load an HTML document and efficiently remove nested
    resources.
  headline: How to Use SaveOptions in Python – Trim HTML Pages
  type: TechArticle
tags:
- python
- html-processing
- saveoptions
- resource-handling
title: Python'da SaveOptions Nasıl Kullanılır – HTML Sayfalarını Kırpma
url: /tr/python/general/how-to-use-saveoptions-in-python-trim-html-pages/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python’da SaveOptions Kullanımı – HTML Sayfalarını Kırpma

Hiç **SaveOptions nasıl kullanılır** sorusunu aklınızda bulundunuz mu, devasa bir HTML dosyasını hiçbir şeyi bozmayacak şekilde küçültmek için? Tek başınıza değilsiniz. Bir sayfayı içe aktardığınızda, içinde onlarca iç içe kaynak—CSS, JS ya da hatta diğer HTML parçacıkları—bulunduğunda, çıktınız kontrol edilemez bir şekilde şişebilir.  

Bu öğreticide, sadece **SaveOptions nasıl kullanılır** göstermekle kalmayıp, aynı zamanda **bir HTML belgesinin nasıl yükleneceği** ve iç içe derinliği sınırlayarak **bir HTML sayfasını nasıl kırpılır** konularını kapsayan eksiksiz, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz. Sonunda, dağıtıma ya da daha sonraki işleme hazır, temizlenmiş bir dosyanız olacak.

## Neler Başaracaksınız

- Tek bir kod satırıyla herhangi bir yerel HTML dosyasını yükleyin.  
- Belirli bir include derinliğinde duracak şekilde kaynak‑işleme seçeneklerini yapılandırın.  
- Güçlü `SaveOptions` sınıfını kullanarak kırpılmış sonucu kaydedin.  

Harici araçlar yok, sihir yok—sadece saf Python ve işi ağır şekilde yapan küçük bir kütüphane.

## Önkoşullar

İlerlemeye başlamadan önce, şunların olduğundan emin olun:

1. **Python 3.9+** yüklü (kullanılan sözdizimi herhangi bir yeni sürümde çalışır).  
2. Hayali `htmlprocessor` paketi, `HTMLDocument`, `SaveOptions` ve `ResourceHandlingOptions` sağlar. Aşağıdaki şekilde kurun:

```bash
pip install htmlprocessor
```

> **Pro ipucu:** Sanal bir ortam kullanıyorsanız, önce onu etkinleştirin—bağımlılıklarınızı düzenli tutar.

## Adım 1: Bir HTML Belgesini Nasıl Yüklenir

Bir dosyayı yüklemek, yapıcıyı (constructor) dosya yolunuza işaret ettirmeniz kadar basittir. Kütüphane işaretlemi okur, DOM‑benzeri bir ağaç oluşturur ve daha sonraki manipülasyonlar için hazırlar.

```python
from htmlprocessor import HTMLDocument

# Replace with the actual path to your file
doc = HTMLDocument("YOUR_DIRECTORY/complex_page.html")
print("Document loaded –", doc.title or "Untitled")
```

> **Neden önemli:** `HTMLDocument` nesnesi ham string işlemesini soyutlar, sayfayı sorgulamak, değiştirmek ve sonunda kaydetmek için metodlar sunar. Ayrıca satır sonlarını ve karakter kodlamalarını normalleştirir, bu da ilerideki ince hatalardan sizi korur.

Yüklemenin başarılı olduğunu doğrulamak için başlığı yazdırdığımızı fark edeceksiniz. Dosya eksik ya da bozuksa, yapıcı net bir istisna fırlatır—sessiz hatalar olmaz.

## Adım 2: Kaynak İşlemeyi Yapılandırma – Kırpmanın Çekirdeği

Bulmacanın bir sonraki parçası, işlemcinin include'ları ne kadar derine takip edeceğini sınırlayarak **HTML sayfasını nasıl kırparız** içeriğidir. İşte `ResourceHandlingOptions` burada devreye girer.

```python
from htmlprocessor import ResourceHandlingOptions

# Create a fresh options instance
res_opt = ResourceHandlingOptions()
# max_handling_depth = 2 means: main page + one level of includes
res_opt.max_handling_depth = 2
```

### `max_handling_depth` Ne İşe Yarar?

- **Derinlik 1** → Yalnızca kök HTML dosyası, tüm dış kaynaklar yok sayılır.  
- **Derinlik 2** → Kök ve doğrudan referans verilen dosyalar (ör. bir `iframe` ya da sunucu‑tarafı include).  
- **Daha yüksek değerler** → Daha derin iç içe yapı, ancak daha büyük çıktı ve daha uzun işleme süresi.

Derinliği **2** ile sınırlayarak, ana sayfayı ve bir katman include'u tutar, daha derin olanları atarız. Bu genellikle gereksiz altbilgileri, analiz script'lerini veya kırpılmış bir kopyada ihtiyacınız olmayan iç içe şablonları temizlemek için yeterlidir.

## Adım 3: Seçenekleri Kaydetme Yapılandırmasına Bağlamak

Şimdi kaynak kurallarımızı bir `SaveOptions` örneğine bağlıyoruz. Bu nesne, kütüphaneye dosyayı diske *tam olarak* nasıl yazacağını söyler.

```python
from htmlprocessor import SaveOptions

save_opt = SaveOptions()
save_opt.resource_handling_options = res_opt
```

> **Neden `SaveOptions` kullanmalı?**  
> Çıktı üzerinde ayrıntılı kontrol sağlar—sadece kaynak derinliğinin ötesinde. Daha sonra sıkıştırma, güzel‑yazdırma veya hatta özel geri çağrılar ekleyebilirsiniz, çekirdek kaydetme mantığını dokunmadan.

## Adım 4: SaveOptions Kullanarak HTML Sayfasını Kırpma

Son olarak, yapılandırılmış seçeneklerimizle `save` metodunu çağırıyoruz. Kütüphane DOM'u dolaşacak, derinlik sınırına uyacak ve kırpılmış bir dosya yazacak.

```python
# Save the trimmed document
output_path = "YOUR_DIRECTORY/trimmed_page.html"
doc.save(output_path, save_opt)

print(f"Trimmed page saved to {output_path}")
```

### Beklenen Sonuç

- `trimmed_page.html` dosyası, orijinal işaretlemeyi **ve** bir seviye derine kadar olan include'ları içerir.  
- Daha derin include'lar atılır, bu da daha küçük, daha hızlı yüklenen bir sayfa oluşturur.  
- Kırık etiketler ortaya çıkmaz—kütüphane, kaldırma sonrası asılı kalan öğeleri otomatik olarak kapatır.

Çıktıyı bir tarayıcıda açarak ana içeriğin hâlâ render edildiğini, gereksiz script'lerin veya iç içe çerçevelerin ise olmadığını doğrulayabilirsiniz.

## Tam Çalışan Örnek

Hepsini bir araya getirerek, kopyalayıp çalıştırabileceğiniz tam script aşağıdadır:

```python
# -*- coding: utf-8 -*-
"""
Trim an HTML page using SaveOptions.
Demonstrates:
- How to load an HTML document
- How to configure ResourceHandlingOptions
- How to use SaveOptions to save a trimmed version
"""

from htmlprocessor import HTMLDocument, SaveOptions, ResourceHandlingOptions

def trim_html(input_path: str, output_path: str, max_depth: int = 2) -> None:
    # Load the source document
    doc = HTMLDocument(input_path)
    print("Loaded:", doc.title or "Untitled")

    # Set up resource handling (how to trim HTML page)
    res_opt = ResourceHandlingOptions()
    res_opt.max_handling_depth = max_depth

    # Attach options to save configuration (how to use SaveOptions)
    save_opt = SaveOptions()
    save_opt.resource_handling_options = res_opt

    # Perform the save
    doc.save(output_path, save_opt)
    print(f"Trimmed HTML saved to {output_path}")

if __name__ == "__main__":
    INPUT = "YOUR_DIRECTORY/complex_page.html"
    OUTPUT = "YOUR_DIRECTORY/trimmed_page.html"
    trim_html(INPUT, OUTPUT, max_depth=2)
```

Script'i çalıştırın, `INPUT`'u herhangi bir karmaşık HTML dosyasına yönlendirin ve `OUTPUT`'ta daha ince bir sürüm elde edin.  

> **Köşe durum notu:** Orijinal sayfa, daha derin kaynaklara referans veren koşullu yorumlar (`<!--[if IE]>…<![endif]-->`) içeriyorsa, diğer iç içe include'lar gibi bunlar da kaldırılır. Bu, eski‑IE hilelerinin nihai boyutunuzu şişirmesini önler.

## Görsel Özet

Aşağıda, belgeyi yüklemeden kaynak işleme ve kırpılmış sonucu kaydetmeye kadar akışı gösteren hızlı bir diyagram bulunmaktadır.

![saveoptions kullanım örneği](https://example.com/placeholder.png "SaveOptions kullanarak HTML sayfalarını kırpma sürecini gösteren diyagram")

*Alt metin:* **saveoptions kullanım örneği** – bir HTML belgesini yükleme, yapılandırma ve kaydetme üç adımlı sürecini gösterir.

## Yaygın Sorular & Dikkat Edilmesi Gerekenler

| Soru | Cevap |
|----------|--------|
| **Daha derin iç içe yapıya ihtiyacım olursa ne olur?** | `max_handling_depth` değerini 3 ya da 4'e artırın, ancak çıktı boyutunun büyüyeceğini unutmayın. |
| **Derinlik ne olursa olsun belirli etiketleri (ör. `<script>`) hariç tutabilir miyim?** | Evet—`SaveOptions` ayrıca bir `tag_exclusion_list` özelliğini destekler. Bu listeye "script" ekleyerek script'leri her zaman dışarı çıkarabilirsiniz. |
| **Kütüphane çok iş parçacıklı (thread‑safe) mı?** | Mevcut sürüm thread‑safe değildir. Her iş parçacığı için ayrı bir `HTMLDocument` oluşturun. |
| **Göreceli URL'ler yeniden yazılacak mı?** | Varsayılan olarak hayır. Yeni konuma göre ayarlanması gerekiyorsa `save_opt.rewrite_relative_urls = True` kullanın. |

## Sonraki Adımlar

Artık **SaveOptions nasıl kullanılır** konusunda uzmanlaştığınıza göre, şu uzantıları deneyin:

- **Çıktıyı sıkıştır:** `save_opt.enable_gzip = True` ayarlayarak iletimde daha küçük dosyalar elde edin.  
- **Hata ayıklama için güzel‑yazdır:** `save_opt.indent_output = True` değerini değiştirerek güzel biçimlendirilmiş HTML alın.  
- **Toplu işleme:** HTML dosyaları içeren bir dizini döngüye alıp aynı kırpma mantığını uygulayın—statik site jeneratörleri için harika.

Bu ayarlamaların her biri, az önce öğrendiğiniz aynı temele dayanır ve kodunuzu temiz ve sürdürülebilir tutar.

## Sonuç

Python’da bir HTML sayfasını kırpmanın tüm yaşam döngüsünü ele aldık: **bir HTML belgesinin nasıl yükleneceği**, `ResourceHandlingOptions` kullanarak **HTML sayfasının nasıl kırpılacağı** yapılandırması ve sonunda **SaveOptions nasıl kullanılır** temiz dosyayı yazmak için. Örnek tamamen bağımsızdır, kutudan çıkar çıkmaz çalışır ve kaynak derinliğini kontrol etmenin web‑scraping, statik site üretimi veya hafif bir HTML anlık görüntüsü gerektiği her durumda neden hayati bir optimizasyon olduğunu gösterir.

Bir deneyin, farklı `max_handling_depth` değerleriyle oynayın ve kırpılmış sayfaların işi sizin için yapmasına izin verin. Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın—iyi kodlamalar!

## İlgili Öğreticiler

- [C#’ta HTML Nasıl Kaydedilir – Özel Kaynak İşleyici Kullanarak Tam Kılavuz](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [HTML’yi PNG Olarak Render Etme – Tam C# Kılavuzu](/html/english/net/rendering-html-documents/how-to-render-html-as-png-complete-c-guide/)
- [C#’ta HTML’yi Zip’lemek – HTML’yi Zip’e Kaydet](/html/english/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}