# Zadanie 1
```sql
SELECT imie, nazwisko, data_urodzenia FROM pracownik;
```
# Zadanie 2
```sql
SELECT imie, nazwisko, YEAR(now()) - YEAR(data_urodzenia) AS wiek FROM pracownik;
```
# Zadanie 3
```sql
SELECT d.nazwa, COUNT(p.id_pracownika) AS liczba_pracownikow FROM pracownik AS p
LEFT JOIN dzial AS d ON p.dzial = d.id_dzialu GROUP BY d.nazwa;
```
# Zadanie 4
```sql
SELECT k.nazwa_kategori, COUNT(t.id_towaru) AS liczba_produktow FROM towar AS t
LEFT JOIN kategoria AS k ON t.kategoria = k.id_kategori GROUP BY nazwa_kategori;
```
# Zadanie 5
```sql
SELECT k.nazwa_kategori, GROUP_CONCAT(t.nazwa_towaru) AS lista_produktow FROM towar AS t
LEFT JOIN kategoria AS k ON t.kategoria = k.id_kategori GROUP BY nazwa_kategori;
```
# Zadanie 6
```sql
SELECT ROUND(AVG(pensja), 2) AS srednie_zarobki FROM pracownik;
```
# Zadanie 7
```sql
SELECT AVG(pensja) AS srednie_zarobki FROM pracownik
WHERE YEAR(now()) - YEAR(data_zatrudnienia) >= 5;
```
# Zadanie 8
```sql
SELECT t.nazwa_towaru, COUNT(p.towar) FROM towar AS t LEFT JOIN pozycja_zamowienia AS p
ON t.id_towaru = p.towar GROUP BY t.nazwa_towaru ORDER BY COUNT(p.towar) DESC LIMIT 10;
```
# Zadanie 9
```sql
SELECT z.numer_zamowienia, SUM(p.cena*p.ilosc) AS wartosc FROM zamowienie AS z
LEFT JOIN pozycja_zamowienia AS p ON z.id_zamowienia = p.zamowienie
WHERE z.data_zamowienia BETWEEN '2017-01-01' AND '2017-03-31' GROUP BY z.numer_zamowienia;
```
# Zadanie 10
```sql
SELECT p.imie, p.nazwisko, SUM(pz.cena*pz.ilosc) AS suma_wartosci FROM pracownik AS p
LEFT JOIN zamowienie AS z ON p.id_pracownika = z.pracownik_id_pracownika
LEFT JOIN pozycja_zamowienia AS pz ON pz.zamowienie = z.id_zamowienia
GROUP BY p.id_pracownika ORDER BY SUM(pz.cena) DESC;
```
