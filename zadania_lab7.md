# Zadanie 1
1.
```sql
SELECT AVG(waga) AS srednia_waga_wikingow FROM kreatura WHERE rodzaj = 'wiking';
```
2.
```sql
SELECT rodzaj, AVG(waga) AS srednia_waga, COUNT(*) AS ilosc FROM kreatura GROUP BY rodzaj;
```
3.
```sql
SELECT rodzaj, AVG(YEAR(now())-YEAR(dataUr)) AS sredni_wiek FROM kreatura GROUP BY rodzaj;
```
# Zadanie 2
1.
```sql
SELECT rodzaj, SUM(waga) AS suma_wag FROM zasob GROUP BY rodzaj;
```
2.
```sql
SELECT nazwa, AVG(waga*ilosc) AS srednia_waga FROM zasob
WHERE ilosc >= 4 GROUP BY nazwa HAVING SUM(waga*ilosc) > 10;
```
3.
```sql
SELECT rodzaj, COUNT(nazwa) AS ilosc_nazw FROM zasob GROUP BY rodzaj HAVING COUNT(nazwa) > 1;
```
# Zadanie 3
1.
```sql
SELECT k.nazwa, e.ilosc FROM kreatura AS k, ekwipunek AS e WHERE k.idKreatury = e.idKreatury;
```
2.
```sql
SELECT k.nazwa, z.nazwa FROM kreatura AS k, ekwipunek AS e, zasob AS z
WHERE k.idKreatury = e.idKreatury AND z.idZasobu = e.idZasobu;
```
3.
```sql
SELECT k.nazwa FROM kreatura AS k LEFT JOIN ekwipunek AS e
ON k.idKreatury = e.idKreatury WHERE e.idKreatury IS NULL;
```
# Zadanie 4
1.
```sql
SELECT k.nazwa, z.nazwa FROM kreatura AS k, zasob AS z, ekwipunek as e
WHERE k.idKreatury = e.idKreatury AND z.idZasobu = e.idZasobu
AND YEAR(k.dataUr) BETWEEN 1670 AND 1679;
```
2.
```sql
SELECT k.nazwa FROM kreatura AS k, zasob AS z, ekwipunek as e
WHERE k.idKreatury = e.idKreatury AND z.idZasobu = e.idZasobu
AND z.rodzaj = 'jedzenie' ORDER BY dataUr ASC LIMIT 5;
```
3.
```sql
SELECT k2.nazwa, k1.nazwa FROM kreatura AS k1 JOIN kreatura AS k2
ON k1.idKreatury = k2.idKreatury + 5;
```
# Zadanie 5
1.
```sql
SELECT k.rodzaj, AVG(z.waga*e.ilosc) FROM kreatura AS k, zasob AS z, ekwipunek AS e
WHERE k.idKreatury = e.idKreatury AND z.idZasobu = e.idZasobu
AND k.rodzaj != 'malpa' AND k.rodzaj != 'waz' GROUP BY rodzaj HAVING SUM(e.ilosc) < 30;
```
2.
```sql
SELECT rodzaj, MIN(nazwa) AS nazwa_najstaszej, min(dataUr) AS data_ur_najstarszej,
max(nazwa) nazwa_najmlodszej, max(dataUr) data_ur_najmlodszej
FROM kreatura GROUP BY rodzaj;
```
