---
category: general
date: 2026-10-12
description: Handelbars kullanarak veriden tablo oluşturmayı ve JSON ile tabloyu doldurmayı
  öğrenin. Dinamik HTML tablolarında satırları tekrarlamak için adım adım rehber.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate table from data
- populate table from json
- repeat table rows
- dynamic html table
- dynamic table rows
language: tr
lastmod: 2026-10-12
og_description: Verilerden tablo oluşturun ve Handlebars kullanarak JSON'dan tabloyu
  doldurun. Tekrarlayan tablo satırlarıyla dinamik HTML tabloları oluşturmak için
  bu öğreticiyi izleyin.
og_image_alt: Screenshot showing generated table from data in a web page
og_title: Handlebars ile veriden tablo oluşturma – kapsamlı rehber
schemas:
- author: Aspose
  dateModified: '2026-10-12'
  description: Learn how to generate table from data and populate table from JSON
    using Handlebars. Step‑by‑step guide for repeat table rows in dynamic HTML tables.
  headline: How to generate table from data with HTML and Handlebars
  type: TechArticle
- description: Learn how to generate table from data and populate table from JSON
    using Handlebars. Step‑by‑step guide for repeat table rows in dynamic HTML tables.
  name: How to generate table from data with HTML and Handlebars
  steps:
  - name: 1. Empty data sets
    text: 'If the JSON array is empty, Handlebars will still render the header row
      but no data rows. To display a friendly message, wrap the table in a conditional
      block:'
  - name: 2. Nested loops (e.g., multiple addresses per person)
    text: 'When a person can have several addresses, you can nest another `{{#foreach}}`
      inside the row:'
  - name: 3. Using a real API
    text: 'Replace the static `<script id="people-data">` with a fetch call:'
  - name: 4. Accessibility considerations
    text: '* Add `scope="col"` to `<th>` elements. * Use `<caption>` to describe the
      table purpose. * Ensure sufficient color contrast if you apply custom CSS.'
  type: HowTo
tags:
- HTML
- Handlebars
- JSON
- templating
title: HTML ve Handlebars ile veriden tablo oluşturma
url: /tr/java/creating-managing-html-documents/how-to-generate-table-from-data-with-html-and-handlebars/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML ve Handlebars ile veriden tablo oluşturma

Bir web sayfasında **veriden tablo oluşturmanız** gerekiyorsa, bu öğretici tam olarak nasıl yapılacağını gösterir. Basit bir Handlebars döngüsü kullanarak **JSON'dan tablo doldurabilir**, **tablo satırlarını tekrarlayabilir** ve kaynak değiştiğinde güncellenen tamamen **dinamik bir HTML tablo** elde edebilirsiniz.

Önümüzdeki birkaç dakikada tam bir, çalıştırılabilir örnek görecek, her parçanın neden önemli olduğunu anlayacak ve koşullu sütunlar ya da iç içe nesneler gibi daha karmaşık senaryolar için bu deseni nasıl uyarlayacağınızı öğreneceksiniz.

## Ne oluşturacağız

* Kişilerin bir listesini içeren bir JSON yükünü okur.
* Her kişi için bir tablo satırını tekrar eder (`repeat table rows`).
* Her kişinin adını, soyadını ve adresini uygun hücrelere ekler.
* Sunucu tarafı renderlaması olmadan çalışır – tüm süreç tarayıcıda gerçekleşir.

**Önkoşullar**

* HTML ve JavaScript hakkında temel bilgi.
* Modern bir tarayıcı (Chrome, Edge, Firefox veya Safari).
* Handlebars.js – bir CDN'den yükleyeceğiz, bu yüzden derleme araçlarına ihtiyaç yok.

---

## Adım 1: JSON veri kaynağını hazırlama

İlk adım, bir API'den alacağınız JSON'a benzer bir JavaScript nesnesi tanımlamaktır. Handlebars düz nesnelerle çalışır, bu yüzden veriyi gösterim amaçlı doğrudan bir `<script>` etiketi içinde gömebilirsiniz.

```html
<script id="people-data" type="application/json">
{
  "Persons": {
    "Person": [
      {
        "FirstName": "Alice",
        "LastName": "Anderson",
        "Address": {
          "Street": "Maple",
          "Number": "123",
          "City": "Springfield"
        }
      },
      {
        "FirstName": "Bob",
        "LastName": "Baker",
        "Address": {
          "Street": "Oak",
          "Number": "456",
          "City": "Rivertown"
        }
      }
    ]
  }
}
</script>
```

**Neden önemli** – Veriyi ayrı bir `<script>` öğesinde tutarak, daha sonra gerçek bir AJAX çağrısıyla kolayca değiştirebilirsiniz. Yapı (`Persons.Person`) Handlebars `{{#foreach Persons.Person}}` bloğunda kullanılan yolla eşleşir ve bu, **JSON'dan tablo doldurmak** için gereklidir.

---

## Adım 2: Satırları tekrarlayan Handlebars şablonunu yazma

Sonra, tablo işaretlemesini içeren bir `<script type="text/x-handlebars-template">` bloğu oluşturun. Handlebars yer tutucuları gerçek değerlerle değiştirir ve her kişi için `<tr>` öğesini tekrar eder.

```html
<script id="table-template" type="text/x-handlebars-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <!-- Header row describing the columns -->
  <tr>
    <th>Person</th>
    <th>Address</th>
  </tr>
  <!-- Data row – this block is repeated for each Person -->
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
</table>
</script>
```

**Ana bölümlerin açıklaması**

* `{{#foreach Persons.Person}}` Handlebars'e `Persons.Person` dizisindeki her giriş için **tablo satırlarını tekrarlamasını** söyler.
* `{{FirstName}} {{LastName}}` ve `{{Address.*}}` ifadeleri mevcut dizi elemanından değerleri çeker.
* Tüm tabloyu bir `data_merge` özniteliğiyle sarmak isteğe bağlıdır; bu, sonraki işleme veya CSS seçicileri için faydalı olabilir.

---

## Adım 3: Handlebars'ı yükleyin ve şablonu derleyin

Handlebars'ı bir CDN'den çekecek, JSON'ı ayrıştıracak, şablonu derleyecek ve son HTML'i sayfaya enjekte edeceğiz.

```html
<script src="https://cdn.jsdelivr.net/npm/handlebars@4.7.7/dist/handlebars.min.js"></script>
<script>
  // Parse the JSON stored in the <script id="people-data">
  const rawData = document.getElementById('people-data').textContent;
  const context = JSON.parse(rawData);

  // Grab the template markup and compile it
  const source = document.getElementById('table-template').innerHTML;
  const template = Handlebars.compile(source);

  // Generate the final HTML by applying the context
  const html = template(context);

  // Insert the generated table into the DOM
  document.getElementById('output').innerHTML = html;
</script>
```

**Neden çalışma zamanında derleyelim?** – Şablonu bir kez derleyip yeniden kullanmak sayfayı hızlı tutar, özellikle veri sık sık değiştiğinde. Bu desen, sayfayı yeniden yüklemeden **JSON'dan tablo doldurmayı** birden çok kez yapmayı da çok basitleştirir.

---

## Adım 4: Oluşturulan tablo için bir konteyner ayırma

Dinamik tablonun görüneceği bir yer tutucu `<div>` ekleyin. Bu, işaretlemenin temiz kalmasını sağlar ve statik düzen ile oluşturulan içerik arasındaki sorumlulukları ayırır.

```html
<div id="output"></div>
```

Adım 3'teki script çalıştığında, `<div id="output">` içinde tamamen oluşturulmuş bir `<table>` öğesi bulunacak ve stil vermeye ya da daha fazla manipülasyona hazır olacaktır.

---

## Adım 5: Çıktıyı doğrulama ve tabloyu stil verme (isteğe bağlı)

Sayfayı bir tarayıcıda açın ve aşağıdaki gibi bir tablo görmelisiniz:

![Veriden oluşturulan tabloyu gösteren ekran görüntüsü](image.png "Veriden oluşturulan tabloyu gösteren ekran görüntüsü")

```html
<table border="1" data_merge="true">
  <tr>
    <th>Person</th>
    <th>Address</th>
  </tr>
  <tr>
    <td>Alice Anderson</td>
    <td>Maple 123, Springfield</td>
  </tr>
  <tr>
    <td>Bob Baker</td>
    <td>Oak 456, Rivertown</td>
  </tr>
</table>
```

**İsteğe bağlı stil** – Daha temiz bir görünüm isterseniz, birkaç CSS kuralı ekleyin:

```html
<style>
  table { border-collapse: collapse; width: 100%; }
  th, td { padding: 8px; text-align: left; }
  th { background-color: #f2f2f2; }
</style>
```

---

## Kenar durumlarını ve yaygın varyasyonları ele alma

### 1. Boş veri setleri

JSON dizisi boşsa, Handlebars başlık satırını yine de render eder ancak veri satırları olmaz. Dostça bir mesaj göstermek için tabloyu koşullu bir blokla sarmalayın:

```handlebars
{{#if Persons.Person.length}}
  {{!-- existing table markup --}}
{{else}}
  <p>No persons found.</p>
{{/if}}
```

### 2. İç içe döngüler (ör. kişi başına birden fazla adres)

Bir kişinin birden fazla adresi olabileceğinde, satır içinde başka bir `{{#foreach}}` döngüsü iç içe yerleştirebilirsiniz:

```handlebars
{{#foreach Persons.Person}}
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>
      {{#foreach Address}}
        {{Street}} {{Number}}, {{City}}<br>
      {{/foreach}}
    </td>
  </tr>
{{/foreach}}
```

### 3. Gerçek bir API kullanma

Statik `<script id="people-data">` öğesini bir fetch çağrısı ile değiştirin:

```javascript
fetch('/api/persons')
  .then(r => r.json())
  .then(context => {
    const html = template(context);
    document.getElementById('output').innerHTML = html;
  });
```

Bu, canlı veri çekerken aynı **dinamik tablo satırları** tekniğini gösterir.

### 4. Erişilebilirlik hususları

* `<th>` öğelerine `scope="col"` ekleyin.
* Tablonun amacını açıklamak için `<caption>` kullanın.
* Özel CSS uyguluyorsanız yeterli renk kontrastı sağlayın.

---

## Tam, çalıştırılabilir örnek

Aşağıdaki bloğu bir `index.html` dosyasına kopyalayın ve bir tarayıcıda açın. Sayfa **veriden tablo oluşturacak**, **JSON'dan tablo dolduracak** ve satırları otomatik olarak tekrarlayacaktır.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Dynamic table from JSON</title>
  <style>
    table { border-collapse: collapse; width: 100%; }
    th, td { padding: 8px; text-align: left; border: 1px solid #ddd; }
    th { background-color: #f2f2f2; }
  </style>
</head>
<body>

<!-- Step 1: JSON data source -->
<script id="people-data" type="application/json">
{
  "Persons": {
    "Person": [
      {
        "FirstName": "Alice",
        "LastName": "Anderson",
        "Address": {
          "Street": "Maple",
          "Number": "123",
          "City": "Springfield"
        }
      },
      {
        "FirstName": "Bob",
        "LastName": "Baker",
        "Address": {
          "Street": "Oak",
          "Number": "456",
          "City": "Rivertown"
        }
      }
    ]
  }
}
</script>

<!-- Step 2: Handlebars template -->
<script id="table-template" type="text/x-handlebars-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <tr>
    <th scope="col">Person</th>
    <th scope="col">Address</th>
  </tr>
  {{#foreach Persons.Person}}
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
  {{/foreach}}
</table>
</script>

<!-- Step 4: Container for the generated table -->
<div id="output"></div>

<!-- Step 3: Load Handlebars, compile, and render -->
<script src="https://cdn.jsdelivr.net/npm/handlebars@4.7.7/dist/handlebars.min.js"></script>
<script>
  const raw = document.getElementById('people-data').textContent;
  const context = JSON.parse(raw);
  const source = document.getElementById('table-template').innerHTML;
  const template = Handlebars.compile(source);
  document.getElementById('output').innerHTML = template(context);
</script>

</body>
</html>
```

**Beklenen sonuç**

İki satırlı bir tablo (başlık dahil) “Alice Anderson” ve “Bob Baker”ı ilgili adresleriyle gösterir. Sayfa çevrim dışı çalışır ve **veriden tablo oluşturabileceğinizi** herhangi bir sunucu bileşeni olmadan kanıtlar.

---

## Sonuç

Artık bir Handlebars şablonu kullanarak **veriden tablo oluşturmayı**, **JSON'dan tablo doldurmayı** ve **dinamik bir HTML tablo** oluşturan **tablo satırlarını tekrarlamayı** biliyorsunuz. Bu desen, daha büyük veri setlerine, iç içe yapılara ve canlı API çağrılarına ölçeklenebilir ve herhangi bir istemci‑tarafı raporlama ya da yönetim arayüzü için sağlam bir temel sağlar.

**Sonraki adımlar**

* Tarih veya sayı formatlamak için Handlebars yardımcılarını keşfedin.
* Bu yaklaşımı responsive tablo düzenleri için CSS Grid veya Flexbox ile birleştirin.
* Çok büyük veri setlerini yönetmek için sayfalama veya sıralama kütüphanelerini entegre edin.

Farklı JSON yapılarıyla denemeler yapmaktan, koşullu sütunlar eklemekten veya Handlebars'ı başka bir şablon motoruyla değiştirmekten çekinmeyin—yeni becerileriniz, esnek ve veri‑odaklı arayüzleri hızlı ve güvenilir bir şekilde oluşturmanızı sağlayacak.

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Create HTML Document with Java – Fetch JSON and Generate Content](/html/english/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/)
- [Data Handling and Stream Management in Aspose.HTML for Java](/html/english/java/data-handling-stream-management/)
- [How to Load HTML in Java – Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/how-to-load-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}