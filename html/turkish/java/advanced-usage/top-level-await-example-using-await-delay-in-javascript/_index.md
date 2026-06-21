---
category: general
date: 2026-03-26
description: Canlı bir demoda, await gecikmesini gösteren üst seviye await örneği,
  sayaç artırma sınıfı ve public sınıf alanları JavaScript.
draft: false
keywords:
- top level await example
- await delay javascript
- increment counter class
- public class fields javascript
- javascript class public field
language: tr
og_description: Kısa bir öğreticide, await gecikmesini, sayaç artırma sınıfını ve
  JavaScript'te public sınıf alanlarını gösteren üst seviye await örneği.
og_title: Üst Düzey Await Örneği – JavaScript'te Await Gecikmesi Kullanımı
tags:
- JavaScript
- ES2022
- async‑await
- classes
title: Üst seviye await örneği – JavaScript'te await gecikmesi kullanma
url: /tr/java/advanced-usage/top-level-await-example-using-await-delay-in-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# top level await örneği – JavaScript'te await delay kullanımı

Modül yürütmesini her şeyi bir async IIFE içine sarmadan nasıl duraklatabileceğinizi hiç merak ettiniz mi? İşte **top level await örneği** tam da bunu yapmanızı sağlıyor. Bu öğreticide, işi ertelemek için `await delay javascript` kullanan küçük bir web sayfasını adım adım inceleyecek, ardından **public class fields javascript**'ı kullanan bir `increment counter class` oluşturacağız. Sonunda, modern bir tarayıcıda çalıştırabileceğiniz tam, kopyala‑yapıştır bir snippet elde edeceksiniz.

Bir sınıfı public bir alanla tanımlamaktan basit bir promise‑tabanlı gecikme yardımcı fonksiyonuna kadar her şeyi ele alacağız. Harici kütüphane yok, derleme adımı yok—sadece düz HTML, bir `<script type="module">` ve en yeni ECMAScript özellikleri. Async fonksiyonlarla zaten rahat iseniz, top‑level await'ın doğal bir uzantı gibi hissettirdiğini göreceksiniz. **javascript class public field** sözdizimine yeniyseniz endişelenmeyin—her satırın nedenini açıklıyoruz.

## Öğrenecekleriniz

- Bir modül betiği içinde **top level await örneğinin** nasıl çalıştığı.
- `await delay javascript` yardımcı fonksiyonunun `setTimeout`'ı promise ile taklit eden kalıbı.
- Public bir alan (`count`) ve statik bir başlatma bloğu kullanan bir **increment counter class** nasıl yazılır.
- Beklenen konsol çıktısı ve statik bloğun scriptin geri kalanından önce çalıştığını nasıl doğrularsınız.
- Top‑level await'ı desteklemeyen eski tarayıcılarda karşılaşılabilecek yaygın sorunların nasıl giderileceği.

> **Pro ipucu:** Modern tarayıcılar (Chrome 106+, Firefox 102+, Edge 106+) zaten top‑level await'ı destekliyor. Daha eski ortamları desteklemeniz gerekiyorsa, Vite ya da Babel gibi bir araçla paketlemeyi düşünün.

## 1. Adım – Public Bir Alan ve Statik Bloğa Sahip Bir Sınıf Tanımlayın

Demo'muzun ilk parçası, sayısal bir sayaç tutan bir sınıf. `count = 0;` satırına dikkat edin—bu, ES2022'de tanıtılan **public class fields javascript** sözdizimidir. Constructor olmadan bir örnek özelliği oluşturur.

```html
<!DOCTYPE html>
<html>
<head>
    <title>ECMAScript 2022 Demo</title>
</head>
<body>
<img src="placeholder.png" alt="top level await example screenshot" title="top level await example">

<script type="module">
    // Step 1: Class definition
    class Counter {
        // Public field holds the current count
        count = 0;

        // Static block runs once when the class is first evaluated
        static {
            console.log('Counter class initialized');
        }

        // Simple method that increments the public field
        increment() {
            this.count++;
        }
    }
```

**Statik blok neden?** Modül ayrıştırıldığı anda (top‑level await çalışmadan *önce*) bir kez çalıştırılacak başlatma mantığını (ör. loglama) yürütmemizi sağlar. Bu, mesajın konsolda ilk olarak görünmesini garantileyerek sınıfın erken değerlendirildiğini kanıtlar.

## 2. Adım – `await delay javascript` Yardımcısını Oluşturun

Şimdi küçük bir promise‑tabanlı gecikme fonksiyonuna ihtiyacımız var. Temelde `setTimeout` etrafında bir sarmalayıcıdır, ancak bir promise döndürdüğü için await edilebilir.

```javascript
    // Step 2: Promise‑based delay helper
    const delay = ms => new Promise(resolve => setTimeout(resolve, ms));
```

**Köşe durumu:** `ms` negatif ya da sayı değilse, `setTimeout` bunu `0` olarak kabul eder. Doğrulama ekleyebilirsiniz, ancak demo için tek satır kod okunabilirliği korur.

## 3. Adım – Top‑Level Await Kullanarak Yürütmeyi Durdurun

Şimdi gösterinin yıldızı geliyor: top‑level await. Script'imiz bir modül olduğundan (`type="module"`), `await` ifadesini doğrudan üst seviyeye koyabiliriz. Bu, promise çözülene kadar modülü duraklatır ve yan etkilerin sırasını kontrol etmemizi sağlar.

```javascript
    // Step 3: Top‑level await – delay half a second
    await delay(500);   // Wait 500 ms so the static block logs first
```

**Sık sorulan soru:** “Normal bir `<script>` etiketinde top‑level await kullanabilir miyim?” Hayır—sadece modül script'leri destekler. `type="module"` eklemeyi unutursanız sözdizimi hatası alırsınız.

## 4. Adım – Sınıfı Örnekleyin, Artırın ve Sonucu Loglayın

Son olarak her şeyi bir araya getiriyoruz: bir örnek oluşturun, `increment()` çağırın ve son sayıyı çıktıya yazdırın. Bu, **increment counter class**'ın çalışmasını gösterir.

```javascript
    // Step 4: Work with the Counter instance
    const counterInstance = new Counter();
    counterInstance.increment();               // count becomes 1
    console.log('Final count:', counterInstance.count);
</script>
</body>
</html>
```

### Beklenen Konsol Çıktısı

```
Counter class initialized
Final count: 1
```

Sayfayı DevTools'ta açarsanız, statik‑blok mesajının gecikme bitmeden **önce** göründüğünü görmelisiniz; bu, sınıfın önce değerlendirildiğini doğrular.

## 5. Adım – Constructor Yerine Public Class Fields Neden Kullanılır?

Şöyle bir şey yazmadığımızı merak edebilirsiniz:

```javascript
class Counter {
    constructor() {
        this.count = 0;
    }
}
```

Her iki yaklaşım da çalışır, ancak **public class fields javascript** daha temiz, deklaratif bir sözdizimi sunar. Alan bir kez tanımlanır, her constructor çağrısında tekrar tanımlanmaz; sınıf büyüdükçe okunması daha kolay olur. Ayrıca statik bloklar constructor içinde bulunamaz, bu da başlatma mantığını ayrı tutmayı doğal hâle getirir.

## 6. Adım – Gerçek Dünya Uygulamaları İçin Örneği Uyarlama

Üretimde tek bir sayaçtan daha fazlasına ihtiyaç duyarsınız. İşte birkaç hızlı fikir:

- **Birden fazla sayaç:** `Map` içinde, kimlik anahtarına göre saklayın.
- **Kalıcı durum:** `console.log` yerine `localStorage` yazmaları kullanın.
- **Async başlatma:** Statik bloğu, herhangi bir örnek oluşturulmadan önce sunucudan yapılandırma çekmek için kullanın.

Bu kalıpların hepsi top‑level await'dan fayda görür; çünkü modül yüklenirken veriyi bir kez çekebilir ve her tüketici için hazır olmasını garantileyebilirsiniz.

## Sık Sorulan Sorular

**S: Top‑level await diğer modülleri bloklar mı?**  
C: Hayır. Her modül bağımsız çalışır. Await içeren modül duraklatılır; diğer modüller paralel olarak yüklenmeye devam eder.

**S: Gecikme promise'ı reddedilirse ne olur?**  
C: Ele alınmamış bir reddetme, modül değerlendirmesini durdurur ve konsolda hata olarak gösterilir. Graceful bir geri dönüş için `await`'ı `try…catch` içinde sarmalayın.

**S: `static` anahtar kelimesi zorunlu mu?**  
C: Sayaç için değil, ancak statik blok kodun *bir kez* yükleme zamanında çalıştığını göstermek için kullanışlıdır—loglama ya da özellik‑tespiti için idealdir.

## Sonuç

Artık `await delay javascript`, bir **increment counter class** ve **public class fields javascript** gücünü gösteren bir **top level await örneği** oluşturmuş oldunuz. Tam, çalıştırılabilir snippet yukarıda yer alıyor ve konsol çıktısı statik bloğun gecikmeli koddan önce çalıştığını kanıtlıyor.

Buradan daha karmaşık async akışlarla deneyler yapabilir, gecikmeyi gerçek bir API çağrısıyla değiştirebilir ya da sınıfa ek metodlar ekleyebilirsiniz. Modern JavaScript, modülleri birinci sınıf async varlıklar olarak ele almanıza izin verir—ekstra sarmalayıcılara gerek yok.

Kodlamanın tadını çıkarın ve varyasyonlarınızı yorumlarda paylaşın. Bu rehberi faydalı bulduysanız, async desenlerle hâlâ mücadele eden bir ekip arkadaşınızla paylaşın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}