# Zadanie 1
1.
```sql
TRUNCATE TABLE kreatura;
INSERT INTO kreatura SELECT * FROM wikingowie.kreatura;
CREATE TABLE uczestnicy SELECT * FROM wikingowie.uczestnicy;
CREATE TABLE etapy_wyprawy SELECT * FROM wikingowie.etapy_wyprawy;
CREATE TABLE sektor SELECT * FROM wikingowie.sektor;
CREATE TABLE wyprawa SELECT * FROM wikingowie.wyprawa;
```
2.
```sql
SELECT k.nazwa FROM kreatura AS k LEFT JOIN uczestnicy as u
ON k.idKreatury = u.id_uczestnika
WHERE u.id_uczestnika IS NULL;
```
3.
```sql
SELECT w.nazwa, SUM(e.ilosc) AS suma_ekwipunku
FROM uczestnicy AS u, wyprawa AS w, ekwipunek AS e
WHERE u.id_wyprawy = w.id_wyprawy AND u.id_uczestnika = e.idKreatury GROUP BY w.nazwa;
```
# Zadanie 2
1.
```sql
SELECT w.nazwa, COUNT(u.id_uczestnika), GROUP_CONCAT(k.nazwa)
FROM wyprawa AS w, uczestnicy AS u, kreatura AS k
WHERE u.id_wyprawy = w.id_wyprawy AND u.id_uczestnika = k.idKreatury GROUP BY w.nazwa;
```
2.
```sql
SELECT e.kolejnosc, s.nazwa, k.nazwa
FROM etapy_wyprawy AS e, sektor AS s, wyprawa AS w, kreatura AS k
WHERE e.sektor = s.id_sektora AND e.idWyprawy = w.id_wyprawy AND w.kierownik = k.idKreatury
ORDER BY w.data_rozpoczecia, e.kolejnosc;
```
# Zadanie 3
1.
```sql
SELECT s.nazwa, COUNT(e.sektor) AS ilosc_odwiedzin
FROM etapy_wyprawy AS e RIGHT JOIN sektor AS s
ON e.sektor = s.id_sektora GROUP BY s.nazwa;
```
2.
```sql
SELECT k.nazwa, IF(COUNT(u.id_wyprawy) > 0,"brał udział w wyprawie",
"nie brał udziału w wyprawie") AS ilosc_wypraw
FROM kreatura AS k LEFT JOIN uczestnicy AS u 
ON k.idKreatury = u.id_uczestnika GROUP BY k.nazwa;
```
# Zadanie 4
1.
```sql
SELECT w.nazwa, IF(SUM(LENGTH(e.dziennik)) < 400, SUM(LENGTH(e.dziennik)), "") AS znaki
FROM wyprawa AS w LEFT JOIN etapy_wyprawy AS e
ON w.id_wyprawy = e.idWyprawy GROUP BY w.nazwa;
```
2.
```sql
SELECT w.nazwa, SUM(z.waga*e.ilosc)/COUNT(DISTINCT u.id_uczestnika) AS srednia_waga_zasobow
FROM ekwipunek AS e, zasob AS z, wyprawa AS w, uczestnicy AS u
WHERE e.idZasobu = z.idZasobu AND u.id_uczestnika = e.idKreatury AND u.id_wyprawy = w.id_wyprawy
GROUP BY w.nazwa;
```
# Zadanie 5
1.
```sql
SELECT k.nazwa, DATEDIFF(w.data_rozpoczecia, k.dataUr) AS wiek_w_dniach
FROM kreatura AS k, wyprawa AS w, uczestnicy AS u, etapy_wyprawy AS e, sektor AS s
WHERE k.idKreatury = u.id_uczestnika AND w.id_wyprawy = u.id_wyprawy AND
w.id_wyprawy = e.idWyprawy AND s.id_sektora = e.sektor AND s.id_sektora = 7;
```
