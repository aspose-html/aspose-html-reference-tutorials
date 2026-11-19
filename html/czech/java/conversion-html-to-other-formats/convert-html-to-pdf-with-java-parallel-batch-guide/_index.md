---
category: general
date: 2026-06-07
description: Převod HTML na PDF pomocí ExecutorService v Javě. Naučte se, jak dávkově
  převádět HTML soubory, uložit HTML dokument jako PDF a elegantně ukončit ExecutorService.
draft: false
keywords:
- convert html to pdf
- save html document as pdf
- shutdown executorservice gracefully
- batch convert html to pdf
language: cs
og_description: Převod HTML na PDF pomocí ExecutorService v Javě. Mistrovská dávková
  konverze, ukládání HTML dokumentu jako PDF a elegantní ukončení ExecutorService.
og_title: Převod HTML do PDF pomocí Javy – Průvodce paralelním dávkovým zpracováním
schemas:
- author: Aspose
  dateModified: '2026-06-07'
  description: Convert HTML to PDF using Java's ExecutorService. Learn how to batch
    convert HTML files, save HTML document as PDF, and shutdown ExecutorService gracefully.
  headline: Convert HTML to PDF with Java – Parallel Batch Guide
  type: TechArticle
- description: Convert HTML to PDF using Java's ExecutorService. Learn how to batch
    convert HTML files, save HTML document as PDF, and shutdown ExecutorService gracefully.
  name: Convert HTML to PDF with Java – Parallel Batch Guide
  steps:
  - name: The HTML file is read into a string.
    text: The HTML file is read into a string.
  - name: '`PdfRendererBuilder` parses the markup, applies CSS, and streams the result
      to a PDF file.'
    text: '`PdfRendererBuilder` parses the markup, applies CSS, and streams the result
      to a PDF file.'
  - name: Any `IOException` bubbles up to `convertAndSave`, where we log success or
      failure.
    text: Any `IOException` bubbles up to `convertAndSave`, where we log success or
      failure.
  type: HowTo
tags:
- Java
- Concurrency
- PDF Generation
title: Převod HTML na PDF pomocí Javy – Průvodce paralelním dávkováním
url: /cs/java/conversion-html-to-other-formats/convert-html-to-pdf-with-java-parallel-batch-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod HTML do PDF pomocí Javy – Průvodce paralelním dávkováním

Už jste někdy potřebovali **převést HTML do PDF**, ale uvízli jste v honbě za desítkami souborů? Nejste v tom sami — mnoho vývojářů narazí na tuto překážku při tvorbě generátorů reportů nebo exportérů faktur. Dobrá zpráva? S několika řádky Javy a chytrým thread pool můžete **dávkově převádět HTML do PDF** během chvilky, **uložit HTML dokument jako PDF** a dokonce **ukončit ExecutorService elegantně**, až když je práce hotová.

V tomto tutoriálu projdeme kompletním, připraveným příkladem. Ukážeme si, proč je fixní velikost thread poolu ideální pro paralelní převod, jak vypadá samotný převodní kód a jak přesně ukončit executor. Na konci budete mít samostatný program, který můžete vložit do libovolného projektu — žádné chybějící části, žádné vágní odkazy „viz dokumentace“.

---

## Co vytvoříte

- Java konzolovou aplikaci, která načte seznam lokálních HTML souborů.  
- Každý soubor předá pracovnímu vláknu, které vytvoří PDF verzi.  
- Aplikace používá **ExecutorService** k paralelnímu spouštění převodů.  
- Jakmile jsou všechny úkoly zařazeny, pool se **ukončí elegantně**, aby žádné vlákno nezůstalo viset.

**Požadavky**  
- Java 17 (nebo jakýkoli novější JDK).  
- PDF knihovna, která dokáže renderovat HTML, například **OpenHTMLtoPDF**, **iText** nebo **Flying Saucer**. V kódu odkazujeme na zástupnou třídu `HTMLDocument`; nahraďte ji API vaší knihovny.  
- Základní znalost Java concurrency (nic složitého).

---

![Diagram showing batch conversion of HTML files to PDF using ExecutorService](batch-convert-diagram.png "Convert HTML to PDF in parallel with ExecutorService")

*Alt text: Diagram ilustrující, jak převádět HTML do PDF pomocí thread poolu pro dávkové zpracování.*

---

## Převod HTML do PDF paralelně (Dávkový převod HTML do PDF)

Když máte desítky — nebo i tisíce — HTML souborů, převádět je jeden po druhém na hlavním vlákně se stane úzkým hrdlem. Fixní velikost thread poolu umožní JVMu znovu použít pevný počet pracovních vláken, udržet vysoké využití CPU, aniž by přetížil systém.

```java
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

/**
 * Simple demo that batch converts HTML files to PDF using a fixed thread pool.
 * Replace HTMLDocument with the actual class from your chosen PDF library.
 */
public class HtmlToPdfBatch {

    public static void main(String[] args) {
        // 1️⃣ Prepare a list of HTML files to convert
        List<String> htmlPaths = List.of(
            "src/main/resources/page1.html",
            "src/main/resources/page2.html",
            "src/main/resources/page3.html"
        );

        // 2️⃣ Create a fixed‑size thread pool – 4 workers is a good starting point
        ExecutorService pool = Executors.newFixedThreadPool(4);

        // 3️⃣ Submit a conversion task for each HTML file
        for (String htmlPath : htmlPaths) {
            pool.submit(() -> convertAndSave(htmlPath));
        }

        // 4️⃣ Shutdown ExecutorService gracefully – no new tasks, wait for running ones
        shutdownGracefully(pool);
    }

    /**
     * Core conversion logic – this is where we **save HTML document as PDF**.
     */
    private static void convertAndSave(String htmlPath) {
        try {
            // Imagine HTMLDocument is from OpenHTMLtoPDF, iText, etc.
            HTMLDocument doc = new HTMLDocument(htmlPath);
            String pdfPath = htmlPath.replace(".html", ".pdf");
            doc.save(pdfPath);
            System.out.println("✅ Converted: " + htmlPath + " → " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Failed to convert " + htmlPath + ": " + e.getMessage());
        }
    }

    /**
     * Helper that **shutdowns ExecutorService gracefully**.
     */
    private static void shutdownGracefully(ExecutorService executor) {
        executor.shutdown(); // stop accepting new tasks
        try {
            // Wait a maximum of 60 seconds for existing tasks to finish
            if (!executor.awaitTermination(60, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("⚠️ Pool didn’t terminate in time – forcing shutdown");
                executor.shutdownNow(); // cancel currently executing tasks
            } else {
                System.out.println("🛑 All tasks completed – executor shut down cleanly.");
            }
        } catch (InterruptedException ie) {
            // Preserve interrupt status & force shutdown
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }
}
```

### Proč to funguje

- **Paralelismus**: Každé volání `submit` předá převod pracovnímu vláknu, takže čtyři soubory mohou být zpracovávány současně na čtyřjádrovém stroji.  
- **Izolace**: Metoda `convertAndSave` obsahuje veškerou logiku potřebnou k **uložení HTML dokumentu jako PDF**, což usnadňuje pozdější výměnu použité knihovny.  
- **Elegantní ukončení**: Voláním `shutdown()` nejprve řekneme poolu „žádné další úkoly, dokončete, co máte“. Smyčka `awaitTermination` dává těm vláknům šanci dokončit práci a jen pokud jsou neústupná, zavoláme `shutdownNow()`. Tento vzor je doporučený způsob, jak **ukončit ExecutorService elegantně**.

---

## Uložení HTML dokumentu jako PDF – Jádrová logika převodu

Srdcem každého **convert HTML to PDF** workflow je převodní knihovna. Zatímco příklad používá dummy `HTMLDocument`, zde je rychlý náhled, jak by to šlo udělat s **OpenHTMLtoPDF**:

```java
import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;

public class HTMLDocument {
    private final String htmlPath;

    public HTMLDocument(String htmlPath) {
        this.htmlPath = htmlPath;
    }

    public void save(String pdfPath) throws IOException {
        try (OutputStream os = new FileOutputStream(pdfPath);
             InputStream is = new FileInputStream(htmlPath)) {

            PdfRendererBuilder builder = new PdfRendererBuilder();
            builder.withHtmlContent(new String(is.readAllBytes()), null);
            builder.toStream(os);
            builder.run();
        }
    }
}
```

**Co se děje?**  
1. HTML soubor se načte do řetězce.  
2. `PdfRendererBuilder` parsuje markup, aplikuje CSS a streamuje výsledek do PDF souboru.  
3. Jakékoli `IOException` se propíjí až do `convertAndSave`, kde zaznamenáme úspěch nebo selhání.

Klidně tento úryvek nahraďte iText‑ovým `HtmlConverter.convertToPdf` nebo Flying Saucer‑ovým `ITextRenderer`. Kód okolo thread‑poolu zůstane naprosto stejný, což je důvod, proč jsme zdůraznili **uložení HTML dokumentu jako PDF** jako samostatnou starost.

---

## Ukončení ExecutorService elegantně – Nejlepší postupy

Častá chyba je volat `shutdownNow()` hned po odeslání úkolů. To okamžitě přeruší vlákna a může zanechat polovičně zapsané PDF soubory na disku. Vzor, který používáme — `shutdown()` → `awaitTermination()` → volitelně `shutdownNow()` — zajišťuje:

- **Žádné nové úkoly** nejsou přijímány po zařazení všeho.  
- **Běžící úkoly** mají šanci čistě dokončit.  
- **Blokovaná vlákna** jsou přerušena jen pokud překročí rozumný timeout (zde 60 sekund).  

Pokud očekáváte velmi velké PDF nebo pomalý renderovací engine, prodlužte timeout nebo použijte `executor.invokeAll(tasks, timeout, unit)` pro přesnější kontrolu.

---

## Kompletní funkční příklad (Vše dohromady)

Níže je celý program, který můžete zkopírovat do jediného souboru `HtmlToPdfBatch.java`. Stačí přidat závislost OpenHTMLtoPDF (nebo vaši preferovanou knihovnu) do `pom.xml` nebo Gradle build a můžete spustit.



## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční kódové příklady s podrobnými vysvětleními, abyste si osvojili další funkce API a prozkoumali alternativní implementační přístupy ve svých projektech.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convert HTML to PDF Java – Configuring Environment in Aspose.HTML](/html/english/java/configuring-environment/)
- [Convert HTML to PDF in Java – Step‑by‑Step Guide with Page Size Settings](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}