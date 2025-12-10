---
date: 2025-12-10
description: Naučte se, jak používat Aspose k řešení poškozených odkazů v Javě, převádět
  HTML na PNG a načítat HTML dokument v Javě pomocí Aspose.HTML pro Javu.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Jak používat zpracovatele zpráv Aspose.HTML v Javě
url: /cs/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat Aspose.HTML Message Handlers v Javě

## Introduction
V tomto tutoriálu je krok za krokem předvedeno, **how to use aspose** pro zpracování chybějících zdrojů v HTML. Vytvoříme jednoduchý HTML dokument, který odkazuje na chybějící obrázek, připojíme vlastní message handler a ukážeme vám, jak **load html document java** s elegantním zacházením s nefunkčními odkazy. Na konci také uvidíte, jak **convert html to png** pomocí Aspose.HTML, což vám poskytne kompletní přehled o konverzi HTML na obrázek v Javě.

## Quick Answers
- **What is the primary purpose of a message handler?** Interceptovat síťové operace a reagovat na stavové kódy, jako jsou chybějící zdroje.  
- **Can Aspose.HTML convert HTML to PNG?** Ano, pomocí `Converter.convertHTML` můžete provést konverzi HTML na obrázek.  
- **Do I need a license for this example?** Dočasná licence odstraňuje omezení hodnocení; trvalá licence je vyžadována pro produkci.  
- **Which Java version is supported?** Jakýkoli JDK 8+ (v tutoriálu je použit JDK 11).  
- **Is it possible to handle multiple broken links?** Rozhodně – můžete řetězit několik handlerů pro správu různých scénářů.

## Prerequisites
1. Java Development Kit (JDK): Ujistěte se, že máte JDK nainstalovaný ve svém systému. Můžete jej stáhnout z [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. Aspose.HTML for Java: Budete potřebovat nainstalovaný Aspose.HTML for Java. Stáhněte jej z [Aspose releases page](https://releases.aspose.com/html/java/).  
3. IDE: Použijte své oblíbené Java Integrated Development Environment (IDE) jako IntelliJ IDEA, Eclipse nebo NetBeans.  
4. Basic Knowledge of Java: Znalost programování v Javě je nezbytná pro efektivní sledování tohoto tutoriálu.  
5. Temporary License: Pokud používáte zkušební verzi Aspose.HTML, zvažte získání [temporary license](https://purchase.aspose.com/temporary-license/), abyste se vyhnuli omezením během vývoje.

## Import Packages
Než začneme, ujistěte se, že máte do svého Java projektu importovány potřebné balíčky. Níže jsou nezbytné importy, které budete potřebovat:
```java
import java.io.IOException;
```
Tyto importy vám poskytnou přístup ke třídám a metodám potřebným pro zpracování síťových operací, tvorbu HTML dokumentů a provádění konverze HTML‑to‑PNG.

## Step 1: Prepare the HTML Code
Prvním krokem je jednoduchý HTML úryvek, který odkazuje na soubor obrázku. Úmyslně odkážeme na obrázek, který neexistuje, aby se spustil mechanismus zpracování chyb.
```java
String code = "<img src='missing.jpg'>";
```
Tento kód vytváří značku `<img>`, která ukazuje na `missing.jpg`. Protože obrázek chybí, síťová služba vrátí stavový kód odlišný od 200, který zachytí náš vlastní handler.

## Step 2: Write the HTML Code to a File
Dále musíme HTML úryvek uložit, aby ho Aspose.HTML mohl načíst jako dokument.
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
Pomocí `FileWriter` uložíme HTML do **document.html**. Tento soubor se stane zdrojem pro krok **load html document java** později.

## Step 3: Create a Custom Message Handler
Nyní si vytvoříme vlastní message handler, který reaguje, když obrázek nelze najít. Handler kontroluje HTTP stavový kód a vypíše přátelskou zprávu.
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
Metoda `invoke` zkoumá `context.getResponse().getStatusCode()`. Pokud není **200**, vypíšeme jasné varování, že soubor chybí. Poslední volání `invoke(context);` předá řízení dalšímu handleru v řetězci.

## Step 4: Configure the Network Service
Aby Aspose.HTML vědělo o našem handleru, zaregistrujeme jej do síťové služby pomocí třídy `Configuration`.
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
Zde vytvoříme instanci `Configuration`, získáme `INetworkService` a přidáme náš vlastní handler do její kolekce. Tím zajistíme, že handler bude spuštěn při každém síťovém požadavku, například při načítání obrázků.

## Step 5: Load the HTML Document
S připravenou konfigurací můžeme nyní načíst HTML soubor, který jsme vytvořili dříve. Tento krok demonstruje **load html document java**, zatímco chybějící obrázek spustí náš handler.
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
Konstruktor `HTMLDocument` přijímá jak cestu k souboru, tak vlastní `configuration`. Když dokument parsuje značku `<img>`, síťová služba se pokusí načíst `missing.jpg`, obdrží 404 a náš handler vypíše varování.

## Step 6: Convert HTML to PNG
Abychom ukázali širší možnosti Aspose.HTML, převedeme načtený dokument na PNG obrázek. Jedná se o klasický scénář **convert html to png**.
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
`Converter.convertHTML` přijímá `HTMLDocument`, volitelné `ImageSaveOptions` (kde můžete nastavit DPI, kvalitu atd.) a název výstupního souboru. Výsledkem je rastrový obrázek vykresleného HTML.

## Step 7: Clean Up Resources
Správná správa zdrojů je v každé Java aplikaci zásadní. Uvolníme jak `Configuration`, tak `HTMLDocument`, aby nedocházelo k únikům paměti.
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
Zabalení úklidu do bloku `finally` zaručuje jeho provedení i v případě, že se dříve vyvolá výjimka.

## Why Use Message Handlers?
Message handlery vám poskytují detailní kontrolu nad síťovými operacemi, jako je **handle broken links java**. Místo tichého selhání knihovny můžete logovat, opakovat požadavky, nahrazovat zdroje nebo poskytovat náhradní obsah – čímž učiníte zpracování HTML robustním a připraveným pro produkci.

## Common Issues and Solutions
- **Handler recursion** – Ujistěte se, že voláte `invoke(context);` jen jednou, aby nedošlo k nekonečným smyčkám.  
- **Missing license** – Bez platné licence může konverze vytvořit obrázek s vodoznakem.  
- **File path errors** – Používejte absolutní cesty nebo správně nastavte pracovní adresář při načítání `document.html`.

## Frequently Asked Questions

**Q: Can I chain multiple message handlers?**  
A: Ano, můžete přidat několik handlerů do kolekce `network.getMessageHandlers()`; budou provedeny v pořadí, v jakém byly přidány.

**Q: Does the handler work for CSS or script resources as well?**  
A: Rozhodně – jakýkoli síťový požadavek vytvořený HTML enginem (obrázky, CSS, JS, fonty) projde skrz handler.

**Q: How do I change the HTTP request before it’s sent?**  
A: Implementujte handler, který upraví `context.getRequest()` před voláním `invoke(context)`.

**Q: Is there a way to suppress the warning for specific URLs?**  
A: V handleru můžete zkontrolovat `context.getRequest().getRequestUri()` a podmíněně vynechat logování.

**Q: What version of Aspose.HTML is required for these APIs?**  
A: Kód funguje s Aspose.HTML for Java 22.10 a novějšími.

## Conclusion
A to je vše – komplexní průvodce **how to use aspose** message handlery v Javě. Pokryli jsme tvorbu HTML souboru, napojení vlastního handleru na **handle broken links java**, načtení dokumentu a provedení **convert html to png**. S tímto přístupem můžete sebejistě spravovat chybějící zdroje, vynucovat vlastní politiky a rozšiřovat síťové možnosti Aspose.HTML v jakékoli Java aplikaci.

---

**Last Updated:** 2025-12-10  
**Tested With:** Aspose.HTML for Java 24.11  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}