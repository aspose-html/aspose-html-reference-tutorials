---
title: Java için Aspose.HTML'de HTML Belgesini Dosyaya Kaydetme
linktitle: Java için Aspose.HTML'de HTML Belgesini Dosyaya Kaydetme
second_title: Aspose.HTML ile Java HTML İşleme
description: Birden fazla bağlantılı kaynağı kolaylıkla yönetmek için mükemmel olan Aspose.HTML for Java'yı kullanarak bir HTML belgesini bir dosyaya nasıl kaydedeceğinizi öğrenin.
type: docs
weight: 11
url: /tr/java/saving-html-documents/save-html-to-file/
---
## giriiş
Bu eğitimde, bağlantılı kaynakları yönetirken bir HTML belgesini bir dosyaya nasıl kaydedeceğinizi keşfedeceğiz. Bu, özellikle birden fazla HTML dosyası içeren projeler üzerinde çalışırken faydalıdır; bunu diğer web sayfalarına referans veren bir web sayfası gibi düşünün. Bu kılavuzun sonunda, HTML belgelerinizi esnek ve verimli bir şekilde yönetmek için Java için Aspose.HTML'i kullanmaya hazır olacaksınız.
## Ön koşullar
Başlamadan önce, yerinde olması gereken birkaç şey var:
1.  Java Geliştirme Kiti (JDK): Makinenizde JDK'nın yüklü olduğundan emin olun. Sürüm 8 veya üzeri önerilir. İndirebilirsiniz[Burada](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html).
2.  Java Kütüphanesi için Aspose.HTML: Aspose.HTML kütüphanesini indirmeniz gerekir. Bunu sürümler sayfasından edinebilirsiniz[Burada](https://releases.aspose.com/html/java/).
3. IDE veya Metin Düzenleyici: Java geliştirme için tercih ettiğiniz herhangi bir IDE veya metin düzenleyiciyi kullanabilirsiniz. IntelliJ IDEA, Eclipse veya hatta Notepad gibi basit bir düzenleyici++ iyi olacak.
4. Temel Java Bilgisi: Java programlama temellerine aşinalık faydalı olacaktır. Dosyalarla nasıl çalışılacağını ve istisnaların nasıl ele alınacağını anlamanız gerekecektir.
Her şey tamamsa, şimdi eğlenceli kısma, yani kodlamaya geçelim!
## Paketleri İçe Aktar
Aspose.HTML'i kullanmak için gerekli paketleri Java projenize aktarmanız gerekir. Bunu şu şekilde yapabilirsiniz:
### Aspose Bağımlılıklarını Dahil Et
 Maven kullanıyorsanız, Aspose.HTML bağımlılığını ekleyebilirsiniz.`pom.xml` dosyası. İşte Maven sözdizimi:
```xml
<dependency>
   <groupId>com.aspose</groupId>
   <artifactId>aspose-html</artifactId>
   <version>{latest_version}</version>
</dependency>
```
 Değiştirdiğinizden emin olun`{latest_version}` Aspose indirme sayfasından gerçek sürüm numarasına ulaşabilirsiniz.
### Java Dosyanıza İfadeleri İçe Aktarma
Ayrıca Java dosyanızın başına ilgili içe aktarma ifadelerini de eklemeniz gerekecektir:
```java
import java.io.IOException;
```

## Adım 1: Çıktı Yolunu Hazırlama
Öncelikle belgenizin nereye kaydedileceğini belirtmeniz gerekir. Bunu kodunuzda bir dosya yolu tanımlayarak yapabilirsiniz.
```java
String documentPath = "save-with-linked-file.html";
```
 Burada ana HTML belgemize isim veriyoruz`save-with-linked-file.html`.
## Adım 2: Ana HTML Dosyasını Oluşturma
Sonra, başka bir belgeye bağlanacak olan ana HTML dosyanızı oluşturmak isteyeceksiniz. HTML içeriğini yazdığımız yer burasıdır.
```java
java.nio.file.Files.write(java.nio.file.Paths.get(documentPath), "<p>Hello World!</p><a href='linked.html'>linked file</a>".getBytes());
```
 Bu adımda, bir paragraf ve başka bir HTML belgesine bağlantı içeren basit bir HTML yapısı oluşturuyoruz`linked.html`.
## Adım 3: Bağlantılı HTML Dosyasını Oluşturma
Şimdi bir önceki adımda bahsettiğimiz bağlantılı HTML dosyasını da oluşturalım.
```java
java.nio.file.Files.write(java.nio.file.Paths.get("linked.html"), "<p>Hello linked file!</p>".getBytes());
```
Bu, ana belgenizdeki bağlantıya tıkladığınızda görüntülenecek bir HTML dosyası oluşturur.
## Adım 4: HTML Belgesini Belleğe Yükleme
Her iki dosya da oluşturulduktan sonraki adım, ana HTML belgenizi belleğe yükleyerek programlı olarak çalışmaktır.
```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument(documentPath);
```
 Bu komutla bir`HTMLDocument` Sonraki adımlarda üzerinde değişiklik yapabileceğiniz nesne.
## Adım 5: Kaydetme Seçenekleri Oluşturma
Belgenizi kaydetmeden önce, nasıl kaydedileceğini yapılandırmak çok önemlidir. Bu, bir örneğinin oluşturulmasını içerir`HTMLSaveOptions`.
```java
com.aspose.html.saving.HTMLSaveOptions options = new com.aspose.html.saving.HTMLSaveOptions();
```
## Adım 6: Kaynak İşleme Seçeneklerini Yapılandırma
Bağlantılı dosyalarınız varsa bu kısım kritiktir. Bunları çıktınıza dahil edip etmeyeceğinize veya hariç tutacağınıza karar vermelisiniz. 
```java
options.getResourceHandlingOptions().setMaxHandlingDepth(1);
```
 Ayarlama`MaxHandlingDepth` ile`1` bağlantılı belgenin ana belgenizle birlikte kaydedilmemesini sağlar. Bu değeri, gerektiği gibi bağlantılı HTML dosyalarını içerecek şekilde değiştirin.
## Adım 7: Belgeyi Kaydetme
Son olarak yapılandırılan seçenekleri kullanarak belgenizi kaydetmenin zamanı geldi.
```java
document.save("save-with-linked-file_out.html", options);
```
 Burada ana belgeyi şu şekilde kaydediyoruz:`save-with-linked-file_out.html`Belirtilen seçeneklerimizi kaydetme işlemine uygulayarak.
## Çözüm
Ve işte karşınızda! Artık Java için Aspose.HTML kullanarak bağlantılı kaynaklara sahip bir HTML belgesi kaydedebilirsiniz. Bu API yalnızca güçlü olmakla kalmaz, aynı zamanda projelerinize entegre edilmesi de kolaydır ve HTML işlemeyi çocuk oyuncağı haline getirir. İster yeni başlayan ister deneyimli bir geliştirici olun, Java için Aspose.HTML iş akışınızı önemli ölçüde iyileştirebilecek özelliklere sahiptir.
## SSS
### Aspose.HTML nedir?  
Aspose.HTML, HTML manipülasyonu, dönüşümü ve işlenmesi için kullanılan güçlü bir API'dir. Geliştiricilerin HTML belgeleriyle sorunsuz bir şekilde çalışmasını sağlar.
### HTML dosyalarıma resim ve diğer kaynakları ekleyebilir miyim?  
Evet! Aspose.HTML, resimler, stiller ve betikler dahil olmak üzere çeşitli kaynak türlerini destekleyerek kapsamlı belge işleme olanağı sağlar.
### Aspose.HTML için ücretsiz deneme sürümü mevcut mu?  
 Kesinlikle! Aspose.HTML'nin ücretsiz denemesini alabilirsiniz[Burada](https://releases.aspose.com/).
### Aspose.HTML için teknik destek nasıl alabilirim?  
 Aspose destek forumunu ziyaret edebilirsiniz[Burada](https://forum.aspose.com/c/html/29) Herhangi bir sorunuz veya yardıma ihtiyacınız varsa.
### Aspose.HTML'i ticari projelerde kullanabilir miyim?  
Evet, Aspose.HTML ticari projelerde kullanılabilir, ancak bir lisans satın almanız gerekir. Lisanslama seçeneklerini bulabilirsiniz[Burada](https://purchase.aspose.com/buy).