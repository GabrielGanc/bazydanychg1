# Zadanie 1
```sql
SELECT d.nazwa, MIN(p.pensja) AS min_pensja, MAX(p.pensja) AS max_pensja,
AVG(p.pensja) AS srednia_pensja FROM dzial AS d LEFT JOIN pracownik AS p
ON d.id_dzialu = p.dzial GROUP BY d.nazwa;
```
# Zadanie 2
```sql
SELECT k.pelna_nazwa, SUM(p.cena) AS wartosc FROM klient AS k
LEFT JOIN zamowienie AS z ON k.id_klienta = z.klient
LEFT JOIN pozycja_zamowienia AS p ON z.id_zamowienia = p.zamowienie
GROUP BY k.pelna_nazwa ORDER BY SUM(p.cena) DESC LIMIT 10;
```
# Zadanie 3
```sql
SELECT YEAR(z.data_zamowienia), SUM(p.cena) FROM zamowienie AS z
LEFT JOIN pozycja_zamowienia AS p ON z.id_zamowienia = p.zamowienie
GROUP BY YEAR(z.data_zamowienia) ORDER BY SUM(p.cena) DESC;
```
# Zadanie 4
```sql
SELECT SUM(p.cena) FROM pozycja_zamowienia AS p LEFT JOIN zamowienie AS z
ON p.zamowienie = z.id_zamowienia WHERE z.status_zamowienia = 6;
```
# Zadanie 5
```sql
SELECT a.miejscowosc, COUNT(z.id_zamowienia) AS ilosc_zamowien, SUM(p.cena) AS suma_zamowien
FROM pozycja_zamowienia AS p LEFT JOIN zamowienie AS z ON p.zamowienie = z.id_zamowienia
LEFT JOIN adres_klienta AS a ON z.klient = a.klient GROUP BY a.miejscowosc;
```
# Zadanie 6
```sql
SELECT SUM(p.cena) FROM zamowienie AS z LEFT JOIN pozycja_zamowienia AS p
ON z.id_zamowienia = p.zamowienie WHERE status_zamowienia = 5;
```
# Zadanie 7
