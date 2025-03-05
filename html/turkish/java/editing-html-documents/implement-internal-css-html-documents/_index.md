---
title: Java için Aspose.HTML ile HTML Belgelerinde Dahili CSS'yi Uygulayın
linktitle: Java için Aspose.HTML ile HTML Belgelerinde Dahili CSS'yi Uygulayın
second_title: Aspose.HTML ile Java HTML İşleme
description: Kolay adım adım eğitimimiz ile Java için Aspose.HTML'i kullanarak HTML belgelerinde dahili CSS'yi uygulamayı öğrenin.
type: docs
weight: 16
url: /tr/java/editing-html-documents/implement-internal-css-html-documents/
---
## giriiş
Güzel ve iyi yapılandırılmış web sayfaları oluşturmak genellikle tek bir önemli unsura dayanır: stil. Web geliştirmede, CSS (Basamaklı Stil Sayfaları) HTML'nizin giydirilmesi gibidir; her şeyi çekici ve düzenli gösterir. Bugün, Java için Aspose.HTML kullanarak dahili CSS'yi HTML belgelerine nasıl entegre edeceğinizi ele alacağız. İster yeni başlayan ister deneyimli bir geliştirici olun, bu eğitim adımları basit ve ilgi çekici bir şekilde açıklayacaktır.
## Ön koşullar
Hemen başlamadan önce, bu öğreticiyi takip etmek için ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım. İşte ön koşullar:
1.  Java Geliştirme Kiti (JDK): Makinenizde JDK'nın yüklü olduğundan emin olun. Bunu şu adresten indirebilirsiniz:[Oracle web sitesi](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html) veya[AçıkJDK](https://openjdk.java.net/).
2.  Java için Aspose.HTML kütüphanesi: HTML belgelerini kolayca işlemek ve düzenlemek için Aspose.HTML kütüphanesine ihtiyacınız olacak. Kütüphaneyi şu adresten indirebilirsiniz:[Aspose web sitesi](https://releases.aspose.com/html/java/).
3. Entegre Geliştirme Ortamı (IDE): IntelliJ IDEA veya Eclipse gibi iyi bir IDE kodlamayı çok daha akıcı hale getirebilir.
4. Temel Java bilgisi: Bu eğitimde Java programlama konusunda bir miktar bilginiz olduğunu varsayıyoruz.
5. Zaman ve Sabır: Bu süreç basit görünse de, adım adım ilerlemek önemlidir.
## Paketleri İçe Aktar
Kodlamaya başlamadan önce programımızın Aspose.HTML'in sağladığı özelliklere erişebilmesini sağlamak için gerekli paketleri import edelim.
```java
import java.io.IOException;
```
Bu içe aktarma ifadelerini Java dosyanızın en üstüne eklediğinizden emin olun. Bu, HTML belgesini oluşturmak ve düzenlemek ve onu PDF olarak işlemek için gereken sınıfları kullanmamızı sağlayacaktır.
Süreci kolayca takip edebilmeniz için süreci farklı adımlara bölelim.
## Adım 1: Bir HTML Belgesinin Örneğini Oluşturun
Öncelikle, HTML belgesinin bir örneğini oluşturmamız gerekiyor. İşte nasıl yapıldığı:
```java
String content = "<div><p>Internal CSS</p><p>An internal CSS is used to define a style for a single HTML page</p></div>";
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument(content, ".");
```
 Burada, iki paragrafın içinde olduğu basit bir HTML yapısı tanımlıyoruz`div` .`HTMLDocument` örnek, bu yapıyı başlatır ve değişiklik ve biçimlendirmeye hazır hale getirir.
## Adım 2: Stil Öğesini Oluşturun ve Ekleyin
Sonra, dahili CSS stillerimizi oluşturacağız. Stilin büyüsü burada başlıyor!
```java
com.aspose.html.dom.Element style = document.createElement("style");
style.setTextContent(".frame1 { margin-top:50px; margin-left:50px; padding:20px; width:360px; height:90px; background-color:#a52a2a; font-family:verdana; color:#FFF5EE;}" +
                      ".frame2 { margin-top:-90px; margin-left:160px; text-align:center; padding:20px; width:360px; height:100px; background-color:#ADD8E6;}");
```
 Bu adımda bir tane oluşturuyoruz`<style>` öğe ve iki CSS sınıfının tanımlanması—`frame1` Ve`frame2`. Her sınıfın kenar boşluğu, dolgu, arka plan rengi ve yazı tipi özellikleri için belirli stilleri vardır. Dahili CSS'imizin şekillenmeye başladığı yer burasıdır.
## Adım 3: Stil Öğesini Belge Başlığına Ekleyin
Stillerimizi oluşturduğumuza göre, şimdi bunları belgenin başlığına eklememiz gerekiyor.
```java
com.aspose.html.dom.Element head = document.getElementsByTagName("head").get_Item(0);
head.appendChild(style);
```
 Bu kod parçacığı şunu bulur:`head` belgenin ve ekler`<style>` Bu, CSS stillerimizi aşağıdaki HTML içeriğiyle birleştirir.
## Adım 4: CSS Sınıflarını HTML Öğelerine Atamak
Şimdi, tanımladığımız stilleri belgemizdeki paragraf öğelerine uygulayalım.
```java
com.aspose.html.HTMLElement paragraph = (com.aspose.html.HTMLElement) document.getElementsByTagName("p").get_Item(0);
paragraph.setClassName("frame1");
HTMLElement lastParagraph = (HTMLElement) document.getElementsByTagName("p").get_Item(document.getElementsByTagName("p").getLength() - 1);
lastParagraph.setClassName("frame2");
```
 Burada, paragraf öğelerini alıyoruz ve sınıf adlarını şu şekilde ayarlıyoruz:`frame1` Ve`frame2`. Artık paragraflarımız az önce tanımladığımız stilleri devralacak!
## Adım 5: Stil Özelliklerini Özelleştirin
Paragraflarımızın stil özelliklerini özelleştirerek görsel sunumu daha da geliştirelim.
```java
paragraph.getStyle().setFontSize("250%");
paragraph.getStyle().setTextAlign("center");
lastParagraph.getStyle().setColor("#434343");
lastParagraph.getStyle().setFontSize("150%");
lastParagraph.getStyle().setFontFamily("verdana");
```
Bu adımda, ilk paragrafın yazı tipi boyutunu ve hizalamasını değiştiririz, ikinci paragrafın rengini ve yazı tipini ayarlarız. Bu özelleştirme, belgenize kişilik ve netlik katar.
## Adım 6: HTML Belgesini Kaydedin
Artık dahili CSS'imizi tamamlayıp değişikliklerimizi yaptığımıza göre, belgeyi bir dosyaya kaydetmenin zamanı geldi.
```java
document.save("edit-internal-css.html");
```
 The`save` yöntem, belgemizi adlı bir HTML dosyasına kaydeder`edit-internal-css.html`Değişikliklerinizi eylem halinde görmek için bu dosyayı herhangi bir web tarayıcısında açabilirsiniz!
## Adım 7: HTML Belgesini PDF'ye Dönüştürün
Son adım olarak, biçimlendirilmiş HTML belgemizi PDF formatına dönüştürelim. Bu, biçimlendirilmiş içeriğinizi paylaşmak veya yazdırmak için özellikle yararlıdır.
```java
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice("edit-internal-css.pdf");
document.renderTo(device);
```
 Burada bir tane yaratıyoruz`PdfDevice` İstenilen çıktı dosyamıza işaret eden örnek.`renderTo` yöntemi daha sonra HTML belgesini PDF'e dönüştürür. Ne kadar harika?
## Çözüm
Ve işte oldu! Artık Java için Aspose.HTML kullanarak HTML belgelerinde dahili CSS'yi nasıl uygulayacağınızı biliyorsunuz. Bu öğreticiyi takip ederek, yalnızca HTML'yi nasıl biçimlendireceğinizi değil, aynı zamanda onu PDF olarak nasıl kaydedeceğinizi ve işleyeceğiniz de öğrendiniz. Bu araçlarla, web sayfalarınızı stil ve profesyonellikle öne çıkarabilirsiniz. Öyleyse neden bekliyorsunuz? Hemen dalın ve stil seçenekleriyle oynayın!

## SSS
### Dahili CSS kullanmanın avantajı nedir?  
Dahili CSS, diğerlerini etkilemeden tek bir HTML belgesini biçimlendirmenize olanak tanır ve bu da onu benzersiz tasarımlar için mükemmel hale getirir.
### Aspose.HTML harici CSS dosyalarını işleyebilir mi?  
Evet, Aspose.HTML harici CSS dosyalarını işleyebilir; bunları da benzer şekilde dahili stillere bağlayabilirsiniz.
### Aspose.HTML açık kaynaklı mı?  
Hayır, Aspose.HTML ticari bir kütüphanedir, ancak özelliklerini keşfetmek için ücretsiz deneme sürümüyle başlayabilirsiniz.
### Sorunlarla karşılaşırsam destek ekibiyle nasıl iletişime geçebilirim?  
 Ziyaret edebilirsiniz[Aspose destek forumu](https://forum.aspose.com/c/html/29) yardım için.
### HTML'yi PDF'ye dönüştürürken performans hususları var mı?  
Evet, karmaşık HTML belgelerinin işlenmesi daha uzun sürebilir; içeriği optimize etmek performansı artırabilir.