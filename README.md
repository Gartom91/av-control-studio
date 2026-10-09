# AV Control — oficjalne wydania

Instalatory i aktualizacje AV Control Studio, Player, Imager oraz silnika Raspberry Pi 3B / 4B / 5.

**[Pobierz aktualne wydanie](https://github.com/Gartom91/av-control-studio/releases/latest)**

Repozytorium zawiera dokumentację dystrybucji i pliki wydań. Historia rozwoju i kod produktu są przechowywane w oddzielnym, prywatnym repozytorium. Automatycznie tworzone przez GitHub archiwa „Source code” obejmują jedynie tę dokumentację; nie są archiwami źródeł aplikacji.

## Pobieranie i aktualizacje

- Studio: projektowanie, logika, symulacja i publikowanie projektów.
- Player: samodzielne wyświetlanie paneli operatora.
- Imager: przygotowanie karty SD i pierwszej konfiguracji Raspberry Pi.
- Obraz RPi: wspólna baza dla modeli 3B, 4B i 5; wybór modelu w Imagerze.
- Pakiet Runtime ARM64: aktualizacja istniejącej instalacji RPi z zachowaniem jej danych.

Pobieraj pliki z sekcji Assets wybranego wydania. Nazwa instalatora określa wersję i platformę. Nie zapisuj obrazu na dysku systemowym. Przed zapisem karty sprawdź wskazany nośnik i jego pojemność.

Adres sprawdzania aktualizacji pozostaje `Gartom91/av-control-studio`, zgodny ze starszymi aplikacjami. Podział repozytoriów nie wymaga ponownego przygotowania karty SD ani zmiany projektu.

## Integralność

Każde nowe wydanie zawiera manifest dystrybucji i sumy SHA-256. W przeniesionym wydaniu 1.4.1 zachowano oryginalne bajty pakietów i historyczne raporty weryfikacji. Archiwum źródeł produktu nie jest publikowane tutaj. Historyczny manifest 1.4.1 może nadal wymieniać to archiwum; aktualna lista publicznych plików znajduje się w `DISTRIBUTION-MANIFEST.json`.

## Licencja i etap planowania

Wcześniej udostępnione wydania MIT zachowują swoje warunki; przeniesienie repozytorium ich nie zmienia. Aktualne archiwalne pakiety 1.4.1 zawierają MIT i wymagane informacje o komponentach innych autorów. Pakiety Python z tych wydań mogą zawierać czytelny kod środowiska wykonawczego — ten podział repozytoriów nie jest obietnicą technicznego uniemożliwienia analizy aplikacji.

Projekt przyszłej EULA z placeholderami wydawcy znajduje się w [EULA-PL-PROJEKT.md](EULA-PL-PROJEKT.md). Jest dokumentem planistycznym. Nie uruchamia opłat, nie zastępuje wcześniejszej licencji i nie stanowi obecnego warunku aktualizacji.

Dokumentacja użytkownika, podręcznik szkoleniowy, projekty demonstracyjne i raporty testów są dołączane do wydań. Wyniki symulacji są raportowane oddzielnie od sprawdzenia na fizycznym sprzęcie.
