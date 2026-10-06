---
category: general
date: 2026-03-04
description: Jak zvýraznit HTML vyhledáváním textu v HTML a obalením každé shody značkou
  <mark>. Krok za krokem průvodce v Javě pro nahrazení textu značkami <mark>.
draft: false
keywords:
- how to highlight html
- search text in html
- highlight word in html
- highlight occurrences of word
- replace text with mark
language: cs
og_description: Jak zvýraznit HTML vyhledáváním textu v HTML a obalením nalezených
  částí tagem <mark>. Kompletní Java příklad pro nahrazení textu tagem <mark>.
og_title: Jak zvýraznit HTML – vyhledat text a nahradit <mark>
tags:
- Aspose.HTML
- Java
- Text Processing
title: Jak zvýraznit HTML – vyhledat text a nahradit <mark>
url: /cs/java/editing-html-documents/how-to-highlight-html-search-text-replace-with-mark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zvýraznit HTML – vyhledat text a nahradit pomocí `<mark>`

Už jste se někdy zamýšleli **jak zvýraznit HTML**, když se určité slovo objeví vícekrát? Možná budujete dokumentační web, blogový engine nebo jen potřebujete zdůraznit název značky na statické stránce. Dobrá zpráva? Je to celkem jednoduché, jakmile víte, jak vyhledat text v HTML a obalit výsledek elementem `<mark>`.

V tomto tutoriálu projdeme kompletní řešení v Javě, které načte HTML soubor, vyhledá cílové slovo, nahradí každé jeho výskyt tagem `<mark>` a nakonec uloží zvýrazněnou verzi. Na konci budete umět **zvýraznit slovo v HTML**, **zvýraznit výskyty slova** a dokonce **nahradit text značkou mark** bez poškození okolního markup.

> **Co budete potřebovat**  
> • Java 17 nebo novější (kód funguje i s dřívějšími verzemi)  
> • Knihovna Aspose.HTML for Java (zkušební verze nebo licencovaná kopie)  
> • Jednoduchý HTML soubor, který chcete zpracovat  

Pokud máte tyto základy připravené, pojďme na to.  

![Screenshot zobrazující zvýrazněný HTML výstup – jak zvýraznit html](/images/highlight-html-example.png "příklad jak zvýraznit html")

## Krok 1 – Načtení HTML dokumentu (Jak zvýraznit HTML)

Nejprve musíme načíst zdrojový soubor do paměti. Třída `Document` z Aspose.HTML provádí veškeré těžké zpracování, parsuje markup do struktury podobné DOM, kterou můžeme dotazovat.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Load the original HTML file
        Document document = new Document("YOUR_DIRECTORY/article.html");
```

**Proč je to důležité:** Načtení dokumentu nám poskytne čistý objektový model, takže můžeme bezpečně manipulovat s textovými uzly, aniž bychom se obávali rozbít tagy nebo atributy. Navíc normalizuje bílé znaky, což činí pozdější **vyhledávání textu v html** spolehlivějším.

## Krok 2 – Vyhledat text v HTML pro cílové slovo

Nyní, když je dokument připraven, vyhledáme každý výskyt slova, které chceme zdůraznit. Metoda `searchText` vrací seznam objektů `TextMatch`, z nichž každý popisuje, kde se shoda nachází v DOM.

```java
        // Define what we want to highlight
        String searchTerm = "Aspose";

        // Find all matches – this is the core of "search text in html"
        List<TextMatch> matches = document.searchText(searchTerm);
```

**Tip:** Vyhledávání je ve výchozím nastavení citlivé na velikost písmen. Pokud potřebujete vyhledávat bez rozlišení velikosti, převedete jak text dokumentu, tak `searchTerm` na stejný případ před voláním `searchText`, nebo použijete přístup založený na regulárních výrazech, který knihovna poskytuje.

## Krok 3 – Nahradit text pomocí `<mark>` (Zvýraznit slovo v HTML)

Pro každou shodu znovu sestavíme text obsahujícího uzlu a vložíme element `<mark>` kolem přesného slova. Tím zajistíme, že ovlivníme jen cílový text a zbytek HTML zůstane nedotčený.

```java
        // Iterate over each match and wrap it with <mark>
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();

            // Preserve text before and after the match
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;

            // Replace the node's content with the new fragment
            parentNode.setTextContent(highlightedFragment);
        }
```

**Vysvětlení:**  
- `getStartOffset`/`getEndOffset` nám dávají přesné pozice znaků shody uvnitř nadřazeného uzlu.  
- Rozdělením původního textu (`textBefore` a `textAfter`) zachováme vše ostatní tak, jak to bylo.  
- Obalení shody tagem `<mark>` je kanonický způsob, jak **nahradit text značkou mark** a získat nativní zvýraznění v prohlížeči bez dalšího CSS.

### Okrajové případy a tipy

- **Více shod ve stejném uzlu:** Smyčka zpracovává každou `TextMatch` postupně. Protože pokaždé nahradíme celý obsah uzlu, posunou se pozdější offsety. Aspose.HTML vrací shody v pořadí dokumentu, takže jednoduchá náhrada funguje ve většině případů. Pokud narazíte na překrývající se shody, zvažte nejprve sesbírání všech shod a poté přestavbu uzlu v jednom průchodu.  
- **Elementy, které nemohou obsahovat surové HTML:** Pokud je nadřazený uzel `<script>` nebo `<style>`, vložení `<mark>` by stránku rozbilo. Tyto uzly můžete přeskočit kontrolou `parentNode.getNodeName()` před náhradou.

## Krok 4 – Uložit zvýrazněný dokument (Zvýraznit výskyty slova)

Po provedení všech náhrad uložíme upravený DOM zpět na disk. Výstupní soubor bude obsahovat původní markup plus nové tagy `<mark>`, čímž efektivně **zvýrazní výskyty slova** „Aspose“.

```java
        // Write the modified HTML back to a new file
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

Otevřete `highlighted.html` v libovolném prohlížeči a uvidíte každé „Aspose“ obalené žlutým pozadím (výchozí styl pro `<mark>`). Pokud chcete vlastní vzhled, přidejte malý CSS pravidlo:

```html
<style>
    mark { background-color: #fffa8b; color: #000; }
</style>
```

## Často kladené otázky (Vyhledávání textu v HTML – FAQ)

**Q: Co když se slovo objeví uvnitř hodnoty atributu?**  
A: `searchText` prohledává jen textový obsah uzlů, ne řetězce atributů. Pro zvýraznění hodnot atributů byste museli iterovat přes elementy a ručně kontrolovat atributy.

**Q: Můžu zvýraznit více různých slov najednou?**  
A: Ano. Vytvořte seznam termínů, projděte jej a aplikujte stejnou logiku náhrady. Jen dejte pozor na překrývající se shody.

**Q: Funguje to s HTML5‑exkluzivními tagy jako `<section>` nebo `<article>`?**  
A: Ano. Aspose.HTML plně podporuje moderní HTML5 elementy, takže procházení DOM funguje bez ohledu na typ tagu.

## Kompletní funkční příklad (Všechny kroky dohromady)

Níže je kompletní, připravený Java program, který demonstruje celý pracovní postup – od načtení souboru po uložení zvýrazněného výstupu.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document
        Document document = new Document("YOUR_DIRECTORY/article.html");

        // Step 2: Search for the word "Aspose"
        String searchTerm = "Aspose";
        List<TextMatch> matches = document.searchText(searchTerm);

        // Step 3: Wrap each found occurrence with a <mark> element
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted HTML fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;
            parentNode.setTextContent(highlightedFragment);
        }

        // Step 4: Save the highlighted document
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

**Očekávaný výstup:** Otevřete `highlighted.html` a uvidíte každé výskyt „Aspose“ zvýrazněný. Ostatní části stránky zůstávají nezměněny a soubor zůstává platným HTML dokumentem.

## Závěr

Probrali jsme **jak zvýraznit HTML** programově **vyhledáváním textu v HTML**, obalením každé shody tagem `<mark>` a následným uložením změn. Tento přístup vám umožní **zvýraznit slovo v HTML**, **zvýraznit výskyty slova** a **nahradit text značkou mark** bez psaní křehkého kódu pro manipulaci s řetězci.

Další kroky? Zkuste rozšířit skript tak, aby:

- Přijímal hledaný termín jako argument příkazové řádky.  
- Generoval CSS soubor definující vlastní barvu zvýraznění.  
- Zpracovával celý adresář HTML souborů najednou.  

Tyto varianty prohloubí vaše pochopení jak Aspose.HTML API, tak obecných vzorů pro zpracování textu.  

Pokud narazíte na problémy nebo máte nápady na další vylepšení, zanechte komentář níže. Šťastné zvýrazňování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}