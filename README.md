# Katalog Produktów Sklepu Komputerowego – NITiJP

## Temat zbioru danych
Zbiór przedstawia uproszczony **katalog produktów sklepu komputerowego i akcesoriów biurowych**. Zawiera 3 przykładowe pozycje asortymentowe (klawiaturę mechaniczną, monitor 4K oraz mysz bezprzewodową) wraz z ich kluczowymi parametrami handlowymi i magazynowymi: identyfikatorem, nazwą, kategorią, ceną jednostkową, walutą oraz statusem dostępności.

Celem repozytorium jest prezentacja tego samego zestawu informacji w trzech standardach wymiany danych oraz pokazanie różnic w ich strukturze, typowaniu i walidacji.

---

## Zawartość repozytorium

* `dane.xml` – dane katalogu w formacie znacznikowym XML, powiązane ze schematem walidacji.
* `schema.xsd` – schemat XML Schema Definition (XSD), wymuszający poprawną hierarchię i typy pól.
* `dane.json` – te same dane zapisane w formacie obiektowym JSON.
* `dane.csv` – płaska tabela tekstowa rozdzielana przecinkami (kodowanie UTF-8, standard RFC 4180).

---

## Różnice w przedstawieniu danych między formatami

Choć wszystkie pliki przechowują identyczne wartości, każdy format organizuje je w inny sposób:

| Cecha | XML + XSD (`dane.xml`, `schema.xsd`) | JSON (`dane.json`) | CSV (`dane.csv`) |
| :--- | :--- | :--- | :--- |
| **Struktura danych** | Drzewiasta (hierarchiczna), oparta na zagnieżdżonych znacznikach (`<katalog>` -> `<produkt>`). | Obiektowo-tablicowa (klucz-wartość), oparta na nawiasach `{}` oraz tablicy obiektów `[]`. | Płaska (dwuwymiarowa) – wyłącznie wiersze i kolumny bez zagnieżdżeń. |
| **Atrybuty i metadane** | Rozróżnia **elementy** (np. `<nazwa>`) i **atrybuty** przypisane do znacznika (`id="101"`, `waluta="PLN"`). | Brak podziału na atrybuty i elementy – wszystkie cechy są równorzędnymi kluczami obiektu (`"id": 101`, `"waluta": "PLN"`). | Brak obsługi atrybutów i metadanych – każda informacja zajmuje osobną kolumnę. |
| **Typowanie danych** | W samym XML wszystko jest tekstem; ścisłe typy (`xs:positiveInteger`, `xs:decimal`, `xs:boolean`) narzuca dopiero zewnętrzny plik `schema.xsd`. | Wbudowane podstawowe typy bezpośrednio w składni: liczby bez cudzysłowu (`349.99`), wartości logiczne (`true`/`false`), tekst w cudzysłowie. | Brak typowania – wszystkie wartości są traktowane jako zwykły ciąg znaków (tekst) oddzielony przecinkami. |
| **Walidacja poprawności** | Rygorystyczna walidacja struktury, kolejności tagów i typów w oparciu o dołączony schemat XSD. | Walidacja ogranicza się domyślnie do poprawności składniowej (opcjonalnie wymaga osobnego pliku JSON Schema). | Brak wbudowanej walidacji – programy odczytujące muszą same interpretować zawartość kolumn. |
| **Rozmiar i czytelność** | Największa objętość pliku przez powtarzające się znaczniki otwierające i zamykające. | Kompaktowy zapis, bardzo czytelny dla aplikacji webowych i API. | Najmniejszy rozmiar pliku; idealny do szybkiego otwarcia w arkuszach kalkulacyjnych (Excel) lub podglądu w tabeli na GitHubie. |

---

## Model pól

| Pole | Opis | Przykładowa wartość |
| :--- | :--- | :--- |
| `id` | Unikalny numer katalogowy produktu | `101` |
| `nazwa` | Handlowa nazwa urządzenia | `Klawiatura mechaniczna RGB` |
| `kategoria` | Dział asortymentowy | `Akcesoria` |
| `cena` | Cena brutto produktu | `349.99` |
| `waluta` | Kod waluty (w XML jako atrybut elementu `<cena>`) | `PLN` |
| `dostepny` | Informacja, czy towar jest aktualnie na stanie | `true` |
