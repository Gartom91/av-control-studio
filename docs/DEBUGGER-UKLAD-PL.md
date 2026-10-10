# Regulowany układ i pełna szerokość konfiguracji

[English](DEBUGGER-LAYOUT-EN.md) | 10 października 2026

W Logice otwórz **Debugger**. Z jego listy wybierz położenie nad, pod, po lewej lub po prawej stronie schematu. Przeciągnij separator, aby zmienić wysokość albo szerokość. Dwuklik daje 50/50; Tab i strzałki umożliwiają regulację klawiaturą. Położenie oraz rozmiary obu podziałów są zapamiętywane osobno.

![Debugger obok schematu](evidence/debugger-layout/debugger-right.png)

**Pełne okno debuggera** przełącza między całym obszarem roboczym a podziałem. **Debugger w osobnym oknie** otwiera niezależny widok Windows lub przeglądarki, który można umieścić na drugim monitorze. W przeglądarce zezwól na otwieranie okien dla Studio. Przenoszenie zachowuje wybraną kartę, pinezki, filtr i zatrzymany ślad. Okno pozostaje aktywne podczas pracy w innych kartach głównego Studio; oba widoki korzystają z tego samego kontrolera i sesji.

![Osobne okno z jasnym motywem](evidence/debugger-layout/debugger-window-light.png)

**Przenieś debugger do Studio** lub zamknięcie osobnego okna przywraca debugger w głównym obszarze Logiki. Wylogowanie i zamknięcie głównej aplikacji zamykają to okno. Przy braku połączenia debugger pokazuje ostrzeżenie i blokuje bodźce. Gdy zwężenie schematu schowa symbole poza widokiem, wybierz **Zmieść schemat**.

Formularz urządzenia i konfiguracja Raspberry Pi wykorzystują pełną dostępną szerokość. Formularz otwarty z Logiki ma dodatkowo przycisk **Rozwiń konfigurację na cały obszar**.

![Formularz urządzenia bez ograniczenia do 1000 pikseli](evidence/debugger-layout/device-full-width.png)

Weryfikacja wersji 1.5.2: [przeglądarka](evidence/debugger-layout-browser-1.5.2.json), [zainstalowane Studio Windows WebView2](evidence/debugger-layout-native-1.5.2.json). Testy używają własnych symulatorów i nie wysyłają poleceń do urządzeń instalacji. Obejmują regulację, zapis ustawień, osobne okno, obsługę pól po powrocie, przejście do bloku z debuggera, motyw, bodźce 1/0, zmianę kart, zwężenie, powrót i wylogowanie. Próby blokady okna i utraty połączenia wykonano w przeglądarce. Brak błędów JavaScript. Wyniki fizycznej aktualizacji RPi są raportowane oddzielnie.

Szczegółowy kurs: [rozdział 34](tutorial/TUTORIAL-PL.md), [sesja 4](tutorial/PROGRAM-SZKOLENIA-PL.md).
