---
category: general
date: 2026-04-26
description: Převod HTML do PDF v Javě pomocí Aspose.HTML – zjistěte, jak nastavit
  velikost stránky PDF, přidat okraje PDF a exportovat HTML jako PDF během několika
  řádků.
draft: false
keywords:
- convert html to pdf
- set pdf page size
- add pdf margins
- export html as pdf
- how to set margins
language: cs
og_description: Převod HTML do PDF v Javě pomocí Aspose.HTML. Tento průvodce vám ukáže,
  jak nastavit velikost stránky PDF, přidat okraje PDF a rychle exportovat HTML jako
  PDF.
og_title: Převod HTML na PDF v Javě – Nastavte velikost stránky a okraje
tags:
- Java
- Aspose.HTML
- PDF conversion
title: Převod HTML na PDF v Javě – Nastavení velikosti stránky a okrajů
url: /cs/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-set-page-size-margins/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod HTML do PDF v Javě – nastavení velikosti stránky a okrajů

Potřebujete **převést HTML do PDF v Javě**? Bojujete s **nastavením velikosti stránky PDF** nebo **přidáním okrajů PDF**? Nejste v tom sami. V mnoha projektech musí finální PDF odpovídat firemnímu brandingu, což vyžaduje přesné rozměry stránky a úhledné okraje.  

V tomto tutoriálu projdeme kompletním, připraveným příkladem, který **exportuje HTML jako PDF** pomocí knihovny Aspose.HTML. Na konci budete vědět *jak nastavit okraje* a proč může být shoda s PDF‑A‑1b záchranou pro archivaci. Žádné vágní odkazy – jen kód, který můžete zkopírovat a spustit.

## Co budete potřebovat

- **Java 17** (nebo jakýkoli aktuální JDK) – API funguje s Java 8+, ale novější verze poskytují lepší výkon.  
- **Aspose.HTML for Java** JAR soubory – můžete je získat z repozitáře Maven Central nebo z webu Aspose.  
- Jednoduchý soubor **input.html**, který chcete převést do PDF.  
- Trochu místa na disku pro výstupní soubor (PDF bude mít několik stovek kilobajtů).  

To je vše. Žádné další frameworky, žádné externí služby. Pokud máte tyto součásti, můžeme začít.

## Převod HTML do PDF – Přehled krok za krokem

Níže je vysokou úrovní tok, který budeme následovat:

1. **Ukázat na zdroj HTML** – lokální soubor, vzdálená URL nebo `InputStream`.  
2. **Konfigurovat možnosti ukládání PDF** – nastavit velikost stránky, okraje a shodu s PDF‑A.  
3. **Spustit konverzi** – nechte Aspose udělat těžkou práci.  

Každý z těchto kroků je rozdělen do vlastní sekce, takže si můžete vybrat jen ty části, které potřebujete.

## Krok 1: Specifikujte zdroj HTML

První věc, kterou konvertor potřebuje, je odkaz na HTML, které chcete převést do PDF. Aspose.HTML je flexibilní: můžete mu předat cestu, URL nebo dokonce stream, pokud je vaše HTML v paměti.

```java
// Step 1 – Define where the HTML comes from
String htmlPath = "YOUR_DIRECTORY/input.html"; // replace with your actual file
```

> **Proč je to důležité:** Použití prostého řetězce udržuje příklad jednoduchý, ale v reálných scénářích můžete HTML načíst z webové služby nebo databáze. API také akceptuje `java.net.URL` nebo `java.io.InputStream`, což je užitečné, když nechcete zapisovat dočasný soubor.

## Krok 2: Nastavte velikost stránky PDF

Většina PDF má ve výchozím nastavení velikost **Letter**, což může vypadat divně, pokud vaše publikum očekává **A4**. Změna velikosti stránky je jednorázová operace pomocí `PdfSaveOptions`.

```java
// Step 2 – Create PDF options and set the page size to A4
PdfSaveOptions pdfOptions = new PdfSaveOptions();
pdfOptions.setPageSize(PdfPageSize.A4); // this is the “set pdf page size” step
```

> **Tip:** Pokud potřebujete vlastní velikost (např. formát účtenky), Aspose vám umožní předat objekt `SizeF` s přesnou šířkou a výškou v bodech.

## Krok 3: Přidejte okraje PDF

Okraje zabraňují tomu, aby se váš obsah dotýkal okraje stránky. Měří se v bodech (1 mm ≈ 2.8346 pt), ale Aspose poskytuje pohodlnou třídu `Margin`, která přijímá milimetry přímo.

```java
// Step 3 – Define 20 mm margins on all sides (how to set margins)
pdfOptions.setMargins(new Margin(20, 20, 20, 20));
```

> **Proč je to důležité:** Bez okrajů mohou být záhlaví oříznuta při tisku a zápatí může zmizet v ne‑tisknutelné oblasti tiskárny. Konzistentní okraje také dodávají PDF profesionální vzhled.

## Krok 4: Povolit shodu s PDF‑A‑1b (volitelné, ale doporučené)

Pokud archivujete dokumenty z právních nebo regulatorních důvodů, PDF‑A‑1b zajišťuje, že soubor je samostatný a budoucnosti odolný.

```java
// Step 4 – Make the PDF archival‑ready
pdfOptions.setPdfACompliance(PdfACompliance.PdfA1b);
```

> **Rychlá poznámka:** Shoda s PDF‑A může mírně zvýšit velikost souboru, protože jsou vloženy fonty. Je to malá cena za dlouhodobou čitelnost.

## Krok 5: Proveďte konverzi

Jakmile je vše nakonfigurováno, samotná konverze je jediným statickým voláním. Aspose se stará o vykreslovací engine, CSS, JavaScript (pokud je povolen) a vkládání obrázků v pozadí.

```java
// Step 5 – Convert the HTML to PDF using the configured options
Converter.convertHtmlToPdf(htmlPath, "YOUR_DIRECTORY/output.pdf", pdfOptions);
```

To je celý program! Spojte všechny úryvky dohromady a získáte spustitelnou třídu.

## Kompletní funkční příklad

Níže je kompletní Java program, který můžete zkopírovat do `ConvertHtmlToPdfCustom.java`. Nahraďte zástupné cesty skutečnými umístěními na vašem počítači.

```java
import com.aspose.html.*;
import com.aspose.html.converters.*;
import com.aspose.html.saving.*;

public class ConvertHtmlToPdfCustom {
    public static void main(String[] args) throws Exception {

        // Step 1: Specify the source HTML file (local file, URL, or stream)
        String htmlPath = "YOUR_DIRECTORY/input.html";

        // Step 2: Configure PDF output options
        //   • A4 page size
        //   • 20 mm margins on all sides
        //   • PDF‑A‑1b compliance for archival
        PdfSaveOptions pdfOptions = new PdfSaveOptions();
        pdfOptions.setPageSize(PdfPageSize.A4);
        pdfOptions.setMargins(new Margin(20, 20, 20, 20));
        pdfOptions.setPdfACompliance(PdfACompliance.PdfA1b);

        // Step 3: Convert the HTML to PDF using the configured options
        Converter.convertHtmlToPdf(htmlPath, "YOUR_DIRECTORY/output.pdf", pdfOptions);
    }
}
```

### Očekávaný výsledek

Spuštěním programu se vytvoří `output.pdf`, který:

- Je **A4** (210 mm × 297 mm).  
- Má **20 mm** okraje vlevo, vpravo, nahoře i dole.  
- Je **PDF‑A‑1b** kompatibilní, což znamená, že všechny fonty jsou vloženy a soubor je samostatný.  
- Věrně reprodukuje rozvržení `input.html` (obrázky, tabulky a CSS styly jsou zachovány).

PDF můžete otevřít v libovolném prohlížeči (Adobe Acrobat, Foxit nebo dokonce Chrome) a měli byste vidět čistou stránku s pohodlným bílým okrajem kolem obsahu.

![convert html to pdf output preview](/images/convert-html-to-pdf.png)

*Obrázek: Rychlý pohled na vygenerované PDF po konverzi.*

## Časté otázky a okrajové případy

### Co když moje HTML obsahuje externí CSS nebo obrázky?

Aspose.HTML se řídí stejnými pravidly jako prohlížeče. Dokud jsou URL přístupné (absolutní nebo relativní k složce HTML souboru), konvertor je načte. Pokud spouštíte kód na serveru bez přístupu k internetu, zvažte vložení zdrojů jako řetězce **data‑URI** nebo jejich přednačtení do `MemoryStream`.

### Jak převést **URL** místo souboru?

Stačí nahradit řetězec `htmlPath` URL:

```java
String htmlPath = "https://example.com/report.html";
```

Stejný přetížený `Converter.convertHtmlToPdf` stáhne a vykreslí stránku.

### Můžu změnit jednotky okrajů na palce nebo body?

Ano. Konstruktor `Margin` také přijímá `float left, float top, float right, float bottom` v **bodech**. Pokud dáváte přednost palcům, vynásobte 72 (1 palec = 72 pt). Například okraje 0,5 palce by byly `new Margin(36, 36, 36, 36)`.

### Co když potřebuji **jinou orientaci stránky** (na šířku)?

Nastavte vlastnost `PageOrientation` před voláním `setPageSize`:

```java
pdfOptions.setPageOrientation(PageOrientation.Landscape);
pdfOptions.setPageSize(PdfPageSize.A4);
```

### Existuje způsob, jak **automaticky přidat záhlaví/zápatí**?

Aspose.HTML vám umožní vložit HTML úryvky, které fungují jako záhlaví nebo zápatí pomocí třídy `PdfPageTemplate`. Vytvoříte malý HTML fragment s požadovaným textem a přiřadíte jej k `pdfOptions.getPageTemplate().setHeaderHtml(...)` (nebo `.setFooterHtml(...)`). To je samostatné téma, ale hlavní myšlenka je: můžete zacházet se záhlavím/zápatím jako s běžným HTML.

## Tipy pro produkční kód

- **Licencujte knihovnu** – the free

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}