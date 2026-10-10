# AV Control 1.5.2 — zakres weryfikacji

Raport z 10 października 2026. Studio, Player, Imager i Runtime mają wersję **1.5.2**; Agent zachowuje **1.0.4**. Manifest wydania wiąże dokładny commit produktu, pięć pomyślnych zadań CI i SHA256 każdego załącznika. Dowody komputerowe, pakiety, emulacja ARM64 i fizyczna aktualizacja kontrolera są rozdzielone.

## Zmiany i odbiór interfejsu

- Nawigacja jest po prawej: **selektor projektu → Projekt / Urządzenia / Panele / Logika → konto → motyw → ustawienia**. Selektor ma wyróżnioną ramkę, gradient, widoczną etykietę PROJEKT i podpowiedź pełnej nazwy. Nie zmieniono położenia ikon konta, motywu i ustawień na prawym końcu nagłówka. Test obejmuje kolejność elementów, brak kolizji i szerokości 2200 oraz 1050 pikseli.
- Debugger obsługuje cztery położenia, regulację wysokości i szerokości myszą/klawiaturą, osobno zapisywane proporcje, cały obszar roboczy oraz niezależne okno. Obserwowane sygnały, filtry, karta i zatrzymany ślad pozostają przy przenoszeniu. Okno działa podczas edycji innych kart; zamknięcie przywraca debugger.
- Przetestowano obsługę pól i list po ponownym osadzeniu, zmianę motywu, wymuszenia 1/0, przejście do bloku, wylogowanie oraz wyrównanie portów. Blokada wyskakującego okna i utrata połączenia mają dodatkowy dowód przeglądarkowy. Brak błędów JavaScript.
- Urządzenia i konfiguracja Raspberry Pi wykorzystują pełną dostępną szerokość. Formularz kontekstowy w Logice można rozwinąć.

Próby wykonano w przeglądarce i w **Studio zainstalowanym z końcowego instalatora**, następnie usunięto izolowaną instalację testową. Dowody: `debugger-layout-browser-1.5.2.json`, `debugger-layout-native-1.5.2.json`, `debugger-installed-1.5.2.json`, `installation-1.5.2.json` oraz `native-studio-1.5.2.json` w `docs/evidence` archiwum dokumentacji.

## Silnik i aktualizacja

Naprawiono anulowanie sekwencji przed uruchomieniem jej pierwszego kroku: stan kończy się jako anulowany, a przejściowe zezwolenie zostaje zwolnione. API poprawnie odpowiada także przy ponownym anulowaniu już anulowanego zadania. Test regresji sprawdza, że polecenia nie są wysłane. Lokalny pełny zestaw Windows bazy 1.5.1 (silnik niezmieniony poza numerem wersji): **370 testów zaliczonych, 12 pominiętych**, dwa ostrzeżenia pySerial. Testy wymagające brakującego środowiska nie są dowodem fizycznego sprzętu.

Launchery skompilowanych narzędzi RPi mają prawidłowy interpreter, a systemd wywołuje aktualizator przez Python. Poprawka jest w Runtime i obrazie SD. Emulacja ARM64 na Raspberry Pi OS potwierdza API, SQLite, zachowanie danych po restarcie, logikę i Python, możliwości ekspanderów oraz pakowanie Agenta. Test paczki obejmuje **1.5.1 → 1.5.2**, ręczne przywrócenie poprzedniej wersji i powrót po nieudanym sprawdzeniu zdrowia. Nie jest testem rzeczywistego systemd ani zaniku zasilania.

UART jest włączony w czystym obrazie dla konfiguracji **3B, 4B i 5**, bez konsoli szeregowej. Zweryfikowano konfigurację rozruchową i ustawienia obrazów; fizyczne sygnały elektryczne wymagają odrębnej próby. Dowody: `arm-1.5.2.json`, `uart-clean-image-1.5.2.json`, `update-arm-1.5.2.json`.

Automatyczna instalacja RPi działa w skonfigurowanym oknie nocnym. Publikacja nie wymusza natychmiastowej instalacji. Na już działającym kontrolerze można wybrać sprawdzenie i instalację aktualizacji; ponowne zapisanie karty nie jest wymagane. Wynik rzeczywistej aktualizacji 4B z publicznego GitHuba jest dołączany **oddzielnie po publikacji**.

## Pakiety i Python użytkownika

Studio, Player i Imager Windows przechodzą instalację, test natywnego interfejsu i deinstalację. Imager sprawdza dołączony obraz, trzy modele RPi, ochronę dysku systemowego, zaszyfrowany plan i wymóg potwierdzenia nośnika. Testy **nie zapisują fizycznej karty SD**. Linux Player przechodzi instalację pakietu Debian 13, GTK/WebKit pod Xvfb, HTTPS/pin, panel operatora, pełny ekran, zapamiętanie profilu oraz blokadę sterowania offline bez odtwarzania zaległych akcji.

Studio korzysta z zamrożonego silnika **CPython 3.12.14** i osobnego SDK użytkownika **3.13.15**. Przez natywny interfejs zainstalowano offline **NumPy 2.5.3**, zaimportowano własny helper i uzyskano wyniki 10, 15, 20, 25, 35. Zmiana helpera unieważnia zatwierdzenie administratora. Pełny Python wykonuje zaufany kod z uprawnieniami procesu; nie stanowi piaskownicy bezpieczeństwa. Paczki natywne Windows i ARM64 muszą pasować do architektury i ABI.

Dowody: `companions-installation-1.5.2.json`, `linux-player-1.5.2.json`, `python-native-windows-1.5.2.json`, `package-verification-1.5.2.json`. Ostatni raport wiąże testy z **ośmioma dokładnymi pakietami**: trzy Windows, dwa Linux, Agent, obraz SD i Runtime. Wydanie nie zawiera archiwum źródeł produktu. Zewnętrzne komponenty zachowują swoje licencje; nowy kod produktu jest kompilowany. Kod bajtowy i zasoby przeglądarkowe nie zapewniają ochrony przed analizą.

## Obciążenie i podręcznik

Benchmark Windows obejmuje **100 urządzeń wirtualnych, 2000 bloków i pięć paneli**. W obu próbach wszystkie panele zobaczyły wartość końcową, bez błędów komend. Dla porcji pięciu akcji p95 komendy wyniosło około **242 ms**, p95 skanu **29 ms**, szczyt RSS **79,1 MiB**. Dla porcji 100 akcji: p95 komendy około **3104 ms**, p95 skanu **32 ms**, RSS **83,1 MiB**. Są to pomiary na komputerze Windows podczas przygotowania wydania, bez gwarancji wydajności konkretnej maliny. Pełne dane: `benchmark-windows-normal-1.5.2.json`, `benchmark-windows-1.5.2.json`.

Podręcznik Signal Workshop ma **154 strony, 37 rozdziałów, cztery dodatki i 59 ilustracji**. Rozdział 34 i sesja 4 opisują regulowany układ oraz osobne okno debuggera. Wszystkie strony PDF poddano przeglądowi wizualnemu; manifest wiąże PDF z treścią źródłową. Kurs obejmuje osiem sesji, około 19 godzin, i neutralne projekty demonstracyjne.

## Granice potwierdzenia

Fizyczna aktualizacja istniejącej 4B ma osobny raport po publikacji. Nowa fizyczna karta SD, RPi 3B/5, RS232/RS485/UART/GPIO, zakupione konwertery, USR-W610, dodatkowy USB–Ethernet, zaniki zasilania i fizyczne urządzenia mobilne wymagają własnych prób. Instalatory AV Control nie mają własnego podpisu Authenticode; podpisy dołączonych instalatorów Microsoft i Raspberry Pi są sprawdzane.

## English

Version **1.5.2** includes right-aligned navigation with account/theme/settings remaining at the right edge, four resizable debugger docks and an independent window, full-width configuration, sequence-cancellation fixes and compiled updater startup fixes. Installed Windows acceptance, Linux GTK/WebKit, ARM64 emulation, image/UART checks and package provenance are separate evidence. The **154-page** Polish handbook covers the new debugger. The physical Pi 4B public-release update is reported separately after publication; fresh SD boot and electrical hardware acceptance remain unverified.
