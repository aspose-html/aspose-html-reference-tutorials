---
category: general
date: 2026-02-16
description: Java'da HTML nasıl yüklenir, cihaz DPI'sı nasıl ayarlanır, sanal ekran
  boyutu nasıl tanımlanır ve herhangi bir öğenin hesaplanmış arka plan rengi nasıl
  okunur?
draft: false
keywords:
- how to load html
- read background color
- set device dpi
- set virtual screen size
- get computed background color
language: tr
og_description: Java'da HTML nasıl yüklenir, cihaz DPI'sı nasıl ayarlanır, sanal ekran
  boyutu nasıl tanımlanır ve herhangi bir öğenin hesaplanan arka plan rengi nasıl
  okunur.
og_title: HTML'yi Yükleme, Cihaz DPI'sını Ayarlama ve Arka Plan Rengini Okuma
tags:
- Aspose.HTML
- Java
title: HTML'yi Yükleme, Cihaz DPI'sını Ayarlama ve Arka Plan Rengini Okuma
url: /tr/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML Yükleme, Cihaz DPI'sı Ayarlama ve Arka Plan Rengini Okuma

Java uygulamasında **html nasıl yüklenir** ve ardından sayfanın stillerini incelemek ister misiniz? Tek başınıza değilsiniz—geliştiriciler sık sık bir web sayfasını ekran dışı render etme, son CSS değerlerini yakalama ve bunları PDF dönüşümü, ekran görüntüsü alma veya otomatik testlerde kullanma ihtiyacı duyar.  

Bu rehberde tam olarak bunu yapacağız: bir HTML dosyasını yükleyecek, **cihaz DPI'sını** ayarlayacak, bir **sanal ekran boyutu** tanımlayacak ve sonunda `<body>` öğesinden **arka plan rengini** okuyacağız. Sonunda **hesaplanmış arka plan rengini** yazdıran tamamen çalışır bir kod parçacığına sahip olacaksınız—hiçbir gizem yok, sadece saf Java.

## Gereksinimler

Başlamadan önce şunların olduğundan emin olun:

* Java 17 veya daha yeni bir sürüm (kod, herhangi bir yeni JDK ile çalışır).  
* Aspose.HTML for Java 23.9 ve üzeri—JAR dosyasını Aspose sitesinden indirin veya Maven aracılığıyla ekleyin.  
* CSS içinde bir arka plan rengi tanımlı basit bir HTML dosyası (ör. `responsive.html`).

Hepsi bu—ekstra framework yok, tarayıcı sürücüsü yok. Hazır mısınız? Başlayalım.

![Diagram illustrating how to load html and extract computed styles](/images/load-html-diagram.png){alt="HTML yükleme ve hesaplanmış stilleri çıkarma diyagramı"}

## Adım 1: HTML'yi Yükleme ve Render Seçeneklerini Yapılandırma

İlk yapmanız gereken bir `HtmlLoadOptions` nesnesi oluşturmaktır. Bu nesne, Aspose.HTML **html nasıl yüklenecek** konusunda sanal ekran boyutları ve taklit etmek istediğiniz DPI gibi bilgileri taşır.

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create load options and define the virtual screen size and DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        // setVirtualScreenSize – width × height in CSS pixels
        loadOptions.setScreenSize(new Size(1280, 800));
        // setDeviceDpi – typical desktop DPI (96 is the default for most monitors)
        loadOptions.setDeviceDpi(96);
```

**Neden önemli:**  
Sanal bir ekran boyutu ayarlamak, `@media (max-width: 600px)` gibi medya sorgularının gerçek bir monitörde render edilmiş gibi davranmasını sağlar. DPI ise CSS `px` birimlerinin fiziksel piksellere nasıl eşleneceğini etkiler—daha sonra görüntü veya PDF oluştururken kritik bir faktördür.

## Adım 2: Yapılandırılmış Seçeneklerle HTML Dosyasını Yükleme

Şimdi dosyayı gerçekten yüklüyoruz. Az önce yapılandırdığımız aynı `loadOptions` nesnesini geçirdiğimize dikkat edin.

```java
        // 2️⃣ Load the HTML file with the options we just set.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);
```

Dosya bulunamazsa, Aspose net bir `FileNotFoundException` fırlatır. Üretim ortamında bunu bir try‑catch bloğuna alıp varsayılan bir HTML dizesine geri dönmek isteyebilirsiniz.

## Adım 3: Sanal Ekran Boyutunu ve Cihaz DPI'sını (Açıkça) Ayarlama

Yukarıda zaten `setScreenSize` ve `setDeviceDpi` çağrısı yapmış olsak da, **sanal ekran boyutunu ayarlama** ve **cihaz DPI'sını ayarlama** işlemlerinin render öncesinde herhangi bir noktada değiştirilebileceğini vurgulamakta fayda var. Örneğin, yüksek çözünürlüklü ekran görüntüleri için DPI'yi artırabilirsiniz:

```java
        // 3️⃣ Adjust DPI for a high‑resolution render (optional).
        loadOptions.setDeviceDpi(300);   // 300 DPI is common for print‑ready images
        // 4️⃣ Change screen size for a mobile layout test.
        loadOptions.setScreenSize(new Size(375, 667)); // iPhone X viewport
```

Bu ayarları ilk yüklemeden sonra değiştirirseniz belgeyi yeniden yüklemeyi unutmayın—Aspose, `Document` oluşturulduktan sonra bu değerleri değiştirilemez olarak kabul eder.

## Adım 4: Arka Plan Rengini Okuma ve Hesaplanmış Arka Plan Rengini Alma

Belge bellekte iken, herhangi bir öğenin hesaplanmış stilini sorgulayabilirsiniz. Burada `<body>` etiketine odaklanıyoruz, ancak aynı yöntem `<div>`, `<p>` veya pseudo‑elementler için de geçerlidir.

```java
        // 5️⃣ Retrieve the <body> element.
        Element bodyElement = document.getBody();

        // 6️⃣ Output the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

**Gözlemlenecek:** `responsive.html` dosyanız `body { background: #ff5722; }` içeriyorsa, konsol şu şekilde bir çıktı verir:

```
Computed background color: rgba(255,87,34,1)
```

Bu, **hesaplanmış arka plan rengini alma** sonucudur—Aspose, tüm CSS cascade kurallarını, medya sorgularını ve hatta `!important` bildirimlerini çözerek son değeri döndürür.

## Tam Çalışan Örnek

Hepsini bir araya getirerek, kopyala‑yapıştır‑hazır program aşağıdadır:

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create load options – virtual screen size + DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        loadOptions.setScreenSize(new Size(1280, 800)); // set virtual screen size
        loadOptions.setDeviceDpi(96);                  // set device DPI (default desktop)

        // Optional: tweak for high‑resolution or mobile rendering.
        // loadOptions.setDeviceDpi(300);
        // loadOptions.setScreenSize(new Size(375, 667));

        // Step 2: Load the HTML document with the options.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);

        // Step 3: Grab the <body> element.
        Element bodyElement = document.getBody();

        // Step 4: Print the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

### Beklenen Çıktı

```
Computed background color: rgba(255,255,255,1)
```

*(Tam RGBA değerleri HTML dosyanızdaki CSS'e bağlı olarak değişir.)*

## Yaygın Tuzaklar ve Profesyonel İpuçları

* **DPI ayarı eksik mi?** Aspose varsayılan olarak 96 DPI kullanır; bu, yüksek çözünürlüklü ekran görüntülerinde bulanıklığa yol açabilir. Keskin bir çıktı istiyorsanız her zaman açıkça ayarlayın.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}