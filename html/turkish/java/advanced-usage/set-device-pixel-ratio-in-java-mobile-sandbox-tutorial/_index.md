---
category: general
date: 2026-10-19
description: Aspose.HTML sandbox kullanarak Java'da device pixel ratio ayarlama. Ekran
  genişliği ve yüksekliğini ayarlamayı ve tam, çalıştırılabilir bir örnekle Java sayfa
  başlığını almayı öğrenin.
draft: false
keywords:
- get page title java
- device pixel ratio java
- create virtual device java
- set screen width height
lastmod: 2026-10-19
og_description: Aspose.HTML sandbox ile Java sayfa başlığını alın. Bu kılavuz, Java'da
  ekran genişliği ve yüksekliğini ve device pixel ratio'yu birkaç kolay adımda nasıl
  ayarlayacağınızı gösterir.
og_image_alt: 'Developer guide: set device pixel ratio in Java using Aspose.HTML sandbox'
og_title: Java sayfa başlığını al – set device pixel ratio in Java sandbox öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-10-19'
  description: set device pixel ratio in Java using Aspose.HTML sandbox. Learn how
    to set screen width height and get page title java with a complete, runnable example.
  headline: Get page title java – set device pixel ratio in Java sandbox tutorial
  type: TechArticle
- questions:
  - answer: Yes—create a new `SandboxOptions` with a different `setDevicePixelRatio`
      value and instantiate a fresh `Sandbox`. Re‑using the same sandbox after changing
      its options is not supported.
    question: Can I change the pixel ratio at runtime?
  - answer: Loop over a list of `SandboxOptions` (e.g., iPhone 8, Pixel 4) and run
      the same load‑and‑title logic for each.
    question: What if I need to test multiple devices?
  - answer: Aspose.HTML respects Java’s default SSL trust store. Add the cert to the
      JVM’s keystore or, for testing only, disable verification (not recommended for
      production).
    question: Does this work with HTTPS sites that have self‑signed certificates?
  - answer: The `HTMLDocument` API provides `save` methods that can export the rendered
      page to PNG or JPEG. Use `htmlDoc.save("output.png", SaveFormat.PNG);` after
      loading.
    question: How do I capture a screenshot instead of just the title?
  - answer: Each `Sandbox` instance is isolated, but you should avoid sharing a single
      instance across multiple threads without synchronization.
    question: Is the sandbox thread‑safe?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- mobile emulation
title: Java sayfa başlığını al – set device pixel ratio in Java sandbox öğreticisi
url: /tr/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sayfa başlığını al java – Java sandbox öğreticisinde cihaz piksel oranını ayarla

Java'da duyarlı bir siteyi test ederken **cihaz piksel oranını ayarlamaya** hiç ihtiyaç duydunuz mu? Tek başınıza değilsiniz. Birçok geliştirici, sayfa masaüstünde mükemmel göründüğünde ancak yüksek DPI telefonlarda bozulduğunda bir engelle karşılaşıyor. İyi haber? Aspose.HTML'in sandbox'ı sayesinde iPhone X'i (veya herhangi bir cihazı) doğrudan Java kodunuzdan taklit edebilirsiniz—tarayıcı gerekmez.

Bu rehberde **ekran genişliği yüksekliğini nasıl ayarlayacağınızı**, **cihaz piksel oranını** yapılandıracağız ve sonunda **get page title java**'yı kullanarak her şeyin doğru render edildiğini doğrulayacağız. Sonunda, herhangi bir projeye ekleyebileceğiniz ve mobil düzenleri anında test etmeye başlayabileceğiniz bağımsız bir programınız olacak.

## Hızlı cevaplar
- **Java'da cihaz piksel oranını nasıl ayarlarım?** Sandbox'ı oluşturmadan önce `SandboxOptions.setDevicePixelRatio(double)` kullanın.  
- **Hangi metod sayfa başlığını döndürür?** Yüklenen `HTMLDocument` üzerinde `htmlDocument.getTitle()` çağırın.  
- **Diğer cihazları taklit edebilir miyim?** Evet—istenen genişlik, yükseklik ve piksel oranı ile yeni bir `SandboxOptions` oluşturun.  
- **Bir tarayıcı sürücüsüne ihtiyacım var mı?** Hayır, Aspose.HTML'in sandbox'ı başlıksızdır ve tamamen Java'da çalışır.  
- **Hangi Aspose.HTML sürümü gereklidir?** Versiyon 23.7 veya üzeri tüm mobil‑taklit özelliklerini destekler.

## get page title java nedir?
`get page title java`, bir HTML belgesinden `<title>` öğesini Java kodu kullanarak almayı sağlayan işlemdir. Sanal cihaz bağlamında yüklenen bir sayfanın beklenen başlığı render ettiğini doğrulamanıza olanak tanır. Başlığı almak, cihaz emülasyonu parametreleri uygulandıktan sonra doğru sayfanın yüklendiğini doğrulamak için otomatik doğrulamada yaygın bir adımdır.

## Mobil taklit için Aspose.HTML sandbox neden kullanılmalı?
Aspose.HTML, **30+** giriş ve çıkış formatını destekler—HTML, CSS, SVG ve PDF dahil—ve tam bir tarayıcı başlatmadan sayfaları render edebilir. Sandbox'ı, bellek kullanımını 200 MB'nin altında tutarak çok sayfalı siteleri işleyebilir, bu da CI boru hatları için ideal kılar.

## Önkoşullar

- Java 8 veya daha yeni (kod JDK 11 ile de derlenir)  
- Aspose.HTML for Java kütüphanesi (versiyon 23.7 veya üzeri) – Maven Central'dan çekebilirsiniz  
- Bir IDE veya basit bir `javac` komut‑satırı kurulumu  
- Demo URL'si için internet erişimi (`https://responsive.example.com`)

Ekstra framework yok, Selenium da yok, sadece saf Java ve Aspose.HTML.

## Java'da ekran genişliği yüksekliği ve cihaz piksel oranını nasıl ayarlarım

`SandboxOptions` sınıfı, sanal cihazın ekran boyutlarını ve piksel yoğunluğunu belirlemenizi sağlar. Belirli bir mobil cihazı taklit etmek için sandbox'ı istenen ekran genişliği, yüksekliği ve cihaz piksel oranı ile yapılandırmalısınız. Bir `SandboxOptions` nesnesi oluşturup bu özellikleri ayarladığınızda, render motoru sayfayı o cihazda gösteriliyormuş gibi işler ve CSS medya sorguları ile görüntü ölçeklendirmesinin doğru çalışmasını sağlar.

`SandboxOptions` bir örneği oluşturun, genişliği **375**, yüksekliği **812** ve cihaz piksel oranını **3.0** olarak ayarlayın. Ardından bu seçenekleri yeni bir `Sandbox`'a geçirin. Bu, herhangi bir sayfa yüklenmeden önce sanal cihazı tam olarak yapılandırır.

`SandboxOptions` sınıfı, sanal cihazın ekran boyutunu ve piksel yoğunluğunu tanımlar. Herhangi bir mobil‑taklit senaryosu için giriş noktasıdır.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Neden önemli:**  
> `setDevicePixelRatio` çağrısı her şeyi ölçeklendirir—görüntülerden yazı tipi render'ına—bu yüzden sayfa gerçek bir telefon üzerindeymiş gibi davranır. Bunu atlayarsanız, düzen masaüstü‑stili CSS medya sorgularına geri dönebilir ve mobil test amacını bozar.

## Sandbox örneğini nasıl oluştururum

`Sandbox` sınıfı, daha önce tanımlanan seçenekleri kullanarak HTML render eden başlıksız bir tarayıcı ortamını temsil eder. `SandboxOptions` yapılandırıldıktan sonra, bu seçeneklerle bir `Sandbox` örneği oluşturun ve izole bir render bağlamı elde edin. Bu sandbox, belirttiğiniz ekran boyutu ve piksel yoğunluğunu uygulayan hafif bir tarayıcı gibi davranır ve ortamı temiz tutarak birden fazla sayfa yüklemesi için yeniden kullanılabilir.

Önceden yapılandırılmış `SandboxOptions` ile bir `Sandbox` örneği oluşturun. Sandbox, tanımladığınız boyutları ve piksel oranını dikkate alan küçük bir başlıksız tarayıcı gibi davranır.

`Sandbox` nesnesi, UI olmadan çalışan Aspose.HTML'in izole render motorudur. Her testin temiz bir ortamda çalışmasını garanti eder.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Pro ipucu:** Aynı `Sandbox` nesnesini birden fazla sayfa yüklemesi için yeniden kullanabilirsiniz; sadece URL'yi değiştirin ve sandbox aynı cihaz özelliklerini korur.

## Sandbox içinde sayfayı nasıl yüklersiniz

`HTMLDocument` sınıfı, bellekte ayrıştırılmış bir HTML dosyasını temsil eder ve DOM erişimi ile render yetenekleri sağlar. Sandbox hazır olduğunda, hedef URL ve sandbox örneğini geçirerek bir `HTMLDocument` oluşturun. Bu, sayfayı sanal cihaz ayarlarıyla yükler ve render eder, DOM ile etkileşime girmenize veya başlık gibi bilgileri çıkarmanıza olanak tanır.

Hedef URL ve `Sandbox` örneğini geçirerek bir `HTMLDocument` oluşturun. Bu, belgenin önceki adımda ayarladığınız sanal cihazı kullanarak render edilmesini zorlar.

`HTMLDocument` sınıfı, bellekte ayrıştırılmış bir HTML dosyasını temsil eder ve DOM manipülasyonu ile meta veri çıkarımı için yöntemler sunar.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

URL erişilemezse veya sayfa hatalar içeriyorsa, Aspose.HTML bir istisna fırlatır. Üretim kodu için bunu bir `try‑catch` bloğuna alıp hatayı kaydedersiniz, ancak öğretici bunu basit tutar.

## get page title java ile nasıl doğrularınız

`getTitle()` metodu, HTML belgesinin `<title>` öğesinin içeriğini düz bir string olarak döndürür. Başlığı okumak en hızlı doğrulama kontrolüdür. Sayfayı yükledikten sonra `htmlDocument.getTitle()` çağırarak başlık metnini alın. Bu basit kontrol, sayfanın taklit edilen cihaz ayarları altında doğru render edildiğini doğrular ve otomatik testlerde gezinme veya içerik değişikliklerini hızlıca doğrulamanın bir yolunu sağlar.

Yüklenmiş belge üzerinde `htmlDocument.getTitle()` çağırın ve sonucu yazdırın. Sandbox **cihaz piksel oranını** doğru bir şekilde uyguladıysa, başlık gerçek bir iPhone X'te gördüğünüzle aynı olacaktır.

`getTitle()` metodu, `<title>` öğesinin içeriğini düz bir string olarak döndürür, böylece görsel inceleme yapmadan render'ı doğrulayabilirsiniz.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Beklenen çıktı (örnek):**

```
Title under sandbox: Responsive Demo – Mobile View
```

Eğer başlık yazdırıldıysa, Java kullanarak **cihaz piksel oranını ayarladınız**, **ekran genişliği ve yüksekliğini ayarladınız** ve **sayfa başlığını aldınız** demektir.

## Tam, çalıştırılabilir örnek

Aşağıda, `SandboxDemo.java` adlı bir dosyaya kopyalayıp yapıştırabileceğiniz tam program yer alıyor. Derlemeden önce Aspose.HTML JAR'larının sınıf yolunuzda (`-cp` bayrağı) olduğundan emin olun.

`SandboxDemo` sınıfı, önceki adımları tek bir çalıştırılabilir örnek içinde birleştirir.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.net.URL;

/**
 * Demonstrates how to set device pixel ratio, set screen width height,
 * and get page title java using Aspose.HTML sandbox.
 */
public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define device characteristics ----------
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS pixels width
        sandboxOptions.setScreenHeight(812);         // CSS pixels height
        sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI screen factor (set device pixel ratio)

        // ---------- Step 2: Create the sandbox ----------
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // ---------- Step 3: Load a web page inside the sandbox ----------
        HTMLDocument htmlDoc = new HTMLDocument(
                new URL("https://responsive.example.com"), mobileSandbox);

        // ---------- Step 4: Verify the document loaded correctly ----------
        System.out.println("Title under sandbox: " + htmlDoc.getTitle());
    }
}
```

Derleyin ve çalıştırın:

```bash
javac -cp "aspose-html-23.7.jar" SandboxDemo.java
java -cp ".:aspose-html-23.7.jar" SandboxDemo
```

Konsolda başlığın yazdırıldığını görmelisiniz, bu da sayfanın istenen **cihaz piksel oranı** ile render edildiğini doğrular.

## Sıkça sorulan sorular ve uç durumlar

**Q: Piksel oranını çalışma zamanında değiştirebilir miyim?**  
A: Evet—farklı bir `setDevicePixelRatio` değeriyle yeni bir `SandboxOptions` oluşturun ve yeni bir `Sandbox` başlatın. Seçenekleri değiştirdikten sonra aynı sandbox'ı yeniden kullanmak desteklenmez.

**Q: Birden fazla cihazı test etmem gerekirse ne yapmalıyım?**  
A: `SandboxOptions` listesi (ör. iPhone 8, Pixel 4) üzerinde döngü kurun ve her biri için aynı yükle‑ve‑başlık mantığını çalıştırın.

**Q: Kendinden imzalı sertifikalara sahip HTTPS siteleriyle çalışır mı?**  
A: Aspose.HTML, Java'nın varsayılan SSL güven mağarasına saygı gösterir. Sertifikayı JVM'nin keystore'una ekleyin veya sadece test amaçlı doğrulamayı devre dışı bırakın (üretim için önerilmez).

**Q: Sadece başlık yerine ekran görüntüsü nasıl alırım?**  
A: `HTMLDocument` API'si, render edilen sayfayı PNG veya JPEG olarak dışa aktarabilen `save` metodları sunar. Yüklemeden sonra `htmlDoc.save("output.png", SaveFormat.PNG);` kullanın.

**Q: Sandbox thread‑safe mi?**  
A: Her `Sandbox` örneği izoledir, ancak birden fazla iş parçacığı arasında senkronizasyon olmadan tek bir örnek paylaşmaktan kaçınmalısınız.

## Görsel genel bakış

![Diagram showing set device pixel ratio in mobile sandbox](https://example.com/images/sandbox-diagram.png "set device pixel ratio diagram")

[Diagram showing set device pixel ratio in mobile sandbox](https://example.com/images/sandbox-diagram.png "set device pixel ratio diagram")

*Yukarıdaki illüstrasyon, `SandboxOptions` yapılandırmasından (**ekran genişliği yüksekliği ayarlama** ve **cihaz piksel oranını ayarlama** dahil) bir URL yüklemeye ve başlığı çıkarmaya kadar olan akışı haritalar.*

## Sonuç

Artık Java'da **cihaz piksel oranını nasıl ayarlayacağınızı**, doğru mobil taklit için **ekran genişliği ve yüksekliğini nasıl ayarlayacağınızı** ve render'ın başarılı olduğunu doğrulamak için **get page title java**'yı nasıl kullanacağınızı biliyorsunuz. Bu kompakt iş akışı, otomatik UI testlerinde ağır tarayıcılara olan ihtiyacı ortadan kaldırır ve CI boru hatlarına sorunsuz bir şekilde entegre olur.

Bir sonraki adıma hazır mısınız? Render edilen sayfayı bir görüntü olarak dışa aktarmayı deneyin veya `devicePixelRatio` değerini 1.0 ile 3.0 arasında değiştirerek CSS medya sorgusu hata ayıklamasını deneyin. Ayrıca mobil görünümün yazdırılabilir bir versiyonunu yakalamak için Aspose.HTML'in PDF dönüşüm özelliklerini keşfedebilirsiniz.

İyi kodlamalar, ve mobil düzenleriniz her zaman net görünsün—piksel yoğunluğundan bağımsız!

**Son güncelleme:** 2026-10-19  
**Test edildiği sürüm:** Aspose.HTML 23.7 for Java  
**Yazar:** Aspose

## İlgili Öğreticiler

- [Ekran Genişliği ile Sandbox'ta HTML Başlığını Al Java Render Sayfası](/html/java/advanced-usage/get-html-title-java-render-page-in-sandbox-with-screen-width/)
- [Aspose HTML Sandbox Oluşturma Tam Java Rehberi](/html/java/configuring-environment/create-aspose-html-sandbox-complete-java-guide/)
- [Java'da Cihaz Piksel Oranını Ayarlama Tam Rehber](/html/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}