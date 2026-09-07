---
category: general
date: 2026-09-07
description: dinamik bir HTML tablosunda verileri bağlama – tablo satırlarını nasıl
  oluşturacağınızı ve ad ile soyad alanlarını verimli bir şekilde nasıl dolduracağınızı
  öğrenin
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to bind data
- dynamic html table
- first and last name
- how to generate table
- populate table rows
language: tr
lastmod: 2026-09-07
og_description: dinamik bir HTML tablosunda verileri bağlama. Bu öğreticide tablo
  satırları nasıl oluşturulur, ad ve soyad nasıl gösterilir ve JavaScript ile tablo
  satırları nasıl doldurulur gösterilmektedir.
og_image_alt: Screenshot of a dynamic HTML table populated with first and last names
  after binding data
og_title: Dinamik bir HTML tabloya veri bağlama – adım adım rehber
schemas:
- author: Aspose
  dateModified: '2026-09-07'
  description: how to bind data in a dynamic HTML table – learn how to generate table
    rows and populate first and last name fields efficiently
  headline: How to bind data to a dynamic HTML table with first and last name columns
  type: TechArticle
tags:
- data binding
- html table
- templating
title: İlk ve soyad sütunları bulunan dinamik bir HTML tabloya verileri nasıl bağlarsınız
url: /tr/java/creating-managing-html-documents/how-to-bind-data-to-a-dynamic-html-table-with-first-and-last/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# İlk ve soyad sütunlarıyla dinamik bir HTML tabloya verileri bağlama

Eğer **verileri bağlama** ihtiyacınız varsa ve tablo her kayıtla büyüyorsa, bu rehber eksiksiz bir çözüm sunar. Dinamik bir HTML tablo oluşturmayı, tablo satırlarını doldurmayı ve her kişinin ilk ve soyadını tekrarlayan işaretleme yazmadan nasıl görüntüleyeceğinizi göreceksiniz.

Örnek, herhangi bir modern tarayıcıda çalışan hafif bir şablonlama sözdizimi kullanır, ancak kavramlar Handlebars, Mustache veya sunucu‑tarafı motorlarına da uygulanabilir. Eğitim sonunda kodu projenize kopyalayıp verileri anında bağlamaya başlayabilirsiniz.

## Bu eğitimde neler ele alınıyor

* Birden fazla kişi içeren bir veri kaynağını nasıl yapılandırılır  
* Her giriş için tekrarlanan yeniden kullanılabilir bir tablo şablonu nasıl oluşturulur  
* Verileri nasıl bağlanır ve son HTML işaretlemesi nasıl üretilir  
* Tablo satırlarını doldururken yaygın tuzaklar ve bunlardan nasıl kaçınılır  

Harici kütüphaneler gerekmez, ancak aynı desen popüler şablonlama çerçeveleriyle de çalışır. Tek ön koşul temel HTML ve JavaScript bilgisi.

## Önkoşullar

* Modern bir tarayıcı (Chrome, Edge, Firefox veya Safari)  
* HTML/JavaScript dosyaları için bir editör  
* İsteğe bağlı: Kişi koleksiyonunu temsil eden bir JSON dosyası veya JavaScript nesnesi  

## Adım 1: Veri kaynağını tanımlama

İlk olarak, şablonda kullanılan yapıyı yansıtan bir JavaScript nesnesi oluşturun. Her kişinin bir ilk adı, soyadı ve bir adres nesnesi vardır.

```html
<script>
  // Data source – an array of person objects
  const data = {
    Persons: {
      Person: [
        {
          FirstName: "Alice",
          LastName: "Johnson",
          Address: {
            Street: "Maple",
            Number: "12A",
            City: "Springfield"
          }
        },
        {
          FirstName: "Bob",
          LastName: "Smith",
          Address: {
            Street: "Oak",
            Number: "34B",
            City: "Riverdale"
          }
        }
        // Add more person objects as needed
      ]
    }
  };
</script>
```

**Neden önemli:** Nesne hiyerarşisi (`Persons.Person`) şablondaki `{{#foreach Persons.Person}}` döngüsüyle eşleşir ve motorun her girişi otomatik olarak yinelemesini sağlar.

## Adım 2: Tekrarlama bloğu ile tablo şablonunu yazma

Aşağıdaki şablon, her kişi için `<tr>` öğesini tekrarlamak amacıyla basit bir Mustache‑stili sözdizimi (`{{#foreach}}`) kullanır. Şablonu, tarayıcının işleme alana kadar görmezden gelmesi için bir `<script type="text/template">` etiketi içine yerleştirin.

```html
<script type="text/template" id="table-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <!-- Table header -->
  <tr>
    <th>Person</th><th>Address</th>
  </tr>
  <!-- Row populated with each person's data -->
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
</table>
</script>
```

**Neden önemli:** `{{#foreach Persons.Person}}` yönergesi, motorun her kişi nesnesi için açılış ve kapanış etiketleri arasındaki her şeyi tekrarlamasını söyler. Satır içinde herhangi bir özelliğe (`{{FirstName}}`, `{{LastName}}`, vb.) başvurarak tablo satırlarını dinamik olarak **doldurabilirsiniz**.

## Adım 3: Küçük bir render fonksiyonu uygulama

Eğitimin kendi içinde olması gerektiğinden, Mustache‑stili yer tutucuları gerçek değerlerle değiştiren minimal bir renderlayıcı yazacağız. Fonksiyon veri nesnesini dolaşır, tekrarlama bloğunu genişletir ve son HTML'i sayfaya ekler.

```html
<script>
  /**
   * Renders a template that contains a single {{#foreach}} block.
   * This implementation is intentionally simple and works for the
   * specific structure used in this tutorial.
   *
   * @param {string} tmpl   The raw template string.
   * @param {object} ctx    The data context (e.g., the `data` object).
   * @returns {string}      The rendered HTML.
   */
  function renderTemplate(tmpl, ctx) {
    // Extract the foreach expression and the block to repeat
    const foreachRegex = /{{#foreach\s+([^}]+)}}([\s\S]*?){{\/foreach}}/;
    const match = tmpl.match(foreachRegex);
    if (!match) return tmpl; // No foreach found

    const path = match[1].trim(); // e.g., "Persons.Person"
    const block = match[2];       // HTML that repeats

    // Resolve the array from the context (supports dot notation)
    const items = path.split('.').reduce((obj, key) => obj && obj[key], ctx);
    if (!Array.isArray(items)) return tmpl;

    // Render each item
    const renderedBlocks = items.map(item => {
      // Replace each {{property}} with the corresponding value
      return block.replace(/{{([^}]+)}}/g, (_, prop) => {
        const value = prop.trim().split('.').reduce((obj, key) => obj && obj[key], item);
        return value !== undefined ? value : '';
      });
    });

    // Replace the whole foreach section with the concatenated rows
    return tmpl.replace(foreachRegex, renderedBlocks.join(''));
  }

  // When the DOM is ready, render the table
  document.addEventListener('DOMContentLoaded', () => {
    const tmpl = document.getElementById('table-template').innerHTML;
    const html = renderTemplate(tmpl, data);
    document.getElementById('output').innerHTML = html;
  });
</script>
```

**Neden önemli:** Renderlayıcı, tam bir kütüphane kullanmadan programatik olarak **tablo oluşturmayı** gösterir. Ayrıca şablondan son HTML'e dönüşümü netleştirir, bu da kodu daha sonra diğer şablon motorlarına uyarlamanıza yardımcı olur.

## Adım 4: Oluşturulan tablonun görüneceği bir yer tutucu ekleyin

Renderlama sonrası scriptin dolduracağı boş bir `<div>` oluşturun.

```html
<div id="output"></div>
```

Sayfa yüklendiğinde, script bu `<div>` içeriğini tamamen doldurulmuş tabloyla değiştirir.

## Adım 5: Sonucu doğrulama

HTML dosyasını bir tarayıcıda açın. Her kişinin tam adı ve adresini listeleyen bir tablo görmelisiniz:

| Kişi          | Adres                         |
|---------------|------------------------------|
| Alice Johnson | Maple 12A, Springfield       |
| Bob Smith     | Oak 34B, Riverdale           |

Eğer `data.Persons.Person` dizisine daha fazla nesne eklerseniz, tablo otomatik olarak büyür—**tablo satırlarını doldurma** gereksinimini karşılar.

## Pro ipucu: Boş koleksiyonları ele alma

Veri dizisi boş olduğunda, renderlayıcı şu anda boş bir tablo başlığı üretir. Daha net bir kullanıcı deneyimi sağlamak için bir koruma ekleyin:

```javascript
if (items.length === 0) {
  return '<p>No records found.</p>';
}
```

Bu küçük değişiklik, boş bir tablonun görünmesini önler ve kullanıcılara anında geri bildirim sağlar.

## Yaygın varyasyonlar ve uç durumlar

| Durum                                 | Ayarlama                                                                 |
|---------------------------------------|--------------------------------------------------------------------------|
| Sunucu‑tarafı bir motor (ör. Handlebars) kullanmak | Özel `renderTemplate` fonksiyonunu `Handlebars.compile` ile değiştirin ve aynı veri nesnesini geçirin. |
| Satırları alfabetik olarak sıralama ihtiyacı | `renderTemplate` çağırmadan önce `data.Persons.Person` dizisini sıralayın. |
| Telefon numarası için bir sütun ekleme | `<tr>` öğesini `<td>{{Phone}}</td>` ile genişletin ve her kişi nesnesine `Phone` özelliğini ekleyin. |
| Büyük veri setleri (yüzlerce satır)   | Satırları parçalar halinde renderlayın veya UI’nın yanıt verebilirliğini korumak için sanal kaydırma kullanın. |

## Tam çalışan örnek

Aşağıda, `index.html` içine kopyalayıp‑yapıştırabileceğiniz tam HTML dosyası bulunmaktadır. Yukarıda tartışılan tüm parçaları içerir.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to bind data to a dynamic HTML table</title>
  <style>
    table { border-collapse: collapse; width: 100%; }
    th, td { padding: 8px; text-align: left; }
    th { background-color: #f2f2f2; }
  </style>
</head>
<body>

<h1>Dynamic HTML table bound to JavaScript data</h1>

<!-- Step 2: Table template -->
<script type="text/template" id="table-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <tr>
    <th>Person</th><th>Address</th>
  </tr>
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
</table>
</script>

<!-- Step 1: Data source -->
<script>
  const data = {
    Persons: {
      Person: [
        {
          FirstName: "Alice",
          LastName: "Johnson",
          Address: { Street: "Maple", Number: "12A", City: "Springfield" }
        },
        {
          FirstName: "Bob",
          LastName: "Smith",
          Address: { Street: "Oak", Number: "34B", City: "Riverdale" }
        }
        // Add more entries as needed
      ]
    }
  };
</script>

<!-- Step 4: Output container -->
<div id="output"></div>

<!-- Step 3: Rendering logic -->
<script>
  function renderTemplate(tmpl, ctx) {
    const foreachRegex = /{{#foreach\s+([^}]+)}}([\s\S]*?){{\/foreach}}/;
    const match = tmpl.match(foreachRegex);
    if (!match) return tmpl;
    const path = match[1].trim();
    const block = match[2];
    const items = path.split('.').reduce((obj, key) => obj && obj[key], ctx);
    if (!Array.isArray(items) || items.length === 0) {
      return '<p>No records found.</p>';
    }
    const renderedBlocks = items.map(item => {
      return block.replace(/{{([^}]+)}}/g, (_, prop) => {
        const value = prop.trim().split('.').reduce((obj, key) => obj && obj[key], item);
        return value !== undefined ? value : '';
      });
    });
    return tmpl.replace(foreachRegex, renderedBlocks.join(''));
  }

  document.addEventListener('DOMContentLoaded', () => {
    const tmpl = document.getElementById('table-template').innerHTML;
    const html = renderTemplate(tmpl, data);
    document.getElementById('output').innerHTML = html;
  });
</script>

</body>
</html>
```

**Beklenen çıktı**

Sayfa, her biri bir kişinin tam adı ve biçimlendirilmiş adresini gösteren iki satırlı bir tablo renderlar. `Person` dizisine daha fazla nesne eklemek otomatik olarak yeni satırlar ekler—verilerden **tablo oluşturmayı** gösterir.

## Sonuç

Artık **verileri bağlamayı** bir **dinamik HTML tabloya**, her kayıt için satır oluşturmayı ve adresin yanında ilk ve soyad değerlerini görüntülemeyi biliyorsunuz.

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki eğitimler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren eksiksiz çalışan kod örnekleri sunar.

- [CSS Nasıl Eklenir – Aspose.HTML for Java'da HTML Belgelerine Satır İçi CSS Ekleme](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [Aspose.HTML for Java'da HTML Belge Ağacını Düzenleme](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Aspose HTML'de JavaScript Nasıl Etkinleştirilir – HTML Yükle & Metin Al](/html/english/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}