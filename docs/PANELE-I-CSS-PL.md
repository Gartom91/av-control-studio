# Wygląd paneli, grafiki i własny CSS

Dotyczy Studio, Playera i interfejsu Raspberry Pi od wersji 1.2.1. Podgląd edytora i panel operatora używają tego samego renderera. Wygląd, CSS i grafiki są przechowywane w pliku .avctrl; komputer operatora nie potrzebuje plików z dysku autora.

Przejścia fade, wipe, wash, slide i zoom konfiguruje sekcja **Przejście na tę stronę** we właściwościach strony. Podgląd oraz ćwiczenie na pięciu stronach istniejącego szkolenia opisuje [Przejścia stron panelu](PRZEJSCIA-STRON-PL.md).

## 1. Grafika z dysku

1. Otwórz Edytor paneli i dodaj element Grafika.
2. Zaznacz go na panelu lub na liście Warstwy.
3. We Właściwościach elementu kliknij Wybierz grafikę z dysku.
4. Wskaż PNG, JPG lub SVG. Grafika zostanie od razu przypisana do tego elementu i dodana do biblioteki projektu.
5. Ustaw pozycję, szerokość i wysokość oraz Dopasowanie grafiki: cała grafika z zachowaniem proporcji, wypełnienie z przycięciem albo rozciągnięcie.
6. Ustaw Zaokrąglenie, Grubość ramki, Kolor ramki i Styl ramki. Grubość 0 lub styl Bez ramki usuwa obramowanie. Promień 0 daje proste rogi.

Nowa grafika domyślnie nie ma widocznego podpisu. Pokaż etykietę tekstową pozwala go włączyć. Usuń grafikę z elementu odłącza obraz, pozostawiając go w bibliotece dla innych elementów. Możesz też wybrać inny plik lub obraz już zapisany w Grafika z biblioteki.

Przycisk Wygląd strony / CSS pokazuje właściwości strony. Jest tam również Dodaj grafikę do biblioteki, jeśli chcesz wcześniej przygotować obrazy bez przypisywania ich do elementów.

Maksymalny plik ma 20 MB. SVG ma limit 4 MB i musi zawierać samodzielne kształty; skrypty, style i zewnętrzne pliki nie są obsługiwane. Złożone SVG można wyeksportować z programu graficznego do PNG. Nieprawidłowy plik nie zastępuje dotychczasowego obrazu.

## 2. Ukrywanie tekstów

Każdy element ma przełącznik Pokaż etykietę tekstową. Wyłączenie usuwa widoczny tekst z przycisku, przełącznika, suwaka, fadera, pokrętła, wartości, kontrolki, tekstu, grafiki i nawigacji. Nazwa pozostaje w edytorze, na liście warstw i jako dostępna nazwa sterowania; nie musisz usuwać jej z projektu.

Suwaki, fadery, pokrętła i kontrolki mają także Pokaż wartość / stan. Wyłącz go, aby ukryć dodatkowy odczyt lub tekst jakości. Pole wartości zachowuje edytowaną liczbę, ponieważ jest ona samym sterowaniem, a nie podpisem. Ukrycie etykiety elementu Tekst pozostawia pusty element, który można nadal zaznaczyć na liście Warstwy.

Ukrywanie podpisów nie zmienia akcji, odczytów ani dostępności elementu. Tekst powiązany z sygnałem również jest ukrywany. Stare projekty zachowują dotychczasowe etykiety; stare grafiki bez ustawionego podpisu nadal go nie pokazują.

## 3. Wygląd bez kodu

We Właściwościach elementu ustaw kolor i rozmiar tekstu, tło, zaokrąglenie rogów, ramkę, odstęp wewnętrzny, krycie 0–1, wyrównanie i grubość tekstu. Wartości w pikselach dotyczą rozmiaru projektu; podgląd Zoom i skalowanie operatora przeskalowują je razem z elementem.

Grafika ma ramkę na zewnętrznym kontenerze, a obraz jest przycinany do zaokrąglonych rogów. Dopasowanie contain zachowuje cały obraz i może zostawić tło po bokach; cover wypełnia kontener i przycina obraz.

## 4. CSS jednego elementu

Rozwiń Zaawansowany wygląd — CSS elementu. W CSS elementu wpisz same właściwości, bez selektora i nawiasów klamrowych:

```css
background: linear-gradient(135deg, #176582, #123247);
box-shadow: 0 8px 24px #0008;
border: 2px solid #55dec0;
border-radius: 24px;
letter-spacing: 1px;
font-family: Arial, sans-serif;
```

Właściwości są nakładane na główny kontener tego sterowania i nadpisują odpowiadające pola formularza. Usunięcie CSS przywraca wartości formularza. Nie musisz używać !important w tym polu. Pseudoklasy, selektory i reguły @ wpisuj w CSS strony.

W Klasy CSS elementu możesz nadać jedną lub kilka nazw, np. scena glowna. Klasa jest zapisana na kontenerze elementu. Kopia elementu zachowuje klasę i wygląd, ale otrzymuje nowy identyfikator.

## 5. CSS strony i stanów sterowania

Kliknij Wygląd strony / CSS i rozwiń Zaawansowany wygląd — CSS strony. Wpisz normalne reguły CSS:

```css
:scope {
  background: linear-gradient(160deg, #07131f, #163d50) !important;
}
.panel-button {
  font-family: Arial, sans-serif;
  letter-spacing: 0.6px;
}
.scena .panel-button {
  border-color: #4addbe;
}
.scena .panel-button:hover {
  filter: brightness(1.18);
}
.widget-toggle[data-value="true"] .panel-toggle {
  background: #146d56 !important;
}
@media (max-width: 700px) {
  .panel-label { font-size: 14px; }
}
```

:scope oznacza kontener bieżącej strony. .widget obejmuje elementy panelu, a .widget-button, .widget-toggle, .widget-slider, .widget-fader, .widget-knob, .widget-number, .widget-indicator, .widget-text, .widget-image i .widget-navigation wybierają typ. .panel-control wybiera główny kontener sterowania, .panel-label jego podpis, .panel-image sam obraz, .panel-image-frame ramkę grafiki, a output dodatkowy odczyt wartości.

Na kontenerze elementu dostępne są data-widget-id, data-widget-type, data-quality oraz data-value. Dwa ostatnie pokazują jakość i wartość powiązanego sygnału. Stan sterowania bez powiązanego odczytu nie jest potwierdzeniem stanu urządzenia.

Zwykłe reguły CSS strony zmieniają wygląd domyślny. Wartości ustawione bezpośrednio w formularzu lub CSS elementu mają pierwszeństwo; użyj !important w regule strony, jeśli celowo chcesz je zastąpić. CSS strony jest ograniczony do jej panelu i nie zmienia menu Studio ani innych stron.

Obsługiwane są selektory, pseudoklasy, @media i @supports. Wpisuj pełne selektory zamiast zagnieżdżania reguł. Nazwy klas mogą zawierać litery, cyfry, myślniki i podkreślenia, a zaczynać się literą lub podkreśleniem. CSS nie pobiera zasobów: url(), image-set(), @import i @font-face są odrzucane. Obrazy dodajesz przez wybór pliku; fonty wybierasz spośród dostępnych w systemie.

Reguły są parsowane przez przeglądarkę. Błąd jest widoczny we właściwościach; nieobsługiwane właściwości mogą zostać pominięte przez przeglądarkę. Nieprawidłowy zestaw reguł nie wyłącza sterowania. Podgląd aktualizuje się na bieżąco, a Cofnij i Ponów obejmują zmiany wyglądu oraz import.

## 6. Zapis, publikowanie i starszy kontroler

Zapisz projekt przez Zapisz. Po otwarciu na innym PC grafiki, ukryte etykiety i CSS zostaną odtworzone. Opublikuj projekt na silniku co najmniej 1.2.1; Studio pokaże komunikat, jeśli kontroler ma wcześniejszy renderer. Aktualizuj także osobny Player, aby wyświetlał wszystkie nowe ustawienia.

Wygląd jest wspólny dla wariantów PC/tablet/telefon. Ich położenie i rozmiar ustawiasz osobno. Zmiana stylu nie wysyła żadnych poleceń do urządzeń.

Podstawy mechanizmu ograniczania CSS do panelu opisuje standard [CSS Cascading and Inheritance](https://www.w3.org/TR/css-cascade-6/#scoped-styles).
