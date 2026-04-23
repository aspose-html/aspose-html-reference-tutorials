---
category: general
date: 2026-04-23
description: Java’da querySelectorAll kullanarak sınıfa göre öğeleri filtreleme, öznitelik
  değerlerini okuma ve ürün verilerini çıkarmak için NodeList’i yineleme.
draft: false
keywords:
- how to use queryselectorall
- how to read attribute
- iterate nodelist java
- filter elements by class
- select elements css selector
language: tr
og_description: Java'da querySelectorAll'ı sınıfa göre öğeleri filtrelemek, öznitelik
  değerlerini okumak ve ürün verilerini çıkarmak için NodeList'i yinelemek nasıl kullanılır.
og_title: Java'da querySelectorAll Nasıl Kullanılır – Sınıfa Göre Filtreleme
tags:
- Java
- HTML parsing
- DOM manipulation
title: Java'da querySelectorAll Nasıl Kullanılır – Sınıfa Göre Filtreleme
url: /tr/java/creating-managing-html-documents/how-to-use-queryselectorall-in-java-filter-by-class/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da querySelectorAll Kullanımı – Sınıfa Göre Filtreleme

Java’da querySelectorAll kullanımı, bir HTML belgesinden belirli öğeleri almanız gerektiğinde anahtar görevi görür. Bu öğreticide sınıfa göre öğeleri filtreleyecek, öznitelik değerlerini okuyacak ve bir NodeList üzerinde yineleme yaparak katalog sayfasından ürün fiyatlarını çekeceğiz.  

Kendinizi devasa bir HTML dosyasına bakarken, özel bir ayrıştırıcı yazmadan sadece “indirimli” kartları nasıl çekeceğinizi merak ederken buldunuz mu? İşte tam da burada çözeceğimiz problem bu—Aspose.HTML dışındaki ekstra kütüphanelere ihtiyaç duymadan, birkaç basit adımla.

Tam, çalıştırılabilir bir program elde edeceksiniz:

* **Selects elements** using a CSS selector (`select elements css selector`),
* **Filters by class** (`filter elements by class`),
* **Reads a custom attribute** (`how to read attribute`),
* **Iterates the resulting NodeList** (`iterate nodelist java`).

Aspose.HTML ile ilgili önceden bir deneyime sahip olmanız gerekmez—sadece temel bir Java kurulumu ve test edeceğiniz bir HTML dosyası yeterlidir.

![Java’da querySelectorAll kullanımı örneği](https://example.com/images/queryselectorall-java.png "Java’da querySelectorAll kullanımı")

---

## Gereksinimler

| Gereksinim | Neden Önemli |
|-------------|----------------|
| **Java 17+** | Modern dil özellikleri ve daha iyi modül yönetimi. |
| **Aspose.HTML for Java** (latest version) | `Document` sınıfını ve CSS‑seçici motorunu sağlar. |
| **catalog.html** (sample HTML) | Sorgulayacağımız kaynak. |
| **IDE or plain `javac`** | Demo'yu derlemek ve çalıştırmak için. |

Eğer henüz Aspose.HTML'i projenize eklemediyseniz, JAR dosyasını `libs` klasörünüze koyun ve sınıf yoluna ekleyin:

```bash
javac -cp "libs/*" CssSelectorDemo.java
java -cp ".:libs/*" CssSelectorDemo
```

---

## 1. Adım – HTML Belgesini Yükleme

Herhangi bir sorgu yapmadan önce, HTML dosyasını temsil eden bir `Document` nesnesine ihtiyacınız var. Bunu, hücreleri okuyabilmek için bir elektronik tabloyu yüklemeye benzetebilirsiniz.

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");
```

> **Neden Önemli:** `Document` sınıfı işaretlemi bir DOM ağacına ayrıştırır ve CSS‑seçici motorunun çalışmasını sağlar. Bu adımı atlamak, sadece düz bir string elde etmenize ve `querySelectorAll` kullanamamanıza yol açar.

---

## 2. Adım – CSS Seçici ile Öğeleri Seçme

Şimdi konunun kalbine geliyoruz: **querySelectorAll nasıl kullanılır**. Metot, geçerli herhangi bir CSS seçiciyi kabul eder, bu yüzden istediğiniz kadar kesin ya da geniş olabilirsiniz. Bizim senaryomuzda ürün kartlarını istiyoruz ki:

* `product-card` sınıfına sahip olsun,
* aynı zamanda `sale` sınıfı ile işaretlenmiş olsun,
* ve `data-price` özniteliğine sahip olsun.

```java
        // Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );
```

> **Açıklama:**  
> * `.product-card.sale` → **her iki** sınıfı da içeren öğeleri filtreler.  
> * `[data-price]` → özniteliğin var olduğunu garanti eder, tek bir çağrıda **sınıfa göre ve** öznitelik göre öğeleri filtrelemiş olur.  
> * Sonuç bir `NodeList`'tir; üzerinde yineleme yapabileceğiniz sıralı bir koleksiyondur.

Farklı bir desen için **select elements css selector** yapmanız gerekirse, sadece dizeyi değiştirin—kod yeniden yazmaya gerek yok.

---

## 3. Adım – Java’da NodeList Üzerinde Yineleme

`NodeList` bir diziye çok benzer davranır, ancak `Iterable` arayüzünü uygulamaz. Bu yüzden klasik bir `for` döngüsü kullanıyoruz—**iterate nodelist java** senaryoları için mükemmeldir.

```java
        // Iterate over the selected elements
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
```

> **Neden `for` döngüsü?**  
> İndexe doğrudan erişim sağlar, bu da günlükleme veya koşullu dallanma için kullanışlı olabilir. `while` döngüsünü tercih ederseniz, mantık aynı kalır—sadece döngü yapısını değiştirin.

---

## 4. Adım – `data-price` Özniteliğini Okuma

Şimdi nihayet **how to read attribute** değerlerini bir öğeden nasıl okuyacağımızı cevaplıyoruz. DOM API'sinde `getAttribute`, işaretlemede göründüğü gibi ham stringi döndürür.

```java
            // Read the price value from the data-price attribute
            String priceValue = productElement.getAttribute("data-price");
```

> **İpucu:** Öznitelik eksik olabilir, bu durumda `getAttribute` `null` döndürür. Basit bir kontrolle buna karşı önlem alabilirsiniz:

```java
            if (priceValue == null) {
                priceValue = "N/A"; // fallback for missing data-price
            }
```

---

## 5. Adım – Sonuçları Çıktılamak

Son olarak, her fiyatı konsola yazdırıyoruz. Bu, değerleri muhtemelen bir veritabanına ya da bir API yüküne göndereceğiniz gerçek dünya senaryosunu yansıtır.

```java
            // Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

### Beklenen Konsol Çıktısı

```
Sale item price: 19.99
Sale item price: 34.50
Sale item price: 12.00
```

Seçici eşleşen bir düğüm bulamazsa, döngü hiç çalışmaz—herhangi bir istisna atılmaz. Bu, katalogun boş olabileceği **edge cases** için güzel bir güvenlik ağıdır.

---

## Tam Çalışan Örnek

Hepsini bir araya getirerek, `CssSelectorDemo.java` dosyasına kopyalayıp yapıştırabileceğiniz tam dosya burada:

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");

        // Step 2: Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );

        // Step 3 & 4: Iterate over the selected elements and read the price attribute
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
            String priceValue = productElement.getAttribute("data-price");
            if (priceValue == null) {
                priceValue = "N/A"; // fallback if attribute is missing
            }

            // Step 5: Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

Dosyayı kaydedin, derleyin ve çalıştırın—fiyatların akışını izleyin. 🎉

---

## Sık Sorulan Sorular & Pro İpuçları

| Soru | Cevap |
|----------|--------|
| *Etiket adına göre de seçmem gerekirse ne olur?* | Just prepend the tag: `document.querySelectorAll("div.product-card.sale[data-price]")`. |
| *Birden fazla öznitelik filtresini zincirleyebilir miyim?* | Absolutely. Example: `[data-price][data-stock]` will keep only elements that have **both** attributes. |
| *`querySelectorAll` büyük/küçük harfe duyarlı mı?* | Yes—CSS selectors treat class and attribute names as case‑sensitive in HTML5. |
| *Büyük bir HTML dosyasını nasıl yönetirim?* | Aspose.HTML streams the document, but you can also limit the selector to a subtree (`someElement.querySelectorAll(...)`). |
| *Ne |  |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}