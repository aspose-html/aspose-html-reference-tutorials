---
category: general
date: 2026-05-25
description: Jak vyhledávat v HTML pomocí Aspose pro Javu. Naučte se vyhledávat text
  v HTML, najít slovo v HTML, spočítat shody a získat rozsahy během několika snadných
  kroků.
draft: false
keywords:
- how to search html
- search text in html
- find word in html
- how to count matches
- how to get ranges
language: cs
og_description: Jak vyhledávat HTML pomocí Aspose pro Java. Tento tutoriál vám ukáže,
  jak vyhledávat text v HTML, najít slovo, spočítat shody a získat rozsahy.
og_title: Jak vyhledávat HTML pomocí Aspose Java – Kompletní průvodce
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: How to search HTML using Aspose for Java. Learn to search text in HTML,
    find word in HTML, count matches, and get ranges in a few easy steps.
  headline: How to search HTML with Aspose Java – Complete Programming Guide
  type: TechArticle
tags:
- Java
- Aspose.HTML
- Text Search
- HTML Parsing
title: Jak vyhledávat HTML pomocí Aspose Java – Kompletní programovací průvodce
url: /cs/java/creating-managing-html-documents/how-to-search-html-with-aspose-java-complete-programming-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vyhledávat HTML pomocí Aspose Java – Kompletní programovací průvodce

Už jste se někdy zamysleli **jak vyhledávat HTML** pro konkrétní slovo, aniž byste museli psát vlastní parser? Nejste v tom sami — vývojáři neustále potřebují spolehlivý způsob, jak najít text ve velkých HTML souborech, ať už pro extrakci dat, validaci obsahu nebo automatizované testování. Dobrou zprávou je, že Aspose.HTML pro Java tuto úlohu činí téměř triviální.

V tomto průvodci projdeme **search text in HTML**, ukážeme **jak spočítat shody** a zobrazíme **jak získat rozsahy** pro každý výskyt. Na konci budete mít připravený Java program, který najde slovo v HTML, vypíše počet výskytů a přesně řekne, které uzly text obsahují. Žádná hádanka, jen přehledný kód a praktické tipy.

## Požadavky

* JDK 8 nebo novější nainstalované.
* Maven nebo Gradle pro správu závislostí (v příkladech použijeme Maven).
* Licence Aspose.HTML pro Java (bezplatná zkušební verze stačí pro učení).
* Ukázkový HTML soubor (`sample.html`) umístěný na místě, na které můžete odkazovat z Javy.

Pokud vám některá z těchto položek není známá, nepanikařte — stačí postupovat podle rychlých kroků nastavení v následující sekci.

## Jak vyhledávat HTML – Nastavení prostředí

Nejprve je třeba přidat knihovnu Aspose.HTML do našeho projektu. Pokud používáte Maven, vložte následující úryvek do souboru `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest version available -->
</dependency>
```

> **Tip:** Sledujte číslo verze; novější vydání často přinášejí vylepšení výkonu pro vyhledávání textu.

Jakmile Maven vyřeší závislost, můžete začít kódovat. Otevřete své oblíbené IDE (IntelliJ, Eclipse, VS Code) a vytvořte novou Java třídu s názvem `FindText`.

## Vyhledávání textu v HTML – Načtení dokumentu

Prvním logickým krokem je **načíst HTML dokument** do objektu `HTMLDocument`. Tento objekt funguje jako strom DOM, což nám umožňuje programově dotazovat a manipulovat se stránkou.

```java
import com.aspose.html.dom.*;
import com.aspose.html.services.search.*;

public class FindText {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document from disk.
        // Replace "YOUR_DIRECTORY/sample.html" with the actual path.
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

Proč potřebujeme úplný `HTMLDocument` místo pouhého načtení souboru jako řetězce? Protože vyhledávací engine Aspose pracuje na DOM, respektuje hranice elementů a ignoruje značky — takže nedostanete falešné pozitivy uvnitř bloků `<script>` nebo `<style>`.

## Vyhledání slova v HTML – Konfigurace možností vyhledávání

Nyní, když je dokument v paměti, musíme motoru říct **co** hledáme a **jak** to má odpovídat. Třída `TextSearchOptions` nám umožňuje jemně nastavit citlivost na velikost písmen, vyhledávání celých slov a dokonce i pravidla specifická pro kulturu.

```java
        // Step 2: Set up text search options.
        TextSearchOptions searchOptions = new TextSearchOptions();
        // Make the search case‑insensitive (e.g., "Aspose" == "aspose").
        searchOptions.setCaseSensitive(false);
        // Restrict matches to whole words only, avoiding partial matches like "AsposeJS".
        searchOptions.setWholeWord(true);
```

Pokud později potřebujete fuzzy vyhledávání, stačí přepnout `setCaseSensitive(true)` nebo nastavit `setWholeWord(false)`. Výchozí hodnoty jsou úmyslně přísné, aby poskytovaly předvídatelné výsledky.

## Jak spočítat shody – Spuštění vyhledávání

S dokumentem a nastavenými možnostmi jsme konečně připraveni **vyhledat požadované slovo**. Metoda `searchText` vrací objekt `TextSearchResult`, který obsahuje jak počet, tak jednotlivé rozsahy.

```java
        // Step 3: Search for the word "Aspose" using the configured options.
        TextSearchResult searchResult = document.searchText("Aspose", searchOptions);
```

Další řádek ukazuje **jak spočítat shody**:

```java
        // Step 4: Output the total number of matches found.
        System.out.println("Found " + searchResult.getCount() + " matches.");
```

Za scénou Aspose prochází strom DOM, vyhodnocuje každý textový uzel a agreguje výsledky. Volání `getCount()` je O(1), protože engine jej již během vyhledávání spočítal.

## Jak získat rozsahy – Zpracování výsledků

Počítání je užitečné, ale často potřebujete vědět **kde** se každá shoda nachází. Zde vstupuje do hry **jak získat rozsahy**. Každý `TextRange` vám udává počáteční a koncový uzel plus posuny znaků.

```java
        // Step 5: Iterate through each match and display the node name where it occurs.
        for (TextRange range : searchResult.getRanges()) {
            // The start node is usually a Text node, but could be any node containing text.
            System.out.println("Match at node: " + range.getStartNode().getNodeName());
        }
```

Pokud chcete ještě podrobnější informace — například přesné číslo řádku nebo okolní HTML — můžete zavolat `range.getStartOffset()` a `range.getEndOffset()` a poté z původního zdroje vyextrahovat úryvek.

### Řešení hraničních případů

* **Prázdný dokument:** `searchResult.getCount()` bude `0`; smyčka se jednoduše neprovede.
* **Více výskytů ve stejném uzlu:** Aspose vrací samostatný `TextRange` pro každou shodu, takže stejný název uzlu bude vytištěn vícekrát.
* **Ne‑ASCII znaky:** Engine respektuje Unicode, ale ujistěte se, že váš zdrojový soubor je uložen v UTF‑8, aby nedošlo k nesouladu.

## Sestavení všeho dohromady – Kompletní spustitelný příklad

Níže je kompletní program, který můžete zkopírovat a vložit do souboru pojmenovaného `FindText.java`. Ujistěte se, že cesta k `sample.html` je správná, přeložte pomocí `javac` a spusťte pomocí `java`.

```java
import com.aspose.html.dom.*;
import com.aspose.html.services.search.*;

public class FindText {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/sample.html");

        // Step 2: Set up text search options (case‑insensitive, whole‑word only)
        TextSearchOptions searchOptions = new TextSearchOptions();
        searchOptions.setCaseSensitive(false);
        searchOptions.setWholeWord(true);

        // Step 3: Search for the desired word in the document
        TextSearchResult searchResult = document.searchText("Aspose", searchOptions);

        // Step 4: Output the total number of matches found
        System.out.println("Found " + searchResult.getCount() + " matches.");

        // Step 5: Iterate through each match and display the node name where it occurs
        for (TextRange range : searchResult.getRanges()) {
            System.out.println("Match at node: " + range.getStartNode().getNodeName());
        }
    }
}
```

**Očekávaný výstup** (předpokládáme, že `sample.html` obsahuje tři výskyty „Aspose“):

```
Found 3 matches.
Match at node: span
Match at node: p
Match at node: div
```

Výsledek můžete ověřit otevřením `sample.html` a ruční kontrolou těchto elementů.

## Časté otázky a praktické tipy

* **Co když potřebuji vyhledat více slov?**  
  Spusťte `searchText` ve smyčce, nebo vytvořte regulární výraz a použijte `searchText` s vlastním `TextSearchOptions`, který zakáže `setWholeWord`.

* **Mohu nahradit nalezená slova?**  
  Určitě. Po získání `TextRange` zavolejte `range.getStartNode().setNodeValue("new text")` nebo použijte službu `replaceText` poskytovanou Aspose.

* **Je vyhledávání thread‑safe?**  
  Instance `HTMLDocument` není thread‑safe, ale můžete bezpečně vytvořit samostatné dokumenty pro každý vlákno.

* **Jak se výkon mění s velikostí?**  
  Pro dokumenty do několika megabajtů vyhledávání skončí během milisekund. Pro větší soubory zvažte streamování dokumentu nebo zúžení rozsahu vyhledávání pomocí CSS selektorů.

## Závěr

Právě jsme prošli **jak vyhledávat HTML** pomocí Aspose pro Java, od načtení souboru po **search text in HTML**, **find word in HTML**, **how to count matches** a **how to get ranges** pro každý výskyt. Kód je kompaktní, API je intuitivní a nyní máte pevný základ pro tvorbu složitějších textových zpracovatelských pipeline.

Jste připraveni na další krok? Zkuste extrahovat okolní odstavec, exportovat výsledky do CSV nebo dokonce zvýraznit shody v generovaném PDF. Všechny tyto úkoly přirozeně navazují na koncepty, které jste právě zvládli.

Máte-li otázky, napište do komentářů — šťastné programování!

## Související tutoriály

- [Jak upravit HTML pomocí Aspose.HTML pro Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Jak upravit strom HTML dokumentu v Aspose.HTML pro Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Jak převést HTML do PDF v Javě – pomocí Aspose.HTML pro Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}