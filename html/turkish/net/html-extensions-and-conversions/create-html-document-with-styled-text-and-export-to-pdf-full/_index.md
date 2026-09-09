---
category: general
date: 2025-12-29
description: C#'ta HTML belgesi oluşturun ve yazı tipi ailesini, yazı tipi boyutunu
  nasıl ayarlayacağınızı öğrenin, ardından HTML'yi PDF olarak kaydedin veya Aspose.HTML
  kullanarak HTML'yi PDF'ye dönüştürün.
draft: false
keywords:
- create html document
- set font family
- set font size
- save html as pdf
- convert html to pdf
language: tr
og_description: C#'ta HTML belgesi oluşturun ve anında yazı tipi ailesi ve yazı tipi
  boyutunu nasıl ayarlayacağınızı görün, ardından HTML'yi PDF olarak kaydedin veya
  Aspose.HTML ile HTML'yi PDF'ye dönüştürün.
og_title: HTML Belgesi Oluştur – Stil Verilmiş Metin ve PDF Dışa Aktarma
tags:
- aspnet
- csharp
- pdf-generation
title: Stil Verilmiş Metinle HTML Belgesi Oluşturma ve PDF Olarak Dışa Aktarma – Tam
  Rehber
url: /tr/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Stilize Metinli HTML Belgesi Oluşturma ve PDF Olarak Dışa Aktarma

Kodunuz içinde **HTML belge oluşturma** ihtiyacınız oldu mu ve bunu PDF’ye dönüştürmek istediniz mi? Belki bir raporlama motoru, fatura üreticisi ya da kullanıcılar için hızlı bir ön izleme oluşturuyorsunuzdur. İyi haber şu ki, Aspose.HTML kullanarak birkaç satır kodla bunu yapabilir ve yazı tipi ailesi, yazı tipi boyutu ve hatta kalın‑eğik stil üzerinde tam kontrol sağlayabilirsiniz.

Bu öğreticide, bellek içinde bir HTML belgesi oluşturup PDF dosyası olarak kaydetmeye kadar tüm süreci adım adım inceleyeceğiz. Sonunda **yazı tipi ailesi ayarlama**, **yazı tipi boyutu ayarlama** ve **HTML’yi PDF olarak kaydetme** (diğer bir deyişle **HTML’yi PDF’ye dönüştürme**) konularını temiz, üretime hazır bir kod örneğiyle öğreneceksiniz.

## Gereksinimler

- .NET 6+ (API, .NET Core ve .NET Framework ile aynı şekilde çalışır)  
- Aspose.HTML for .NET NuGet paketi (`Aspose.Html`) – `dotnet add package Aspose.Html` komutuyla kurun  
- Oluşturulan PDF’nin yazılacağı bir klasör  

Ek HTML şablonları, harici dönüştürücüler yok; sadece saf C#.

![HTML belge oluşturma görseli](/images/create-html-document.png){alt="HTML belge oluşturma örneği"}

## Adım 1: HTML Belgesini Oluşturma

İlk olarak boş bir HTML belge nesnesine ihtiyacımız var. Bunu, daha sonra stilize paragrafınızı çizeceğiniz temiz bir tuval olarak düşünün.

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

// Step 1 – initialize a new HTML document in memory
HTMLDocument htmlDocument = new HTMLDocument();

// Grab a reference to the <body> element for later use
HTMLBodyElement body = htmlDocument.Body;
```

**Neden önemli:** `HTMLDocument`, programatik olarak manipüle edebileceğiniz bir DOM‑benzeri yapı sunar. Ham stringlerle ya da dosya I/O işlemleriyle uğraşmanız en sona kalır.

## Adım 2: Paragraf Ekleyin ve Yazı Tipi Ailesi ile Boyutunu Ayarlayın

Şimdi bir `<p>` elementi oluşturup içine metin ekleyecek ve açıkça yazı tipi ailesi ve boyutunu tanımlayacağız. İşte **yazı tipi ailesi ayarlama** ve **yazı tipi boyutu ayarlama** anahtar kelimelerinin devreye girdiği yer.

```csharp
// Step 2 – create a <p> element with some sample text
HtmlElement paragraph = htmlDocument.CreateElement("p");
paragraph.InnerHtml = "Bold & Italic text";

// Define the base font style
paragraph.Style.FontFamily = "Arial";   // set font family
paragraph.Style.FontSize = "18px";      // set font size

// Attach the paragraph to the document body
body.AppendChild(paragraph);
```

**İpucu:** Web‑güvenli bir yedekleme istiyorsanız, `"Arial, Helvetica, sans-serif"` gibi virgülle ayrılmış bir liste verebilirsiniz; tarayıcı (veya Aspose) ilk kullanılabilir fontu seçecektir.

## Adım 3: WebFontStyle Bayraklarıyla Kalın ve Eğik Stil Uygulama

Aspose.HTML, stilleri bit‑wise OR ile birleştirmenizi sağlayan kullanışlı bir `WebFontStyle` enum’u sunar. Metni hem kalın **hem** eğik yapalım.

```csharp
// Step 3 – apply bold and italic using WebFontStyle flags
paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

**Arka planda ne oluyor?** `FontStyle` özelliği, CSS `font-weight` ve `font-style` bildirimlerine karşılık gelir. Bayrakları OR‑lamak, iki ayrı CSS satırı yazmaktan kaçınmanızı sağlar.

## Adım 4: HTML’yi PDF’ye Dönüştürme (HTML’yi PDF Olarak Kaydetme)

Son adım gerçek dönüşüm. Tek bir `Save` çağrısıyla Aspose.HTML DOM’u render eder ve PDF dosyasını diske yazar. Böylece **save html as pdf** ve **convert html to pdf** gereksinimleri karşılanır.

```csharp
// Step 4 – save the HTML document as a PDF file
string outputPath = @"C:\Temp\styled.pdf";
htmlDocument.Save(outputPath, new PDFSaveOptions());

// Optional: open the PDF automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Beklenen sonuç:** `styled.pdf` dosyasını açtığınızda “Bold & Italic text” metninin 18‑px Arial ile kalın ve eğik olarak göründüğünü göreceksiniz. PDF boyutları standart A4 sayfasına uyar ve metin seçilebilir—vektörel render sayesinde.

## Tam Çalışan Örnek

Her şeyi bir araya getirdiğimizde, çalıştırmaya hazır tam program aşağıdadır:

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new HTML document
        HTMLDocument htmlDocument = new HTMLDocument();
        HTMLBodyElement body = htmlDocument.Body;

        // 2️⃣ Add a styled paragraph
        HtmlElement paragraph = htmlDocument.CreateElement("p");
        paragraph.InnerHtml = "Bold & Italic text";

        // Set font family and size
        paragraph.Style.FontFamily = "Arial";
        paragraph.Style.FontSize = "18px";

        // 3️⃣ Apply bold + italic
        paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // Append to body
        body.AppendChild(paragraph);

        // 4️⃣ Save as PDF (convert HTML to PDF)
        string outputFile = @"C:\Temp\styled.pdf";
        htmlDocument.Save(outputFile, new PDFSaveOptions());

        Console.WriteLine($"PDF generated at: {outputFile}");
    }
}
```

### Kodu Çalıştırma

1. Aspose.HTML NuGet paketini kurun:  
   ```bash
   dotnet add package Aspose.Html
   ```
2. `C:\Temp\styled.pdf` yolunu, yazma izniniz olan bir klasörle değiştirin.  
3. Derleyip çalıştırın: `dotnet run`.  

Konsolda dosya konumunu belirten bir mesaj göreceksiniz ve PDF stilize paragrafı içerecek.

## Sık Sorulan Sorular & Özel Durumlar

- **Özel bir web fontuna ihtiyacım olursa?**  
  Paragrafı oluşturmadan önce `HTMLFontFaceRule` ile fontu yükleyin ya da uzaktaki bir `@font-face` CSS dosyasına referans verin.

- **Dönüştürmeden önce resim ekleyebilir miyim?**  
  Kesinlikle. `HTMLImageElement img = (HTMLImageElement)htmlDocument.CreateElement("img");` kodunu kullanın ve `img.Source` özelliğini yerel bir yol ya da data URI ile ayarlayın.

- **Çok sayfalı PDF’ler nasıl olur?**  
  Daha fazla öğe (tablolar, div’ler vb.) ekleyin; içerik sayfa yüksekliğini aştığında Aspose.HTML otomatik olarak sayfalama yapar.

- **PDF meta verilerini kontrol etmenin bir yolu var mı?**  
  Bir `PdfSaveOptions` örneği oluşturup `Author`, `Title` ya da `PdfAConformanceLevel` gibi özellikleri ayarlayın.

## Özet

C# içinde **HTML belge oluşturma**, **yazı tipi ailesi ayarlama**, **yazı tipi boyutu ayarlama**, kalın‑eğik stiller uygulama ve sonunda **HTML’yi PDF olarak kaydetme**—dolayısıyla **HTML’yi PDF’ye dönüştürme** işlemlerini Aspose.HTML ile nasıl yapacağınızı öğrendik. Bu snippet, herhangi bir .NET projesine kolayca eklenebilecek kadar kısa, ancak daha karmaşık raporlama senaryoları için sağlam bir temel oluşturacak kadar kapsamlıdır.

## Sonraki Adımlar

- Yeniden kullanılabilir stiller için CSS sınıflarıyla deneyler yapın.  
- Daha zengin PDF’ler oluşturmak üzere birden fazla paragraf, tablo ve resim birleştirin.  
- Arşivleme kalitesinde belgeler gerekiyorsa PDF/A uyumluluğunu keşfedin.  

Yazı tipini, boyutu ya da renkleri dilediğiniz gibi değiştirin—programatik olarak üretebileceğiniz şeylerin sınırı yok. İyi kodlamalar, PDF’leriniz her zaman hayal ettiğiniz gibi render olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}