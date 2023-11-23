# Zadanie 1
a)
```sql
DELETE FROM postac WHERE rodzaj = "wiking" AND nazwa != "Bjorn" ORDER BY wiek DESC LIMIT 2;
```
b)
```sql
ALTER TABLE postac DROP FOREIGN KEY postac_ibfk_1;
ALTER TABLE walizka DROP FOREIGN KEY walizka_ibfk_1;
ALTER TABLE przetwory DROP FOREIGN KEY przetwory_ibfk_1;
ALTER TABLE przetwory DROP FOREIGN KEY przetwory_ibfk_2;
ALTER TABLE postac MODIFY id_postaci INT;
ALTER TABLE postac DROP PRIMARY KEY;
```
# Zadanie 2
a)
```sql
ALTER TABLE postac ADD pesel CHAR(11);
UPDATE postac SET pesel="76453625431" + id_postaci;
ALTER TABLE postac ADD PRIMARY KEY (pesel);
```
b)
```sql
ALTER TABLE postac MODIFY rodzaj ENUM('wiking', 'ptak', 'kobieta', 'syrena');
```
c)
```sql
INSERT INTO postac (id_postaci, nazwa, rodzaj, data_ur, wiek) VALUES
(9, "Gertruda Nieszczera", "syrena", "1350-05-13", 152);
```
# Zadanie 3
a)
```sql
UPDATE postac SET statek = "Heimdall" WHERE nazwa LIKE "%a%";
```
b)
```sql
UPDATE statek SET max_ladownosc = max_ladownosc*0.7 WHERE data_wodowania > "1521-01-01";
```
c)
```sql
SELECT * FROM postac WHERE wiek > 1000;
```
# Zadanie 4
a)
```sql
INSERT INTO postac (id_postaci, nazwa, data_ur, wiek) VALUES
(10, "Loko", "315-02-22", 1212);
```
b)
```sql
CREATE TABLE marynarz (
id_postaci INT NOT NULL,
nazwa VARCHAR(40),
rodzaj ENUM('wiking','ptak','kobieta','syrena'),
data_ur DATE,
wiek INT UNSIGNED DEFAULT NULL,
funkcja VARCHAR(40),
statek VARCHAR(40),
pesel INT(11)
);
INSERT INTO marynarz
SELECT * FROM postac
WHERE statek != "";
```
c)
```sql
ALTER TABLE marynarz MODIFY pesel INT(11) NOT NULL AUTO_INCREMENT PRIMARY KEY;
```
# Zadanie 5
a)
```sql
UPDATE postac SET statek = "" WHERE statek != "";
UPDATE marynarz SET statek = "" WHERE statek != "";
```
b)
```sql
DELETE FROM postac WHERE nazwa = "Olaf";
DELETE FROM marynarz WHERE nazwa = "Olaf";
```
c)
```sql
DELETE FROM statek;
```
d)
```sql
DROP TABLE statek;
```
e)
```sql
CREATE TABLE zwierz (
id INT NOT NULL AUTO_INCREMENT,
nazwa VARCHAR(40),
wiek INT,
PRIMARY KEY(id)
);
```
f)
```sql
INSERT INTO zwierz (nazwa, wiek)
SELECT nazwa, wiek FROM postac
WHERE rodzaj != "wiking" AND rodzaj != "kobieta" OR nazwa = "Loko";
```
