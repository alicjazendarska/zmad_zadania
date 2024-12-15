# Moduł 3 - Podstawowe struktury danych, część 2.
                                                                                                        
> ## **Zadania**

**Zadanie 1**  
Stwórz listę z wartościami od 1 do 10. Następnie podziel listę tak, aby pierwsze 5 liczb zostało w oryginalnej liście a pozostałe 5 znalazło się w nowej liście.

```python
lista = [1,2,3,4,5,6,7,8,9,10]
ciag= len(lista)//2
pierwsza = lista[:ciag]
druga = lista[ciag:]
print("pierwsza lista:", pierwsza)
print("druga lista:", druga)
```

**Zadanie 2**  
Połącz te listy ponownie. Dodaj do listy wartość „0” na początku. Utwórz kopię połączonej listy i wyświetl listę posortowaną malejąco.

```python
lista_suma = pierwsza + druga
print("razem:", lista_suma)
lista_suma.insert(0,0)
print(lista_suma)
lista_kopia = lista_suma.copy()
lista_kopia.sort(reverse=True)
print(lista_kopia)
import string
from calendar import month
```

**Zadanie 3**  
Napisz skrypt, który pobierze dowolny tekst ze standardowego wejścia poprzez funkcję `input()`. Następnie wyświetl ciąg unikalnych znaków z wczytanego zdania, zapisanych alfabetycznie małymi literami.*
\* wykorzystaj rzutowanie typu `str` na `set` oraz `set` na `list` i użyj funkcji sortującej listę

```python
tekst = input('wpisz swój tekst:')
tekst_2 = tekst.lower()
print(sorted(list(set(tekst_2)), reverse= False))
```

**Zadanie 4**  
Stwórz słownik gdzie kluczami będą numery miesięcy (rozpoczynając od 1) a wartościami nazwy polskich miesięcy.

```python
miesiące = {
        1: "styczeń",
        2: "luty",
        3: "marzec",
        4: "kwiecień",
        5: "maj",
        6: "czerwiec",
        7: "lipiec",
        8: "sierpień",
        9: "wrzesień",
        10: "październik",
        11: "listopad",
        12: "grudzień"}
print(miesiące)
```

**Zadanie 5**  
Stwórz podobny słownik jak w zadaniu 4, ale z angielskimi nazwami miesięcy. Połącz teraz słowniki tak, żeby przykładowo dla kwietnia, dostać się poprzez wyrażenie: months['pl'][4] a dla wersji angielskiej poprzez months['en'][4].

```python
month = {
        1: "january",
        2: "february",
        3: "march",
        4: "april",
        5: "may",
        6: "june",
        7: "july",
        8: "august",
        9: "september",
        10: "october",
        11: "november",
        12: "december"}

razem = {"pl":miesiące, "eng": month}
print(razem["pl"][3])
print(razem["eng"][3])
```

**Zadanie 6**  
Wykorzystując ciąg tekstowy 'Marianna' oraz metodę **fromkeys()** dla słowników stwórz słownik, który będzie zawierał jako klucze unikalne litery w/w imienia a jako wartość każdy klucz będzie miał przypisaną wartość 1.
Poprawne wyjście: `{'M': 1, 'a': 1, 'r': 1, 'i': 1, 'n': 1}`

```python
tekst = 'Marianna'
nowy_tekst = dict.fromkeys(tekst, 1)
print(nowy_tekst)
```

**Zadanie 7**  
Wykorzystaj moduł `string` (dodaje się go poprzez instrukcję `import string` zapisaną zazwyczaj na początku skryptu) i następnie:
* wczytaj ze standardowego wejścia dowolny łańcuch znaków,
* używając formatowania znaków wyświetl ile znaków oraz jaki procent (zamienionych na małe litery) z nich pokrywa się ze zbiorem znaków z: `string.ascii_lowercase, string.digits` (podpowiedź: operator `in` lub przecięcie zbiorów (`set.intersection()`)

```python
import string
data = input("wpisz dowolny ciąg znaków")
letters = set(data.lower()).intersection(string.ascii_letters)
digits = set(data).intersection(string.digits)
print(f'{letters} -> {len(letters)}, {100 * len(letters) / len(string.ascii_lowercase):.1f}%')
print(f'{digits} -> {len(digits)}, {100 * len(digits) / len(string.digits):.1f}%')
```

**Zadanie 8**  
Napisz kod, w którym pobierzesz za pomocą funkcji `input()` 3 wartości przypisując je do zmiennych: start, stop oraz step.
Następnie użyj ich jako parametrów funkcji `range` i wykorzystując przykłady z listingu 10 wypisz wszystkie wartości ciągu wygenerowane przez tę funkcję. Zwróć uwagę na typ danych, który zwraca funkcja `input()` - będzie konieczna konwersja (rzutowanie).

```python
start = int(input("Podaj wartość (start): "))
stop = int(input("Podaj wartość (stop): "))
step = int(input("Podaj wartość (step): "))
range_sequence = range(start, stop, step)
print("Wygenerowane wartości ciągu:")
for value in range_sequence:
    print(value)
print(f"Typ obiektu funkcji range: {type(range_sequence)}")
range_list = list(range_sequence)
print(f"Lista wygenerowanych wartości: {range_list}")
```
