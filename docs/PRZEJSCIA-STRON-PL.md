# Przejścia stron panelu

W Edytorze paneli wybierz stronę i **Wygląd strony / CSS → Przejście na tę stronę**.
Ustawienie dotyczy strony docelowej: działa z zakładek odtwarzacza i z przycisków nawigacji.
Podgląd uruchamia przycisk **Odtwórz podgląd przejścia**.

| Efekt | Przebieg |
| --- | --- |
| Bez animacji | Natychmiastowa zmiana strony. |
| Fade | Nowa strona stopniowo przykrywa poprzednią. |
| Wipe | Nowa strona odsłania się w lewo, w prawo, w górę lub w dół. |
| Wash | Obraz przechodzi przez wybrany jednolity kolor. |
| Slide | Poprzednia i nowa strona przesuwają się w wybranym kierunku. |
| Zoom | Nowa strona pojawia się od 92% wielkości do pełnego rozmiaru. |

Czas wynosi 0–2000 ms; 0 wyłącza animację. Tempo stałe lub z łagodnym rozpoczęciem i zakończeniem.
Pierwsze wyświetlenie panelu nie uruchamia przejścia. Wybranie bieżącej strony nie powtarza efektu.
W przeglądarce szybka zmiana zakładek kończy poprzednie przejście i pokazuje ostatnio wybraną stronę.
Odtwarzacz respektuje systemowe ograniczenie ruchu. Migawka poprzedniej strony nie wykonuje komend;
podczas animacji elementy sterujące nowej strony są nieaktywne.

Ustawienia zapisują się w `.avctrl` i są wspólne dla Studio, panelu WWW, Windows Playera,
HDMI Raspberry Pi i natywnego TAB5. Starszy kontroler musi zostać zaktualizowany przed
publikacją projektu z aktywnymi przejściami. TAB5 wymaga firmware 0.3.0 lub nowszego
oraz ponownego wysłania panelu. W razie braku pamięci na dwie klatki TAB5 natychmiast
wyświetla stronę docelową; sterowanie i bieżące dane pozostają dostępne.

## Ćwiczenie w istniejącym szkoleniu

Załaduj aktualny `Szkolenie-Wirtualna-sala.avctrl` i uruchom podgląd albo opublikowany panel.
Pięć istniejących stron zachowuje swoje ćwiczenia; każda pokazuje efekt wejścia przez 520 ms:

1. **Sala — fade.** Wróć tu z dowolnej innej strony.
2. **Sceny i logika — wipe w lewo.** Obserwuj odsłanianie od prawej krawędzi.
3. **Laboratorium — wash.** W połowie czasu ekran ma jednolity kolor `#123b4b`.
4. **Łączność — slide w górę.** Obie strony przesuwają się pionowo.
5. **Ekspandery — zoom.** Nowa strona łagodnie rośnie do pełnego rozmiaru.

Porównaj zakładki z nawigacją wewnątrz panelu. W edytorze zmień wipe na pozostałe trzy
kierunki, wash na własny kolor oraz czas na 0 ms. Na WWW włącz systemowe ograniczenie
ruchu. Powtórz przejścia na HDMI, Windows Playerze i TAB5. Zapisz osobno wyniki na
fizycznym urządzeniu i w przeglądarce; emulacja ekranu nie jest próbą fizycznego dotyku.

Studio udostępnia niezależny podgląd w **Animacje stron — ćwiczenie** obok przycisku podręcznika.
Przykładowe urządzenia fizyczne szkolenia pozostają wyłączone, bez komend startowych.
