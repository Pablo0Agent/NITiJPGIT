# Katalog Produktów – NITiJP

Repozytorium zawiera przykładowy, spójny zestaw danych opisujących katalog produktów w trzech popularnych formatach wymiany danych: **XML (wraz ze schematem walidacji XSD)**, **JSON** oraz **CSV**.

## Struktura repozytorium

* `dane.xml` – główne dane katalogu zapisane w formacie XML, powiązane ze schematem walidacji.
* `schema.xsd` – definicja schematu XML (XML Schema Definition), określająca wymaganą strukturę, typy danych (liczby, wartości logiczne) oraz atrybuty.
* `dane.json` – reprezentacja tych samych rekordów w lekkim formacie obiektowym JSON.
* `dane.csv` – płaska struktura tabelaryczna rozdzielana przecinkami (kodowanie UTF-8, standard RFC 4180).

## Model danych

Każdy rekord w katalogu reprezentuje pojedynczy produkt i składa się z następujących pól:

| Pole | Typ danych | Opis | Przykład |
| :--- | :--- | :--- | :--- |
| `id` | Liczba całkowita dodatnia | Unikalny identyfikator produktu | `101` |
| `nazwa` | Tekst (`string`) | Pełna nazwa produktu | `Klawiatura mechaniczna RGB` |
| `kategoria` | Tekst (`string`) | Grupa asortymentowa | `Akcesoria` |
| `cena` | Liczba dziesiętna (`decimal`) | Cena jednostkowa produktu | `349.99` |
| `waluta` | Tekst (`string`) | Kod waluty (atrybut ceny w XML) | `PLN` |
| `dostepny` | Wartość logiczna (`boolean`) | Status dostępności w magazynie (`true`/`false`) | `true` |

## Walidacja i podgląd

* **XML + XSD:** Plik `dane.xml` zawiera odwołanie `xsi:noNamespaceSchemaLocation="schema.xsd"`. Otwarcie projektu w edytorze wspierającym XML (np. Visual Studio Code z rozszerzeniem *Red Hat XML*) automatycznie weryfikuje poprawność danych względem schematu.
* **CSV:** Plik `dane.csv` jest automatycznie renderowany przez GitHuba w formie przeszukiwalnej tabeli bezpośrednio w przeglądarce.
