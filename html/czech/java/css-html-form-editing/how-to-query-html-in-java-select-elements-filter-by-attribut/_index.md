---
category: general
date: 2026-02-16
description: Jak dotazovat HTML pomocí Aspose.HTML pro Javu. Naučte se vybírat HTML
  elementy, filtrovat elementy podle atributu, iterovat přes NodeList a získat textový
  obsah během několika kroků.
draft: false
keywords:
- how to query html
- select html elements
- get text content
- iterate over nodelist
- filter elements by attribute
language: cs
og_description: Jak dotazovat HTML pomocí Aspose.HTML pro Java. Tento tutoriál ukazuje,
  jak vybrat HTML elementy, filtrovat podle atributu, iterovat přes NodeList a získat
  textový obsah.
og_title: Jak dotazovat HTML v Javě – kompletní průvodce
tags:
- Java
- Aspose.HTML
- DOM manipulation
title: Jak dotazovat HTML v Javě – Vybrat prvky, filtrovat podle atributu a získat
  textový obsah
url: /cs/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/
---

.

Also there are markdown blockquotes with >. Keep them and translate inside.

Also there are lists.

Make sure to keep markdown formatting.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak dotazovat HTML v Javě – Kompletní průvodce

Už jste se někdy zamýšleli **jak dotazovat HTML**, když potřebujete získat data ze statické stránky? Možná vytváříte nástroj pro sledování cen nebo sbíráte produktové nabídky do katalogu. V každém případě brzy zjistíte, že výběr správných uzlů a získání jejich textu je jádrem úkolu.  

V tomto tutoriálu projdeme reálný příklad, který **vybírá HTML elementy**, **filtruje elementy podle atributu**, **iteruje přes NodeList** a nakonec **získává textový obsah** z každého shody. Na konci budete mít připravený spustitelný Java program, který vypíše každý název produktu, jehož cena je vyšší než 100 USD.

> **Tip:** Aspose.HTML pro Javu poskytuje CSS‑stylové selektory jako nativní, takže nepotřebujete samostatnou knihovnu pro parsování.

---

## Co budete potřebovat

- **Java 17** (nebo jakýkoli aktuální JDK) – API funguje s Java 8+, ale novější verze poskytují lepší výkon.  
- **Aspose.HTML pro Javu** JAR‑y – můžete si stáhnout bezplatnou zkušební verzi z webu Aspose nebo přidat Maven závislost.  
- Jednoduchý soubor **catalog.html** obsahující produktové karty s atributem `data-price` (ukázku níže).  

Žádné další frameworky nejsou potřeba; kód běží jako čistá Java aplikace.

---

## Krok 1: Načtení HTML dokumentu z disku  

První, co musíte udělat, je říct Aspose.HTML, kde se nachází váš zdrojový soubor. Třída `Document` představuje celý DOM strom, stejně jako ho vytvoří prohlížeč.

```java
import com.aspose.html.dom.*;
import com.aspose.html.load.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Load the HTML document from a local file
        Document htmlDoc = new Document("YOUR_DIRECTORY/catalog.html");
```

> **Proč je to důležité:** Načtení dokumentu vytvoří živý DOM, který vám umožní později spouštět CSS selektory. Pokud soubor není nalezen, Aspose vyhodí jasnou `FileNotFoundException`, takže přesně víte, co opravit.

---

## Krok 2: Filtrace elementů podle atributu – výběr drahých produktových karet  

Nyní chceme jen ty elementy `.product‑card`, jejichž atribut `data-price` přesahuje 100. Selektor `.product-card[data-price>100]` dělá právě to.

```java
        // Select product cards where data-price > 100
        NodeList highPricedCards = htmlDoc.querySelectorAll(".product-card[data-price>100]");
```

> **Jak to funguje:**  
> - `.product-card` odpovídá libovolnému elementu s touto třídou.  
> - `[data-price>100]` je filtr atributu, který ponechá jen uzly, jejichž číselná hodnota `data-price` je větší než 100.  
> Toto je stejná syntaxe, jakou používáte v konzoli DevTools prohlížeče, takže je intuitivní pro front‑end vývojáře.

---

## Krok 3: Iterace přes NodeList a získání textového obsahu  

`NodeList` se chová jako kolekce podobná poli, ale stále potřebujete smyčku, která projde každý element. V cyklu **vybereme podřízený element** (`.title`) a přečteme jeho text, poté získáme cenu z atributu.

```java
        // Loop through each matching card
        for (Node node : highPricedCards) {
            Element cardElement = (Element) node; // cast to Element for convenience

            // Get the product title text
            String productTitle = cardElement.querySelector(".title").getTextContent();

            // Retrieve the raw price from the attribute
            String productPrice = cardElement.getAttribute("data-price");

            // Output the result
            System.out.println(productTitle + " – $" + productPrice);
        }
    }
}
```

**Očekávaný výstup** (při předpokladu, že HTML obsahuje dvě vyhovující karty):

```
Deluxe Coffee Maker – $149
Smart LED TV – $799
```

> **Častý úskalí:** Pokud karta neobsahuje element `.title`, `querySelector` vrátí `null` a volání `getTextContent()` by vyvolalo `NullPointerException`. Pro produkční kód je vhodná obranná kontrola (`if (titleElement != null)`).

---

## Krok 4: Kompletní, spustitelný příklad  

Spojením všeho dohromady získáte kompletní program, který můžete zkopírovat a vložit do svého IDE. Nezapomeňte nahradit `YOUR_DIRECTORY/catalog.html` skutečnou cestou k vašemu HTML souboru.

```java
import com.aspose.html.dom.*;
import com.aspose.html.load.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document from a file
        Document htmlDoc = new Document("YOUR_DIRECTORY/catalog.html");

        // Step 2: Select product cards whose data-price attribute is greater than 100
        NodeList highPricedCards = htmlDoc.querySelectorAll(".product-card[data-price>100]");

        // Step 3: Iterate over the matching elements and extract title and price
        for (Node node : highPricedCards) {
            Element cardElement = (Element) node;
            String productTitle = cardElement.querySelector(".title").getTextContent();
            String productPrice = cardElement.getAttribute("data-price");

            // Step 4: Output the product information
            System.out.println(productTitle + " – $" + productPrice);
        }
    }
}
```

Uložte soubor jako `CssSelectorDemo.java`, zkompilujte pomocí `javac` a spusťte `java CssSelectorDemo`. Pokud je vše nastaveno správně, uvidíte v konzoli vytištěné drahé produkty.

---

## Krok 5: Porozumění základním konceptům  

### Výběr HTML elementů  

Metoda `querySelectorAll` přijímá libovolný platný CSS selektor. To znamená, že můžete kombinovat názvy tříd, ID, filtry atributů, pseudo‑třídy a dokonce i descendant selektory. Například `".category[data-active=true] a[href]"` načte všechny odkazy uvnitř aktivních kategorií.

### Získání textového obsahu  

`Element.getTextContent()` vrací spojený text elementu a jeho potomků, přičemž odstraňuje HTML značky. Je to nejspolehlivější způsob, jak získat viditelný text, na rozdíl od `innerHTML`, který zahrnuje markup.

### Iterace přes NodeList  

`NodeList` implementuje `Iterable<Node>`, takže můžete použít rozšířený `for‑each` cyklus, jak je ukázáno výše. Pokud potřebujete přístup podle indexu, můžete zavolat `item(int index)` nebo převést na `List<Node>`.

### Filtrace elementů podle atributu  

Selektory atributů podporují operátory jako `=`, `~=`, `|=`, `^=`, `$=`, `*=` a číselné porovnávací operátory (`>`, `<`, `>=`, `<=`). To vám dává jemnou kontrolu bez psaní extra Java kódu.

---

## Krok 6: Hraniční případy a varianty  

- **Číselné vs. řetězcové porovnání:** Selektor `[data-price>100]` funguje, protože hodnota atributu může být parsována jako číslo. Pokud váš atribut obsahuje ne‑číselné znaky (např. `"100USD"`), porovnání selže. Odstraňte jednotky nejprve nebo použijte vlastní filtr v Javě.  
- **Rozlišování velikosti písmen u tříd:** CSS selektory jsou v XML režimu citlivé na velikost písmen. Ujistěte se, že názvy tříd ve vašem HTML přesně odpovídají.  
- **Více shod na kartu:** Pokud karta obsahuje několik elementů `.title`, `querySelector` vrátí první. Použijte `querySelectorAll(".title")` a iterujte, pokud potřebujete všechny názvy.

---

## Krok 7: Další kroky – co můžete dál?  

Nyní, když ovládáte **jak dotazovat HTML**, zvažte rozšíření skriptu:

1. **Zapsat výsledky do CSV** – užitečné pro import do tabulek.  
2. **Kombinovat s HTTP klientem** – načítat vzdálené stránky za běhu pomocí `java.net.http.HttpClient`.  
3. **Použít složitější filtry** – např. vybírat položky ve slevě (`[data-discount>0]`) nebo řadit podle ceny pomocí Java streamů.  
4. **Integrovat s databází** – uložit extrahované produkty do SQLite nebo MySQL pro pozdější analýzu.

Všechny tyto nápady znovu využívají stejné jádro: **vybrat HTML elementy**, **filtrovat elementy podle atributu**, **iterovat přes NodeList** a **získat textový obsah**.

---

## Závěr  

Probrali jsme **jak dotazovat HTML** pomocí Aspose.HTML pro Javu od začátku až po konec. Načtením dokumentu, použitím CSS selektoru, který filtruje podle `data-price`, procházením výsledného `NodeList` a extrakcí názvu i ceny máte nyní solidní vzor, který můžete přizpůsobit libovolnému úkolu sběru nebo extrakce dat.

Vyzkoušejte kód, upravte selektor podle vlastní struktury a sledujte, jak data odtekají ze stránky do vaší Java aplikace. Šťastné programování!

---

![příklad dotazu HTML](/images/query-html-example.png "příklad dotazu HTML")

*Obrázek ukazuje výstup programu v konzoli, ilustrující extrahované názvy produktů a jejich ceny.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}