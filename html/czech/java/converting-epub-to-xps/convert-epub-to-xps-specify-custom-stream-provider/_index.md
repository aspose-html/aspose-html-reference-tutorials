---
date: 2026-01-07
description: Jednoduše převádějte EPUB na XPS pomocí Aspose.HTML pro Javu. Postupujte
  podle tohoto krok‑za‑krokem průvodce pro bezproblémový proces konverze.
linktitle: How to Convert EPUB to XPS with a Custom Stream Provider
second_title: Java HTML Processing with Aspose.HTML
title: Jak převést EPUB na XPS pomocí vlastního poskytovatele streamu
url: /cs/java/converting-epub-to-xps/convert-epub-to-xps-specify-custom-stream-provider/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod EPUB na XPS s vlastním poskytovatelem proudu

V dnešním světě digitálního publikování je **convert EPUB to XPS** běžnou požadavkem — ať už potřebujete fixní rozložení pro tisk, archivaci nebo sdílení mezi zařízeními Windows. Aspose.HTML pro Java usnadňuje tento převod a použitím vlastního poskytovatele paměťových proudů udržujete celý proces v paměti, což je ideální pro cloudové nebo vysoce výkonné scénáře. Níže najdete vše, co potřebujete k zahájení, od předpokladů po kompletní spustitelný příklad.

## Rychlé odpovědi
- **Co převod produkuje?** XPS dokument, který zachovává rozložení a písma.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro testování; pro produkci je vyžadována komerční licence.  
- **Mohu to spustit v kontejneru?** Ano — není potřeba zapisovat na souborový systém, pokud vše držíte v paměti.  
- **Která verze Javy je podporována?** Java 8 nebo vyšší.  
- **Je vlastní poskytovatel proudu povinný?** Ne, ale poskytuje úplnou kontrolu nad využitím paměti a zpracováním výstupu.

## Co je „convert EPUB to XPS“?
Převod souboru EPUB na XPS transformuje reflowable formát e‑knihy do fixního rozložení, nezávislého na zařízení. XPS (XML Paper Specification) je Microsoftová alternativa k PDF, ideální pro scénáře, kde potřebujete věrnou vizuální reprezentaci, která se napříč platformami nemění.

## Proč použít vlastní poskytovatel proudu?
Vlastní `MemoryStreamProvider` vám umožní uchovat výsledek převodu v RAM místo zápisu do dočasného souboru na disku. Tento přístup:
- Snižuje režii I/O.
- Zlepšuje výkon v serverless nebo mikro‑servisních architekturách.
- Poskytuje flexibilitu streamovat výsledek přímo klientovi, cloudovému úložišti nebo jinému API.

## Předpoklady

Pro úspěšný **convert EPUB to XPS** se ujistěte, že máte následující předpoklady:

### 1. Knihovna Aspose.HTML pro Java  

Musíte mít nainstalovanou a nakonfigurovanou knihovnu Aspose.HTML pro Java ve vašem Java prostředí. Pokud ji ještě nemáte, můžete si ji stáhnout z [download link](https://releases.aspose.com/html/java/).

### 2. Vstupní soubor EPUB  

Potřebujete existující soubor EPUB, který chcete převést na XPS. Ujistěte se, že máte tento soubor připravený pro proces převodu.

Nyní, když máte všechny předpoklady, projděme krok za krokem převod.

## Import balíčků

Před začátkem se ujistěte, že importujete potřebné balíčky pro Aspose.HTML pro Java, aby bylo možné využívat jeho funkce.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.XpsSaveOptions;
import com.aspose.html.saving.MemoryStreamProvider;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
```

## Otevření souboru EPUB

Nejprve musíte otevřít existující soubor EPUB pro čtení. V tomto kroku používáme `FileInputStream` pro přístup k souboru EPUB.

```java
try (FileInputStream fileInputStream = new FileInputStream("path/to/your/input.epub")) {
    // Your code for Step 1
}
```

## Vytvoření MemoryStreamProvider

Dále vytvořte instanci `MemoryStreamProvider`. Tento objekt bude uchovávat výstup převodu v paměti.

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
    // Your code for Step 2
}
```

## Převod EPUB na XPS

Nyní převádějte soubor EPUB na XPS pomocí metody `Converter.convertEPUB`. `MemoryStreamProvider` poskytuje cílový proud.

```java
Converter.convertEPUB(
    fileInputStream,
    new XpsSaveOptions(),
    streamProvider.getStream().findFirst().get()
);
```

## Získání výsledných dat

Po dokončení převodu načtěte paměťový proud, který obsahuje data XPS.

```java
InputStream inputStream = streamProvider.getStream().findFirst().get();
```

## Uložení výstupu (volitelné)

Pokud potřebujete fyzický soubor — například pro ladění nebo offline kontrolu — zapište paměťový proud na disk. Ve většině produkčních scénářů můžete tento krok přeskočit a streamovat data přímo klientovi.

```java
try (FileOutputStream fileOutputStream = new FileOutputStream("path/to/your/output.xps")) {
    byte[] buffer = new byte[inputStream.available()];
    inputStream.read(buffer);
    fileOutputStream.write(buffer);
}
```

## Kompletní zdrojový kód

Níže je kompletní, připravený k spuštění příklad, který spojuje všechny části. Klidně jej zkopírujte, vložte a přizpůsobte svému projektu.

```java
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of MemoryStreamProvider
            try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
                // Convert EPUB to XPS by using the MemoryStreamProvider
                com.aspose.html.converters.Converter.convertEPUB(
                        fileInputStream,
                        new com.aspose.html.saving.XpsSaveOptions(),
                        streamProvider.lStream
                );
                // Get access to the memory stream that contains the resulted data
                java.io.InputStream inputStream = streamProvider.lStream.stream().findFirst().get();
                // Flush the result data to the output file
                try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("output.xps"))) {
                    byte[] buffer = new byte[inputStream.available()];
                    inputStream.read(buffer);
                    fileOutputStream.write(buffer);
                }
            }
        }
```

## Časté problémy a řešení

| Problém | Proč se vyskytuje | Oprava |
|---------|-------------------|--------|
| **`java.lang.OutOfMemoryError`** | Velké soubory EPUB mohou překročit výchozí velikost haldy, když jsou celé v paměti. | Zvyšte haldu JVM (`-Xmx`) nebo pokud je to možné, zpracovávejte EPUB po částech. |
| **Missing fonts in XPS** | Písma, která nejsou vložena do EPUB, nejsou na převodní stroji k dispozici. | Ujistěte se, že požadovaná písma jsou nainstalována na serveru nebo je vložte do EPUB. |
| **`UnsupportedOperationException` from `MemoryStreamProvider`** | Použití zastaralé verze Aspose.HTML. | Aktualizujte na nejnovější verzi Aspose.HTML pro Java. |

## Často kladené otázky

### 1. Co je EPUB?

EPUB, zkratka pro Electronic Publication, je široce používaný souborový formát pro e‑knihy. Je navržen tak, aby byl snadno čitelný na různých zařízeních, jako jsou e‑čtečky, tablety a chytré telefony.

### 2. Co je XPS?

XPS znamená XML Paper Specification, dokumentový formát vytvořený společností Microsoft. Používá se pro sdílení a archivaci dokumentů s konzistentním vzhledem a rozložením.

### 3. Proč použít Aspose.HTML pro Java?

Aspose.HTML pro Java je výkonná knihovna, která zjednodušuje manipulaci s dokumenty, jejich převod a vykreslování. Poskytuje rozsáhlé funkce a podporu různých formátů dokumentů, což z ní činí cenný nástroj pro vývojáře.

### 4. Mohu převádět jiné formáty dokumentů pomocí Aspose.HTML pro Java?

Ano, Aspose.HTML pro Java podporuje převod různých formátů dokumentů, včetně HTML, EPUB, XPS a dalších. Je to univerzální nástroj pro správu dokumentů.

### 5. Kde najdu další zdroje a podporu?

Pro dokumentaci a podporu navštivte [Aspose.HTML for Java documentation](https://reference.aspose.com/html/java/) a [support forum](https://forum.aspose.com/).

**Poslední aktualizace:** 2026-01-07  
**Testováno s:** Aspose.HTML for Java 24.12 (nejnovější v době psaní)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}