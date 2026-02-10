---
category: general
date: 2026-02-10
description: Aspose.HTML sandbox kullanarak Java'da cihaz piksel oranını ayarlayın.
  Ekran genişliği ve yüksekliğini nasıl ayarlayacağınızı ve Java ile sayfa başlığını
  nasıl alacağınızı, tam ve çalıştırılabilir bir örnekle öğrenin.
draft: false
keywords:
- set device pixel ratio
- get page title java
- set screen width height
language: tr
og_description: Aspose.HTML sandbox ile Java’da cihaz piksel oranını ayarlayın. Bu
  kılavuz, ekran genişliği ve yüksekliğini ayarlamayı ve Java’da sayfa başlığını almayı
  birkaç kolay adımda gösterir.
og_title: Java’da cihaz piksel oranını ayarlama – Mobile Sandbox Öğreticisi
tags:
- Aspose.HTML
- Java
- Mobile Emulation
title: Java'da cihaz piksel oranını ayarlama – Mobil Sandbox Öğreticisi
url: /tr/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da cihaz piksel oranını ayarlama – Mobil Sandbox Öğreticisi

Ever needed to **set device pixel ratio** while testing a responsive site in Java? You're not the only one. Many developers hit a wall when the page looks perfect on desktop but breaks on high‑DPI phones. The good news? With Aspose.HTML’s sandbox you can emulate an iPhone X (or any device) right from your Java code—no browser required.

Bu rehberde **how to set screen width height**'i, **device pixel ratio**'yu yapılandırmayı ve sonunda **get page title java**'yı nasıl alacağımızı adım adım göstereceğiz, böylece her şeyin doğru render edildiğini doğrulayabilirsiniz. Sonunda, herhangi bir projeye ekleyebileceğiniz ve mobil düzenleri anında test etmeye başlayabileceğiniz bağımsız bir programınız olacak.

## Önkoşullar

- Java 8 ve üzeri (kod JDK 11 ile de derlenir)  
- Aspose.HTML for Java kütüphanesi (versiyon 23.7 veya sonrası) – Maven Central'dan çekebilirsiniz  
- Bir IDE veya basit bir `javac` komut satırı kurulumu  
- Demo URL'si için internet erişimi (`https://responsive.example.com`)

Ekstra çerçeve yok, Selenium yok, sadece saf Java ve Aspose.HTML.

---

## Adım 1: Ekran genişliği yüksekliğini ve cihaz piksel oranını ayarlama

İlk olarak ihtiyacımız olan, sandbox'a hangi “cihaz” olduğumuzu söyleyen bir `SandboxOptions` nesnesidir. Burada iPhone X boyutlarını (375 × 812 CSS piksel) ve **device pixel ratio** değeri 3.0 olan bir ayarı kullanacağız; bu, yüksek DPI'lı retina ekranını taklit eder.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Neden önemli:**  
> `setDevicePixelRatio` çağrısı her şeyi ölçeklendirir—görüntülerden yazı tipi render'ına kadar—bu sayede sayfa gerçek bir telefon üzerinde olduğunu düşünür. Bunu atlayarsanız, düzen masaüstü‑stili CSS medya sorgularına geri dönebilir ve mobil test amacını bozar.

---

## Adım 2: Sandbox örneğini oluşturma

Şimdi bu seçenekleri çalışan bir sandbox'a dönüştürüyoruz. Sandbox'ı, tanımladığımız boyutları ve piksel oranını dikkate alan küçük, başsız bir tarayıcı olarak düşünün.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Pro ipucu:** Aynı `Sandbox` nesnesini birden fazla sayfa yüklemesi için yeniden kullanabilirsiniz; sadece URL'yi değiştirin ve sandbox aynı cihaz özelliklerini korur.

---

## Adım 3: Sayfayı sandbox içinde yükleme

Sandbox hazır olduğunda, bir sayfa yüklemek `HTMLDocument` oluşturup sandbox'ı ikinci argüman olarak geçirmek kadar basittir. Bu, belgenin daha önce ayarladığımız sanal cihazı kullanarak render edilmesini sağlar.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

URL erişilemezse veya sayfada hatalar varsa, Aspose.HTML bir istisna fırlatır. Üretim kodunda muhtemelen bunu bir `try‑catch` bloğuna alıp hatayı kaydedersiniz, ancak öğreticide basit tutuyoruz.

---

## Adım 4: get page title java ile doğrulama

En hızlı doğrulama, belgenin başlığını okumaktır. Sandbox **device pixel ratio**'yu doğru uyguladıysa, başlık gerçek bir iPhone X'te gördüğünüzle aynı olacaktır.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Beklenen çıktı (örnek):**

```
Title under sandbox: Responsive Demo – Mobile View
```

Eğer başlık yazdırılmış olarak görürseniz, Java kullanarak **set device pixel ratio**, **set screen width height** ve **got the page title** işlemlerini başarıyla gerçekleştirmiş olursunuz.

---

## Tam, Çalıştırılabilir Örnek

Aşağıda `SandboxDemo.java` adlı bir dosyaya kopyalayıp yapıştırabileceğiniz tam program bulunmaktadır. Derlemeden önce Aspose.HTML JAR'larının sınıf yolunuzda (`-cp` bayrağı) olduğundan emin olun.

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

Konsolda başlığın yazdırıldığını görmelisiniz; bu, sayfanın istenen **device pixel ratio** ile render edildiğini doğrular.

---

## Sık Sorulan Sorular & Kenar Durumları

| Soru | Cevap |
|----------|--------|
| **Pixel oranını çalışma zamanında değiştirebilir miyim?** | Evet—sadece farklı bir `setDevicePixelRatio` değeriyle yeni bir `SandboxOptions` oluşturup yeni bir `Sandbox` örneği başlatın. Seçeneklerini değiştirdikten sonra aynı sandbox'ı yeniden kullanmak desteklenmez. |
| **Birden fazla cihazı test etmem gerekirse ne yapmalıyım?** | `SandboxOptions` listesi (ör. iPhone 8, Pixel 4) üzerinde döngü kurarak her biri için aynı yükleme‑ve‑başlık mantığını çalıştırın. |
| **Kendinden imzalı sertifikalara sahip HTTPS siteleriyle çalışır mı?** | Aspose.HTML, Java’nın varsayılan SSL güven mağarasına saygı duyar. Sertifikayı JVM’in keystore’una ekleyin veya sadece test amaçlı doğrulamayı devre dışı bırakın (üretimde önerilmez). |
| **Sadece başlık yerine ekran görüntüsü nasıl alırım?** | `HTMLDocument` API'si, render edilen sayfayı PNG veya JPEG olarak dışa aktarabilen `save` metodları sağlar. Yüklemeden sonra `htmlDoc.save("output.png", SaveFormat.PNG);` kullanın. |
| **Sandbox çoklu iş parçacığı için güvenli mi?** | Her `Sandbox` örneği izole edilmiştir, ancak birden fazla iş parçacığı arasında aynı örneği senkronizasyon olmadan paylaşmaktan kaçınmalısınız. |

---

## Görsel Genel Bakış

![Diagram showing set device pixel ratio in mobile sandbox](https://example.com/images/sandbox-diagram.png "set device pixel ratio diagram")

*Yukarıdaki illüstrasyon, `SandboxOptions` yapılandırmasından (**set screen width height** ve **set device pixel ratio** dahil) bir URL yüklemeye ve başlığı çıkarmaya kadar olan akışı gösterir.*

---

## Sonuç

Artık Java’da **how to set device pixel ratio**'yi, doğru mobil taklit için **set screen width height**'i ve render işleminin başarılı olduğunu doğrulamak için **get page title java**'yı nasıl yapacağınızı biliyorsunuz. Bu kompakt iş akışı, otomatik UI testlerinde ağır tarayıcılara olan ihtiyacı ortadan kaldırır ve CI boru hatlarına sorunsuz şekilde uyar.

Bir sonraki adıma hazır mısınız? Render edilen sayfayı bir görüntü olarak dışa aktarmayı deneyin veya `devicePixelRatio`'yu 1.0 ile 3.0 arasında değiştirerek CSS medya sorgusu hata ayıklamasını deneyin. Ayrıca Aspose.HTML’in PDF dönüşüm özelliklerini keşfederek mobil görünümün yazdırılabilir bir versiyonunu yakalayabilirsiniz.

Kodlamaktan keyif alın, ve mobil düzenleriniz her zaman net görünsün—piksel yoğunluğuna bakılmaksızın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}