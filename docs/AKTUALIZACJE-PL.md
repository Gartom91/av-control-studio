# Aktualizacje AV Control z GitHub

Dotyczy Studio, Playera, Imagera i silnika Raspberry Pi. Aktualizację Imagera uruchamia się ręcznie w aplikacji.

## 1. Skąd pochodzą aktualizacje

Studio, Player i RPi pobierają najnowsze stabilne wydanie publicznego repozytorium **Gartom91/av-control-studio**. Wydania robocze i przedpremierowe są pomijane. Od instalacji wersji 1.6.4 aktualizator wymaga też manifestu podpisanego niezależnym kluczem ECDSA; nazwa, rozmiar i SHA256 pakietu muszą być zgodne z tym manifestem. HTTPS korzysta z weryfikacji certyfikatów systemowych. Starszy aktualizator zainstalowany przed 1.6.4 sprawdza wyłącznie dotychczasowe metadane GitHub, dlatego pierwszy przeskok do 1.6.4 nie korzysta jeszcze z tej dodatkowej ochrony.

Domyślnie automatyczne sprawdzanie i instalacja są wyłączone, aby nowa instalacja mogła działać bez internetu. Po jednorazowym włączeniu ustawienia pozostają zapisane. Sterowanie urządzeniami nie wymaga internetu; potrzebuje go tylko pobranie aktualizacji. Błąd sieci jest widoczny w oknie aktualizacji i nie zatrzymuje sterowania.

## 2. Studio i Player na Windows

- **Studio:** otwórz **Ustawienia → Aktualizacje Studio**.
- **Player:** kliknij **Aktualizacje** na górnym pasku. Nie potrzeba konta administratora kontrolera, ponieważ zmieniana jest lokalna aplikacja Windows.
**Imager od 1.6.4:** zakończ zapis karty SD, wybierz **Aktualizacje → Sprawdź aktualizacje → Pobierz i zainstaluj podpisaną aktualizację**, a następnie potwierdź monit Windows. Podniesiony proces Imagera sam pobiera instalator do chronionego katalogu i przed uruchomieniem sprawdza go z podpisanym manifestem. Automatyczne sprawdzanie oraz instalacja są wyłączone. Program wymaga katalogu `Program Files\AV Control Imager`; zainstalowana aplikacja odrzuca zapis karty z innej lokalizacji.

Przejście ze starszego Imagera 1.6.3 wymaga szczególnej uwagi: tamten program nie ma jeszcze wbudowanej weryfikacji podpisu wydania. Pobierz instalator 1.6.4 z [oficjalnych wydań](https://github.com/Gartom91/av-control-studio/releases/latest) i sprawdź jego sumę SHA-256 niezależnie przed pierwszą instalacją. Dopiero następne aktualizacje będą korzystać z mechanizmu podpisu w Imagerze.

Wybierz **Sprawdzaj automatycznie raz dziennie**. Sprawdzanie odbywa się przy uruchomieniu i podczas działania programu, najwyżej raz na dobę po udanym sprawdzeniu. Po błędzie aplikacja ponawia sprawdzenie najwcześniej przy kolejnym sprawdzaniu godzinnym.

Jeżeli zaznaczysz **Pobieraj w tle i instaluj po zamknięciu aplikacji**, program sam pobierze nowy instalator, zweryfikuje go, a po zamknięciu zainstaluje aktualizację i uruchomi program ponownie. Okno aktualizacji pokazuje postęp. Zamknięcie podczas nieukończonego pobierania nie uruchomi niepełnego instalatora. Automatyczna instalacja włącza również sprawdzanie.

Tryb ręczny Studio/Player: **Sprawdź aktualizacje → Pobierz aktualizację → Zainstaluj i uruchom ponownie**. Studio zapisuje bieżący projekt lokalny przed zamknięciem. Instalator używa dotychczasowego katalogu aplikacji i identyfikatora instalacji. Robocze projekty, biblioteka, zapisane połączenia i dane logowania pozostają w magazynie użytkownika.

Zamknięcie Studio lub Playera nie zatrzymuje projektu na RPi. Nie ma obietnicy automatycznego cofnięcia instalatora Windows po błędzie instalacji: komunikat ostatniej instalacji jest dostępny w tym oknie, a poprawny instalator można uruchomić ponownie. Instalatory obecnego wydania nie mają podpisu Authenticode producenta AV Control; podpis manifestu zabezpiecza automatyczną aktualizację Studio/Player/RPi od wersji 1.6.4, ale nie zastępuje podpisu Authenticode pliku instalatora.

## 3. Aktualizacja istniejącego Raspberry Pi

1. Połącz Studio z właściwym RPi i zaloguj się jako administrator.
2. Otwórz **Ustawienia → Aktualizacje Raspberry Pi**. Sprawdź nazwę instalacji i wersję kontrolera.
3. Kliknij **Sprawdź aktualizacje**. Po pobraniu metadanych pojawi się dostępna wersja.
4. Kliknij **Zainstaluj aktualizację RPi**, albo włącz **Instaluj automatycznie w wybranym oknie** i wybierz godzinę 0–23.
5. Obserwuj status. Podczas wymiany silnika połączenie z panelami znika na krótko; aplikacje ponownie odczytują stan kontrolera po jego uruchomieniu.

Można zarządzać aktualizacją również przez Studio w przeglądarce po zalogowaniu jako administrator. Operator nie ma dostępu do ustawień ani API aktualizatora RPi.

Od 1.6.8 pakiet Runtime zawiera również zweryfikowany firmware TAB5. Po aktualizacji maliny pojawia się on w **Ustawienia → Panele M5Stack TAB5 → Wersja do wgrania**. Wybierz właściwe urządzenie i zleć **Aktualizuj firmware** przez Wi-Fi. Aktualizacja TAB5 jest osobnym krokiem po aktualizacji kontrolera; przejścia stron wymagają firmware 0.3.0 oraz ponownego wysłania panelu. Szczegóły: [Instrukcja TAB5](TAB5-PL.md).

Okno automatyczne trwa od wybranej godziny do jej końca, według czasu lokalnego **RPi**, nie komputera PC. Usługa sprawdza warunki co około 15 minut i po rozruchu. Udane sprawdzenie GitHub odbywa się raz dziennie; błąd jest ponawiany nie częściej niż raz na godzinę. Ustaw poprawny zegar i strefę czasową kontrolera. Ręczna instalacja nie czeka na to okno.

Aktualizowany jest pakiet **AV-Control-Runtime-WERSJA-arm64.zip**: silnik, interfejs przeglądarkowy, zależności ARM64 i dokumentacja. Aktualizacja nie zapisuje obrazu na kartę, nie zmienia partycji, ustawień sieciowych, kont systemu Linux, kernela ani Raspberry Pi OS. Nie uruchamiaj Imagera na karcie działającej instalacji w celu aktualizacji, bo Imager służy do przygotowania nowej karty i ją wymazuje.

## 4. Co jest zachowywane i jak działa powrót

Aktualizator najpierw pobiera, weryfikuje i rozpakowuje pakiet, podczas gdy stary silnik nadal działa. Dopiero po przygotowaniu zatrzymuje usługę, kopiuje cały katalog danych **/var/lib/avcontrol** i zamienia katalog programu. Kopia obejmuje aktywny projekt, historię wdrożeń, wybrane pamięci trwałe, użytkowników, sesje, ustawienia aktualizacji i certyfikaty. Dane parowania pozostają te same.

Kontrola uruchomienia sprawdza wersję nowego procesu i jego HTTPS przy użyciu odcisku istniejącego certyfikatu serwera. Gdy nowa wersja nie uruchomi się, aktualizator przywraca stary program oraz dane z kopii i uruchamia go ponownie. Znacznik transakcji pozwala dokończyć powrót po przerwaniu wymiany, także przy następnym rozruchu. Zachowana kopia pozostaje lokalna, dostępna tylko dla usługi systemowej.

Wersja, której instalacja się nie powiodła, nie jest ponownie instalowana automatycznie. Administrator może ponowić próbę ręcznie po usunięciu przyczyny; kolejna nowsza wersja znów kwalifikuje się do instalacji automatycznej.

Wersja cofnięta ręcznie również wymaga ręcznej ponownej instalacji, aby automatyka nie anulowała decyzji administratora.

Po udanej aktualizacji przycisk **Przywróć WERSJA** pozwala wrócić do ostatniej wersji. Przywracane są również dane **sprzed aktualizacji**. Projekty, konta i inne zmiany wykonane później nie znajdują się w tej kopii; przed ręcznym powrotem eksportuj potrzebny aktualny projekt. Przechowywana jest jedna poprzednia wersja.

Restarty stosują ustawienia pamięci projektu: trwałe pamięci są odtwarzane, pozostałe wracają do wartości początkowych. Timery i sekwencje nie są wznawiane, a poprzednie polecenia nie są ponownie wysyłane. Skonfigurowane przez użytkownika akcje startowe wykonują się tak jak podczas zwykłego restartu. Wybierz okno aktualizacji odpowiadające pracy danej instalacji.

Wymagane są wolne miejsce na pakiet, rozpakowanie oraz dwie kopie danych w czasie przywracania. Brak miejsca jest zgłaszany przed wymianą programu. Nie odłączaj zasilania podczas aktualizacji; odzyskiwanie transakcji nie zastępuje odpornej na uszkodzenia karty SD ani kopii poza kontrolerem.

## 5. Starsze wersje i diagnostyka

Obraz 1.3.0 ma nową usługę konfiguracji WWW już zainstalowaną. Przy aktualizacji starszego obrazu 1.2.x jego dotychczasowy aktualizator wymienia runtime, lecz nie potrafi dodać nowej usługi root. Po pobraniu 1.3.0 administrator wykonuje raz `sudo python3 /opt/avcontrol/runtime/avcontrol/system_helpers/install.py` i `sudo systemctl restart avcontrol.service`. Pełna procedura i UART starego obrazu: **KONFIGURACJA-RPI-PL.md**. Kolejne aktualizacje odświeżają usługę automatycznie.

Wersja 1.1 nie miała aktualizatora. Na PC zainstaluj pakiety 1.2 zwykłymi instalatorami. Na istniejącym RPi 1.1 zachowaj dane **/var/lib/avcontrol** i zastosuj procedurę jednorazowej migracji z **BUDOWANIE.md**; od obrazu 1.2 następne wydania można instalować bez ponownego przygotowywania karty.

Administrator systemu może odczytać diagnozę:

```sh
sudo systemctl status avcontrol-update.path avcontrol-update.timer
sudo journalctl -u avcontrol-update.service --no-pager
sudo cat /var/lib/avcontrol-updater/status.json
```

Żądanie z interfejsu trafia do niewielkiego pliku w katalogu danych. Silnik działa jako użytkownik bez uprawnień root; osobna usługa root obsługuje tylko sprawdzenie stałego repozytorium, instalację jego zweryfikowanego pakietu i przywrócenie poprzedniej wersji. Nie przyjmuje dowolnych adresów URL, ścieżek ani poleceń systemowych z projektu.

## 6. Weryfikacja i ograniczenia

Testy aktualizatora obejmują porównanie wersji, weryfikację SHA256, uszkodzony pakiet, niebezpieczne ścieżki ZIP, zachowanie danych, odrzucenie uprawnień operatora, nieudane uruchomienie, powrót i odzyskiwanie przerwanej transakcji. Szczegółowe rzeczywiście wykonane sprawdzenia podaje **WERYFIKACJA-1.3.0.md**. Testy plików i emulatora są oddzielone od testów na fizycznym RPi.

Dokumentacja źródła wydań: https://docs.github.com/en/rest/releases/releases#get-the-latest-release oraz https://docs.github.com/en/rest/releases/assets#get-a-release-asset.
