---
date: 2026-02-02
description: Naučte se, jak vytvořit PDF z plátna pomocí JavaScriptu a Aspose.HTML
  pro Javu. Převádějte plátno na PDF, generujte PDF z HTML a uložte plátno jako PDF
  s vysokou věrností.
linktitle: Convert Canvas to PDF Using JavaScript
second_title: Java HTML Processing with Aspose.HTML
title: Vytvořte PDF z plátna pomocí Aspose.HTML pro Javu
url: /cs/java/advanced-usage/html5-canvas-manipulation-using-javascript/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření PDF z Canvasu pomocí Aspose.HTML pro Java

Interaktivní webové zážitky často využívají element **Canvas** v HTML5. Když potřebujete **vytvořit PDF z canvasu**, můžete vygenerovat tisknutelný, sdílený dokument, který zachová přesný vzhled vašich grafik. V tomto tutoriálu se naučíte, jak převést canvas na PDF pomocí JavaScriptu spolu s **Aspose.HTML pro Java**. Provedeme vás vytvořením canvasu, kreslením textu, uložením HTML a nakonec exportem výsledku do PDF souboru.

## Rychlé odpovědi
- **Co znamená „convert canvas to pdf“?** Znamená to převzetí vizuálního obsahu vykresleného v HTML5 Canvas a vytvoření PDF dokumentu, který zachovává tento vzhled.  
- **Která knihovna provádí konverzi?** Aspose.HTML pro Java poskytuje spolehlivé server‑side API pro převod HTML (včetně Canvas) na PDF.  
- **Potřebuji pro konverzi prohlížeč?** Ne. Konverze běží na Java runtime, takže můžete automatizovat generování PDF na serveru nebo v backendové službě.  
- **Mohu před konverzí nakreslit text na canvas?** Ano – ukážeme jednoduchý JavaScriptový příklad, který napíše „Hello World“ na canvas.  
- **Jaké jsou hlavní předpoklady?** Java JDK, knihovna Aspose.HTML pro Java a Java IDE (Eclipse, IntelliJ atd.).

## Co je „convert canvas to pdf“?
Převod canvasu na PDF znamená vykreslení pixel‑založeného kreslení z elementu `<canvas>` do PDF stránky přátelské k vektorům. To vám umožní zachovat přesný vzhled canvasu a zároveň získat funkce PDF, jako je stránkování, prohledávatelný text a snadné sdílení.

## Proč použít Aspose.HTML pro Java pro tento úkol?
- **Plná podpora HTML5** – Canvas, CSS3 a moderní JavaScript fungují během konverze správně.  
- **Server‑side zpracování** – Není potřeba headless prohlížeč; knihovna provád Java8 nebo vyšší.  
- **Aspose.HTML pro Java** – Stáhněte z oficiálního webu [zde](https://releases.aspose.com/html/java/).  
- **IDE** – Eclipse, IntelliJ IDEA nebo jakýkoli Java‑kompatibilní editor.

S těmito předpoklady jste připraveni začít vytvářet a exportovat grafiku z canvasu.

## Import balíčků
Nejprve importujte třídy, které budeme potřebovat z Aspose.HTML a Java I/O.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.PdfSaveOptions;
import java.io.FileWriter;
```

## vytvořit PDF z canvasu – krok za krokem průvodce

### Krok 1: Vytvořte element Canvas a nakreslete text

#### 1.1 Připravte HTML a JavaScript (nakreslete text na canvas)
Níže je Java řetězec, který obsahuje jednoduchou HTML stránku s elementem `<canvas>`. Vložený JavaScript získá kontext canvasu, nastaví písmo a vykreslí frázi **„Hello World“**.

```java
String code = "<canvas id='myCanvas' width='200' height='100' style='border:1px solid #d3d3d3;'></canvas>\n" +
              "<script>\n" +
              "    var c = document.getElementById('myCanvas');\n" +
              "    var context = c.getContext('2d');\n" +
              "    context.font = '20px Arial';\n" +
              "    context.fillStyle = 'red';\n" +
              "    context.fillText('Hello World', 40, 50);\n" +
              "</script>\n";
```

#### 1.2 Uložte HTML kód do souboru (html to pdf java)
Zapíšeme HTML řetězec do souboru `document.html`. Tento soubor bude později načten knihovnou Aspose.HTML.

```java
try (FileWriter fileWriter = new FileWriter("document.html")) {
    fileWriter.write(code);
}
```

### Krok 2: Inicializujte HTML dokument
Načtěte HTML soubor do objektu `HTMLDocument`, aby ho Aspose.HTML mohl zpracovat.

```java
HTMLDocument document = new HTMLDocument("document.html");
```

### Krok 3: Převod HTML (s Canvas) na PDF
Nakonec použijte třídu `Converter` k převodu HTML dokumentu do PDF souboru. Tento krok **uloží canvas jako PDF** a dokončí workflow „convert canvas to pdf“.

```java
try {
    Converter.convertHTML(
        document,
        new PdfSaveOptions(),
        "output.pdf"
    );
} finally {
    if (document != null) {
        document.dispose();
    }
}
```

#### Očekávaný výsledek
Spuštěním programu se vytvoří `output.pdf`. Otevřením PDF se zobrazí červený text „Hello World“ přesně tak, jak se objevil na canvasu v původní HTML stránce.

## Časté problémy a řešení
- **Canvas se v PDF nevykresluje** – Ujistěte se, že používáte aktuální verzi Aspose.HTML, která plně podporuje HTML5 Canvas.  
- **Chybějící písma** – Pokud písmo není vloženo, PDF může použít výchozí. V případě potřeby použijte `PdfSaveOptions` k vložení písem.  
- **Cesty k souborům** – Relativní cesty fungují, když Java proces běží ze stejného adresáře jako `document.html`. V opačném případě zadejte absolutní cestu.

## Často kladené otázky

**Q: Co je Aspose.HTML pro Java?**  
A: Aspose.HTML pro Java je výkonná knihovna, která umožňuje vývojářům vytvářet, manipulovat a převádět HTML dokumenty v Java aplikacích, podporující HTML5 funkce jako Canvas.

**Q: Mohu to použít v komerčních projektech?**  
A: Ano, pro produkční použití je vyžadována komerční licence. Podrobnosti jsou k dispozici na [stránce nákupu](https://purchase.aspose.com/buy).

**Q: Existuje bezplatná zkušební verze?**  
A: Rozhodně. Můžete si stáhnout zkušební verzi z [zde](https://releases.aspose.com/).

**Q: Jak získám dočasnou licenci pro testování?**  
A: Dočasné licence jsou poskytovány pro evaluační účely prostřednictvím odkazu [zde](https://purchase.aspose.com/temporary-license/).

**Q: Kde najdu podrobnou dokumentaci?**  
A: Kompletní reference API je k dispozici [zde](https://reference.aspose.com/html/java/).

## Závěr
Nyní máte kompletní řešení od začátku do konce pro **vytváření PDF z canvasu** pomocí JavaScriptu a Aspose.HTML pro Java. Kreslením zachytí jakoukoli dynamickou grafiku vytvořenou na webu. Experimentujte s různými tvary, barvami a dokonce animacemi (zachycenými jako série snímků), abyste rozšířili možnosti vašich Java‑backendových webových aplikací.

Pokud narazíte na jakékoli potíže nebo chcete prozkoumat pokročilé funkce, neváhejte navštívit [Aspose.HTML fórum](https://forum.aspose.com/) pro podporu komunity.

---

**Poslední aktualizace:** 2026-02-02  
**Testováno s:** Aspose.HTML pro Java 24.11  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}