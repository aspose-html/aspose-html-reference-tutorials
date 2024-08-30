---
title: Java için Aspose.HTML'de HTML Belgelerine Harici CSS Uygulama
linktitle: Java için Aspose.HTML'de HTML Belgelerine Harici CSS Uygulama
second_title: Aspose.HTML ile Java HTML İşleme
description: Java için Aspose.HTML kullanarak harici CSS'yi HTML belgelerine nasıl uygulayacağınızı keşfedin! Tam bir eğitim için bu adım adım kılavuzu izleyin.
type: docs
weight: 12
url: /tr/java/editing-html-documents/apply-external-css-html-documents/
---
## giriiş
HTML belgeleriyle çalışırken, stilleri uygulamak sunum ve kullanıcı deneyiminde büyük fark yaratabilir. Java'ya dalıyorsanız ve Aspose.HTML kitaplığını kullanarak harici CSS stillerini HTML belgelerinize nasıl uygulayacağınızı öğrenmek istiyorsanız, doğru yerdesiniz! Bu kılavuz, Java veya CSS'ye yeni başlayanlar için bile kolaylaştırarak süreci adım adım aydınlatmayı amaçlamaktadır.
## Ön koşullar
Koda dalmadan önce, yerinde olması gereken birkaç şey var:
### 1. Java Geliştirme Kiti (JDK)
 Makinenizde JDK'nın yüklü olduğundan emin olun. En son sürümü şu adresten indirebilirsiniz:[Oracle'ın Java web sitesi](https://www.oracle.com/java/technologies/javase-downloads.html).
### 2. Java için Aspose.HTML
Java için Aspose.HTML'i kurmanız gerekecek. Bunu henüz yapmadıysanız, şuraya gidin:[Aspose indirme sayfası](https://releases.aspose.com/html/java/) ve kütüphaneyi al.
### 3. Bir IDE veya Metin Düzenleyici
Java kodunuzu yazmak için IntelliJ IDEA, Eclipse veya basit bir metin düzenleyicisi gibi Entegre Geliştirme Ortamı (IDE) seçin.
### 4. Java'nın Temel Bilgileri
Java programlama ve CSS temellerine aşina olmanız, kesinlikle daha rahat takip etmenize yardımcı olacaktır.
## Paketleri İçe Aktar
Her şeyi ayarladıktan sonra, bir sonraki adım Java projenize gerekli paketleri içe aktarmaktır. İhtiyacınız olanlar şunlardır:
```java
import com.aspose.html.HTMLDocument;
```
Bu içe aktarımlar HTML belgelerini düzenlemenize ve bunları PDF gibi farklı biçimlere dönüştürmenize olanak tanır.

Eğitimimizi yönetilebilir adımlara böleceğiz. Her adım, Java için Aspose.HTML kullanarak harici CSS stillerini bir HTML belgesine uygulama sürecinde size rehberlik edecektir.
## Adım 1: Bir HTML Belgesi Oluşturun
Öncelikle HTML dokümanımızı oluşturmamız gerekiyor. İçeriği basit bir HTML yapısıyla tanımlayarak başlayacağız.
```java
String content = "<div><p>Internal CSS</p><p>An internal CSS is used to define a style for a single HTML page</p></div>";
HTMLDocument document = new HTMLDocument(content, ".");
```

 Burada, aşağıdakileri içeren temel bir HTML yapısı tanımladık:`<div>` iki paragrafla.`HTMLDocument` sınıfı, HTML içeriğimizin belge gösterimini oluşturmak için kullanılır.
## Adım 2: Bir Stil Öğesi Oluşturun
 Daha sonra bir tane oluşturacağız`style` CSS kurallarımızı tutacak öğe.
```java
Element style = document.createElement("style");
style.setTextContent(".frame1 { margin-top:50px; margin-left:50px; padding:20px; width:360px; height:90px; background-color:#a52a2a; font-family:verdana; color:#FFF5EE;} \n" +
        ".frame2 { margin-top:-90px; margin-left:160px; text-align:center; padding:20px; width:360px; height:100px; background-color:#ADD8E6;}");
```

 Kullanımı`createElement` yöntemi`HTMLDocument` , yeni bir tane yaratıyoruz`<style>` öğesini oluşturup içeriğini iki sınıf için CSS tanımlarımızı içerecek şekilde ayarlayalım:`frame1` Ve`frame2`Bu sınıflar kenar boşluklarını, dolguyu, boyutları, arka plan renklerini, yazı tipi ailelerini ve metin renklerini tanımlar.
## Adım 3: Stili Belge Başlığına Ekleyin
Artık CSS'imiz hazır olduğuna göre, stil öğemizi belgenin başlığına eklememiz gerekiyor.
```java
Element head = document.getElementsByTagName("head").get_Item(0);
head.appendChild(style);
```

 Belgenin başlığını alıyoruz ve yeni oluşturduğumuz başlığı ekliyoruz`style` Bu eylem CSS'imizi HTML belgesine etkili bir şekilde entegre ederek HTML içeriğimizi biçimlendirmemize olanak tanır.
## Adım 4: Sınıfları HTML Elemanlarına Uygulayın
Daha sonra, daha önce tanımlanmış olan CSS sınıflarını paragraf elemanlarımıza uygulayacağız.
```java
HTMLElement paragraph = (HTMLElement) document.getElementsByTagName("p").get_Item(0);
paragraph.setClassName("frame1");
HTMLElement lastParagraph = (HTMLElement) document.getElementsByTagName("p").get_Item(document.getElementsByTagName("p").getLength() - 1);
lastParagraph.setClassName("frame2");
```

Burada, belgedeki ilk ve son paragraf öğelerine erişiyoruz ve onlara oluşturduğumuz CSS sınıflarını atıyoruz. Bu atama, CSS'mizde tanımlanan stillere uymalarını sağlar.
## Adım 5: Ek Stil Özelliklerini Ayarlayın
Görünümü daha da geliştirmek için paragraflarımıza ek stil özellikleri koyacağız.
```java
paragraph.getStyle().setFontSize("250%");
paragraph.getStyle().setTextAlign("center");
lastParagraph.getStyle().setColor("#434343");
lastParagraph.getStyle().setFontSize("150%");
lastParagraph.getStyle().setFontFamily("verdana");
```

Bu adımda, stillerimizi ince ayarlıyoruz. İlk paragrafın yazı tipi boyutu artırılır ve ortalanırken, son paragrafın rengi, yazı tipi boyutu ve yazı tipi ailesi tanımlanır. Bu ince ayar, okunabilirlik ve estetik çekicilik açısından önemlidir.
## Adım 6: HTML Belgesini Kaydedin
Stillerimizi uyguladıktan sonra, HTML belgesini kaydetme zamanı geldi.
```java
document.save("edit-internal-css.html");
```

 Burada, şunu kullanıyoruz:`save` yöntemi`HTMLDocument` Değiştirilen HTML içeriğini bir dosyaya yazmak için kullanılan sınıftır, böylece stillerimiz ve değişikliklerimiz korunur.
## Adım 7: Belgeyi PDF'ye Dönüştürün
Son olarak belgeyi çıktı olarak PDF formatına dönüştürelim.
```java
PdfDevice device = new PdfDevice("edit-internal-css.pdf");
document.renderTo(device);
```

 Kullanımı`PdfDevice` sınıfta, HTML belgemizin PDF'ye dönüştürülmesini ayarladık. Bu adım, biçimlendirilmiş belgeyi evrensel olarak erişilebilir bir biçimde paylaşmak istediğinizde önemlidir.
## Çözüm
Ve işte karşınızda—Aspose.HTML for Java kullanarak HTML belgelerine harici CSS uygulamak hem basit hem de ödüllendirici! Sadece birkaç satır kodla, düz metni görsel olarak çekici ve profesyonelce biçimlendirilmiş belgelere dönüştürebilirsiniz. Dolayısıyla, ister kişisel kullanım için tasarım yapın, ister raporlar oluşturun veya web içeriği geliştirin, Java'da HTML ve CSS'yi nasıl işleyeceğinizi anlamak, araç setinizde bulundurmanız gereken güçlü bir beceridir.
## SSS
### Java için Aspose.HTML nedir?
Java için Aspose.HTML, geliştiricilerin Java uygulamalarında HTML belgeleriyle çalışmasına olanak tanıyan, HTML düzenlemeden görüntülemeye kadar çok çeşitli özellikler sunan güçlü bir kütüphanedir.
### Aspose.HTML'i kullanmak için internet bağlantısına ihtiyacım var mı?
Hayır, gerekli kütüphane dosyalarını indirdikten sonra Aspose.HTML'yi çevrimdışı kullanabilirsiniz.
### Bir HTML belgesine birden fazla CSS dosyası uygulayabilir miyim?
 Evet, birden fazla oluşturabilirsiniz`<link>` Çeşitli CSS dosyaları için öğeleri belgenin başlığına ekleyin.
### Dahili ve harici CSS arasında bir fark var mı?
Evet! Dahili CSS bir HTML belgesi içerisinde tanımlanırken, harici CSS ayrı bir dosyaya yerleştirilir ve belgeye bağlanır.
### Java için Aspose.HTML desteğini nasıl alabilirim?
 Topluluk desteğine şu şekilde erişebilirsiniz:[Aspose forumu](https://forum.aspose.com/c/html/29) Herhangi bir soru veya sorununuzda bize ulaşabilirsiniz.