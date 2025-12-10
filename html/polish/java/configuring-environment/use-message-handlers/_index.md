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

## Introduction
W tym samouczku, **how to use aspose** do obsługi brakujących zasobów w HTML jest demonstrowane krok po kroku. Stworzymy prosty dokument HTML, który odwołuje się do brakującego obrazu, dołączymy niestandardowy message handler i pokażemy, jak **load html document java** przy eleganckiej obsłudze zepsutych linków. Na koniec zobaczysz także, jak **convert html to png** przy użyciu Aspose.HTML, dając peł obraz konwersji HTML‑do‑obrazu w Javie.

## Quick Answers
- **Jaki jest podstawowy cel handlera wiadomości?** Aby przechwytywać operacje sieciowe i reagować na kody statusu, takie jak brakujące zasoby.  
- **Czy Aspose.HTML może konwertować HTML do PNG?** Tak, używając `Converter.convertHTML` możesz wykonać konwersję HTML na obraz.  
- **Czy potrzebuję licencji do tego przykładu?** Tymczasowa licencja usuwa ograniczenia wersji próbnej; stała licencja jest wymagana w produkcji.  
- **Która wersja Javy jest wspierana?** Każdy JDK 8+ (tutorial używa JDK 11).  
- **Czy można obsłużyć wiele zepsutych linków?** Oczywiście – możesz łańcuchowo połączyć kilka handlerów, aby zarządzać różnymi scenariuszami.

## Prerequisites
Zanim przejdziemy do przewodnika krok po kroku, upewnijmy się, że masz wszystko, czego potrzebujesz:
1. Java Development Kit (JDK): Upewnij się, że masz zainstalowany JDK w swoim systemie. Możesz go pobrać ze [strony Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).
2. Aspose.HTML for Java: Musisz mieć zainstalowane Aspose.HTML for Java. Możesz je pobrać ze [strony z wydaniami Aspose](https://releases.aspose.com/html/java/).
3. IDE: Użyj swojego ulubionego zintegrowanego środowiska programistycznego (IDE) dla Javy, takiego jak IntelliJ IDEA, Eclipse lub NetBeans.
4. Podstawowa znajomość Javy: Znajomość programowania w Javie jest niezbędna, aby skutecznie podążać za tym samouczkiem.
5. Tymczasowa licencja: Jeśli używasz wersji próbnej Aspose.HTML, rozważ uzyskanie [tymczasowej licencji](https://purchase.aspose.com/temporary-license/), aby uniknąć ograniczeń podczas rozwoju.

## Import Packages
Zanim zaczniemy, upewnij się, że niezbędne pakiety zostały zaimportowane do Twojego projektu Java. Poniżej znajdują się niezbędne importy, które będą Ci potrzebne:
```java
import java.io.IOException;
```
Te importy zapewnią dostęp do klas i metod potrzebnych do obsługi operacji sieciowych, tworzenia dokumentów HTML oraz wykonywania konwersji HTML‑do‑PNG.

## Step 1: Prepare the HTML Code
Krok 1: Przygotuj kod HTML
Pierwszą rzeczą, której potrzebujemy, jest prosty fragment HTML odwołujący się do pliku obrazu. Celowo odwołamy się do obrazu, który nie istnieje, aby wywołać mechanizm obsługi błędów.
```java
String code = "<img src='missing.jpg'>";
```
Ten kod tworzy znacznik `<img>`, który wskazuje na `missing.jpg`. Ponieważ obraz jest brakujący, usługa sieciowa zwróci kod statusu różny od 200, który nasz niestandardowy handler przechwyci.

## Step 2: Write the HTML Code to a File
Krok 2: Zapisz kod HTML do pliku
Następnie musimy zapisać fragment HTML, aby Aspose.HTML mógł go wczytać jako dokument.
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
Używając `FileWriter` zapisujemy HTML do **document.html**. Ten plik staje się źródłem dla kroku **load html document java** później.

## Step 3: Create a Custom Message Handler
Krok 3: Utwórz niestandardowy Message Handler
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

## Step 4: Configure the Network Service
Krok 4: Skonfiguruj usługę sieciową
Aby Aspose.HTML był świadomy naszego handlera, rejestrujemy go w usłudze sieciowej za pomocą klasy `Configuration`.
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
Tutaj tworzymy instancję `Configuration`, pobieramy `INetworkService` i dodajemy nasz niestandardowy handler do jego kolekcji. To zapewnia, że handler będzie uruchamiany przy każdym żądaniu sieciowym, takim jak ładowanie obrazów.

## Step 5: Load the HTML Document
Krok 5: Wczytaj dokument HTML
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

## Step 6: Convert HTML to PNG
Krok 6: Konwertuj HTML do PNG
Aby zilustrować szersze możliwości Aspose.HTML, przekonwertujemy wczytany dokument na obraz PNG. To klasyczny scenariusz **convert html to png**.
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
`Converter.convertHTML` przyjmuje `HTMLDocument`, opcjonalne `ImageSaveOptions` (gdzie możesz ustawić DPI, jakość itp.) oraz nazwę pliku wyjściowego. Wynikiem jest obraz rastrowy renderowanego HTML.

## Step 7: Clean Up Resources
Krok 7: Oczyść zasoby
Właściwe zarządzanie zasobami jest niezbędne w każdej aplikacji Java. Usuwamy zarówno `Configuration`, jak i `HTMLDocument`, aby uniknąć wycieków pamięci.
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
Umieszczenie czyszczenia w bloku `finally` zapewnia jego wykonanie, nawet jeśli wcześniej wystąpi wyjątek.

## Why Use Message Handlers?
Dlaczego używać Message Handlers?
Message handlers dają precyzyjną kontrolę nad operacjami sieciowymi, takimi jak **handle broken links java**. Zamiast pozwalać bibliotece na ciche niepowodzenie, możesz logować, ponawiać próby, zamieniać zasoby lub dostarczać treść awaryjną — co sprawia, że przetwarzanie HTML jest solidne i gotowe do produkcji.

## Common Issues and Solutions
Typowe problemy i rozwiązania
- **Handler recursion** – Upewnij się, że wywołujesz `invoke(context);` tylko raz, aby uniknąć nieskończonych pętli.  
- **Missing license** – Bez ważnej licencji konwersja może generować obraz z znakami wodnymi.  
- **File path errors** – Używaj ścieżek bezwzględnych lub prawidłowo ustaw katalog roboczy przy ładowaniu `document.html`.

## Frequently Asked Questions

**Q: Czy mogę łańcuchowo połączyć wiele message handlers?**  
A: Tak, możesz dodać kilka handlerów do kolekcji `network.getMessageHandlers()`; będą wykonywane w kolejności dodania.

**Q: Czy handler działa również dla zasobów CSS lub skryptów?**  
A: Absolutnie — każde żądanie sieciowe wykonywane przez silnik HTML (obrazy, CSS, JS, czcionki) przechodzi przez handler.

**Q: Jak zmienić żądanie HTTP przed jego wysłaniem?**  
A: Zaimplementuj handler, który modyfikuje `context.getRequest()` przed wywołaniem `invoke(context)`.

**Q: Czy istnieje sposób, aby wyciszyć ostrzeżenie dla konkretnych URL-i?**  
A: Wewnątrz handlera sprawdź `context.getRequest().getRequestUri()` i warunkowo pomiń logowanie.

**Q: Jaka wersja Aspose.HTML jest wymagana dla tych API?**  
A: Kod działa z Aspose.HTML for Java 22.10 i nowszymi.

## Conclusion
Podsumowanie
I oto masz — kompleksowy przewodnik o **how to use aspose** message handlers w Javie. Omówiliśmy tworzenie pliku HTML, podłączanie niestandardowego handlera do **handle broken links java**, wczytywanie dokumentu oraz wykonywanie **convert html to png**. Dzięki temu podejściu możesz pewnie zarządzać brakującymi zasobami, egzekwować własne zasady i rozszerzać możliwości sieciowe Aspose.HTML w dowolnej aplikacji Java.

---

**Last Updated:** 2025-12-10  
**Tested With:** Aspose.HTML for Java 24.11  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}