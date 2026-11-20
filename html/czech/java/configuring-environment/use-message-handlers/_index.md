---
date: 2026-05-04
description: Naučte se, jak provádět konverzi HTML na PNG, zachytávat síťové požadavky
  v Javě a řešit nefunkční odkazy v Javě pomocí Aspose.HTML pro Javu.
keywords:
- html to png conversion
- intercept network requests java
- html to image conversion
- load html document java
- handle broken links java
linktitle: Použijte zpracovatele zpráv v Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Konverze HTML na PNG s Aspose.HTML Message Handlers v Javě
url: /cs/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod HTML na PNG s Aspose.HTML Message Handlers v Javě

## Úvod do převodu HTML na PNG
V tomto tutoriálu objevíte **how to convert HTML to PNG** při elegantním zacházení s chybějícími zdroji pomocí Aspose.HTML pro Javu. Provedeme vás vytvořením malé HTML stránky, která odkazuje na neexistující obrázek, připojením **custom message handler** k **intercept network requests**, konfigurací **network service**, načtením dokumentu a nakonec provedením **html to image conversion**. Na konci budete mít osvědčený vzor jak pro **handle broken links java**, tak pro výstup PNG vysoké kvality — ideální pro zprávy, náhledy nebo e‑mailové ukázky.

## Rychlé odpovědi
- **What does a message handler do?** Zachycuje síťové operace (např. požadavky na obrázky) a umožňuje reagovat na stavové kódy jako 404.  
- **Can Aspose.HTML convert HTML to PNG?** Ano—`Converter.convertHTML` provádí převod v jediném volání.  
- **Do I need a license for this example?** Dočasná licence odstraňuje omezení hodnocení; pro produkční použití je vyžadována trvalá licence.  
- **Which Java version works?** Jakákoli verze JDK 8+ (ukázka běží na JDK 11).  
- **Can I configure the network service?** Rozhodně—použijte `configuration.getService(INetworkService.class)` k přidání vašeho handleru.

## Co je převod HTML na PNG?
Převod HTML na PNG vykreslí webovou stránku (nebo fragment HTML) do rastrového obrázku. To je užitečné, když potřebujete statické náhledy dynamického obsahu, generovat miniatury pro e‑mailové zpravodaje nebo archivovat webové stránky jako obrázky.

## Proč používat Message Handlers k zachycení síťových požadavků v Javě?
Message handlery vám poskytují **fine‑grained control** nad každým síťovým požadavkem — ať už jde o obrázek, CSS, JavaScript nebo soubor fontu. Zachycením těchto požadavků můžete **log missing assets**, poskytnout náhradní obsah nebo dokonce opakovat neúspěšné stahování, čímž učiníte vaši HTML zpracovatelskou pipeline **robust** a **production‑ready**.

## Požadavky
Než se pustíme dál, ujistěte se, že máte připraveno následující:

1. **Java Development Kit (JDK)** – stáhněte z [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – získejte knihovnu ze [Aspose releases page](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse nebo NetBeans fungují dobře.  
4. **Basic Java knowledge** – měli byste být obeznámeni s třídami, try‑with‑resources a ošetřováním výjimek.  
5. **Temporary License** – pokud používáte zkušební verzi, pořiďte si [temporary license](https://purchase.aspose.com/temporary-license/) pro odstranění vodoznaků.

## Import balíčků
Nejprve načtěte třídu Java I/O, kterou budeme potřebovat pro práci se soubory. Zbytek tříd Aspose je později odkazován pomocí plně kvalifikovaných názvů, což udržuje seznam importů přehledný.

```java
import java.io.IOException;
```

## Krok 1: Připravte HTML kód
Vytvoříme minimální úryvek HTML, který úmyslně odkazuje na chybějící obrázek. To spustí náš handler, když engine bude chtít načíst zdroj.

```java
String code = "<img src='missing.jpg'>";
```

## Krok 2: Zapište HTML kód do souboru
Dále uložíme úryvek do *document.html*. Použití bloku try‑with‑resources zaručuje, že `FileWriter` bude správně uzavřen.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Krok 3: Napište vlastní Message Handler
Nyní vytvoříme **custom message handler**, který kontroluje HTTP stav každého síťového požadavku. Pokud odpověď není `200`, zaznamenáme přátelské varování. Všimněte si volání `invoke(context);` na konci — toto předá požadavek dalšímu handleru v řetězci a zabrání rekurzi.

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
Aby Aspose.HTML rozpoznal náš handler, získáme **network service** z instance `Configuration` a přidáme handler do její kolekce. Toto je krok, kde **configure network service** pro vlastní chování.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Krok 5: Načtěte HTML dokument
Po připravení konfigurace načteme *document.html*. Engine nyní používá naši síťovou službu, takže požadavek na chybějící obrázek je zachycen handlerem, který jsme právě přidali.

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
Dobrá praxe v Javě vyžaduje uvolnění všech nativních prostředků. Blok `finally` zajišťuje, že `Configuration` je uvolněna i v případě, že se vyhodí výjimka.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Časté problémy a řešení
- **Handler recursion** – Zavolejte `invoke(context);` pouze jednou, aby se zabránilo nekonečným smyčkám.  
- **Missing license** – Bez platné licence bude výstupní PNG obsahovat vodoznak.  
- **Incorrect file paths** – Použijte absolutní cesty nebo správně nastavte pracovní adresář při načítání `document.html`.  
- **Unsupported resource types** – Ujistěte se, že zdroj, který chcete zachytit (obrázek, CSS atd.), je skutečně požadován HTML enginem.

## Často kladené otázky

**Q: Můžu řetězit více message handlerů?**  
A: Ano, můžete přidat několik handlerů do kolekce `network.getMessageHandlers()`; budou provedeny v pořadí, v jakém byly přidány.

**Q: Funguje handler také pro CSS nebo skriptové zdroje?**  
A: Rozhodně — jakýkoli síťový požadavek vytvořený HTML enginem (obrázky, CSS, JS, fonty) prochází handlerem.

**Q: Jak změním HTTP požadavek před jeho odesláním?**  
A: Implementujte handler, který upraví `context.getRequest()` před voláním `invoke(context)`.

**Q: Existuje způsob, jak potlačit varování pro konkrétní URL?**  
A: V handleru prozkoumejte `context.getRequest().getRequestUri()` a podmíněně přeskočte zápis.

**Q: Jaká verze Aspose.HTML je vyžadována pro tyto API?**  
A: Kód funguje s Aspose.HTML for Java 22.10 a novější.

---

**Poslední aktualizace:** 2026-05-04  
**Testováno s:** Aspose.HTML for Java 24.11  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}