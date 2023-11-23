# Zadanie 1
1)
```sql
CREATE TABLE kreatura LIKE wikingowie.kreatura;
INSERT INTO kreatura SELECT * FROM wikingowie.kreatura;
CREATE TABLE zasob LIKE wikingowie.zasob;
INSERT INTO zasob SELECT * FROM wikingowie.zasob;
CREATE TABLE ekwipunek LIKE wikingowie.ekwipunek;
INSERT INTO ekwipunek SELECT * FROM wikingowie.ekwipunek;
```
2)
```sql
SELECT * FROM zasob;
```
3)
```sql
SELECT * FROM zasob WHERE rodzaj = "jedzenie";
```
4)
```sql
SELECT idZasobu, ilosc FROM zasob, kreatura WHERE idKreatury IN (1, 3, 5);
```
# Zadanie 2
1)
```sql
SELECT * FROM kreatura WHERE rodzaj != "wiedzma" AND udzwig >= 50;
```
2)
```sql
SELECT * FROM zasob WHERE waga BETWEEN 2 AND 5;
```
3)
```sql
SELECT * FROM kreatura WHERE nazwa LIKE "%or%" AND udzwig BETWEEN 30 AND 70;
```
# Zadanie 3
1)
```sql
SELECT * FROM zasob WHERE MONTH(dataPozyskania) IN (7, 8);
```
2)
```sql
SELECT * FROM zasob WHERE rodzaj != "NULL" ORDER BY waga ASC;
```
3)
```sql
SELECT * FROM kreatura ORDER BY dataUr ASC LIMIT 5;
```
# Zadanie 4
1)
```sql
SELECT DISTINCT rodzaj FROM zasob;
```
2)
```sql
SELECT CONCAT(nazwa, ' - ', rodzaj) AS postac FROM kreatura WHERE rodzaj LIKE "wi%";
```
3)
```sql
SELECT nazwa, ilosc*waga AS calkowita_waga FROM zasob WHERE YEAR(dataPozyskania) BETWEEN 2000 AND 2007;
```
# Zadanie 5
1)
```sql
SELECT nazwa, waga*0.7 AS masa_wlasciwa, waga*0.3 AS waga_odpadkow FROM zasob WHERE rodzaj = "jedzenie";
```
2)
```sql
SELECT * FROM zasob WHERE rodzaj IS NULL;
```
3)
```sql
SELECT DISTINCT nazwa FROM zasob WHERE nazwa LIKE "Ba%" OR nazwa LIKE "%os" ORDER BY nazwa ASC;
```
