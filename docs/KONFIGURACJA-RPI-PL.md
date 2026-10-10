# Konfiguracja Raspberry Pi przez WWW

Konfigurator jest dostępny dla administratora w zakładce **Raspberry Pi**. Otwórz adres kontrolera, np. **https://av-control.local:8443**, lub połącz z nim Studio na Windows. Zaloguj się kontem AV Control, domyślnie `admin`, i hasłem ustawionym w Imagerze. Konto systemowe SSH, np. `avoperator`, jest osobnym kontem.

## 1. Co można ustawić

- Nazwę kontrolera i jego adres `nazwa.local`.
- Ethernet: automatyczne DHCP albo stały adres IPv4 z prefiksem, bramą i DNS.
- Dodatkowe adaptery USB–Ethernet: rozpoznanie kart, przypisanie konfiguracji do MAC, osobna podsieć oraz rola sieci urządzeń bez przejmowania domyślnej bramy i DNS.
- Wi-Fi: nazwę SSID, hasło WPA Personal, kraj i sieć ukrytą; DHCP lub stałe IPv4.
- UART na GPIO 14/15, domyślnie włączony w nowym obrazie.
- Dostęp SSH dla konta systemowego utworzonego podczas przygotowania karty.
- Strefę czasową, synchronizację NTP i opcjonalny ręczny czas dla instalacji bez internetu.
- Restart kontrolera z potwierdzeniem w interfejsie.

Ekran pokazuje model RPi, temperaturę, wolne miejsce, stan synchronizacji czasu, interfejsy sieciowe, dostępność UART, zalecany adres i odcisk certyfikatu. Operator nie ma dostępu do konfiguracji systemu. Symulator nie zmienia ustawień Windows.

## 2. Pierwsze połączenie

1. W AV Control Imager wybierz model, kartę SD, nazwę, hasło administratora, konto systemowe i opcjonalnie Wi-Fi/SSH. Zapisz kartę i uruchom RPi.
2. Odczytaj `AV-Control-parowanie.txt` i publiczny `AV-Control-CA.crt` z partycji boot albo przez skonfigurowane SSH.
3. W Studio/Player wpisz adres i odcisk SHA256 z parowania. W przeglądarce zaufaj publicznemu CA w magazynie zaufanych certyfikatów urządzenia.
4. Otwórz adres z nazwą kontrolera. Sam adres IP wymaga obecności tego IP w certyfikacie; nazwa `nazwa.local` działa także po zmianie DHCP.
5. Zaloguj się jako administrator i wybierz **Raspberry Pi**.

Prywatnych plików `.key` nie eksportuj. Przycisk **Pobierz publiczny certyfikat CA** pobiera wyłącznie publiczny certyfikat.

## 3. Zapis zwykłych ustawień

1. Zmień wymagane pola nazwy, UART, SSH lub czasu.
2. Kliknij **Sprawdź zmiany konfiguracji**. Walidacja jeszcze niczego nie zapisuje.
3. Przeczytaj podsumowanie. Zmiana UART wymaga restartu; zmiana nazwy odnowi certyfikat HTTPS.
4. Kliknij **Zapisz konfigurację kontrolera** i zaczekaj na komunikat o zapisaniu.
5. Jeśli wymagany jest restart, zaznacz **Potwierdzam restart kontrolera** i kliknij **Uruchom RPi ponownie**.

Nazwa przyjmuje małe litery, cyfry i myślnik, do 63 znaków. Po zmianie nazwy połącz się z nowym `nazwa.local`, odczytaj nowy odcisk i zapisz go w Studio oraz Player. Publiczny CA pozostaje ten sam, więc przeglądarka, która mu ufa, może zweryfikować nowy certyfikat. Projekt i dane kont nie są zastępowane.

## 4. Zmiana sieci z możliwością powrotu

1. Zaznacz **Zmień ustawienia sieci**. Bez tego pola formularz pozostawia sieć bez zmian.
2. Wybierz wykryty interfejs, np. `eth0` lub `wlan0`.
3. Wybierz DHCP albo stały IPv4. Dla stałego adresu wpisz np. `192.168.1.23/24`, właściwą bramę i ewentualne DNS. Sprawdź, że adres jest przeznaczony dla tego kontrolera i nie jest używany przez inne urządzenie.
4. Dla Wi-Fi wpisz SSID i hasło (8–63 bajty lub 64 znaki HEX), kraj `PL` oraz ukrycie SSID, jeśli potrzebne. Obsługiwane są sieci WPA Personal; konfigurator nie konfiguruje uwierzytelniania korporacyjnego 802.1X.
5. Sprawdź zmiany, następnie zapisz. NetworkManager tworzy punkt przywracania dla wybranego interfejsu, a nowy profil pozostaje tymczasowy.
6. Jeśli połączenie zniknie, otwórz ponownie `https://nazwa.local:8443`. W Studio/Player połącz się ponownie z kontrolerem. Od utworzenia punktu przywracania masz **120 sekund**.
7. Po sprawdzeniu dostępu kliknij **Połączenie działa — zachowaj sieć**. Dopiero wtedy nowy profil otrzymuje automatyczne uruchamianie.
8. **Przywróć poprzednią sieć**, brak potwierdzenia lub zamknięcie przeglądarki powodują powrót do poprzednich ustawień. Mechanizm NetworkManager działa niezależnie od otwartego panelu i usługi AV Control.

Puste hasło Wi-Fi zachowuje hasło tylko tej samej aktywnej, zapisanej sieci. Nowy SSID wymaga hasła. Hasła nie trafiają do publicznego stanu ani dziennika audytu; profil NetworkManager jest dostępny tylko dla root. Zmiana jednego interfejsu nie zastępuje konfiguracji pozostałych.

## 5. Dodatkowa sieć USB–Ethernet od wersji 1.4.0

Podłącz adapter do maliny, odśwież listę i wybierz go po oznaczeniu USB–Ethernet oraz MAC. Zaznacz **Sieć urządzeń — bez domyślnej bramy**, metrykę np. 600 oraz wolną podsieć inną od głównej (np. 192.168.50.1/24). Dla połączenia tylko z ekspanderami brama i DNS mogą pozostać puste. Zapis odbywa się z tym samym 120-sekundowym potwierdzeniem. Profil Ethernet wiąże się z MAC i wraca po podłączeniu tej samej karty, także przy innej nazwie interfejsu. Nie powstaje automatycznie serwer DHCP, most ani udostępnianie internetu.

Każdą kolejną kartę skonfiguruj osobno, z inną podsiecią. Nakładające się ręcznie ustawiane podsieci są odrzucane. Aplikacja pokazuje karty obsłużone przez sterownik Raspberry Pi OS. Pełna instrukcja i kreator konwerterów: [USB–Ethernet i ekspandery](EKSPANDERY-SIECIOWE-PL.md); ilustrowane ćwiczenia: [rozdziały 29–32 kursu](tutorial/index.html).

## 6. UART w czystym obrazie

Nowy obraz AV Control ma UART dostępny od pierwszego uruchomienia i wyłączoną konsolę szeregową:

| Model | Port złącza GPIO | Realizacja |
| --- | --- | --- |
| RPi 3B | `/dev/serial0` → `/dev/ttyAMA0` | Pełny PL011; Bluetooth wyłączony na rzecz UART |
| RPi 4B | `/dev/serial0` → `/dev/ttyAMA0` | Pełny PL011; Bluetooth wyłączony na rzecz UART |
| RPi 5 | `/dev/ttyAMA0` | UART0 na GPIO14/15; `serial0` może oznaczać oddzielne złącze debug |

GPIO14/TX to pin fizyczny 8, GPIO15/RX to pin 10, GND np. pin 6. Poziomy wynoszą 3,3 V. Do urządzeń RS-232 lub RS-485 użyj odpowiedniego transceivera. W zakładce **Urządzenia** odśwież listę i wybierz port z tabeli, zamiast przypisywać GPIO14/15 jednocześnie do cyfrowych wyjść.

Dla USB-RS232/485 preferuj `/dev/serial/by-id`. Gdy konwerter nie ma numeru seryjnego, wybierz `/dev/serial/by-path` i używaj tego samego gniazda. USB nie wymaga przełączania UART. Szczegóły: **USB-RS485-UART-PL.md**.

## 7. Czas, restart i aktualizacje

NTP włącza synchronizację wtedy, gdy dostępny jest serwer czasu. W instalacji offline zegar kontynuuje pracę lokalnie. Przy ręcznej zmianie podaj pełną datę ze strefą, np. `2026-10-07T16:00:00+02:00`, i wyłącz NTP. Data musi mieścić się w okresie ważności certyfikatu HTTPS. Timery logiki używają osobnego zegara monotonicznego.

Restart chwilowo rozłącza panele. Nie odtwarza poprzednich żądań wykonania komend; działają tylko akcje startowe zadeklarowane w projekcie. Zachowane pamięci są odczytywane z bazy. API nie pozwala zrestartować kontrolera podczas wykonywania poleceń lub sekwencji. Aktualizacja oprogramowania i konfiguracja systemu korzystają ze wspólnej blokady; nie zatwierdzaj zmiany sieci w trakcie aktualizacji.

## 8. Starszy obraz 1.2.x

Aktualizacja silnika z GitHub zachowuje projekt, ale stary obraz 1.2.x nie ma nowej uprzywilejowanej usługi. Po pobraniu wersji 1.3 administrator systemu wykonuje jednorazowo przez SSH:

```sh
sudo python3 /opt/avcontrol/runtime/avcontrol/system_helpers/install.py
sudo systemctl restart avcontrol.service
```

Ten krok instaluje stałą usługę konfiguratora i włącza API. W świeżym obrazie 1.3 jest już wykonany. Dla wcześniejszego obrazu należy też włączyć UART w nowym konfiguratorze i zrestartować RPi. Kolejne aktualizacje odświeżają usługę automatycznie.

## 9. Diagnostyka i ograniczenia potwierdzenia

Od wersji 1.5.4 sekcja **Panel lokalny HDMI** pozwala włączyć automatyczny kiosk i wybrać stronę początkową. Patrz [szczegółowa instrukcja oraz ćwiczenia HDMI/USB/tty2](PANEL-HDMI-PL.md).

Użyj **Odczytaj ponownie**, aby zastąpić formularz rzeczywistymi ustawieniami kontrolera. Jeżeli usługa jest niedostępna, administrator systemu może sprawdzić:

```sh
sudo systemctl status avcontrol.service avcontrol-config.service
sudo journalctl -u avcontrol-config.service -b --no-pager
readlink -f /dev/serial0
```

Wykrycie portu i poprawne otwarcie nie dowodzą komunikacji z konkretnym urządzeniem. Osobno sprawdza się przewody, parametry transmisji i odpowiedzi urządzenia. Wyniki testów emulatora i fizycznego RPi są opisane w raporcie wydania.

Podstawa konfiguracji: [dokumentacja Raspberry Pi](https://www.raspberrypi.com/documentation/computers/configuration.html#configuring-uarts) oraz [punkty przywracania NetworkManager](https://networkmanager.dev/docs/api/latest/gdbus-org.freedesktop.NetworkManager.html#org-freedesktop-NetworkManager.CheckpointCreate).
