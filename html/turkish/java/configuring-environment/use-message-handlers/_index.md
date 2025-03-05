---
title: Java için Aspose.HTML'de Mesaj İşleyicilerini Kullanma
linktitle: Java için Aspose.HTML'de Mesaj İşleyicilerini Kullanma
second_title: Aspose.HTML ile Java HTML İşleme
description: Java için Aspose.HTML'de eksik resimleri ve diğer ağ işlemlerini etkili bir şekilde yönetmek için ileti işleyicilerinin nasıl kullanılacağını öğrenin.
type: docs
weight: 12
url: /tr/java/configuring-environment/use-message-handlers/
---
## giriiş
Bu eğitimde, Java için Aspose.HTML'de mesaj işleyicileri kullanmanın pratik bir örneğini size göstereceğiz. Eksik bir görüntüye başvuran basit bir HTML belgesi hazırlayacağız ve özel bir mesaj işleyicisi kullanarak hatayı nasıl yakalayacağınızı ve işleyeceğinizi göstereceğiz. Aspose.HTML'e yeni başlıyor olun veya becerilerinizi genişletmek istiyor olun, bu kılavuz size ağ operasyonlarını etkili bir şekilde yönetmek için ihtiyaç duyduğunuz içgörüleri sağlayacaktır.
## Ön koşullar
Adım adım kılavuza dalmadan önce ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım:
1.  Java Geliştirme Kiti (JDK): Sisteminizde JDK'nın yüklü olduğundan emin olun. Bunu şu adresten indirebilirsiniz:[Oracle web sitesi](https://www.oracle.com/java/technologies/javase-downloads.html).
2.  Java için Aspose.HTML: Java için Aspose.HTML'in yüklü olması gerekir. Bunu şuradan indirebilirsiniz:[Aspose sürüm sayfası](https://releases.aspose.com/html/java/).
3. IDE: IntelliJ IDEA, Eclipse veya NetBeans gibi favori Java Entegre Geliştirme Ortamınızı (IDE) kullanın.
4. Temel Java Bilgisi: Bu eğitimi etkili bir şekilde takip edebilmek için Java programlamaya aşina olmak şarttır.
5.  Geçici Lisans: Aspose.HTML'nin deneme sürümünü kullanıyorsanız, bir tane edinmeyi düşünün.[geçici lisans](https://purchase.aspose.com/temporary-license/) geliştirme sırasında herhangi bir sınırlamayla karşılaşmamak için.

## Paketleri İçe Aktar
Başlamadan önce, Java projenize gerekli paketlerin aktarıldığından emin olun. Aşağıda ihtiyacınız olacak temel içe aktarımlar yer almaktadır:
```java
import java.io.IOException;
```
Bu içe aktarımlar, ağ işlemlerini yönetmek, HTML belgeleri oluşturmak ve HTML'den PNG'ye dönüştürmeyi gerçekleştirmek için gereken sınıflara ve yöntemlere erişmenizi sağlayacaktır.

## Adım 1: HTML Kodunu Hazırlayın
İlk ihtiyacımız olan şey bir resim dosyasına başvuran basit bir HTML kodudur. Hata işleme mekanizmasını tetiklemek için var olmayan bir resme kasıtlı olarak başvuracağız.
```java
String code = "<img src='missing.jpg'>";
```
 Bu kod parçacığı, adlı bir resmi yüklemeye çalışan bir HTML öğesi oluşturur.`missing.jpg`. Bu resim dosyası mevcut olmadığından, belge yükleme işlemi sırasında bir hata tetiklenecektir.
## Adım 2: HTML Kodunu Bir Dosyaya Yazın
Daha sonra bu HTML kodunu daha sonra yükleyebileceğimiz bir dosyaya yazmamız gerekiyor.
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
 Burada bir`FileWriter` HTML kodumuzu adlı bir dosyaya yazmak için`document.html`Bu dosya aşağıdaki adımlarda bir HTML belgesi oluşturmak için kullanılacaktır.
## Adım 3: Özel bir Mesaj İşleyicisi Oluşturun
Şimdi, eksik resim senaryosunu işlemek için özel bir mesaj işleyicisi oluşturalım. Mesaj işleyicisi yanıtın durum kodunu kontrol edecek ve dosya bulunamazsa bir mesaj yazdıracaktır.
```java
com.aspose.html.net.MessageHandler handler = new com.aspose.html.net.MessageHandler() {
    @Override
    public void invoke(com.aspose.html.net.INetworkOperationContext context) {
        if (context.getResponse().getStatusCode() != 200) {
            System.out.println(String.format("File '%s' Not Found", context.getRequest().getRequestUri().toString()));
        }
        invoke(context);
    }
};
```
 Bu işleyicide,`invoke` yöntem, ağ işleminin yanıtının durum kodunu kontrol eder. Durum kodu 200 değilse (başarıyı gösterir), dosyanın bulunamadığını belirten bir ileti yazdırır.`invoke(context);` satırı, zincirdeki bir sonraki işleyicinin çağrılmasını sağlar.
## Adım 4: Ağ Hizmetini Yapılandırın
 Özel mesaj işleyicimizi kullanmak için, onu ağ hizmetindeki mevcut mesaj işleyicileri zincirine eklememiz gerekir. Bu,`Configuration` sınıf.
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
Burada, bir örnek oluşturuyoruz`Configuration` ve geri al`INetworkService`. Sonra, özel işleyicimizi mesaj işleyicileri listesine ekleriz. Bu kurulum, işleyicimizin ağ işlemleri sırasında çağrılmasını sağlar.
## Adım 5: HTML Belgesini Yükleyin
Yapılandırma yerindeyken artık HTML belgemizi yükleyebiliriz. Belge eksik resmi yüklemeye çalışacak ve özel mesaj işleyicimizi tetikleyecektir.
```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Ek işlemler buraya gelecek
} finally {
    if (document != null) {
        document.dispose();
    }
}
```
Bu kod parçası, daha önce kurduğumuz yapılandırmayı kullanarak HTML belgesini yükler. Belgenin yükleme işlemi eksik resmi yüklemeyi deneyecek ve mesaj işleyicimiz ortaya çıkan hatayı yakalayıp işleyecektir.
## Adım 6: HTML'yi PNG'ye dönüştürün
Özetlemek gerekirse, HTML belgesini PNG resmine dönüştürelim. Bu adım, eksik resmi işlemek için kesinlikle gerekli değildir, ancak Aspose.HTML'nin daha geniş işlevselliğini gösterir.
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
 Burada şunu kullanıyoruz:`Converter.convertHTML` HTML belgesini PNG dosyasına dönüştürme yöntemi.`ImageSaveOptions`Görüntüyü kaydetmek için çözünürlük ve format gibi seçenekleri belirtmemizi sağlar.
## Adım 7: Kaynakları Temizleyin
 Son olarak, işlem sırasında kullanılan tüm kaynakları her zaman temizlediğinizden emin olun. Bu,`Configuration` Ve`HTMLDocument` nesneler.
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
Bu, tüm kaynakların serbest bırakılmasını sağlayarak, uygulamanızdaki bellek sızıntılarını ve diğer potansiyel sorunları önler.

## Çözüm
Ve işte karşınızda—Java için Aspose.HTML'de ileti işleyicilerini kullanma konusunda kapsamlı bir kılavuz! Bir HTML belgesi kurma, özel bir ileti işleyicisi oluşturma ve eksik kaynakları bir profesyonel gibi yönetme sürecini ele aldık. Eksik resimlerle, bozuk bağlantılarla veya diğer ağla ilgili sorunlarla uğraşıyor olun, bu yaklaşım size bunları Java uygulamalarınızda etkili bir şekilde yönetmek için ihtiyaç duyduğunuz kontrolü sağlayacaktır.

## SSS
### Java için Aspose.HTML nedir?
Java için Aspose.HTML, geliştiricilerin Java uygulamalarında HTML belgeleri oluşturmasına, düzenlemesine ve dönüştürmesine olanak tanıyan güçlü bir kütüphanedir.
### Java için Aspose.HTML'de neden mesaj işleyicileri kullanılır?
İleti işleyicileri, eksik kaynakları yönetme veya istekleri ve yanıtları değiştirme gibi ağ işlemlerini engellemenize ve yönetmenize olanak tanır.
### Tek bir yapılandırmada birden fazla mesaj işleyicisi kullanabilir miyim?
Evet, ağ işlemleri sırasında farklı senaryoları ele almak için birden fazla mesaj işleyicisini birbirine bağlayabilirsiniz.
### Configuration ve HTMLDocument nesnelerini elden çıkarmak gerekli mi?
Evet, bu nesnelerin elden çıkarılması tüm kaynakların düzgün bir şekilde serbest bırakılmasını sağlayarak bellek sızıntılarının önlenmesini sağlar.
### Mesaj işleyicileriyle diğer hata türlerini de işleyebilir miyim?
Kesinlikle! Mesaj işleyicileri yalnızca eksik kaynakları değil, çeşitli hata türlerini de işleyecek şekilde özelleştirilebilir.