---
date: 2026-04-05
description: Naučte se, jak vytvořit PDF z HTML nastavením vlastního uživatelského
  stylu v Aspose.HTML pro Java, a snadno převést HTML do PDF pomocí služby User Agent.
keywords:
- create pdf from html
- convert html to pdf
- java html to pdf
- generate pdf with css
- configure user agent
linktitle: Nastavit uživatelský stylový list v Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Vytvořit PDF z HTML – nastavit uživatelský stylový list v Aspose.HTML pro Javu
url: /cs/java/configuring-environment/set-user-style-sheet/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořit PDF z HTML – Nastavit uživatelský stylový list v Aspose.HTML pro Java

## Úvod
V tomto tutoriálu se naučíte, jak **create PDF from HTML** pomocí Aspose.HTML pro Java a aplikovat vlastní uživatelský stylový list. Už jste někdy chtěli upravit vzhled svých HTML dokumentů svým jedinečným stylem? Představte si, že vytváříte webovou stránku a potřebujete, aby nadpisy vynikly konkrétní barvou nebo odstavce vypadaly konzistentně napříč zařízeními. Právě zde přichází do hry *user stylesheet* a **User Agent Service**. Provedeme vás každým krokem – od napsání jednoduchého HTML souboru, konfigurace uživatelského agenta až po finální **convert HTML to PDF** – abyste výsledek viděli okamžitě.

## Rychlé odpovědi
- **What does “create PDF from HTML” mean?** Znamená to vykreslení HTML dokumentu (s CSS, obrázky, fonty atd.) a uložení vizuálního výstupu jako PDF soubor.  
- **Which Aspose component is required?** Knihovna Aspose.HTML pro Java poskytuje konverzní engine a User Agent Service.  
- **Do I need a license for testing?** Bezplatná zkušební verze funguje pro vývoj; pro produkci je vyžadována komerční licence.  
- **Can I use an external CSS file?** Ano – můžete odkazovat na externí stylové listy stejně jako v běžném prohlížeči.  
- **How long does the conversion take?** U jednoduchého dokumentu, jako je ten v tomto průvodci, konverze proběhne za méně než sekundu.  
- **Why configure the User Agent Service?** Umožňuje vám vložit vlastní stylový list, nastavit výchozí znakové sady a řídit možnosti vykreslování, což zajišťuje konzistentní výstup PDF.  

## Co je “create PDF from HTML”?
Vytvoření PDF z HTML je proces převzetí webově orientovaného dokumentu (HTML + CSS) a jeho vykreslení do PDF souboru s pevnou rozlohou. To je užitečné pro generování zpráv, faktur nebo jakéhokoli tisknutelného materiálu přímo z webového obsahu.

## Proč použít User Agent Service v Aspose.HTML?
**User Agent Service** vám poskytuje nízkoúrovňovou kontrolu nad možnostmi vykreslování, jako je výchozí znaková sada, jazyk, fonty a – nejdůležitější pro tento tutoriál – vlastní uživatelský stylový list. Aplikací stylů na této úrovni zajistíte konzistentní vizuální výstup i když původní HTML neobsahuje vlastní CSS.

## Požadavky
Než se ponoříme do kódu, ujistěte se, že máte následující:

1. **Aspose.HTML for Java** – stáhněte nejnovější JAR ze [Aspose releases page](https://releases.aspose.com/html/java/).  
2. **Java Development Kit (JDK) 8+** – ujistěte se, že `java -version` vrací 8 nebo vyšší.  
3. **IDE** – IntelliJ IDEA, Eclipse nebo NetBeans budou fungovat.  
4. **Basic HTML/CSS knowledge** – užitečné, ale není povinné.

## Import balíčků
Pro začátek importujte nezbytné třídy Java. Jediný explicitní import, který pro tento příklad potřebujete, je `java.io.IOException`; třídy Aspose jsou později odkazovány pomocí plně kvalifikovaných názvů.

```java
import java.io.IOException;
```

## Krok 1: Vytvořit jednoduchý HTML dokument
Nejprve napíšeme minimální HTML soubor (`document.html`), který bude sloužit jako zdroj pro naši konverzi do PDF.

```java
String code = "<h1>User Agent Service</h1>\r\n" +
        "<p>The User Agent Service allows you to specify a custom user stylesheet, a primary character set for the document, language, and fonts settings.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Tip:** Uchovávejte HTML soubor ve stejném adresáři jako váš Java zdroj, aby se předešlo problémům souvisejícím s cestami.

## Krok 2: Nastavit konfiguraci Aspose.HTML
Vytvořte objekt `Configuration`. Tento objekt funguje jako kontejner pro všechny služby (včetně User Agent Service), které později použijete.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Krok 3: Přístup k User Agent Service  
**User Agent Service** vám umožňuje vložit vlastní stylový list, nastavit výchozí znakovou sadu a řídit další možnosti vykreslování.

```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

## Krok 4: Definovat a použít uživatelský stylový list  
Nyní poskytneme CSS pravidla, která budou stylovat HTML při jeho vykreslování. Zde **používáme user agent service** k nastavení stylového listu.

```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; font-size:2em; }\r\n" +
        "p { background-color:GhostWhite; color:SlateGrey; font-size:1.2em; }\r\n");
```

> **Proč je to důležité:** Aplikací stylového listu na úrovni user‑agent zajistíte, že styly budou respektovány i když původní HTML neodkazuje na CSS soubor.

## Krok 5: Načíst HTML dokument s vlastní konfigurací  
Předávejte jak cestu k souboru, tak instanci `Configuration` konstruktoru `HTMLDocument`. Tím se spojí uživatelský stylový list s dokumentem.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```

## Krok 6: Převést HTML na PDF  
S plně stylovaným dokumentem zavolejte statickou metodu `convertHTML` k **convert HTML to PDF**. Objekt `PdfSaveOptions` vám umožní jemně doladit výstup (např. velikost stránky, komprese).

```java
com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.PdfSaveOptions(),
        "user-agent-stylesheet_out.pdf"
);
```

> **Výsledek:** `user-agent-stylesheet_out.pdf` bude obsahovat nadpis v hnědé barvě a odstavec s pozadím GhostWhite, přesně tak, jak je definováno ve stylovém listu.

## Krok 7: Vyčistit zdroje
Vždy uvolněte objekty Aspose, aby se uvolnila nativní paměť.

```java
if (document != null) {
    document.dispose();
}
if (configuration != null) {
    configuration.dispose();
}
```

## Časté problémy a řešení
| Problém | Příčina | Řešení |
|-------|-------|-----|
| **Blank PDF output** | Nebyl aplikován žádný stylový list nebo dokument nebyl načten s konfigurací. | Ověřte, že `configuration` je předána do `HTMLDocument` a že `setUserStyleSheet` je volána před načtením. |
| **Unsupported CSS property warning** | Aspose.HTML nepodporuje některé pokročilé CSS vlastnosti. | Používejte pouze CSS vlastnosti uvedené v dokumentaci Aspose.HTML nebo se vraťte k jednodušším stylům. |
| **FileNotFoundException** | Špatná cesta k `document.html`. | Použijte absolutní cestu nebo umístěte HTML soubor do kořenového adresáře projektu. |

## Často kladené otázky

**Q: Můžu použít různé styly pro různé HTML elementy?**  
A: Rozhodně! Můžete definovat tolik CSS pravidel, kolik potřebujete v uživatelském stylovém listu.

**Q: Co když potřebuji změnit stylový list dynamicky?**  
A: Zavolejte `setUserStyleSheet` znovu před vytvořením nové instance `HTMLDocument`; nové styly budou aplikovány při další konverzi.

**Q: Je možné použít externí CSS soubory s Aspose.HTML pro Java?**  
A: Ano, můžete buď odkazovat na externí stylový list v HTML, nebo načíst jeho obsah a předat jej `setUserStyleSheet`.

**Q: Jak Aspose.HTML zachází s nepodporovanými CSS vlastnostmi?**  
A: Nepodporované vlastnosti jsou ignorovány, což umožňuje zbytku stylového listu renderovat bez chyb.

**Q: Můžu převést HTML do formátů jiných než PDF?**  
A: Ano, Aspose.HTML podporuje konverzi do XPS, TIFF, PNG, JPEG a dalších pomocí odpovídající třídy `SaveOptions`.

---

**Poslední aktualizace:** 2026-04-05  
**Testováno s:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}