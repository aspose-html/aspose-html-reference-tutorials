---
title: DOM Mutation Observer z Aspose.HTML dla Java
linktitle: DOM Mutation Observer - Obserwowanie dodatków węzłów
second_title: Przetwarzanie HTML w Javie za pomocą Aspose.HTML
description: Dowiedz się, jak używać Aspose.HTML dla Java do implementacji DOM Mutation Observer w tym przewodniku krok po kroku. Monitoruj i reaguj na zmiany DOM skutecznie.
weight: 11
url: /pl/java/advanced-usage/dom-mutation-observer-observing-node-additions/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# DOM Mutation Observer z Aspose.HTML dla Java


Czy jesteś programistą Java, który chce obserwować i reagować na zmiany w Document Object Model (DOM) dokumentu HTML? Aspose.HTML for Java zapewnia potężne rozwiązanie tego zadania. W tym przewodniku krok po kroku pokażemy, jak używać Aspose.HTML for Java do tworzenia dokumentu HTML i obserwowania dodawania węzłów za pomocą Mutation Observer. Ten samouczek przeprowadzi Cię przez proces, dzieląc każdy przykład na wiele kroków. Na koniec będziesz w stanie z łatwością zaimplementować DOM Mutation Observers w swoich projektach Java.

## Wymagania wstępne

Zanim przejdziemy do szczegółów dotyczących używania Aspose.HTML w Javie, upewnijmy się, że spełnione są niezbędne wymagania wstępne:

1. Środowisko programistyczne Java: Upewnij się, że w systemie zainstalowany jest Java Development Kit (JDK).

2.  Aspose.HTML dla Java: Musisz pobrać i zainstalować Aspose.HTML dla Java. Link do pobrania znajdziesz[Tutaj](https://releases.aspose.com/html/java/).

3. IDE (zintegrowane środowisko programistyczne): do pisania i uruchamiania kodu Java użyj preferowanego środowiska IDE Java, takiego jak IntelliJ IDEA lub Eclipse.

## Importuj pakiety

Aby rozpocząć pracę z Aspose.HTML dla Javy, musisz zaimportować wymagane pakiety do swojego kodu Java. Oto, jak możesz to zrobić:

```java
// Importuj niezbędne pakiety
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.mutations.MutationObserver;
import com.aspose.html.dom.mutations.MutationCallback;
import com.aspose.html.dom.mutations.MutationRecord;
import com.aspose.html.dom.mutations.MutationObserverInit;
import com.aspose.html.dom.Element;
import com.aspose.html.dom.Text;
import com.aspose.html.generic.IGenericList;

// Utwórz pusty dokument HTML
HTMLDocument document = new HTMLDocument();
```

Teraz, gdy zaimportowałeś wymagane pakiety, możemy przejść do przewodnika krok po kroku, który pokaże Ci, jak wdrożyć obserwatora mutacji DOM w Javie.

## Krok 1: Utwórz instancję obserwatora mutacji

Najpierw musisz utworzyć instancję Mutation Observer. Ten obserwator będzie obserwował zmiany w DOM i wykonywał funkcję wywołania zwrotnego, gdy wystąpią mutacje.

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

W tym kroku tworzymy obserwatora z funkcją wywołania zwrotnego, która drukuje komunikat w momencie dodania węzłów do DOM.

## Krok 2: Skonfiguruj Obserwatora

Teraz skonfigurujmy obserwatora z pożądanymi opcjami. Chcemy obserwować zmiany listy dzieci i zmiany poddrzewa, a także zmiany danych znaków.

```java
MutationObserverInit config = new MutationObserverInit();
config.setChildList(true);
config.setSubtree(true);
config.setCharacterData(true);

// Przekaż węzeł docelowy do obserwacji z określoną konfiguracją
observer.observe(document.getBody(), config);
```

 Tutaj ustawiamy`config` obiekt umożliwiający obserwację zmian listy dzieci, poddrzewa i danych znaków. Następnie przekazujemy węzeł docelowy (w tym przypadku dokument`<body>`) i konfigurację obserwatorowi.

## Krok 3: Modyfikuj DOM

Teraz wprowadzimy kilka zmian w DOM, aby uruchomić obserwatora. Utworzymy element akapitu i dodamy go do treści dokumentu.

```java
// Utwórz element akapitu i dołącz go do treści dokumentu
Element p = document.createElement("p");
document.getBody().appendChild(p);

// Utwórz tekst i dołącz go do akapitu
Text text = document.createTextNode("Hello World");
p.appendChild(text);
```

W tym kroku tworzymy element akapitu HTML i dodajemy go do treści dokumentu. Następnie tworzymy węzeł tekstowy z treścią „Hello World” i dołączamy go do akapitu.

## Krok 4: Czekaj na obserwacje (asynchronicznie)

Ponieważ mutacje są obserwowane asynchronicznie, musimy odczekać chwilę, aby umożliwić obserwatorowi uchwycenie zmian. Użyjemy`synchronized` I`wait` w tym celu, jak pokazano poniżej.

```java
// Ponieważ mutacje działają w trybie asynchronicznym, odczekaj kilka sekund
synchronized (this) {
    wait(5000);
}
```

Tutaj czekamy 5 sekund, aby mieć pewność, że obserwator będzie miał szansę wychwycić wszelkie mutacje.

## Krok 5: Przestań obserwować

Na koniec, po zakończeniu obserwacji, należy koniecznie odłączyć obserwatora i zwolnić zasoby.

```java
// Przestań obserwować
observer.disconnect();
```

Ten krok kończy obserwację i pozwala na oczyszczenie zasobów.

## Wniosek

W tym samouczku przeprowadziliśmy proces korzystania z Aspose.HTML dla Java w celu zaimplementowania DOM Mutation Observer. Nauczyłeś się, jak utworzyć obserwatora, skonfigurować go, wprowadzić zmiany w DOM, czekać na obserwacje i zatrzymać obserwację. Teraz masz umiejętności, aby zastosować DOM Mutation Observers w swoich projektach Java w celu monitorowania i reagowania na zmiany w DOM dokumentów HTML.

Jeśli masz jakiekolwiek pytania lub napotkasz problemy, nie wahaj się szukać pomocy w[Forum Aspose.HTML](https://forum.aspose.com/) Dodatkowo możesz uzyskać dostęp do[dokumentacja](https://reference.aspose.com/html/java/) aby uzyskać szczegółowe informacje na temat Aspose.HTML dla Java.

## Najczęściej zadawane pytania

### P1: Czym jest obserwator mutacji DOM?

A1: DOM Mutation Observer to funkcja JavaScript, która umożliwia obserwowanie zmian w Document Object Model (DOM) dokumentu HTML. Zapewnia sposób reagowania na dodawanie, usuwanie lub modyfikowanie węzłów DOM w czasie rzeczywistym.

### P2: Czy mogę używać Aspose.HTML for Java w moich projektach komercyjnych?

 A2: Tak, możesz używać Aspose.HTML dla Java w projektach komercyjnych. Informacje o licencjonowaniu i zakupie można znaleźć[Tutaj](https://purchase.aspose.com/buy).

### P3: Czy jest dostępna bezpłatna wersja próbna Aspose.HTML dla Java?

 A3: Tak, możesz otrzymać bezpłatną wersję próbną Aspose.HTML dla Java[Tutaj](https://releases.aspose.com/)Dzięki temu możesz zapoznać się z jego funkcjami i możliwościami przed dokonaniem zakupu.

### P4: Jakie korzyści daje obserwacja zmian danych cech za pomocą Mutation Observer?

A4: Obserwowanie zmian danych znakowych jest przydatne w scenariuszach, w których chcesz monitorować i reagować na zmiany w treści tekstowej elementów HTML. Na przykład możesz użyć go do śledzenia i reagowania na dane wprowadzane przez użytkownika w formularzach internetowych.

### P5: W jaki sposób mogę pozbyć się zasobów, korzystając z Aspose.HTML dla Java?

 A5: Ważne jest, aby zwolnić zasoby, gdy skończysz. W naszym przykładzie użyliśmy`document.dispose()` aby oczyścić zasoby powiązane z dokumentem HTML. Upewnij się, że pozbędziesz się wszystkich obiektów i zasobów, które utworzysz, aby uniknąć wycieków pamięci.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
