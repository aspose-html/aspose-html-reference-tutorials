---
date: 2025-12-10
description: Dowiedz się, jak używać Aspose do obsługi uszkodzonych linków w Javie,
  konwertować HTML na PNG oraz ładować dokument HTML w Javie przy użyciu Aspose.HTML
  dla Javy.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Jak używać obsługi wiadomości Aspose.HTML w Javie
url: /pl/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać Aspose.HTML Message Handlers w Javie

## Wstęp
W tym samouczku, **jak używać aspose** do obsługi hamulców zasobów w HTML jest demonstrowane krok po kroku. Tworzymy prosty dokument HTML, który jest dostępny do brakującego obrazu, dołączymy niestandardowy moduł obsługi wiadomości i udostępniamy, jak **load html document java** przy uruchamianiu końcowych zepsutych linków. Na koniec zobacz także, jak **konwertuj html na png** przy użyciu Aspose.HTML, podczas pełnego użycia HTML‑do‑obrazu w Javie.

## Szybkie odpowiedzi
- **Jaki jest podstawowy cel obsługi wiadomości?** Aby przechwycić operacje sieciowe i reagować na kody wystąpienia, takie jak brakujące zasoby.
- **Czy Aspose.HTML może konwertować HTML do PNG?** Tak, używając `Converter.convertHTML`, możesz zakończyć konwersję HTML na obraz.
- **Czy licencja jest dostępna na tym przykładzie?** Tymczasowa licencja na wersję próbną; licencjat jest wymagany w produkcji.
- **Która wersja Javy jest wspierana?** Każdy JDK 8+ (samouczek używa JDK11).
- **Czy można obsłużyć wiele zepsutych linków?** Oczywiście – można połączyć kilka modułów obsługi, aby zakończyć zestawami scenariuszy.

## Warunki wstępne
Zanim przejdziemy do przewodnika krok po kroku, sterujemy się, że masz wszystko, czego potrzebujesz:
1. Java Development Kit (JDK): atak się, że masz podłączony JDK w swoim systemie. Możesz go otrzymać ze [strony Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).
2. Aspose.HTML dla Java: Trzeba mieć dostęp do Aspose.HTML dla Java. Możesz je otrzymać ze [strony z wydaniem Aspose](https://releases.aspose.com/html/java/).
3. IDE: ulubionego ulubionego środowiska programistycznego (IDE) dla Javy, takiego jak IntelliJ IDEA, Eclipse lub NetBeans.
4. Podstawowa przyjemność Javy: oprogramowanie w Javie jest równe, aby skutecznie podążać za tym samouczkiem.
5. Tymczasowa licencja: Jeśli znajdziesz wersję próbną Aspose.HTML, rozwiązanie alternatywne [tymczasowej licencji](https://purchase.aspose.com/temporary-license/), aby przejść do ograniczenia podczas rozwoju.

## Importuj pakiety
Zanim zaczniemy, upewnij się, że niezbędne pakiety zostały zaimportowane do Twojego projektu Java. Poniżej znajdują się niezbędne importy, które będą Ci potrzebne:
```java
import java.io.IOException;
```
Te importy zapewnią dostęp do klas i metod potrzebnych do obsługi operacji sieciowych, tworzenia dokumentów HTML oraz wykonywania konwersji HTML‑do‑PNG.

## Krok 1: Przygotuj kod HTML
Pierwszą rzeczą, której potrzebujemy, jest prosty fragment HTML odwołujący się do pliku obrazu. Celowo odwołamy się do obrazu, który nie istnieje, aby wywołać mechanizm obsługi błędów.
```java
String code = "<img src='missing.jpg'>";
```
Ten kod tworzy znacznik `<img>`, który wskazuje na `missing.jpg`. Ponieważ obraz jest brakujący, usługa sieciowa zwróci kod statusu różny od 200, który nasz niestandardowy handler przechwyci.

## Krok 2: Zapisz kod HTML do pliku
Następnie musimy zapisać fragment HTML, aby Aspose.HTML mógł go wczytać jako dokument.
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
Używając `FileWriter` zapisujemy HTML do **document.html**. Ten plik staje się źródłem dla kroku **load html document java** później.

## Krok 3: Utwórz niestandardowy Message Handler
Teraz zbudujmy niestandardowy handler wiadomości, który reaguje, gdy obraz nie może zostać znaleziony. Handler sprawdza kod statusu HTTP i wypisuje przyjazny komunikat.
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
Metoda `invoke` analizuje `context.getResponse().getStatusCode()`. Jeśli nie jest **200**, wypisujemy wyraźne ostrzeżenie, że plik jest brakujący. Ostateczne wywołanie `invoke(context);` przekazuje kontrolę do kolejnego handlera w łańcuchu.

## Krok 4: Skonfiguruj usługę sieciową
Aby Aspose.HTML był świadomy naszego handlera, rejestrujemy go w usłudze sieciowej za pomocą klasy `Configuration`.
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
Tutaj tworzymy instancję `Configuration`, pobieramy `INetworkService` i dodajemy nasz niestandardowy handler do jego kolekcji. To zapewnia, że handler będzie uruchamiany przy każdym żądaniu sieciowym, takim jak ładowanie obrazów.

## Krok 5: Wczytaj dokument HTML
Po przygotowaniu konfiguracji możemy teraz wczytać plik HTML, który utworzyliśmy wcześniej. Ten krok demonstruje **load html document java**, podczas gdy brakujący obraz wywołuje nasz handler.
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
Konstruktor `HTMLDocument` otrzymuje zarówno ścieżkę do pliku, jak i niestandardową `configuration`. Gdy dokument analizuje znacznik `<img>`, usługa sieciowa próbuje pobrać `missing.jpg`, otrzymuje 404 i nasz handler wypisuje ostrzeżenie.

## Krok 6: Konwertuj HTML do PNG
Aby zilustrować szersze możliwości Aspose.HTML, przekonwertujemy wczytany dokument na obraz PNG. To klasyczny scenariusz **convert html to png**.
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
`Converter.convertHTML` przyjmuje `HTMLDocument`, opcjonalne `ImageSaveOptions` (gdzie możesz ustawić DPI, jakość itp.) oraz nazwę pliku wyjściowego. Wynikiem jest obraz rastrowy renderowanego HTML.

## Krok 7: Oczyść zasoby
Właściwe zarządzanie zasobami jest niezbędne w każdej aplikacji Java. Usuwamy zarówno `Configuration`, jak i `HTMLDocument`, aby uniknąć wycieków pamięci.
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
Umieszczenie czyszczenia w bloku `finally` zapewnia jego wykonanie, nawet jeśli wcześniej wystąpi wyjątek.

## Dlaczego warto używać programów obsługi wiadomości?
Dlaczego legalne moduły obsługi wiadomości?
Programy obsługi wiadomości zapewniają precyzyjną kontrolę nad operacjami sieciowymi, aplikatorem jak **obsługa uszkodzonych linków java**. Zamiast tego biblioteka pozwala na ciche niepowodzenie, może logować, ponawiać próbę, dostarczyć dostawę lub dostarczyć treść awaryjną — co sprawia, że ​​HTML jest solidny i gotowy do produkcji.

## Typowe problemy i rozwiązania
Typowe problemy i rozwiązania
- **Rekursja obsługi** – obciążenie się, że następstwsz `invoke(context);` tylko raz, aby zakończyć nieskończone.
- **Brak licencji** – Bez ważnej licencji konwersja może generować obraz z znakami wodnymi.
- **Błędy ścieżki pliku** – Używanie parametrów bezwzględnych lub prawidłowy katalog roboczy przy ładowaniu `document.html`.

## Często zadawane pytania

**P: Czy mogę połączyć wiele programów obsługi wiadomości?**
A: Tak, możesz poprosić kilka handlerów do kolekcji `network.getMessageHandlers()`; Będzie następować w kolejności dodania.

**P: Czy handler działa również dla zasobów CSS lub skryptów?**
A: Absolutnie — każde żądanie sieciowe przez silnik HTML (obrazy, CSS, JS, przejście) przez moduł obsługi.

**Q: Jak włączyć HTTP przed jego wydaniem?**
A: Zaimplementuj procedurę obsługi, która modyfikuje `context.getRequest()` przed wywołaniem `invoke(context)`.

**P: Czy istnieje sposób, aby wyciszyć ostrzeżenie dla kolejnego adresu URL-i?**
A: Wewnętrzna obsługa sprawdzania `context.getRequest().getRequestUri()` i warunkowo pomiń logowanie.

**P: Jaka wersja Aspose.HTML jest wymagana dla tych API?**
O: Kod działa z Aspose.HTML dla Java 22.10 i terazmi.

## Wniosek
Podsumowanie
I oto masz — kompleksowy przewodnik o **jak korzystać z modułów obsługi wiadomości aspose** w Javie. Oświadczenie o utworzeniu pliku HTML, podłączonego do uchwytu do **obsługa uszkodzonych linków java**, wczytanie dokumentu oraz **convert html to png**. Dzięki temu możliwe jest bezpieczne wyłączenie zasilania, egzekwowanie własnych zasad i rozszerzanie możliwości sieciowych Aspose.HTML w dostępnej aplikacji Java.

---

**Ostatnia aktualizacja:** 10.12.2025 r
**Testowano z:** Aspose.HTML dla Java 24.11
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}