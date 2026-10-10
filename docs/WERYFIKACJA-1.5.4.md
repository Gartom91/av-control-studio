# Weryfikacja AV Control 1.5.4

## Zakres wydania

Lokalny panel HDMI Raspberry Pi: wykrywanie monitora, uruchamianie i zatrzymywanie sesji Cage/GTK/WebKit, operator bez interfejsu konfiguracji, USB HID/libinput, konsola tty2, strona początkowa i konfiguracja WWW. Rozłączenie urządzenia wejściowego restartuje widok, aby nie odnawiał przytrzymania przycisku; przejście do konsoli nie powoduje wymuszonego powrotu do kiosku. Obraz ma partycję 6 GiB, z zapasem na graficzne zależności i kopię wycofania aktualizacji.

## Weryfikacja programowa

- Windows: **373 testy silnika zaliczone, 12 pominiętych** — platformowe przypadki systemu Linux. Nowe testy obejmują ograniczony klucz operatora, odrzucenie dostępu przez sieć i do administracji, rotację klucza, unieważnienie po wyłączeniu, interlock, aktywny projekt, HDMI hotplug, awarię widoku, konsolę i usunięcie urządzenia wejściowego.
- Natywny GTK/WebKit w **Cage Wayland z wirtualnym ekranem**: panel, strony, suwak, polecenie izolowanego scenariusza, blokada dodatkowych okien i innych adresów, blokada menu kontekstowego i wyjścia z pełnego ekranu, utrata połączenia, powrót i restart bez ponowienia żądania. [Dowód](evidence/hdmi-1.5.4/kiosk-view.json) · [screenshot](hdmi/hdmi-panel.png).
- Czysty obraz ARM64: skompilowane importy GTK/WebKit i mostu operatora, polecenia Cage, osobne konto bez logowania, włączone usługi kiosku/seatd/tty2, brak wpisanych danych dostępu, **186 pakietów systemowych** do aktualizacji offline. [Dowód obrazu](evidence/hdmi-1.5.4/image.json).
- Silnik ARM64 i migracja: rzeczywiste procesy ARM w emulacji QEMU, SQLite, zachowanie projektu/pamięci/certyfikatu, instalacja ze starszym aktualizatorem oraz ręczne i wymuszone wycofanie. [ARM](evidence/arm-1.5.4.json) · [aktualizacja](evidence/update-arm-1.5.4.json).
- UART pozostaje domyślnie włączony; konfiguracja firmware i device tree sprawdzona oddzielnie dla RPi 3B/4B/5. [Dowód](evidence/uart-clean-image-1.5.4.json).

## Pakiety i bramka wydania

Każdy pakiet musi odpowiadać temu samemu odciskowi źródeł. Raport [powiązania dowodów z pakietami](evidence/package-verification-1.5.4.json) zawiera testy instalacji, działania i odinstalowania Studio, Player i Imager, natywnego Studio/Pythona oraz rzeczywistego pakietu Linux. Pełne CI i hashe plików są zawarte w `RELEASE-MANIFEST.json`. Publikacja wymaga pozytywnego wyniku wszystkich kontroli, w tym osobnego testu natywnego kiosku.

Benchmark obejmuje 100 wirtualnych urządzeń, 2000 bloków i pięć paneli. [Normalny ruch](evidence/benchmark-normal-1.5.4.json) oraz [przeciążenie](evidence/benchmark-stress-1.5.4.json) raportowane są oddzielnie. To pomiary na komputerze testowym, nie Raspberry Pi.

Podręcznik PDF: 154 strony, 37 rozdziałów, 4 dodatki i 59 obrazków — zachowane dotychczasowe sprawdzenie wyglądu. Nowa [instrukcja HDMI z obrazkiem i modułem 60 minut](PANEL-HDMI-PL.md) stanowi osobny dodatek. Program szkolenia i archiwum offline zawierają odsyłacz do tego modułu.

## Odbiór sprzętowy i granice dowodów

Wynik aktualizacji fizycznej RPi 4B z publicznego wydania będzie dołączony po publikacji jako osobny raport. Nie utożsamiamy emulacji ani wirtualnego wyświetlacza z odbiorem sprzętowym.

Na stanowisku testowym oba HDMI były odłączone. **Nie potwierdzono fizycznego obrazu HDMI, działania konkretnej myszy/touchpada/dotyku USB ani przejścia Ctrl+Alt+F2 na podłączonej klawiaturze.** Potrzebne jest wykonanie ćwiczeń odbioru z instrukcji na monitorze podłączonym do RPi. Nie potwierdzono także świeżego startu fizycznej karty SD, RPi 3B/5, elektrycznych RS232/RS485/UART/GPIO ani przerwania zasilania w czasie aktualizacji.

Nie zastosowano własnego podpisu Authenticode. Składniki dostawców pozostają osobno licencjonowane; pakiety systemowe pobrano ze standardowo weryfikowanych, podpisanych repozytoriów Debian/Raspberry Pi.
