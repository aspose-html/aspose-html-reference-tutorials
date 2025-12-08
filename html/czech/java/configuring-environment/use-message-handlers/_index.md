---
date: 2025-12-08
description: Naučte se, jak převést HTML na PNG pomocí Aspose.HTML pro Javu, přičemž
  budete zpracovávat nefunkční odkazy a zachytávat chybějící zdroje pomocí vlastních
  zpracovatelů zpráv.
language: cs
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Jak převést HTML na PNG a použít zpracovatele zpráv v Aspose.HTML pro Javu
url: /java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod HTML na PNG pomocí Aspose.HTML pro Java – Použití zpracovatelů zpráv

## Úvod  
V tomto tutoriálu se naučíte **jak převést HTML na PNG** pomocí Aspose.HTML pro Java a zároveň **zpracovávat nefunkční odkazy** nebo chybějící zdroje pomocí vlastního zpracovatele zpráv. Provedeme vás vytvořením jednoduchého souboru HTML, jeho zápisem na disk, načtením a zachycením jakýchkoli síťových chyb – ideální pro vývojáře, kteří potřebují spolehlivý **převod HTML na obrázek** v produkčních Java aplikacích.

## Rychlé odpovědi
- **Co tutoriál pokrývá?** Převod HTML na PNG a zpracování chybějících zdrojů pomocí zpracovatele zpráv.  
- **Která knihovna je použita?** Aspose.HTML pro Java.  
- **Potřebuji licenci?** Doporučuje se dočasná licence pro zkušební sestavy.  
- **Mohu soubor HTML vytvořit z Javy?** Ano – viz krok „write html file java“.  
- **Zachytí zpracovatel nefunkční odkazy?** Rozhodně; zaznamená jakékoli odpovědi jiné než 200.

## Co je zpracovatel zpráv v Aspose.HTML?  
Zpracovatel zpráv je háček do síťového zásobníku, který vám umožní **zachytit chybějící zdroje** (např. nefunkční URL obrázku) dříve, než vyvolají výjimku. Inspekcí stavového kódu odpovědi můžete zaznamenat, nahradit nebo znovu požádat – získáte tak plnou kontrolu nad síťovými operacemi.

## Proč převádět HTML na PNG?  
Převod HTML na obrázek je užitečný pro generování miniatur, náhledů e‑mailů nebo snímků podobných PDF, když nepotřebujete kompletní převod do PDF. Aspose.HTML poskytuje rychlý server‑side **html to image conversion** engine, který funguje bez prohlížeče.

## Požadavky
1. **Java Development Kit (JDK)** – stáhněte z [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – získejte nejnovější JAR soubory ze [Aspose releases page](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse nebo NetBeans.  
4. **Základní znalost Javy** – měli byste být obeznámeni s try‑with‑resources a uvolňováním objektů.  
5. **Dočasná licence** (volitelně) – vyhněte se omezením zkušební verze pomocí [temporary license](https://purchase.aspose.com/temporary-license/).

## Import balíčků
Před začátkem importujte požadované třídy Java:

```java
import java.io.IOException;
```

Tyto importy nám poskytují přístup k souborovému I/O a síťovým API Aspose.HTML.

## Krok 1: Zapsat soubor HTML (write html file java)  
Nejprve vytvořte malý úryvek HTML, který odkazuje na obrázek, který **neexistuje**. To nám umožní otestovat zpracovatel.

```java
String code = "<img src='missing.jpg'>";
```

## Krok 2: Uložit HTML na disk  
Uložte úryvek do souboru s názvem `document.html`. Tento soubor bude později načten pomocí engine Aspose.HTML.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Krok 3: Vytvořit vlastní zpracovatel zpráv (catch missing resource)  
Nyní definujeme zpracovatel, který kontroluje HTTP stavový kód. Pokud není `200`, zaznamenáme přátelskou zprávu.

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

## Krok 4: Zaregistrovat zpracovatel do síťové služby  
Přidejte vlastní zpracovatel do síťové služby Aspose.HTML, aby se podílel na každém požadavku.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Krok 5: Načíst HTML dokument (load html document java)  
S připravenou konfigurací načtěte soubor HTML. Chybějící obrázek spustí zpracovatel, který jsme právě přidali.

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

## Krok 6: Převést HTML na PNG (convert html to png)  
Nakonec převěďte načtený dokument na PNG obrázek. Toto demonstruje celý workflow **html to image conversion**.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Krok 7: Vyčistit zdroje  
Vždy uvolněte objekt `Configuration`, aby se uvolnily nativní zdroje a předešlo se únikům paměti.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Časté úskalí a tipy
- **Rekurzivní volání invoke:** Vlastní zpracovatel musí volat `invoke(context);` *po* vaší logice, aby pokračoval v řetězci. Zapomenutí může zastavit ostatní zpracovatele.  
- **Varování o chybějící licenci:** Bez platné licence může převod přidat vodoznak nebo omezit velikost výstupu.  
- **Problémy s cestou:** Ujistěte se, že `document.html` je zapsán do pracovního adresáře nebo poskytněte absolutní cestu.

## Často kladené otázky

**Q: Co je Aspose.HTML pro Java?**  
A: Jedná se o robustní knihovnu, která umožňuje vývojářům Javy vytvářet, manipulovat a převádět HTML dokumenty bez prohlížeče.

**Q: Proč používat zpracovatele zpráv v Aspose.HTML pro Java?**  
A: Umožňují vám **zpracovávat nefunkční odkazy**, zaznamenávat chybějící zdroje nebo za běhu upravovat požadavky/odpovědi.

**Q: Mohu řetězit více zpracovatelů zpráv?**  
A: Ano – přidejte každý zpracovatel do seznamu `network.getMessageHandlers()`; budou se vykonávat v pořadí přidání.

**Q: Je nutné uvolňovat objekty Configuration a HTMLDocument?**  
A: Rozhodně; uvolnění uvolní nativní paměť a zabrání únikům v dlouho běžících aplikacích.

**Q: Kromě chybějících obrázků, jaké další chyby mohou zpracovatelé zvládnout?**  
A: Jakýkoli HTTP odpověď jiná než 200 – timeouty, 404 stránky, selhání autentizace atd. – lze zachytit a zpracovat.

## Závěr  
Nyní máte kompletní, připravený pro produkci příklad **převodu HTML na PNG**, který **zpracovává nefunkční odkazy** a **zachytává chybějící zdroje** pomocí Aspose.HTML pro Java. Začleňte tento vzor do větších projektů, abyste získali jemnou kontrolu nad síťovými operacemi a generovali spolehlivé snímky vašich HTML obsahů.

---

**Last Updated:** 2025-12-08  
**Tested With:** Aspose.HTML for Java 24.12 (latest)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}