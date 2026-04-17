---
category: general
date: 2026-03-05
description: Jak dotazovat HTML v Javě pro načtení HTML souboru a extrahování obrázků.
  Naučte se načíst HTML soubor v Javě, získat URL obrázků v Javě a iterovat přes NodeList
  v Javě.
draft: false
keywords:
- how to query html
- read html file java
- how to extract images
- iterate over nodelist java
- get image urls java
language: cs
og_description: Jak dotazovat HTML v Javě a získat URL obrázků. Tento průvodce ukazuje,
  jak načíst HTML soubor v Javě, najít obrázky a iterovat přes NodeList v Javě.
og_title: Jak dotazovat HTML v Javě – Extrahovat URL obrázků
tags:
- html parsing
- java
- aspose-html
- xpath
- css selector
title: Jak dotazovat HTML v Javě – extrahovat URL obrázků
url: /cs/java/creating-managing-html-documents/how-to-query-html-in-java-extract-image-urls/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak dotazovat HTML v Javě – Extrahovat URL obrázků

Už jste se někdy zamýšleli **jak dotazovat HTML** v Javě, abyste získali každý obrázek na stránce? Nejste jediní – vývojáři často potřebují číst HTML soubory, stahovat obrázky a pak s URL něco užitečného udělat. V tomto tutoriálu projdeme praktickým příkladem, který přesně ukazuje **jak dotazovat HTML**, číst HTML soubor v Javě a získat URL obrázků v Javě.

Použijeme Aspose.HTML pro Javu, ale koncepty – XPath, CSS selektory a iterace přes `NodeList` – platí pro jakoukoli DOM knihovnu. Na konci tohoto průvodce budete pohodlně ovládat **jak extrahovat obrázky**, budete vědět, jak **iterovat přes NodeList v Javě**, a budete mít připravený kód, který můžete vložit do svého projektu.

![Jak dotazovat HTML v Javě – příklad](https://example.com/placeholder.png "Jak dotazovat HTML v Javě")

---

## Co se naučíte

- Načíst HTML dokument z disku (číst HTML soubor v Javě)
- Najít značky `<img>` pomocí XPath i CSS selektorů (jak extrahovat obrázky)
- Procházet výsledný `NodeList` (iterovat přes NodeList v Javě)
- Vytisknout atribut `src` každého obrázku (získat URL obrázků v Javě)

Žádné externí služby, žádné složité nástroje pro sestavení – jen čistá Java a jediná Maven závislost.

---

## Požadavky

- Nainstalovaná Java 8 nebo novější
- Maven nebo Gradle pro správu závislostí
- Základní znalost struktury HTML
- Volitelné, ale užitečné: jednoduchý HTML soubor (`sample.html`) obsahující některé elementy `<figure><img …></figure>`

Pokud je máte, můžeme rovnou začít.

---

## Krok 1: Číst HTML soubor v Javě – Načíst dokument

Nejprve musíme načíst HTML do paměti. Třída `HTMLDocument` z Aspose.HTML provádí těžkou práci. Představte si to jako otevření knihy, abyste mohli přejít na libovolnou stránku.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.NodeList;
import com.aspose.html.dom.Element;

/**
 * Demonstrates how to query HTML in Java and extract image URLs.
 */
public class QueryExample {
    public static void main(String[] args) throws Exception {

        // ① Load the HTML document from a local file.
        // Replace "YOUR_DIRECTORY/sample.html" with the actual path.
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

**Proč je to důležité:** Načtení souboru vám poskytne DOM strom, který můžete dotazovat. Pokud je cesta špatná, získáte `FileNotFoundException`, takže před spuštěním zkontrolujte umístění.

---

## Krok 2: Najít obrázky pomocí XPath – Jak extrahovat obrázky

XPath je výkonný dotazovací jazyk, který vám umožní přesně vybrat uzly. Zde požadujeme každý `<img>` uvnitř `<figure>`, který má také atribut `alt`.

```java
        // ② Use XPath to find <img> elements that have an "alt" attribute.
        NodeList xpathImages = document.evaluateXPath("//figure/img[@alt]");
        System.out.println("XPath found " + xpathImages.getLength() + " images.");
```

**Proč XPath?** Je stručný a funguje i při nečistém HTML. Výraz `//figure/img[@alt]` znamená: „každý `<img>` pod `<figure>`, který má atribut `alt`.“ Pokud potřebujete filtrovat podle jiných atributů, stačí upravit závorky.

---

## Krok 3: Najít obrázky pomocí CSS selektoru – Alternativní způsob, jak extrahovat obrázky

Někdy dáváte přednost CSS syntaxi, protože odráží to, co píšete v stylech. `querySelectorAll` přijímá stejný selektor, jaký byste použili v prohlížeči.

```java
        // ③ Same query using a CSS selector.
        NodeList cssImages = document.querySelectorAll("figure img[alt]");
        System.out.println("CSS selector found " + cssImages.getLength() + " images.");
```

**Proč oba?** Ukázka obou vám umožní vybrat si nástroj, se kterým jste nejpohodlnější. V praxi byste se drželi jednoho, ale mít oba příklady dělá tutoriál kompletnějším.

---

## Krok 4: Iterovat přes NodeList v Javě – Získat URL obrázků v Javě

Nyní, když máme kolekci, musíme ji projít. Zde vstupuje do hry **iterovat přes NodeList v Javě**. Vytáhneme atribut `src` každého obrázku a vytiskneme jej.

```java
        // ④ Loop through the NodeList returned by the CSS query.
        for (int i = 0; i < cssImages.getLength(); i++) {
            Element imageElement = (Element) cssImages.item(i);
            // Extract the "src" attribute – that’s the image URL.
            System.out.println("Image src: " + imageElement.getAttribute("src"));
        }
    }
}
```

**Proč klasický `for` cyklus?** Aspose `NodeList` neimplementuje `Iterable`, takže rozšířená syntaxe `for‑each` se neskompiluje. Použití cyklu s indexem je spolehlivý způsob, jak **iterovat přes NodeList v Javě**.

---

## Očekávaný výstup

Spuštění programu proti ukázkovému HTML jako:

```html
<figure>
    <img src="images/pic1.jpg" alt="First picture">
</figure>
<figure>
    <img src="images/pic2.png" alt="Second picture">
</figure>
```

Vygeneruje něco podobného:

```
XPath found 2 images.
CSS selector found 2 images.
Image src: images/pic1.jpg
Image src: images/pic2.png
```

Pokud váš soubor obsahuje více značek `<img>`, které splňují kritéria, čísla se podle toho zvýší.

---

## Časté úskalí a tipy

- **Problémy s cestou k souboru:** Použijte absolutní cestu nebo umístěte `sample.html` relativně k pracovnímu adresáři vašeho projektu.  
- **Chybějící atribut `alt`:** Naše XPath/CSS dotazy filtrují podle `[@alt]`. Pokud potřebujete *všechny* obrázky, odstraňte filtr atributu (`//figure/img` nebo `figure img`).  
- **Výkon:** Pro obrovské dokumenty zvažte streamovací parsery, ale pro většinu úloh web‑scrapingu je DOM přístup v pořádku.  
- **Problémy s kódováním:** Aspose.HTML respektuje charset deklarovaný v HTML. Pokud vidíte poškozené znaky, ujistěte se, že soubor je uložený jako UTF‑8.  

---

## Rozšíření příkladu

Nyní, když můžete **získat URL obrázků v Javě**, můžete chtít:

1. **Stáhnout obrázky** pomocí `java.net.URL` a `Files.copy`.  
2. **Uložit URL do databáze** pro pozdější zpracování.  
3. **Filtrovat podle přípony souboru** (`src.endsWith(".png")`).  

Všechny tyto jsou jednoduchými rozšířeními smyčky ukázané v Kroku 4.

---

## Závěr

V tomto průvodci jsme pokryli **jak dotazovat HTML** v Javě od začátku do konce: načtení souboru, vyhledání obrázků pomocí XPath i CSS selektorů a **iteraci přes NodeList v Javě** pro vytištění `src` každého obrázku. Nyní máte pevný základ pro **jak extrahovat obrázky**, a přesně víte **jak číst HTML soubor v Javě** pomocí Aspose.HTML.

Neváhejte upravit kód podle svých potřeb scrapování – ať už jde o získání dalších atributů, zpracování značek `<a>` nebo předání URL do stahovače. Vzor zůstává stejný: načíst, dotazovat, iterovat a jednat.

Máte otázky nebo chcete sdílet zajímavý případ použití? Zanechte komentář níže a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}