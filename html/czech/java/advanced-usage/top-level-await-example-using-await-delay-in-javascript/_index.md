---
category: general
date: 2026-03-26
description: Příklad top‑level await ukazující await delay v JavaScriptu, třídu pro
  inkrementaci čítače a veřejná pole třídy v JavaScriptu v živé demonstraci.
draft: false
keywords:
- top level await example
- await delay javascript
- increment counter class
- public class fields javascript
- javascript class public field
language: cs
og_description: Příklad top‑level await, který ukazuje await delay v JavaScriptu,
  třídu pro inkrementaci čítače a veřejná pole třídy v JavaScriptu v stručném tutoriálu.
og_title: příklad top‑level await – Použití await delay v JavaScriptu
tags:
- JavaScript
- ES2022
- async‑await
- classes
title: Příklad top-level await – Použití await delay v JavaScriptu
url: /cs/java/advanced-usage/top-level-await-example-using-await-delay-in-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# top level await example – Použití await delay v JavaScriptu

Už jste se někdy zamýšleli, jak pozastavit provádění modulu, aniž byste museli vše zabalit do async IIFE? Přesně to vám umožní **top level await example**. V tomto tutoriálu projdeme malou webovou stránku, která používá `await delay javascript` k odložení práce, a poté vytvoří `increment counter class`, která využívá **public class fields javascript**. Na konci budete mít kompletní, připravený k zkopírování úryvek, který běží v každém moderním prohlížeči.

Probereme vše od definice třídy s veřejným polem až po zapojení jednoduchého helperu pro zpoždění založeného na promise. Žádné externí knihovny, žádný build krok — jen čisté HTML, `<script type="module">` a nejnovější funkce ECMAScriptu. Pokud už s async funkcemi pracujete, uvidíte, proč se top‑level await cítí jako přirozené rozšíření. Pokud jste noví v syntaxi **javascript class public field**, nebojte se — vysvětlíme, proč je každá řádka tam, kde je.

## Co se naučíte

- Jak **top level await example** funguje uvnitř modulového skriptu.
- Vzor pro helper `await delay javascript`, který napodobuje `setTimeout` pomocí promise.
- Jak napsat **increment counter class**, která používá veřejné pole (`count`) a statický inicializační blok.
- Očekávaný výstup do konzole a jak ověřit, že statický blok se spustí před zbytkem skriptu.
- Tipy pro řešení běžných problémů, například starších prohlížečů, které top‑level await nepodporují.

> **Pro tip:** Moderní prohlížeče (Chrome 106+, Firefox 102+, Edge 106+) již podporují top‑level await. Pokud potřebujete podporovat starší prostředí, zvažte bundlování pomocí nástroje jako Vite nebo Babel.

## Krok 1 – Definujte třídu s veřejným polem a statickým blokem

Prvním kusem našeho demoa je třída, která ukládá číselný čítač. Všimněte si řádky `count = 0;` — to je syntaxe **public class fields javascript** zavedená v ES2022. Vytváří vlastnost instance bez konstruktoru.

```html
<!DOCTYPE html>
<html>
<head>
    <title>ECMAScript 2022 Demo</title>
</head>
<body>
<img src="placeholder.png" alt="top level await example screenshot" title="top level await example">

<script type="module">
    // Step 1: Class definition
    class Counter {
        // Public field holds the current count
        count = 0;

        // Static block runs once when the class is first evaluated
        static {
            console.log('Counter class initialized');
        }

        // Simple method that increments the public field
        increment() {
            this.count++;
        }
    }
```

**Proč statický blok?** Umožňuje nám spustit jednorázovou inicializační logiku (např. logování) v momentě, kdy je modul parsován, *před* tím, než se spustí jakýkoli top‑level await. Tím se zaručí, že zpráva se objeví jako první v konzoli, což dokazuje, že třída byla vyhodnocena brzy.

## Krok 2 – Vytvořte helper `await delay javascript`

Dále potřebujeme malou funkci založenou na promise, která provádí zpoždění. V podstatě jde o obal kolem `setTimeout`, ale vrácení promise ji činí awaitovatelnou.

```javascript
    // Step 2: Promise‑based delay helper
    const delay = ms => new Promise(resolve => setTimeout(resolve, ms));
```

**Hraniční případ:** Pokud je `ms` záporné nebo není číslo, `setTimeout` ho interpretuje jako `0`. Můžete přidat validaci, ale pro demo je jednorázový řádek čitelnější.

## Krok 3 – Použijte top‑level await k pozastavení provádění

Nyní přichází hvězda představení: top‑level await. Protože je náš skript modul (`type="module"`), můžeme umístit `await` přímo do vrchního rozsahu. To pozastaví modul, dokud se promise nevyřeší, a umožní nám řídit pořadí vedlejších efektů.

```javascript
    // Step 3: Top‑level await – delay half a second
    await delay(500);   // Wait 500 ms so the static block logs first
```

**Často kladená otázka:** „Mohu použít top‑level await v normálním `<script>` tagu?“ Ne — pouze modulové skripty to podporují. Pokud zapomenete `type="module"`, získáte syntaktickou chybu.

## Krok 4 – Vytvořte instanci třídy, inkrementujte a zalogujte výsledek

Nakonec všechno spojíme: vytvoříme instanci, zavoláme `increment()` a vypíšeme konečný počet. Tím demonstrujeme **increment counter class** v akci.

```javascript
    // Step 4: Work with the Counter instance
    const counterInstance = new Counter();
    counterInstance.increment();               // count becomes 1
    console.log('Final count:', counterInstance.count);
</script>
</body>
</html>
```

### Očekávaný výstup do konzole

```
Counter class initialized
Final count: 1
```

Pokud stránku otevřete v DevTools, měli byste vidět zprávu ze statického bloku **před** dokončením zpoždění, což potvrzuje, že třída byla vyhodnocena jako první.

## Krok 5 – Proč použít veřejná pole třídy místo konstruktoru?

Možná se ptáte, proč jsme nepsali:

```javascript
class Counter {
    constructor() {
        this.count = 0;
    }
}
```

Oba přístupy fungují, ale **public class fields javascript** vám poskytují čistší, deklarativnější syntaxi. Pole je definováno jednou, ne uvnitř každého volání konstruktoru, což může být přehlednější, když třída roste. Navíc statické bloky nelze umístit do konstruktoru, takže oddělení inicializační logiky je přirozenější.

## Krok 6 – Přizpůsobení příkladu pro reálné aplikace

V produkci často potřebujete více než jeden čítač. Zde je několik rychlých nápadů:

- **Více čítačů:** Uložte je do `Map` s klíčem identifikátoru.
- **Persistovaný stav:** Nahraďte `console.log` zápisy do `localStorage`.
- **Async inicializace:** Použijte statický blok k načtení konfigurace ze serveru před vytvořením jakýchkoli instancí.

Všechny tyto vzory stále těží z top‑level await, protože můžete načíst data jednou při načtení modulu a zajistit, že jsou připravena pro každého spotřebitele.

## Často kladené otázky

**Q: Blokuje top‑level await jiné moduly?**  
A: Ne. Každý modul běží nezávisle. Pouze modul, který obsahuje await, je pozastaven; ostatní moduly se nadále načítají paralelně.

**Q: Co když promise z zpoždění odmítne?**  
A: Nezachycené odmítnutí přeruší vyhodnocení modulu a objeví se jako chyba v konzoli. Zabalte await do `try…catch`, pokud potřebujete elegantní fallback.

**Q: Je klíčové slovo `static` povinné?**  
A: Ne pro samotný čítač, ale statický blok je užitečný způsob, jak demonstrovat, že kód běží *jednou* při načtení — skvělé pro logování nebo detekci funkcí.

## Závěr

Právě jste vytvořili **top level await example**, který představuje `await delay javascript`, **increment counter class** a sílu **public class fields javascript**. Kompletní, spustitelný úryvek najdete výše a výstup do konzole dokazuje, že statický blok se spustí před kódem se zpožděním.

Odtud můžete experimentovat s složitějšími async toky, nahradit zpoždění skutečným API voláním nebo rozšířit třídu o další metody. Pamatujte, moderní JavaScript vám umožňuje zacházet s moduly jako s prvotřídními async entitami — žádné další obaly nejsou potřeba.

Šťastné kódování a klidně sdílejte své variace v komentářích. Pokud se vám tento průvodce hodil, pošlete ho kolegovi, který se stále potýká s async vzory!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}