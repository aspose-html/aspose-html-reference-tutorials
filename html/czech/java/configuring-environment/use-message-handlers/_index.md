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

## Úvod
V tomto tutoriálu je krok za krokem předvedeno, **how to use aspose** pro zpracování chybějících zdrojů v HTML. Vytvoříme jednoduchý HTML dokument, který odkazuje na chybějící obrázek, připojíme vlastní handler zpráv a ukážeme vám, jak **načtete html dokument java** s elegantním zacházením s nefunkčními odkazy. Na konci také uvidíte, jak **convert html to png** pomocí Aspose.HTML, což vám poskytne kompletní přehled o konverzi HTML na obrázek v Javě.

## Rychlé odpovědi
- **Jaký je primární účel obsluhy zpráv?** Interceptovat síťové operace a reagovat na stavové kódy, jako jsou chybějící zdroje.
- **Can Aspose.HTML convert HTML to PNG?** Ano, pomocí `Converter.convertHTML` můžete provést konverzi HTML na obrázek.
- **Potřebuji pro tento příklad licenci?** Dočasná licence hodnocení hodnocení; trvalá licence je vyžadována pro produkci.
- **Jaká verze Java je podporována?** Jakýkoli JDK8+ (v tutoriálu je použit JDK11).
- **Je možné zpracovat více nefunkčních odkazů?** Rozhodně – můžete řetězit několik handlerů pro správu různých scénářů.

## Předpoklady
1. Java Development Kit (JDK): přichází se, že máte J nainstalovaný ve svém systému. Můžete si jej stáhnout z [web Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).
2. Aspose.HTML for Java: Budete potřebovat nainstalovaný Aspose.HTML for Java. Stáhněte jej z [Stránka vydání Aspose](https://releases.aspose.com/html/java/).
3. IDE: Použijte své oblíbené Java Integrated Development Environment (IDE) jako IntelliJ IDEA, Eclipse nebo NetBeans.
4. Basic Knowledge of Java: Znalost programování v Javě je nezbytná pro efektivní sledování tohoto tutoriálu.
5. Dočasná licence: Pokud používáte zkušební verzi licence Aspose.HTML, získáte získání [dočasná licence](https://purchase.aspose.com/temporary-license/) , abyste se vyhnuli omezením během vývoje.

## Importujte balíčky
Než začneme, ujistěte se, že máte do svého Java projektu importovány potřebné balíčky. Níže jsou nezbytné importy, které budete potřebovat:
```java
import java.io.IOException;
```
Tyto importy vám poskytnou přístup ke třídám a metodám potřebným pro zpracování síťových operací, tvorbu HTML dokumentů a provádění konverze HTML‑to‑PNG.

## Krok 1: Příprava HTML kódu
Prvním krokem je jednoduchý HTML úryvek, který odkazuje na soubor obrázku. Úmyslně odkážeme na obrázek, který neexistuje, aby se spustil mechanismus zpracování chyb.
```java
String code = "<img src='missing.jpg'>";
```
Tento kód vytváří značku `<img>`, která ukazuje na `missing.jpg`. Protože obrázek chybí, síťová služba vrátí stavový kód odlišný od 200, který zachytí náš vlastní handler.

## Krok 2: Zapište HTML kód do souboru
Dále musíme HTML úryvek uložit, aby ho Aspose.HTML mohl načíst jako dokument.
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
Pomocí `FileWriter` uložíme HTML do **document.html**. Tento soubor se stane zdrojem pro krok **load html document java** později.

## Krok 3: Vytvořte vlastní obslužnou rutinu zpráv
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

## Krok 4: Konfigurace síťové služby
Aby Aspose.HTML vědělo o našem handleru, zaregistrujeme jej do síťové služby pomocí třídy `Configuration`.
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
Zde vytvoříme instanci `Configuration`, získáme `INetworkService` a přidáme náš vlastní handler do její kolekce. Tím zajistíme, že handler bude spuštěn při každém síťovém požadavku, například při načítání obrázků.

## Krok 5: Načtěte HTML dokument
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

## Krok 6: Převod HTML do PNG
Abychom ukázali širší možnosti Aspose.HTML, převedeme načtený dokument na PNG obrázek. Jedná se o klasický scénář **convert html to png**.
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
`Converter.convertHTML` přijímá `HTMLDocument`, volitelné `ImageSaveOptions` (kde můžete nastavit DPI, kvalitu atd.) a název výstupního souboru. Výsledkem je rastrový obrázek vykresleného HTML.

## Krok 7: Vyčištění zdrojů
Správná správa zdrojů je v každé Java aplikaci zásadní. Uvolníme jak `Configuration`, tak `HTMLDocument`, aby nedocházelo k únikům paměti.
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
Zabalení úklidu do bloku `finally` zaručuje jeho provedení i v případě, že se dříve vyvolá výjimka.

## Proč používat obslužné rutiny zpráv?
Message handlery vám poskytují detailní kontrolu nad síťovými operacemi, jako je **handle broken links java**. Místo tichého selhání knihovny můžete logovat, opakovat požadavky, nahrazovat zdroje nebo poskytovat náhradní obsah – čímž učiníte zpracování HTML robustním a připraveným pro produkci.

## Běžné problémy a řešení
- **Her recursion** – `and naplní se, že voláte invoke(context);` jen jednou, aby nedošlo k nekonečným smyčkám.
- **Chybí licence** – Bez platné licence může být vytvořen obrázek s vodoznakem.
- **Chyby cesty k souboru** – Používejte absolutní cestu nebo správně nastavte pracovní adresář při načítání `document.html`.

## Často kladené otázky

**Otázka: Mohu řetězit více obslužných programů zpráv?**
A: Ano, můžete přidat několik handlerů do kolekce `network.getMessageHandlers()`; budou provedeny v pořadí, v jakém byly přidány.

**Otázka: Funguje obslužný program také pro zdroje CSS nebo skriptů?**
A: Rozhodně – jakýkoli síťový požadavek vytvořený HTML enginem (obrázky, CSS, JS, fonty) projde skrz handler.

**Otázka: Jak změním požadavek HTTP před jeho odesláním?**
A: Implementujte handler, který upraví `context.getRequest()` před voláním `invoke(context)`.

**Otázka: Existuje způsob, jak potlačit varování pro konkrétní adresy URL?**
A: V handleru můžete zkontrolovat `context.getRequest().getRequestUri()` a podmíněně vynechat logování.

**Otázka: Jaká verze Aspose.HTML je pro tato rozhraní API vyžadována?**
A: Kód funguje s Aspose.HTML pro Java 22.10 a novější.

## Závěr
A to je vše – komplexní průvodce **jak používat správu zpráv aspose** v Javě. Pokryli jsme tvorbu HTML souboru, napojení vlastního handleru na **handle broken links java**, načtení dokumentu a provedení **convert html to png**. S tímto přístupem můžete sebejistě zachovat chybějící zdroje, vynucovat vlastní politiku a rozšiřovat síťové Aspose.HTML v jakékoli aplikaci Java.

---

**Poslední aktualizace:** 2025-12-10
**Testováno s:** Aspose.HTML pro Javu 24.11
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}