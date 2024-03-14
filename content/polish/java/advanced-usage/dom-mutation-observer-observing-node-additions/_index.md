---
title: Obserwator mutacji DOM z Aspose.HTML dla Java
linktitle: Obserwator mutacji DOM - obserwacja dodań węzłów
second_title: Przetwarzanie HTML w Javie za pomocą Aspose.HTML
description: Z tego przewodnika krok po kroku dowiesz się, jak używać Aspose.HTML dla Java do implementacji obserwatora mutacji DOM. Skutecznie monitoruj i reaguj na zmiany DOM.
type: docs
weight: 11
url: /pl/java/advanced-usage/dom-mutation-observer-observing-node-additions/
---

Czy jesteś programistą Java i chcesz obserwować zmiany w obiektowym modelu dokumentu (DOM) dokumentu HTML i reagować na nie? Aspose.HTML dla Java zapewnia potężne rozwiązanie tego zadania. W tym przewodniku krok po kroku odkryjemy, jak używać Aspose.HTML dla Java do tworzenia dokumentu HTML i obserwowania dodawania węzłów za pomocą obserwatora mutacji. Ten samouczek przeprowadzi Cię przez cały proces, dzieląc każdy przykład na wiele kroków. Na koniec będziesz mógł z łatwością wdrożyć obserwatorów mutacji DOM w swoich projektach Java.

## Warunki wstępne

Zanim zagłębimy się w używanie Aspose.HTML dla Java, upewnijmy się, że masz niezbędne wymagania wstępne:

1. Środowisko programistyczne Java: Upewnij się, że w systemie jest zainstalowany zestaw Java Development Kit (JDK).

2.  Aspose.HTML dla Java: Musisz pobrać i zainstalować Aspose.HTML dla Java. Możesz znaleźć link do pobrania[Tutaj](https://releases.aspose.com/html/java/).

3. IDE (Zintegrowane środowisko programistyczne): Użyj preferowanego środowiska Java IDE, takiego jak IntelliJ IDEA lub Eclipse, do pisania i uruchamiania kodu Java.

## Importuj pakiety

Aby rozpocząć korzystanie z Aspose.HTML dla Java, musisz zaimportować wymagane pakiety do swojego kodu Java. Oto jak możesz to zrobić:

```java
// Zaimportuj niezbędne pakiety
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

Teraz, gdy zaimportowałeś wymagane pakiety, przejdźmy do przewodnika krok po kroku dotyczącego implementacji obserwatora mutacji DOM w Javie.

## Krok 1: Utwórz instancję obserwatora mutacji

Najpierw musisz utworzyć instancję obserwatora mutacji. Ten obserwator będzie obserwował zmiany w DOM i wykona funkcję wywołania zwrotnego, gdy wystąpią mutacje.

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

W tym kroku tworzymy obserwatora z funkcją wywołania zwrotnego, która wypisuje komunikat po dodaniu węzłów do DOM.

## Krok 2: Skonfiguruj Observera

Teraz skonfigurujmy obserwatora z żądanymi opcjami. Chcemy obserwować zmiany w listach podrzędnych i poddrzewie, a także zmiany w danych znakowych.

```java
MutationObserverInit config = new MutationObserverInit();
config.setChildList(true);
config.setSubtree(true);
config.setCharacterData(true);

// Przekaż węzeł docelowy do obserwacji z określoną konfiguracją
observer.observe(document.getBody(), config);
```

 Tutaj ustawiamy`config` obiekt, aby umożliwić obserwację zmian w listach podrzędnych, poddrzewie i danych znakowych. Następnie przekazujemy węzeł docelowy (w tym przypadku dokument`<body>`) i konfigurację dla obserwatora.

## Krok 3: Zmodyfikuj DOM

Teraz wprowadzimy pewne zmiany w DOM, aby wyzwolić obserwatora. Utworzymy element akapitu i dołączymy go do treści dokumentu.

```java
// Utwórz element akapitu i dołącz go do treści dokumentu
Element p = document.createElement("p");
document.getBody().appendChild(p);

// Utwórz tekst i dołącz go do akapitu
Text text = document.createTextNode("Hello World");
p.appendChild(text);
```

Na tym etapie tworzymy element akapitu HTML i dodajemy go do treści dokumentu. Następnie tworzymy węzeł tekstowy o treści „Hello World” i dołączamy go do akapitu.

## Krok 4: Poczekaj na obserwacje (asynchronicznie)

Ponieważ mutacje obserwuje się asynchronicznie, musimy poczekać chwilę, aby obserwator mógł uchwycić zmiany. Użyjemy`synchronized` I`wait` w tym celu, jak pokazano poniżej.

```java
// Ponieważ mutacje działają w trybie asynchronicznym, poczekaj kilka sekund
synchronized (this) {
    wait(5000);
}
```

Tutaj czekamy 5 sekund, aby mieć pewność, że obserwator ma szansę uchwycić wszelkie mutacje.

## Krok 5: Przestań obserwować

Na koniec, po zakończeniu obserwacji, konieczne jest odłączenie obserwatora w celu uwolnienia zasobów.

```java
// Przestań obserwować
observer.disconnect();
```

Na tym etapie zakończyłeś obserwację i możesz oczyścić zasoby.

## Wniosek

W tym samouczku omówiliśmy proces używania Aspose.HTML dla Java do implementacji obserwatora mutacji DOM. Nauczyłeś się, jak stworzyć obserwatora, skonfigurować go, wprowadzić zmiany w DOM, czekać na obserwacje i przestać obserwować. Teraz masz umiejętności stosowania obserwatorów mutacji DOM w swoich projektach Java w celu skutecznego monitorowania i reagowania na zmiany w DOM dokumentów HTML.

Jeśli masz jakieś pytania lub napotkasz problemy, nie wahaj się szukać pomocy w[Forum Aspose.HTML](https://forum.aspose.com/) . Dodatkowo możesz uzyskać dostęp do[dokumentacja](https://reference.aspose.com/html/java/) aby uzyskać szczegółowe informacje na temat Aspose.HTML dla Java.

## Często zadawane pytania

### P1: Co to jest obserwator mutacji DOM?

O1: Obserwator mutacji DOM to funkcja języka JavaScript, która umożliwia śledzenie zmian w modelu obiektowym dokumentu (DOM) dokumentu HTML. Umożliwia reagowanie w czasie rzeczywistym na dodawanie, usuwanie lub modyfikacje węzłów DOM.

### P2: Czy mogę używać Aspose.HTML dla Java w moich projektach komercyjnych?

 O2: Tak, możesz używać Aspose.HTML dla Java w projektach komercyjnych. Można znaleźć informacje dotyczące licencji i zakupów[Tutaj](https://purchase.aspose.com/buy).

### P3: Czy dostępna jest bezpłatna wersja próbna Aspose.HTML dla Java?

 Odpowiedź 3: Tak, możesz uzyskać bezpłatną wersję próbną Aspose.HTML dla Java[Tutaj](https://releases.aspose.com/). Dzięki temu możesz zapoznać się z jego funkcjami i możliwościami przed dokonaniem zakupu.

### P4: Jaka jest korzyść z obserwacji zmian danych postaci za pomocą Obserwatora Mutacji?

O4: Obserwowanie zmian danych znakowych jest przydatne w scenariuszach, w których chcesz monitorować i reagować na zmiany w zawartości tekstowej elementów HTML. Można go na przykład używać do śledzenia danych wprowadzanych przez użytkowników w formularzach internetowych i odpowiadania na nie.

### P5: Jak pozbyć się zasobów podczas korzystania z Aspose.HTML dla Java?

 Odpowiedź 5: Ważne jest, aby zwolnić zasoby, gdy skończysz. W naszym przykładzie użyliśmy`document.dispose()` aby wyczyścić zasoby powiązane z dokumentem HTML. Pamiętaj, aby pozbyć się wszelkich utworzonych obiektów i zasobów, aby uniknąć wycieków pamięci.