---
title: Použít externí CSS na HTML dokumenty v Aspose.HTML pro Java
linktitle: Použít externí CSS na HTML dokumenty v Aspose.HTML pro Java
second_title: Java HTML zpracování s Aspose.HTML
description: Objevte, jak použít externí CSS na HTML dokumenty pomocí Aspose.HTML pro Java! Postupujte podle tohoto podrobného průvodce pro kompletní tutoriál.
type: docs
weight: 12
url: /cs/java/editing-html-documents/apply-external-css-html-documents/
---
## Zavedení
Při práci s dokumenty HTML může použití stylů znamenat zásadní rozdíl v prezentaci a uživatelské zkušenosti. Pokud se noříte do Javy a chcete se naučit, jak aplikovat externí styly CSS na vaše HTML dokumenty pomocí knihovny Aspose.HTML, jste na správném místě! Tato příručka si klade za cíl osvětlit proces krok za krokem a usnadnit ho i těm, kteří mohou být nováčky v Javě nebo CSS.
## Předpoklady
Než se ponoříte do kódu, musíte mít připraveno několik věcí:
### 1. Java Development Kit (JDK)
 Ujistěte se, že máte na svém počítači nainstalovaný JDK. Nejnovější verzi si můžete stáhnout z[Web společnosti Oracle Java](https://www.oracle.com/java/technologies/javase-downloads.html).
### 2. Aspose.HTML pro Java
Budete muset mít nastaven Aspose.HTML pro Java. Pokud jste to ještě neudělali, zamiřte na[Aspose stránku stahování](https://releases.aspose.com/html/java/) a vezměte si knihovnu.
### 3. IDE nebo textový editor
Vyberte si integrované vývojové prostředí (IDE), jako je IntelliJ IDEA, Eclipse, nebo dokonce jednoduchý textový editor pro psaní kódu Java.
### 4. Základní znalost Javy
Znalost programování v Javě a základy CSS vám jistě pomohou pohodlněji sledovat.
## Importujte balíčky
Jakmile máte vše nastaveno, dalším krokem je import potřebných balíčků do vašeho projektu Java. Zde je to, co potřebujete:
```java
import com.aspose.html.HTMLDocument;
```
Tyto importy vám umožní manipulovat s dokumenty HTML a vykreslovat je do různých formátů, jako je PDF.

Náš tutoriál rozdělíme do zvládnutelných kroků. Každý krok vás provede procesem aplikace externích stylů CSS na dokument HTML pomocí Aspose.HTML for Java.
## Krok 1: Vytvořte dokument HTML
Nejprve musíme vytvořit náš HTML dokument. Začneme definováním obsahu pomocí jednoduché struktury HTML.
```java
String content = "<div><p>Internal CSS</p><p>An internal CSS is used to define a style for a single HTML page</p></div>";
HTMLDocument document = new HTMLDocument(content, ".");
```

 Zde jsme definovali základní strukturu HTML, včetně a`<div>` se dvěma odstavci. The`HTMLDocument` třída se používá k vytvoření reprezentace dokumentu našeho obsahu HTML.
## Krok 2: Vytvořte prvek stylu
 Dále vytvoříme a`style` prvek, který bude dodržovat naše pravidla CSS.
```java
Element style = document.createElement("style");
style.setTextContent(".frame1 { margin-top:50px; margin-left:50px; padding:20px; width:360px; height:90px; background-color:#a52a2a; font-family:verdana; color:#FFF5EE;} \n" +
        ".frame2 { margin-top:-90px; margin-left:160px; text-align:center; padding:20px; width:360px; height:100px; background-color:#ADD8E6;}");
```

 Pomocí`createElement` způsob`HTMLDocument` , vytvoříme nový`<style>` element a nastavte jeho obsah tak, aby zahrnoval naše definice CSS pro dvě třídy:`frame1` a`frame2`. Tyto třídy definují okraje, odsazení, rozměry, barvy pozadí, rodiny písem a barvy textu.
## Krok 3: Přidejte styl do záhlaví dokumentu
Nyní, když máme naše CSS na místě, musíme přidat náš prvek stylu do hlavy dokumentu.
```java
Element head = document.getElementsByTagName("head").get_Item(0);
head.appendChild(style);
```

 Načteme hlavu dokumentu a připojíme náš nově vytvořený`style` živel. Tato akce efektivně integruje naše CSS do dokumentu HTML, což mu umožňuje stylizovat náš obsah HTML.
## Krok 4: Aplikujte třídy na prvky HTML
Dále použijeme dříve definované třídy CSS na naše prvky odstavce.
```java
HTMLElement paragraph = (HTMLElement) document.getElementsByTagName("p").get_Item(0);
paragraph.setClassName("frame1");
HTMLElement lastParagraph = (HTMLElement) document.getElementsByTagName("p").get_Item(document.getElementsByTagName("p").getLength() - 1);
lastParagraph.setClassName("frame2");
```

Zde přistupujeme k prvním a posledním prvkům odstavce v dokumentu a přiřadíme jim třídy CSS, které jsme vytvořili. Toto přiřazení zajišťuje, že dodržují styly definované v našem CSS.
## Krok 5: Nastavte další vlastnosti stylu
Pro další vylepšení vzhledu nastavíme pro naše odstavce další vlastnosti stylu.
```java
paragraph.getStyle().setFontSize("250%");
paragraph.getStyle().setTextAlign("center");
lastParagraph.getStyle().setColor("#434343");
lastParagraph.getStyle().setFontSize("150%");
lastParagraph.getStyle().setFontFamily("verdana");
```

V tomto kroku dolaďujeme naše styly. Velikost písma prvního odstavce se zvětší a vycentruje, zatímco barva, velikost písma a rodina písem posledního odstavce jsou definovány. Toto vylepšení je zásadní pro čitelnost a estetickou přitažlivost.
## Krok 6: Uložte dokument HTML
Jakmile použijeme naše styly, je čas uložit HTML dokument.
```java
document.save("edit-internal-css.html");
```

 Zde využíváme`save` metoda`HTMLDocument` třídy zapsat upravený obsah HTML do souboru, a tím zachovat naše styly a změny.
## Krok 7: Přeneste dokument do formátu PDF
Nakonec vykreslíme dokument do formátu PDF pro výstup.
```java
PdfDevice device = new PdfDevice("edit-internal-css.pdf");
document.renderTo(device);
```

 Pomocí`PdfDevice` třídy, nastavíme vykreslování našeho HTML dokumentu do PDF. Tento krok je klíčový, chcete-li sdílet stylizovaný dokument v univerzálně přístupném formátu.
## Závěr
A tady to máte – použití externích CSS na HTML dokumenty pomocí Aspose.HTML pro Java je jednoduché a přínosné! Pomocí několika řádků kódu můžete proměnit prostý text na vizuálně přitažlivé dokumenty s profesionálním stylem. Ať už tedy navrhujete pro osobní použití, vytváříte sestavy nebo vyvíjíte webový obsah, pochopení toho, jak manipulovat s HTML a CSS v Javě, je mocná dovednost, kterou musíte mít ve své sadě nástrojů.
## FAQ
### Co je Aspose.HTML pro Java?
Aspose.HTML for Java je výkonná knihovna, která umožňuje vývojářům pracovat s dokumenty HTML v aplikacích Java a poskytuje širokou škálu funkcí, od manipulace s HTML po vykreslování.
### Potřebuji k použití Aspose.HTML připojení k internetu?
Ne, jakmile si stáhnete potřebné soubory knihovny, můžete Aspose.HTML používat offline.
### Mohu na dokument HTML použít více souborů CSS?
 Ano, můžete vytvořit více`<link>` prvky a připojit je k hlavičce dokumentu pro různé soubory CSS.
### Existuje rozdíl mezi interním a externím CSS?
Ano! Interní CSS je definováno v dokumentu HTML, zatímco externí CSS je umístěno v samostatném souboru a propojeno s dokumentem.
### Jak mohu získat podporu pro Aspose.HTML pro Java?
 Můžete získat přístup k podpoře komunity prostřednictvím[Aspose fórum](https://forum.aspose.com/c/html/29) pro jakékoli dotazy nebo problémy, se kterými se můžete setkat.