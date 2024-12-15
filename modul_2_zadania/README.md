# Moduł 2 - Pierwszy skrypt. Podstawowe typy danych.
> **Ćwiczenia**

1. Napisz fragment kodu, który wczyta trzy zmienne ze standardowego wejścia (np. funkcja input()):
   * linię danych rozdzielonych jakimś separatorem (spacja, średnik, itd.)
   * separator źródłowy
   * separator docelowy  
   
Następnie zaimplementuj z użyciem metod `str.split()` oraz `str.join()` podzielenie danych wejściowych pierwszym separatorem, połączenie i wypisanie danych połączonych drugim separatorem.
Czy można to zrobić prościej wykorzystując inne wbudowane metody?

```python
data = input("Wprowadź dane: ")
źródło = input("Wprowadź separator źródłowy: ")
docelowy = input("Wprowadź separator docelowy: ")
podziel = data.split(źródło)
wynik = docelowy.join(podziel)

# wersja szybsza
wynik = data.replace(źródło, docelowy)
print(wynik)
```

2. Użyj funkcji `input()` aby pobrać łańcuch znaków z klawiatury i z użyciem wycinków (slice) wykonaj:
  * podziel łańcuch na dwie części, w miarę możliwości równe, ale jeżeli długość łańcucha jest nieparzysta, np. 11 znaków to pierwszy ma długość 5, a drugi 6. Wyświetl te łańcuchy w oknie konsoli.
  * wyświetl łańcuch składający się z co drugiego znaku licząc od końca łańcucha

```python
ciąg = "12345678913254"
podział = len(ciąg)
środek = (podział) // 2
pierwsza = ciąg[:środek]
druga = ciąg[środek:]
print("Pierwsza część:", pierwsza)
print("Druga część:", druga)
co_drugi = ciąg[::-2]
print("Co drugi znak od końca:", co_drugi)
```

3. Wyświetl na konsoli dowolny ciąg znaków i wykorzystaj wbudowane metody:
* `title()`, 
* `capitalize()`,
* `zfill()`,
* `upper()`,
* `count()`,
* `center()`.

```python
lista = 'Mam na imię Ala'
print(lista.title())
print(lista.capitalize())
print(lista.zfill(19))
print(lista.upper())
print(lista.count('i'))
print(lista.center(50))
```

4. Wprowadź z klawiatury dowolny łańcuch znaków i zapisz go do zmiennej. Następnie bazując na przykładzie poniżej zapisz również wyniki dla metod `isalpha(), isascii(), isprintable(), istitle(), isupper()`.
`wejscie = input()`
`print(f"Łańcuch {wejscie} isdecimal: {wejscie.isdecimal()}")`.

```python
ciąg = 'Dowolny łańcuch znaków'
print(ciąg.isalpha())
print(ciąg.isascii())
print(ciąg.isprintable())
print(ciąg.istitle())
print(ciąg.isupper())
wejscie = input("Podaj łańcuch znaków: ")
print(f"Łańcuch {wejscie} isdecimal: {wejscie.isdecimal()}")
```

6. Przejdź na stronę https://pyformat.info/, a następnie zapisz w oddzielnym pliku .py i wykonaj 5 wybranych przykładów formatowania ciągów oznaczonego jako „New”, których nie było w przykładach z tego podrozdziału (np. z wyrównaniem do prawej lub lewej strony, ilością pozycji liczby, znakiem, wypełnieniem spacji itp.). Przerób zaprezentowane tam przykłady na postać z użyciem f-string.

```python
osoba = {'imię': 'Ben', 'środkowe': 'Marek', 'nazwisko': 'Biały'}
print('{p[imię]} {p[środkowe]} {p[nazwisko]}'.format(p=osoba))
```


7. Wykorzystując **listing 10** wypisz na konsoli 10 wybranych znaków niestandardowych (np. litery z alfabetu greckiego, symbole walut - (funt, bitcoin)) wypisując jednocześnie jego kod z tablicy unicode.

```python
symbols = [
    ("α"),
    ("β"),
    ("γ"),
    ("£"),
    ("€"),
    ("₿"),
    ("¥"),
    ("∞"),
    ("®"),
    ("§")
]
for symbol in symbols:
    print(f"{symbol} - U+{ord(symbol):08X}")
```
