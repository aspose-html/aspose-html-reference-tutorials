---
title: DOM Mutation Observer s Aspose.HTML pro Javu
linktitle: DOM Mutation Observer - Pozorování přidání uzlů
second_title: Java HTML zpracování s Aspose.HTML
description: V tomto podrobném průvodci se dozvíte, jak používat Aspose.HTML pro Java k implementaci DOM Mutation Observer. Efektivně monitorujte změny DOM a reagujte na ně.
weight: 11
url: /cs/java/advanced-usage/dom-mutation-observer-observing-node-additions/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# DOM Mutation Observer s Aspose.HTML pro Javu


Jste vývojář Java a chcete pozorovat a reagovat na změny v objektovém modelu dokumentu (DOM) dokumentu HTML? Aspose.HTML for Java poskytuje výkonné řešení pro tento úkol. V tomto podrobném průvodci prozkoumáme, jak používat Aspose.HTML pro Java k vytvoření dokumentu HTML a pozorovat přidání uzlů pomocí Mutation Observer. Tento tutoriál vás provede celým procesem a rozdělí každý příklad do několika kroků. Na konci budete schopni snadno implementovat DOM Mutation Observers ve svých projektech Java.

## Předpoklady

Než se pustíme do používání Aspose.HTML pro Java, ujistěte se, že máte připravené nezbytné předpoklady:

1. Vývojové prostředí Java: Ujistěte se, že máte v systému nainstalovanou sadu Java Development Kit (JDK).

2.  Aspose.HTML for Java: Budete si muset stáhnout a nainstalovat Aspose.HTML for Java. Odkaz ke stažení najdete[zde](https://releases.aspose.com/html/java/).

3. IDE (Integrated Development Environment): Pro psaní a spouštění kódu Java použijte preferované Java IDE, jako je IntelliJ IDEA nebo Eclipse.

## Importujte balíčky

Chcete-li začít s Aspose.HTML for Java, musíte importovat požadované balíčky do kódu Java. Můžete to udělat takto:

```java
// Importujte potřebné balíčky
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.mutations.MutationObserver;
import com.aspose.html.dom.mutations.MutationCallback;
import com.aspose.html.dom.mutations.MutationRecord;
import com.aspose.html.dom.mutations.MutationObserverInit;
import com.aspose.html.dom.Element;
import com.aspose.html.dom.Text;
import com.aspose.html.generic.IGenericList;

// Vytvořte prázdný dokument HTML
HTMLDocument document = new HTMLDocument();
```

Nyní, když jste importovali požadované balíčky, přejděme k podrobnému průvodci implementací DOM Mutation Observer v Javě.

## Krok 1: Vytvořte instanci Mutation Observer

Nejprve musíte vytvořit instanci Mutation Observer. Tento pozorovatel bude sledovat změny v DOM a spustí funkci zpětného volání, když dojde k mutacím.

```java
MutationObserver observer = new MutationObserver(new MutationCallback() {
    @Override
    public void invoke(IGenericList<MutationRecord> mutations, MutationObserver mutationObserver) {
        mutations.forEach(mutationRecord -> {
            mutationRecord.getAddedNodes().forEach(node -> {
                synchronized (this) {
                    System.out.println("The '" + node + "' node was added to the document.");
                    notifyAll();
                }
            });
        });
    }
});
```

V tomto kroku vytvoříme pozorovatele s funkcí zpětného volání, která vytiskne zprávu, když jsou do DOM přidány uzly.

## Krok 2: Nakonfigurujte Observer

Nyní nakonfigurujme pozorovatele s požadovanými možnostmi. Chceme pozorovat změny seznamu potomků a změny podstromu, stejně jako změny dat znaků.

```java
MutationObserverInit config = new MutationObserverInit();
config.setChildList(true);
config.setSubtree(true);
config.setCharacterData(true);

// Předejte cílový uzel, abyste mohli pozorovat se zadanou konfigurací
observer.observe(document.getBody(), config);
```

 Zde nastavíme`config` objekt pro umožnění sledování změn podřízených seznamů, podstromů a znakových dat. Poté předáme do cílového uzlu (v tomto případě dokumentu`<body>`) a konfiguraci pro pozorovatele.

## Krok 3: Upravte DOM

Nyní provedeme nějaké změny v DOM, abychom spustili pozorovatele. Vytvoříme prvek odstavce a připojíme jej k tělu dokumentu.

```java
// Vytvořte prvek odstavce a připojte jej k tělu dokumentu
Element p = document.createElement("p");
document.getBody().appendChild(p);

// Vytvořte text a připojte jej k odstavci
Text text = document.createTextNode("Hello World");
p.appendChild(text);
```

V tomto kroku vytvoříme element odstavce HTML a přidáme jej do těla dokumentu. Poté vytvoříme textový uzel s obsahem „Hello World“ a připojíme jej k odstavci.

## Krok 4: Počkejte na pozorování (asynchronně)

Protože jsou mutace pozorovány asynchronně, musíme chvíli počkat, abychom umožnili pozorovateli zachytit změny. Využijeme`synchronized` a`wait` pro tento účel, jak je uvedeno níže.

```java
// Protože mutace fungují v asynchronním režimu, počkejte několik sekund
synchronized (this) {
    wait(5000);
}
```

Zde počkáme 5 sekund, abychom zajistili, že pozorovatel má šanci zachytit případné mutace.

## Krok 5: Zastavte pozorování

Nakonec, když skončíte s pozorováním, je nezbytné odpojit pozorovatele, aby se uvolnily zdroje.

```java
// Přestaňte pozorovat
observer.disconnect();
```

Tímto krokem jste dokončili pozorování a můžete vyčistit zdroje.

## Závěr

V tomto tutoriálu jsme prošli procesem použití Aspose.HTML pro Java k implementaci DOM Mutation Observer. Naučili jste se, jak vytvořit pozorovatele, nakonfigurovat jej, provádět změny v DOM, čekat na pozorování a přestat pozorovat. Nyní máte dovednosti používat DOM Mutation Observers ve svých projektech Java, abyste mohli efektivně sledovat změny v DOM dokumentů HTML a reagovat na ně.

Pokud máte nějaké dotazy nebo narazíte na problémy, neváhejte vyhledat pomoc v[Fórum Aspose.HTML](https://forum.aspose.com/) . Kromě toho můžete přistupovat k[dokumentace](https://reference.aspose.com/html/java/) pro podrobné informace o Aspose.HTML pro Java.

## FAQ

### Q1: Co je to DOM Mutation Observer?

A1: DOM Mutation Observer je funkce JavaScriptu, která vám umožňuje sledovat změny v modelu DOM (Document Object Model) dokumentu HTML. Poskytuje způsob, jak reagovat na přidání, odstranění nebo úpravy uzlů DOM v reálném čase.

### Q2: Mohu použít Aspose.HTML pro Java ve svých komerčních projektech?

 A2: Ano, můžete použít Aspose.HTML pro Java v komerčních projektech. Můžete najít informace o licencích a nákupu[zde](https://purchase.aspose.com/buy).

### Q3: Je k dispozici bezplatná zkušební verze pro Aspose.HTML pro Java?

 A3: Ano, můžete získat bezplatnou zkušební verzi Aspose.HTML pro Java[zde](https://releases.aspose.com/). To vám umožní prozkoumat jeho funkce a možnosti před nákupem.

### Q4: Jaká je výhoda pozorování změn znakových dat pomocí Mutation Observer?

Odpověď 4: Sledování změn znakových dat je užitečné pro scénáře, kde chcete sledovat změny v obsahu textu prvků HTML a reagovat na ně. Můžete jej například použít ke sledování vstupu uživatele ve webových formulářích a odpovídání na něj.

### Q5: Jak mohu nakládat se zdroji při použití Aspose.HTML pro Java?

 A5: Je důležité uvolnit zdroje, až budete hotovi. V našem příkladu jsme použili`document.dispose()` k vyčištění prostředků spojených s dokumentem HTML. Ujistěte se, že jste zlikvidovali všechny objekty a prostředky, které vytvoříte, abyste předešli úniku paměti.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
