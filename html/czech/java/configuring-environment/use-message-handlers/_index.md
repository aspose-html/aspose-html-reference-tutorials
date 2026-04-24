---
date: 2026-02-10
description: Naučte se, jak používat Aspose k řešení poškozených odkazů v Javě, převádět
  HTML na PNG a načítat HTML dokument v Javě pomocí Aspose.HTML pro Javu.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Převod HTML na PNG s Aspose.HTML Message Handlers v Javě
url: /cs/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod HTML na PNG pomocí Aspose.HTML Message Handlers v Javě

## Úvod
V tomto tutoriálu se dozvíte **jak převést HTML na PNG** a zároveň elegantně zacházet s chybějícími zdroji pomocí Aspose.HTML pro Javu. Provedeme vás vytvořením malé HTML stránky, která odkazuje na neexistující obrázek, nastavením **vlastního message handleru** k **zachycení síťových požadavků**, konfigurací **síťové služby**, načtením dokumentu a nakonec provedením **převodu HTML na obrázek**. Na konci budete mít solidní vzor jak pro **handle broken links java**, tak pro výstup PNG vysoké kvality — ideální pro zprávy, miniatury nebo náhledy e‑mailů.

## Rychlé odpovědi
- **Co dělá message handler?** Zachycuje síťové operace (např. požadavky na obrázky) a umožňuje reagovat na stavové kódy jako 404.  
- **Umí Aspose.HTML převést HTML na PNG?** Ano — `Converter.convertHTML` provádí převod jedním voláním.  
- **Potřebuji licenci pro tento příklad?** Dočasná licence odstraňuje omezení hodnocení; pro produkční použití je vyžadována trvalá licence.  
- **Která verze Javy funguje?** Jakýkoli JDK 8+ (ukázka běží na JDK 11).  
- **Mohu konfigurovat síťovou službu?** Samozřejmě — použijte `configuration.getService(INetworkService.class)` k přidání vašeho handleru.

## Požadavky
Než se ponoříme dál, ujistěte se, že máte následující připravené:

1. **Java Development Kit (JDK)** — stáhněte z [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** — získejte knihovnu ze [Aspose releases page](https://releases.aspose.com/html/java/).  
3. **IDE** — IntelliJ IDEA, Eclipse nebo NetBeans jsou v pořádku.  
4. **Základní znalost Javy** — měli byste být obeznámeni s třídami, try‑with‑resources a zpracováním výjimek.  
5. **Dočasná licence** — pokud používáte zkušební verzi, pořiďte si [temporary license](https://purchase.aspose.com/temporary-license/) pro odstranění vodoznaků.

## Import balíčků
Nejprve načtěte třídu Java I/O, kterou budeme potřebovat pro práci se soubory. Ostatní třídy Aspose jsou později odkazovány pomocí plně kvalifikovaných názvů, což udržuje seznam importů přehledný.

```java
import java.io.IOException;
```

## Krok 1: Připravte HTML kód
Vytvoříme minimální úryvek HTML, který úmyslně odkazuje na chybějící obrázek. To spustí náš handler, když engine bude chtít načíst zdroj.

```java
String code = "<img src='missing.jpg'>";
```

## Krok 2: Zapište HTML kód do souboru
Dále uložíme úryvek do *document.html*. Použití bloku try‑with‑resources zajišťuje, že `FileWriter` bude řádně uzavřen.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Krok 3: Napište vlastní Message Handler
Nyní vytvoříme **vlastní message handler**, který kontroluje HTTP stav každého síťového požadavku. Pokud odpověď není `200`, zaznamenáme přátelské varování. Všimněte si volání `invoke(context);` na konci — tím se požadavek předá dalšímu handleru v řetězci, čímž se zabrání rekurzi.

```java
com.aspose.html.net.MessageHandler handler = new com.aspose.html.net.MessageHandler() {
    @Override
    public void invoke(com.aspose.html.net.INetworkOperationContext context) {
        if (context.getResponse().getStatusCode() != 200) {
            System.out.println(String.format("File '%s' Not Found", context.getRequest().getRequestUri().toString()));
        }
        invoke(context);
    }
};
```

## Krok 4: Nakonfigurujte síťovou službu
Aby Aspose.HTML poznal náš handler, získáme **síťovou službu** z instance `Configuration` a přidáme handler do její kolekce. Toto je krok, kde **konfigurujeme síťovou službu** pro vlastní chování.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Krok 5: Načtěte HTML dokument
Po připravení konfigurace načteme *document.html*. Engine nyní používá naši síťovou službu, takže požadavek na chybějící obrázek zachytí právě přidaný handler.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Additional operations will go here
} finally {
    if (document != null) {
        document.dispose();
    }
}
```

## Krok 6: Převod HTML na PNG
Zde je jádro procesu **html to image conversion**. Metoda `Converter.convertHTML` přijímá načtený `HTMLDocument`, volitelné `ImageSaveOptions` (kde můžete upravit DPI nebo kvalitu) a název výstupního souboru.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Krok 7: Vyčistěte prostředky
Dobrá praxe v Javě vyžaduje uvolnění všech nativních prostředků. Blok `finally` zajišťuje, že `Configuration` bude uvolněna i v případě, že se vyhodí výjimka.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Proč používat Message Handlery?
Message handlery vám poskytují **jemnou kontrolu** nad každým síťovým požadavkem — ať už jde o obrázek, CSS, JavaScript nebo soubor fontu. Místo toho, aby knihovna selhala tiše, můžete zaznamenávat chybějící zdroje, poskytovat záložní obsah nebo dokonce požadavek opakovat. To činí váš HTML zpracovatelský řetězec **robustním**, **připraveným pro produkci** a snáze laditelným.

## Časté problémy a řešení
- **Rekurze handleru** — volání `invoke(context);` pouze jednou, aby se předešlo nekonečným smyčkám.  
- **Chybějící licence** — bez platné licence bude výstupní PNG obsahovat vodoznak.  
- **Nesprávné cesty k souborům** — použijte absolutní cesty nebo správně nastavte pracovní adresář při načítání `document.html`.  
- **Nepodporované typy zdrojů** — ujistěte se, že zdroj, který chcete zachytit (obrázek, CSS atd.), je skutečně požadován HTML engine.

## Často kladené otázky

**Q: Mohu řetězit více message handlerů?**  
A: Ano, můžete přidat několik handlerů do kolekce `network.getMessageHandlers()`; budou provedeny v pořadí, v jakém byly přidány.

**Q: Funguje handler také pro CSS nebo skriptové zdroje?**  
A: Rozhodně — každý síťový požadavek vytvořený HTML engine (obrázky, CSS, JS, fonty) prochází handlerem.

**Q: Jak mohu změnit HTTP požadavek před jeho odesláním?**  
A: Implementujte handler, který upraví `context.getRequest()` před voláním `invoke(context)`.

**Q: Existuje způsob, jak potlačit varování pro konkrétní URL?**  
A: V handleru prozkoumejte `context.getRequest().getRequestUri()` a podmíněně vynechejte zápis do logu.

**Q: Jaká verze Aspose.HTML je pro tyto API vyžadována?**  
A: Kód funguje s Aspose.HTML pro Java 22.10 a novější.

## Závěr
Nyní máte kompletní, end‑to‑end příklad **jak převést HTML na PNG** a zároveň použít **vlastní message handler** k **zachycení síťových požadavků** a **handle broken links java**. Konfigurací síťové služby, načtením dokumentu a voláním konvertoru můžete spolehlivě generovat PNG miniatury nebo snímky celé stránky v jakékoli Java aplikaci.

---

**Last Updated:** 2026-02-10  
**Tested With:** Aspose.HTML for Java 24.11  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}