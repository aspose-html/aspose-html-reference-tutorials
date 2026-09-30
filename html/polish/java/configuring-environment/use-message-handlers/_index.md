---
date: 2026-02-10
description: Dowiedz się, jak używać Aspose do obsługi uszkodzonych linków w Javie,
  konwertować HTML na PNG i ładować dokument HTML w Javie przy użyciu Aspose.HTML
  for Java.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Konwertuj HTML do PNG przy użyciu obsługiwaczy komunikatów Aspose.HTML w Javie
url: /pl/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwertowanie HTML do PNG przy użyciu obsługi wiadomości Aspose.HTML w Javie

## Wstęp
W tym samouczku dowiesz się, **jak konwertować HTML do PNG** przy zachowaniu eleganckiej obsługi hamulców przy użyciu Aspose.HTML dla Javy. Przejdziemy przez tworzenie strony HTML, która jest udostępniana do nieistniejącego obrazu, **niestandardowego obsługi wiadomości** do **przechwytywania sieciowych**, dostępna **Usługi sieciowej**, dostępnie do dokumentu oraz ostateczne wykonanie **conwerssji HTML do obrazu**. Aby mieć solidną stronę internetową, możesz pobrać ją z łącza Java, a następnie użyć PNG - idealnego raportu, miniatury i adresu e-mail.

## Szybkie odpowiedzi
- **Co robi obsługiwacz wiadomości?** Przechwytuje operacje sieciowe (np. wyzwalanie) i pozwala na reagowanie na kody stanu, takie jak 404.
- **Czy Aspose.HTML jak przekonwertować HTML na PNG?** Również — `Converter.convertHTML` to jak to przekonwertować.
- **Czy licencja jest do tego przykładu?** Tymczasowa wersja licencji ewaluacyjnej; Licencja stała jest wymagana w środowisku produktu.
- **Jaką wersję Javy obsługuje?** Dowolny JDK8+ (przykład ziała na JDK11).
- **Czy mogę korzystać z połączenia sieciowego?** Oczywiście — `configuration.getService(INetworkService.class)`, aby uzyskać dostęp do obsługiwacza.

## Warunki wstępne
Zanim zaczniemy, wykonaj się, że możemy uruchomić następujące elementy:

1. **Java Development Kit (JDK)** – pobierz ze [strony Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).
2. **Aspose.HTML dla Java** – dostępna biblioteka dla Aspose](https://releases.aspose.com/html/java/).
3. **IDE** – obsługiwane są IntelliJ IDEA, Eclipse i NetBeans.
4. **Podstawowa przyjemność Javy** – być zaznajomiony z klasami, try-with-resources oraz obsługi wyjątków.
5. **Licencja tymczasowa** – dostępna z wersji próbnej, zdobądź [tymczasową dostęp](https://purchase.aspose.com/temporary-license/), aby uzyskać dostęp do znaków wodnych.

## Importuj pakiety
Najpierw zaimportuj klasę Java I/O, której będziemy potrzebować do obsługi plików. Reszta klas Aspose jest odwoływana pełnymi nazwami później, co utrzymuje listę importów schludną.

```java
import java.io.IOException;
```

## Krok 1: Przygotuj kod HTML  
Tworzymy minimalny fragment HTML, który celowo odwołuje się do brakującego obrazu. To spowoduje wywołanie naszego obsługiwacza, gdy silnik spróbuje pobrać zasób.

```java
String code = "<img src='missing.jpg'>";
```

## Krok 2: Zapisz kod HTML do pliku  
Następnie zapisujemy fragment do *document.html*. Użycie bloku try‑with‑resources zapewnia, że `FileWriter` zostanie prawidłowo zamknięty.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Krok 3: Napisz własny obsługiwacz wiadomości  
Teraz tworzymy **niestandardowy obsługiwacz wiadomości**, który sprawdza kod statusu HTTP każdego żądania sieciowego. Jeśli odpowiedź nie jest `200`, logujemy przyjazne ostrzeżenie. Zwróć uwagę na wywołanie `invoke(context);` na końcu — przekazuje ono żądanie do kolejnego obsługiwacza w łańcuchu, zapobiegając rekurencji.

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

## Krok 4: Skonfiguruj usługę sieciową  
Aby Aspose.HTML był świadomy naszego obsługiwacza, pobieramy **usługę sieciową** z instancji `Configuration` i dodajemy obsługiwacz do jej kolekcji. To jest krok, w którym **konfigurujemy usługę sieciową** dla niestandardowego zachowania.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Krok 5: Załaduj dokument HTML  
Po przygotowaniu konfiguracji ładujemy *document.html*. Silnik teraz używa naszej usługi sieciowej, więc żądanie brakującego obrazu jest przechwytywane przez właśnie dodany obsługiwacz.

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

## Krok 6: Konwertuj HTML do PNG  
Oto serce procesu **konwersji HTML do obrazu**. Metoda `Converter.convertHTML` przyjmuje załadowany `HTMLDocument`, opcjonalne `ImageSaveOptions` (gdzie możesz dostosować DPI lub jakość) oraz nazwę pliku wyjściowego.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Krok 7: Posprzątaj zasoby  
Dobre praktyki Javy nakazują zwolnienie wszystkich zasobów natywnych. Blok `finally` zapewnia, że `Configuration` zostanie zwolniona, nawet jeśli wyjątek zostanie wyrzucony.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Dlaczego używać obsługiwaczy wiadomości?  
Obsługiwacze wiadomości dają **precyzyjną kontrolę** nad każdym żądaniem sieciowym — czy to obraz, CSS, JavaScript, czy plik czcionki. Zamiast pozwalać bibliotece na ciche niepowodzenie, możesz logować brakujące zasoby, dostarczać treść zastępczą lub nawet ponowić żądanie. Dzięki temu Twój potok przetwarzania HTML staje się **solidny**, **gotowy do produkcji** i łatwiejszy w debugowaniu.

## Typowe problemy i rozwiązania
- **Rekurencja obsługiwacza** — wywołaj `invoke(context);` tylko raz, aby uniknąć nieskończonych pętli.  
- **Brak licencji** — bez ważnej licencji wygenerowany PNG będzie zawierał znak wodny.  
- **Nieprawidłowe ścieżki plików** — używaj ścieżek bezwzględnych lub poprawnie ustaw katalog roboczy przy ładowaniu `document.html`.  
- **Nieobsługiwane typy zasobów** — upewnij się, że zasób, który chcesz przechwycić (obraz, CSS itp.) jest rzeczywiście żądany przez silnik HTML.

## Najczęściej zadawane pytania

**P: Czy mogę łączyć wiele obsługiwaczy wiadomości?**  
O: Tak, możesz dodać kilka obsługiwaczy do kolekcji `network.getMessageHandlers()`; zostaną one wykonane w kolejności dodania.

**P: Czy obsługiwacz działa również dla zasobów CSS lub skryptów?**  
O: Absolutnie — każde żądanie sieciowe wykonywane przez silnik HTML (obrazy, CSS, JS, czcionki) przechodzi przez obsługiwacz.

**P: Jak zmienić żądanie HTTP przed jego wysłaniem?**  
O: Zaimplementuj obsługiwacz, który modyfikuje `context.getRequest()` przed wywołaniem `invoke(context)`.

**P: Czy istnieje sposób, aby wyciszyć ostrzeżenie dla konkretnych URL-i?**  
O: W obsługiwaczu sprawdź `context.getRequest().getRequestUri()` i warunkowo pomiń logowanie.

**P: Jakiej wersji Aspose.HTML wymaga ten kod?**  
O: Kod działa z Aspose.HTML for Java 22.10 i nowszymi.

## Podsumowanie  
Masz teraz kompletny, end‑to‑end przykład **jak konwertować HTML do PNG** przy użyciu **niestandardowego obsługiwacza wiadomości**, aby **przechwytywać żądania sieciowe** i **obsługiwać zepsute linki java**. Konfigurując usługę sieciową, ładując dokument i wywołując konwerter, możesz niezawodnie generować miniatury PNG lub pełno‑stronne zrzuty ekranu w dowolnej aplikacji Java.

---

**Ostatnia aktualizacja:** 2026-02-10  
**Testowano z:** Aspose.HTML for Java 24.11  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}