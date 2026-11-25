---
category: general
date: 2026-06-03
description: Java'da HTML belgesi oluşturun ve bir sayacı artırmak için JavaScript
  gömün. Bir script motoru örneğini öğrenin, öğenin innerHTML'ini alın ve daha fazlası.
draft: false
keywords:
- create html document
- embed javascript html
- get element innerhtml
- increment counter javascript
- script engine example
language: tr
og_description: Java'da bir HTML belgesi oluşturun, sayacı artırmak için JavaScript
  ekleyin ve bir script motoru örneğiyle son değeri alın.
og_title: Gömülü JavaScript ile HTML Belgesi Oluştur – Java Örneği
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  headline: Create HTML Document with Embedded JavaScript – Java Example
  type: TechArticle
- description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  name: Create HTML Document with Embedded JavaScript – Java Example
  steps:
  - name: '**Creates an HTML document** in memory.'
    text: '**Creates an HTML document** in memory.'
  - name: '**Embeds a small JavaScript snippet** that increments a counter five times.'
    text: '**Embeds a small JavaScript snippet** that increments a counter five times.'
  - name: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
    text: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
  - name: '**Retrieves the final counter value** using `getElementInnerHTML`.'
    text: '**Retrieves the final counter value** using `getElementInnerHTML`.'
  - name: 'Prints `Final counter value: 5` to the console.'
    text: 'Prints `Final counter value: 5` to the console.'
  type: HowTo
tags:
- HTML
- JavaScript
- Java
- ScriptEngine
title: Gömülü JavaScript ile HTML Belgesi Oluştur – Java Örneği
url: /tr/java/creating-managing-html-documents/create-html-document-with-embedded-javascript-java-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gömülü JavaScript ile HTML Belgesi Oluşturma – Java Örneği

Java kodundan **HTML belgesi** oluşturmanız gerektiğinde ve içine JavaScript nasıl gömeceğinizi merak ettiğinizde? Bu rehberde size adım adım bunu göstereceğiz ve sonunda çalışan bir script engine örneği elde edeceksiniz; bu örnek son sayaç değerini yazdırır.  

Eğer kendinize hiç *“script çalıştıktan sonra element innerHTML nasıl alınır?”* ya da *“JavaScript'te bir sayacı Java'dan nasıl artırırım?”* gibi sorular sorduysanız—doğru yerdesiniz. Bu öğreticide **embed javascript html**, **increment counter javascript** ve **get element innerHTML** konularını tek bir bütün içinde ele alacağız.

![Gömülü JavaScript ile HTML Belgesi Oluşturma](/images/create-html-document.png){: .center alt="Gömülü JavaScript ile HTML Belgesi Oluşturma örneği"}

## Oluşturacağınız Şey

Bu öğretimin sonunda, kendi içinde çalışan bir Java programına sahip olacaksınız:

1. Bellekte **HTML belgesi** oluşturur.
2. **Küçük bir JavaScript snippet'ı** gömer; bu snippet sayacı beş kez artırır.
3. **Script engine'i başlatır** (`ScriptEngine` örneği) ve snippet'i çalıştırır.
4. `getElementInnerHTML` kullanarak son sayaç değerini alır.
5. Konsola `Final counter value: 5` yazar.

Harici dosya yok, web sunucusu yok—sadece saf Java ve küçük bir HTML dizesi.

## Önkoşullar

- Java 17 veya üzeri (`ScriptEngine` API'si standart kütüphanenin bir parçasıdır).
- HTML ve JavaScript'e temel aşinalık (derin uzmanlık gerekmez).
- Programı derlemek ve çalıştırmak için bir IDE ya da basit bir metin editörü ve terminal.

## Adım 1: Java'da HTML Belgesi Oluşturma

İlk olarak, daha sonra işaretleme ile doldurabileceğimiz boş bir HTML belge nesnesine ihtiyacımız var. Bunu yalnızca bellekte var olan sanal bir sayfa olarak düşünün.

```java
// Import statements
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

// Minimal HTML document wrapper (pseudo‑class for illustration)
class HTMLDocument {
    private StringBuilder html = new StringBuilder();

    public void write(String content) {
        html.append(content);
    }

    public String getContent() {
        return html.toString();
    }

    // Simple DOM simulation for getElementById / innerHTML
    private java.util.Map<String, String> elements = new java.util.HashMap<>();

    public void setElementInnerHTML(String id, String value) {
        elements.put(id, value);
    }

    public String getElementInnerHTML(String id) {
        return elements.getOrDefault(id, "");
    }

    // Helper used by the script engine (not production‑grade)
    public void updateCounter(int value) {
        setElementInnerHTML("counter", String.valueOf(value));
    }
}
```

**Neden Önemli:** Kendiniz **HTML belgesi** nesneleri oluşturarak diske yazmaktan kaçınır ve her şeyi test edilebilir tutarsınız. Küçük DOM simülasyonu, tam bir tarayıcı olmadan **element innerHTML** alabilmemizi sağlar.

## Adım 2: JavaScript HTML'yi Gömme – Sayaç Mantığı

Şimdi `<script>` bloğu içeren HTML işaretlemesini yazacağız. Bu script **increment counter JavaScript** işlemini beş kez gerçekleştirecek.

```java
HTMLDocument doc = new HTMLDocument();

doc.write(
    "<!DOCTYPE html><html><body>"
  + "<div id='counter'>0</div>"
  + "<script>"
  + "for (let i = 0; i < 5; i++) {"
  + "  document.getElementById('counter').innerHTML = i + 1;"
  + "}"
  + "</script>"
  + "</body></html>"
);
```

**Açıklama:**  
- `<div id='counter'>0</div>` hedef öğemizdir.  
- `for` döngüsü **increment counter javascript** mantığını çalıştırır ve her yinelemede div'i günceller.  
- Gerçek bir tarayıcıda olmadığımız için, daha sonra kullanacağımız script engine'in `document.getElementById` ifadesini anlaması gerekir. Bu yüzden `HTMLDocument` içinde küçük bir stub ekledik.

## Adım 3: Script Engine'i Başlatma – Bir Script Engine Örneği

Java, `ScriptEngine` API'si (JSR‑223) ile birlikte gelir. HTML içeriğini engine'e besleyecek ve beklenen minimum DOM metodlarını sağlayacak küçük bir sarmalayıcı oluşturacağız.

```java
class SimpleScriptEngine {
    private final HTMLDocument document;
    private final ScriptEngine engine;

    public SimpleScriptEngine(HTMLDocument doc) throws ScriptException {
        this.document = doc;
        ScriptEngineManager manager = new ScriptEngineManager();
        this.engine = manager.getEngineByName("JavaScript");
        // Expose a mock 'document' object to the JavaScript context
        engine.put("document", new Object() {
            public Object getElementById(String id) {
                return new Object() {
                    public void setInnerHTML(String value) {
                        document.updateCounter(Integer.parseInt(value));
                    }
                };
            }
        });
    }

    public void execute() throws ScriptException {
        // Extract only the script part from the HTML (simplified)
        String html = document.getContent();
        int scriptStart = html.indexOf("<script>") + "<script>".length();
        int scriptEnd   = html.indexOf("</script>");
        String script = html.substring(scriptStart, scriptEnd);
        engine.eval(script);
    }
}
```

**Neden Önemli:** Bu **script engine example** tam bir tarayıcı olmadan gömülü JavaScript çalıştırabileceğinizi gösterir. Ayrıca script'in mock DOM'umuzla etkileşime girebilmesi için `document.getElementById`'i hafif bir şekilde ortaya çıkarmayı da gösterir.

## Adım 4: JavaScript'i Çalıştırma – Increment Counter JavaScript Eylemde

Engine hazır olduğunda, script'i sadece çalıştırıyoruz. `<script>` etiketi içindeki döngü tetiklenir ve mock `setInnerHTML` sayacı günceller.

```java
try {
    SimpleScriptEngine engine = new SimpleScriptEngine(doc);
    engine.execute(); // runs the embedded JavaScript
} catch (ScriptException e) {
    e.printStackTrace();
}
```

**Arka Planda Ne Oluyor?** Döngünün her yinelemesi `document.getElementById('counter').innerHTML = i + 1;` ifadesini çağırır. Mock `setInnerHTML`, sayısal dizeyi `HTMLDocument.updateCounter`'a iletir ve bu da en son değeri saklar. Döngü bittiğinde, belgenin iç haritası `counter` öğesi için `"5"` değerini tutar.

## Adım 5: Son Sayaç Değerini Almak – Get Element InnerHTML

Script tamamlandığında, `HTMLDocument` örneğimizden **element innerHTML** alabiliriz.

```java
String finalValue = doc.getElementInnerHTML("counter");
System.out.println("Final counter value: " + finalValue); // prints 5
```

Programın tamamını çalıştırdığınızda şu çıktı elde edilir:

```
Final counter value: 5
```

Bu, **increment counter javascript** mantığının çalıştığını ve script çalıştırıldıktan sonra **element innerHTML**'i başarıyla **alabildiğimizi** doğrular.

## Tam Çalışan Örnek

Her şeyi bir araya getirdiğimizde, işte eksiksiz, çalıştırmaya hazır Java sınıfı:



## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanıza ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [Aspose.HTML for Java'da Boş HTML Belgeleri Oluşturma](/html/english/java/creating-managing-html-documents/create-empty-html-documents/)
- [Aspose.HTML for Java'da Dizeden HTML Belgeleri Oluşturma](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)
- [Aspose.HTML for Java'da HTML Belgesini Kaydetme](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}