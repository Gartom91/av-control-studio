<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="media/logo-light.svg" />
  <img src="media/logo-dark.svg" width="310" alt="AV Control — Control Systems" />
</picture>

# Jedna instalacja. Twoje urządzenia. Twoja logika.

Projektuj panele, podłączaj urządzenia i programuj instalację lokalnie.

**Polski · [English](README.en.md)**

[**Pobierz 1.5.5 — Signal Workshop**](https://github.com/Gartom91/av-control-studio/releases/tag/v1.5.5) · [Historia wydań](CHANGELOG.md) · [Kurs szkoleniowy](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/AV-Control-Szkolenie-1.5.5.zip)

**Windows · Raspberry Pi 3B / 4B / 5 · Player Linux · Panele WWW**

</div>

---

AV Control to konfigurowalna platforma do sal AV, wystaw i innych instalacji. Definiujesz urządzenia, protokoły, panele i logikę; Raspberry Pi wykonuje projekt samodzielnie po zamknięciu Studio. Codzienne sterowanie działa lokalnie, bez chmury i internetu.

To **oficjalne repozytorium dystrybucyjne**: instalatory, obrazy kontrolera, aktualizacje, instrukcje i raporty weryfikacji. Źródła i historia rozwoju produktu znajdują się w osobnym prywatnym repozytorium. Automatyczne archiwa „Source code” GitHub zawierają dokumentację tego repozytorium dystrybucyjnego.

<picture>
  <source media="(prefers-color-scheme: light)" srcset="media/studio-light.png" />
  <img src="media/signal-workshop.png" alt="Signal Workshop — logika, sygnały, urządzenia i uporządkowane połączenia" />
</picture>

*Rzeczywiste zrzuty aplikacji. Przykłady używają wirtualnych transportów i wyłączonych połączeń sprzętowych.*

## Wybierz aplikację

| Aplikacja | Zastosowanie | Pobierz 1.5.5 |
| --- | --- | --- |
| **Studio** | Urządzenia, protokoły, panele i logika; symulacja, debugger i publikowanie. | [Windows x64](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/AV-Control-Studio-1.5.5-Windows-x64.exe) |
| **Player** | Obsługa opublikowanych paneli na osobnym komputerze, także w pełnym ekranie. | [Windows x64](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/AV-Control-Player-1.5.5-Windows-x64.exe) · [Linux .deb](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/AV-Control-Player-1.5.5-Linux-all.deb) · [Archiwum Linux](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/AV-Control-Player-1.5.5-Linux.tar.gz) |
| **Imager** | Wybór modelu RPi, ustawienia kont i sieci, zapis i weryfikacja karty SD. Obraz jest dołączony. | [Windows x64](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/AV-Control-Imager-1.5.5-Windows-x64.exe) |
| **Kontroler RPi** | Samodzielne wykonywanie logiki i komunikacja z urządzeniami. | [Obraz SD, ARM64](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/AV-Control-RPi-1.5.5-arm64.img.xz) · [Aktualizacja Runtime](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/AV-Control-Runtime-1.5.5-arm64.zip) |
| **Panel WWW** | Obsługa tych samych paneli na komputerze, tablecie lub telefonie. | Otwórz adres HTTPS kontrolera. |

Windows: Windows 10 22H2 / Windows 11, x64; .NET i instalator WebView2 offline są dołączone. Publiczny Player Linux: Debian 13 / CPython 3.13 z GTK i WebKit. Obraz RPi: Raspberry Pi OS Lite 64-bit. Pakiet Runtime służy do aktualizacji istniejącego kontrolera AV Control.

## Signal Workshop

- **Panel lokalny HDMI:** automatyczny kiosk na Raspberry Pi, mysz/touchpad/dotyk USB, strona początkowa i konsola tty2. [Instrukcja i ćwiczenia](docs/PANEL-HDMI-PL.md).
- **Jeden obszar logiki:** urządzenia, sygnały, protokoły, komendy, sekwencje i Python we wspólnym eksploratorze z ustawieniami kontekstowymi. Nazwa i ikona urządzenia opisują rzeczywisty sprzęt.
- **Czytelne schematy:** porty wyrównane z opisami, prowadzenie przewodów wokół symboli, rozdzielanie tras i oznaczanie przecięć. Bramki o zmiennej liczbie wejść, Truth table, impulsowy Interlock z SET ALL/CLEAR, timery, liczniki, pamięci, zatrzaski i przerzutniki.
- **Pełny Python:** edytor kodu, typowane porty, stan, parametry, moduły pomocnicze i dokładne wersje bibliotek. Import NumPy i innych bibliotek, instalacja z PyPI lub zgodnych wheel offline oraz próba w Studio. Administrator zatwierdza konkretny kod, helpery i wymagania; zmiana unieważnia zgodę. Pełny CPython wykonuje zaufany kod i nie jest piaskownicą bezpieczeństwa.
- **Wybór projektu:** wyszukiwanie, pełne nazwy i znacznik bieżącego projektu w dopasowanej do motywu liście; strzałki, Enter i Escape. Konto, motyw i ustawienia pozostają po prawej.
- **Debugger:** wartości i jakość sygnałów, pamięci, timery, sekwencje, TX/RX, ślad zdarzeń i przyczyny blokad. Wymuszanie wejść oraz pauza/krok logiki w symulatorze. Pauza nie zamraża komunikacji, trwających sekwencji ani procesów Python. Regulowany podział w czterech położeniach, pełny obszar roboczy i osobne okno z zachowaniem sesji.
- **Codzienna edycja:** prawy klik i skróty do wycinania, kopiowania, wklejania, duplikacji, usuwania, zmiany nazwy, wyrównywania, grup, warstw, kopiowania wyglądu, blokowania pozycji i przechodzenia do końców połączenia.
- **Własny wygląd:** jasny, ciemny i systemowy motyw programu, dopasowane przewijanie oraz osiem motywów paneli z dostrajaniem poszczególnych elementów.

![Panel Liquid — filtrowanie treści w tle i subtelne odbicia](media/liquid-panel.png)

*Glass, Liquid, Frost i Szron filtrują rzeczywistą treść pod kontrolkami. Soft Dark zapewnia delikatne wypukłości i gradienty; Paper, Workshop i Contrast mają odmienny charakter. Efekty mają wariant oszczędny. Zdjęcie przedstawia rzeczywisty rendering panelu.*

[Instrukcja wyboru projektu ze zrzutami](docs/WYBOR-PROJEKTU-PL.md)

## Połączenia i automatyzacja

| Obszar | Funkcje |
| --- | --- |
| **Porty szeregowe i GPIO** | USB–RS232/RS485, UART RPi i cyfrowe GPIO; stabilne identyfikatory USB, wykrywanie linii, konflikty, format transmisji, kontrola przepływu i kierunek RS485. UART jest domyślnie włączony w czystym obrazie bez konsoli szeregowej. |
| **Rozbudowa sieci** | Klient/nasłuch TCP, UDP, dodatkowe adaptery USB–Ethernet na malinie oraz ekspandery Ethernet/Wi-Fi z ustawieniami kanałów, TCP/UDP i standardowym RFC2217, jeśli sprzęt go obsługuje. Presety wyjaśniają Unitek Y-105, USR-W610 i CH343P TTL. |
| **Własne protokoły** | ASCII/UTF-8/HEX, parametry, końce/długości ramek, kolejność bajtów, SUM/XOR/CRC, pola odpowiedzi, mapowanie stanów, komunikaty spontaniczne i odpytywanie. Profile wielokrotnego użytku z osobnymi adresami instalacji. |
| **Panele WYSIWYG** | Strony, przyciski, przełączniki, fadery, slidery, pokrętła, wartości, kontrolki, tekst i grafiki z dysku; opcjonalne etykiety, ramki, rogi, CSS i warianty PC/tablet/telefon. Edytor i operator używają wspólnego renderera. |
| **Akcje i sekwencje** | Oczekiwanie, timeouty i anulowanie; zezwolenia oraz wzajemne wykluczanie sprawdzane przez silnik dla API i wielu paneli. Jakość sygnału rozróżnia wartości poprawne, przeterminowane, nieznane i błędne. |
| **Publikowanie i praca** | Walidacja, przygotowanie, aktywacja, historia/przywracanie, role administrator/operator, HTTPS i przypięcie certyfikatu. Ustawienia RPi przez WWW z potwierdzeniem/powrotem sieci. Aktualizacje GitHub wszystkich aplikacji Windows i Runtime ze sprawdzeniem SHA256 i powrotem RPi po błędzie uruchomienia. |

Nie ma stałego limitu liczby urządzeń, stron ani bloków. Praktyczna pojemność zależy od kontrolera i obciążenia. Jeden kontroler wykonuje jeden aktywny projekt; Studio przechowuje wiele projektów i połączeń z kontrolerami.

## Zacznij bez sprzętu

1. Zainstaluj **Studio** i zaloguj się do lokalnego symulatora: `admin` / `simulation`.
2. Wybierz **Otwórz projekt szkoleniowy** oraz **Podręcznik szkoleniowy**.
3. Sprawdź przykłady i wybierz **Uruchom symulację**. Przed włączeniem transportów fizycznych zdefiniuj własne polecenia sprzętu.
4. Przygotuj SD aplikacją **Imager**; przed jej wymazaniem potwierdź wybrany nośnik.
5. Opublikuj projekt i obsługuj go w **Playerze** albo panelu WWW kontrolera.

## Nauka i weryfikacja

- [Kurs offline](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/AV-Control-Szkolenie-1.5.5.zip) — **37 rozdziałów, cztery dodatki, 59 ilustracji** i neutralne projekty przykładowe.
- [PDF: 154 strony](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/AV-Control-Studio-Tutorial-PL-Signal-Workshop.pdf) · [Program szkolenia](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/PROGRAM-SZKOLENIA-PL.md) — **osiem sesji / 19 godzin**.
- [Pełna dokumentacja](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/AV-Control-Studio-1.5.5-Dokumentacja.zip) · [Python](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/SYMBOLE-PYTHON-PL.md) · [USB, RS485 i UART](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/USB-RS485-UART-PL.md) · [Ekspandery](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/EKSPANDERY-SIECIOWE-PL.md).
- [Raport weryfikacji](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/WERYFIKACJA-1.5.5.md) · [Manifest budowania i testów](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/RELEASE-MANIFEST.json) · [Sumy SHA256](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/SHA256SUMS.txt).

Szczegółowy kurs i interfejs są obecnie po polsku. README i opisy wydań są w obu językach; wybór znajduje się u góry.

[Fizyczna RPi 4B przeszła aktualizację GitHub 1.5.2 → 1.5.3](docs/WERYFIKACJA-RPI-1.5.3-PO-PUBLIKACJI.md), z zachowaniem projektu, ustawień, kont, sesji i certyfikatu oraz zgodnością pięciu paneli. Testy komputerowe i emulacja ARM64 mają odrębne dowody. Fizyczne 3B/5, rozruch nowej karty, komunikacja elektryczna UART/RS232/RS485/GPIO, zakupione adaptery i rzeczywiste urządzenia mobilne wymagają osobnych prób sprzętowych. Instalatory AV Control nie mają obecnie podpisu Authenticode wydawcy; instalatory producentów są sprawdzane osobno.

## Dystrybucja i licencja

Pobieraj załączniki z sekcji **Assets**. Manifest wiąże sprawdzone paczki z produktem i udanym CI dokładnego commitu. Wersja 1.5 dostarcza skompilowane aplikacje i dokumentację, bez ZIP-a źródeł produktu. Kod bajtowy i pakiety przeglądarkowe nie są szyfrowaniem ani gwarancją ochrony przed analizą. [Szczegóły pakowania](https://github.com/Gartom91/av-control-studio/releases/download/v1.5.5/PAKOWANIE-BINARNE-1.5-PL.md).

Aplikacje nadal korzystają z tego repozytorium do aktualizacji. Podział repozytoriów nie wymaga ponownego zapisu SD ani wymiany projektu. Aktualizacje online i instalacja z PyPI wymagają internetu; praca lokalna pozostaje od nich niezależna.

Wcześniejsze wydania MIT i pochodzący z nich kod zachowują [pierwotne warunki MIT](LICENSE-MIT-1.4.1.txt). MIT nie jest ogólną licencją wszystkich nowych elementów rozwijanych po 1.4.1; zobacz [zakres licencji](LICENSE). Komponenty innych autorów zachowują swoje licencje.

[Projekt przyszłej EULA](EULA-PL-PROJEKT.md) wskazuje osobę fizyczną z placeholderami danych, adresu i kontaktu. Opisuje możliwe przyszłe opłaty; nie uruchamia płatności ani nowych wiążących warunków. Licencjonowanie przez TECHNIKAV pozostaje planowaną usługą opcjonalną.

[Zgłoś błąd lub propozycję](https://github.com/Gartom91/av-control-studio/issues) · [Standard dwujęzycznych wydań](RELEASING.md) · [English](README.en.md)

- [Konta użytkowników i wysuwana klawiatura](docs/KONTA-I-LOGOWANIE-PL.md): logowanie do paneli, własne hasło, administracja i moduł szkoleniowy.
