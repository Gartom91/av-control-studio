# Weryfikacja AV Control 1.5.5

## Zakres

Zarządzanie kontami, zmiana haseł, wymagane logowanie do paneli WWW/Player/HDMI, opcjonalne pamiętanie sesji na 30 dni, wylogowanie z panelu oraz klawiatura ekranowa z Alt/Shift w motywie opublikowanej strony. Poprawiono instalację zależności kiosku offline przy istniejących indeksach APT — przyczynę rzeczywistego wycofania 1.5.4 do działającej 1.5.3.

## Testy

- Windows, silnik: **376 zaliczonych, 12 pominiętych testów platformowych**. Testy kont sprawdzają uprawnienia, własne hasło, reset i zmianę nazwy, odwołanie sesji, ochronę ostatniego administratora, okres sesji, opcjonalne pamiętanie HDMI oraz blokadę dostępu przed logowaniem.
- Interfejs przeglądarkowy: rzeczywiste logowanie, wpisanie `ąĄ!` przez Alt/Shift, cztery rzędy znaków i rząd sterowania bez dodatkowego rzędu akcentów, jednakowe wymiary klawiszy, wysuwanie po wybraniu pola i przeciągnięciu uchwytu, widoczne pole hasła na telefonie, edycja zaznaczenia, Escape przed zamknięciem okna i wyłączenie animacji przy preferencji ograniczonego ruchu, zmiana hasła, rename/reset/delete i wylogowanie zapamiętanej sesji. Widok 390 px jest emulacją telefonu. [Dowód](evidence/accounts-ui-1.5.5.json).
- Kiosk GTK/WebKit w Cage Wayland z wirtualnym ekranem: logowanie i wylogowanie, nawigacja stron, izolowana akcja, blokady okien/adresów/menu, utrata połączenia i restart bez ponowienia polecenia. [Dowód](evidence/hdmi-1.5.5/kiosk-view.json).
- ARM64/QEMU: rzeczywiste procesy, SQLite i HTTPS, aktualizacja starszym aktualizatorem, przywracanie oraz firmware UART trzech modeli. [ARM](evidence/arm-1.5.5.json), [aktualizacja](evidence/update-arm-1.5.5.json), [UART](evidence/uart-clean-image-1.5.5.json), [kiosk w obrazie](evidence/hdmi-1.5.5/image.json).
- Gotowe pakiety: instalacja, natywne próby i odinstalowanie trzech aplikacji Windows; rzeczywisty skompilowany Player Linux; pełny CPython/NumPy i helper w natywnym Studio. Dowody związane z hashami pakietów: [package-verification](evidence/package-verification-1.5.5.json). Publikacja jest blokowana do zakończenia tych prób i wszystkich sześciu zadań CI dla dokładnego commitu.

## Wydajność i dokumentacja

Benchmark Windows obejmuje 100 urządzeń wirtualnych, 2000 bloków i pięć paneli: [normalny ruch](evidence/benchmark-windows-normal-1.5.5.json) i [100 równoległych żądań](evidence/benchmark-windows-1.5.5.json). Wszystkie panele zobaczyły wartość końcową bez błędów komend. Próby prowadzono podczas budowania pakietów; nie stanowią pomiaru wydajności Raspberry Pi. Przy przeciążeniu istotnie wzrosły opóźnienia kolejki — wyniki należy odczytać z raportu, nie traktować jako gwarantowanych czasów reakcji.

PDF Signal Workshop zachowuje poprzednią weryfikację 154 stron, 37 rozdziałów, 4 dodatków i 59 obrazków. Nowa [ilustrowana instrukcja kont](KONTA-I-LOGOWANIE-PL.md) i 60-minutowy moduł uzupełniają go jako osobny materiał. Instrukcja HDMI, program i kurs offline zawierają aktualizacje dotyczące obowiązkowego logowania.

## Sprzęt i granice potwierdzenia

Poprawiona konfiguracja pamięci APT przeszła na fizycznej 4B próbę pobrania offline bez instalacji pakietów. Pełna aktualizacja fizycznej 4B z publicznego wydania i zachowanie jej danych będą miały oddzielny raport po publikacji.

**Nie potwierdzono fizycznego HDMI, myszy/touchpada/dotyku USB ani Ctrl+Alt+F2 na rzeczywistej klawiaturze.** Oba HDMI testowej maliny były odłączone. Emulacja i wirtualny ekran nie zastępują odbioru sprzętowego. Nie potwierdzono także świeżego rozruchu fizycznej karty SD, modeli 3B/5, elektrycznych RS232/RS485/UART/GPIO ani przerwania zasilania podczas aktualizacji. Własny Authenticode pozostaje niedostępny; składniki dostawców są osobno licencjonowane i weryfikowane.
