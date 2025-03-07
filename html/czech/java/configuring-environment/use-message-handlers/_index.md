---
title: Použijte Message Handlers v Aspose.HTML pro Java
linktitle: Použijte Message Handlers v Aspose.HTML pro Java
second_title: Java HTML zpracování s Aspose.HTML
description: Naučte se používat obslužné nástroje zpráv v Aspose.HTML pro Java k efektivnímu zpracování chybějících obrázků a dalších síťových operací.
weight: 12
url: /cs/java/configuring-environment/use-message-handlers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Použijte Message Handlers v Aspose.HTML pro Java

## Zavedení
V tomto tutoriálu vás provedeme praktickým příkladem použití obslužných rutin zpráv v Aspose.HTML pro Java. Připravíme jednoduchý HTML dokument, který bude odkazovat na chybějící obrázek, a předvedeme, jak chybu zachytit a ošetřit pomocí vlastní obslužné rutiny zpráv. Ať už jste v Aspose.HTML noví nebo si chcete rozšířit své dovednosti, tato příručka vám poskytne informace, které potřebujete k efektivní správě síťových operací.
## Předpoklady
Než se ponoříme do podrobného průvodce, ujistěte se, že máte vše, co potřebujete:
1.  Java Development Kit (JDK): Ujistěte se, že máte v systému nainstalovaný JDK. Můžete si jej stáhnout z[Web společnosti Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).
2.  Aspose.HTML for Java: Musíte mít nainstalovaný Aspose.HTML for Java. Můžete si jej stáhnout z[Aspose stránku vydání](https://releases.aspose.com/html/java/).
3. IDE: Použijte své oblíbené Java Integrated Development Environment (IDE), jako je IntelliJ IDEA, Eclipse nebo NetBeans.
4. Základní znalost Javy: Znalost programování v Javě je nezbytná pro efektivní absolvování tohoto návodu.
5.  Dočasná licence: Pokud používáte zkušební verzi Aspose.HTML, zvažte získání a[dočasná licence](https://purchase.aspose.com/temporary-license/) abyste se vyhnuli jakýmkoli omezením během vývoje.

## Importujte balíčky
Než začneme, ujistěte se, že máte do svého projektu Java importovány potřebné balíčky. Níže jsou uvedeny základní importy, které budete potřebovat:
```java
import java.io.IOException;
```
Tyto importy vám poskytnou přístup ke třídám a metodám potřebným pro zpracování síťových operací, vytváření dokumentů HTML a provádění převodu HTML na PNG.

## Krok 1: Připravte HTML kód
První věc, kterou potřebujeme, je jednoduchý HTML kód, který odkazuje na soubor obrázku. Záměrně budeme odkazovat na obrázek, který neexistuje, abychom spustili mechanismus zpracování chyb.
```java
String code = "<img src='missing.jpg'>";
```
 Tento fragment kódu vytvoří prvek HTML, který se pokusí načíst obrázek s názvem`missing.jpg`. Vzhledem k tomu, že tento soubor s obrázkem neexistuje, způsobí během procesu načítání dokumentu chybu.
## Krok 2: Napište HTML kód do souboru
Dále musíme zapsat tento HTML kód do souboru, který můžeme načíst později.
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
 Zde používáme a`FileWriter` zapsat náš HTML kód do souboru s názvem`document.html`. Tento soubor bude použit k vytvoření dokumentu HTML v následujících krocích.
## Krok 3: Vytvořte vlastní obslužnou rutinu zpráv
Nyní vytvoříme vlastní obslužnou rutinu zpráv, která zvládne scénář chybějícího obrázku. Obsluha zprávy zkontroluje stavový kód odpovědi a vytiskne zprávu, pokud soubor není nalezen.
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
 V tomto ovladači je`invoke` metoda kontroluje stavový kód odezvy síťové operace. Pokud stavový kód není 200 (což znamená úspěch), vytiskne zprávu, že soubor nebyl nalezen. The`invoke(context);` line zajistí, že bude zavolán další handler v řetězci.
## Krok 4: Nakonfigurujte síťovou službu
 Abychom mohli používat naši vlastní obslužnou rutinu zpráv, musíme ji přidat do řetězce stávajících obslužných rutin v síťové službě. To se provádí prostřednictvím`Configuration` třída.
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
Zde vytvoříme instanci`Configuration` a získat`INetworkService`. Potom přidáme naši vlastní obslužnou rutinu do seznamu obslužných rutin zpráv. Toto nastavení zajišťuje, že náš handler bude vyvolán během síťových operací.
## Krok 5: Načtěte dokument HTML
S nastavenou konfigurací nyní můžeme načíst náš HTML dokument. Dokument se pokusí načíst chybějící obrázek a spustí naši vlastní obsluhu zpráv.
```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Sem budou probíhat další operace
} finally {
    if (document != null) {
        document.dispose();
    }
}
```
Tento fragment načte dokument HTML pomocí konfigurace, kterou jsme nastavili dříve. Proces načítání dokumentu se pokusí načíst chybějící obrázek a naše obsluha zpráv zachytí a zpracuje výslednou chybu.
## Krok 6: Převeďte HTML na PNG
Abychom to uzavřeli, převedeme dokument HTML na obrázek PNG. Tento krok není nezbytně nutný pro manipulaci s chybějícím obrázkem, ale ukazuje širší funkčnost Aspose.HTML.
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
 Zde používáme`Converter.convertHTML` metoda pro převod dokumentu HTML na soubor PNG. The`ImageSaveOptions`nám umožňuje určit možnosti pro uložení obrázku, jako je rozlišení a formát.
## Krok 7: Vyčistěte zdroje
 Nakonec se vždy ujistěte, že jste vyčistili všechny zdroje použité během procesu. To zahrnuje likvidaci`Configuration` a`HTMLDocument` objektů.
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
Tím zajistíte, že budou uvolněny všechny prostředky, čímž se zabrání únikům paměti a dalším potenciálním problémům ve vaší aplikaci.

## Závěr
A tady to máte – komplexní průvodce používáním obslužných programů zpráv v Aspose.HTML pro Java! Prošli jsme procesem nastavení dokumentu HTML, vytvořením vlastního obslužného programu zpráv a zpracováním chybějících zdrojů jako profesionál. Ať už řešíte chybějící obrázky, nefunkční odkazy nebo jiné problémy související se sítí, tento přístup vám poskytne kontrolu, kterou potřebujete k jejich efektivní správě ve vašich aplikacích Java.

## Nejčastější dotazy
### Co je Aspose.HTML pro Java?
Aspose.HTML for Java je výkonná knihovna, která umožňuje vývojářům vytvářet, manipulovat a převádět HTML dokumenty v aplikacích Java.
### Proč používat obslužné rutiny zpráv v Aspose.HTML pro Javu?
Obslužné programy zpráv vám umožňují zachytit a spravovat síťové operace, jako je zpracování chybějících zdrojů nebo úprava požadavků a odpovědí.
### Mohu použít více obslužných rutin zpráv v jedné konfiguraci?
Ano, můžete zřetězit více obslužných rutin zpráv dohromady a zvládnout různé scénáře během síťových operací.
### Je nutné zlikvidovat objekty Configuration a HTMLDocument?
Ano, likvidace těchto objektů zajišťuje správné uvolnění všech prostředků a zabraňuje úniku paměti.
### Mohu pomocí obslužných programů zpráv zpracovat jiné typy chyb?
Absolutně! Obslužné nástroje zpráv lze přizpůsobit tak, aby zpracovávaly různé typy chyb, nejen chybějící zdroje.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
