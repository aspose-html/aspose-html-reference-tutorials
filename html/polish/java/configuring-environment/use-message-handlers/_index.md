---
date: 2025-12-08
description: Dowiedz się, jak konwertować HTML na PNG przy użyciu Aspose.HTML dla
  Javy, obsługując uszkodzone linki i przechwytując brakujące zasoby przy pomocy własnych
  obsługujących komunikatów.
language: pl
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Jak konwertować HTML na PNG i używać obsługi komunikatów w Aspose.HTML dla
  Javy
url: /java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwersja HTML do PNG przy użyciu Aspose.HTML dla Java – z obsługą Message Handlers

## Wprowadzenie  
W tym samouczku dowiesz się, **jak konwertować HTML do PNG** przy użyciu Aspose.HTML dla Java oraz, jednocześnie, **jak obsługiwać uszkodzone linki** lub brakujące zasoby za pomocą własnego message handlera. Przejdziemy przez tworzenie prostego pliku HTML, zapisywanie go na dysku, ładowanie oraz przechwytywanie błędów sieciowych – idealne rozwiązanie dla programistów potrzebujących niezawodnej **konwersji html na obraz** w aplikacjach Java klasy produkcyjnej.

## Szybkie odpowiedzi
- **Co obejmuje samouczek?** Konwersję HTML do PNG oraz obsługę brakujących zasobów przy użyciu message handlera.  
- **Jakiej biblioteki użyto?** Aspose.HTML dla Java.  
- **Czy potrzebna jest licencja?** Zalecana jest tymczasowa licencja dla wersji próbnych.  
- **Czy mogę zapisać plik HTML z poziomu Javy?** Tak – zobacz krok „write html file java”.  
- **Czy handler przechwyci uszkodzone linki?** Zdecydowanie; loguje wszystkie odpowiedzi inne niż 200.

## Co to jest Message Handler w Aspose.HTML?  
Message handler to punkt zaczepienia w stosie sieciowym, który pozwala **przechwycić brakujące zasoby** (np. uszkodzony URL obrazu) zanim spowodują wyjątek. Analizując kod statusu odpowiedzi, możesz logować, zastępować lub ponawiać żądanie – dając pełną kontrolę nad operacjami sieciowymi.

## Dlaczego konwertować HTML do PNG?  
Konwersja HTML na obraz jest przydatna przy generowaniu miniatur, podglądów e‑mailowych lub zrzutów przypominających PDF, gdy nie potrzebujesz pełnej konwersji do PDF. Aspose.HTML oferuje szybki, po‑stronnego **html to image conversion** silnik, który działa bez przeglądarki.

## Wymagania wstępne
1. **Java Development Kit (JDK)** – pobierz ze [strony Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML dla Java** – pobierz najnowsze pliki JAR ze [strony wydań Aspose](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse lub NetBeans.  
4. **Podstawowa znajomość Javy** – powinieneś być zaznajomiony z try‑with‑resources i zwalnianiem obiektów.  
5. **Tymczasowa licencja** (opcjonalnie) – uniknij ograniczeń wersji próbnej dzięki [tymczasowej licencji](https://purchase.aspose.com/temporary-license/).

## Importowanie pakietów
Zanim zaczniemy, zaimportuj wymagane klasy Javy:

```java
import java.io.IOException;
```

Te importy dają dostęp do operacji I/O oraz API sieciowych Aspose.HTML.

## Krok 1: Zapisz plik HTML (write html file java)  
Najpierw utwórz mały fragment HTML, który odwołuje się do obrazu **nieistniejącego**. To pozwoli nam przetestować handler.

```java
String code = "<img src='missing.jpg'>";
```

## Krok 2: Zapisz HTML na dysku  
Zapisz fragment do pliku o nazwie `document.html`. Plik ten zostanie później wczytany przez silnik Aspose.HTML.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Krok 3: Utwórz własny Message Handler (catch missing resource)  
Teraz definiujemy handler, który sprawdza kod statusu HTTP. Jeśli nie jest `200`, logujemy przyjazną wiadomość.

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

## Krok 4: Zarejestruj handler w usłudze sieciowej  
Dodaj własny handler do usługi sieciowej Aspose.HTML, aby uczestniczył w każdym żądaniu.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Krok 5: Wczytaj dokument HTML (load html document java)  
Po skonfigurowaniu, wczytaj plik HTML. Brakujący obraz wywoła handler, który właśnie dodaliśmy.

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

## Krok 6: Konwertuj HTML do PNG (convert html to png)  
Na koniec skonwertuj wczytany dokument do obrazu PNG. To pokazuje pełny **html to image conversion** workflow.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Krok 7: Posprzątaj zasoby  
Zawsze zwalniaj obiekt `Configuration`, aby uwolnić zasoby natywne i uniknąć wycieków pamięci.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Typowe pułapki i wskazówki
- **Recursive invoke call:** Własny handler musi wywołać `invoke(context);` *po* Twojej logice, aby kontynuować łańcuch. Pominięcie tego może zatrzymać działanie innych handlerów.  
- **Ostrzeżenia o braku licencji:** Bez ważnej licencji konwersja może dodać znak wodny lub ograniczyć rozmiar wyjścia.  
- **Problemy ze ścieżkami:** Upewnij się, że `document.html` jest zapisany w katalogu roboczym lub podaj pełną ścieżkę.  

## Najczęściej zadawane pytania

**Q: Czym jest Aspose.HTML dla Java?**  
A: To solidna biblioteka, która pozwala programistom Javy tworzyć, modyfikować i konwertować dokumenty HTML bez przeglądarki.

**Q: Dlaczego używać message handlerów w Aspose.HTML dla Java?**  
A: Pozwalają **obsługiwać uszkodzone linki**, logować brakujące zasoby lub modyfikować żądania/odpowiedzi w locie.

**Q: Czy mogę łączyć wiele message handlerów?**  
A: Tak – dodaj każdy handler do listy `network.getMessageHandlers()`; będą wykonywane w kolejności dodania.

**Q: Czy zwalnianie obiektów Configuration i HTMLDocument jest wymagane?**  
A: Zdecydowanie; zwalnianie uwalnia pamięć natywną i zapobiega wyciekom w aplikacjach działających długo.

**Q: Poza brakującymi obrazami, jakie inne błędy mogą obsługiwać handlery?**  
A: Każda odpowiedź HTTP różna od 200 – timeouty, strony 404, błędy uwierzytelniania itp. – mogą być przechwycone i obsłużone.

## Zakończenie  
Masz teraz kompletny, gotowy do produkcji przykład **konwersji HTML do PNG** przy jednoczesnym **obsługiwaniu uszkodzonych linków** i **przechwytywaniu brakujących zasobów** przy użyciu Aspose.HTML dla Java. Włącz ten wzorzec do większych projektów, aby uzyskać precyzyjną kontrolę nad operacjami sieciowymi i generować niezawodne zrzuty obrazu Twojej treści HTML.

---

**Ostatnia aktualizacja:** 2025-12-08  
**Testowane z:** Aspose.HTML dla Java 24.12 (najnowsza)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}