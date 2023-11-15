# Zadanie 1
1.  
```sql
CREATE TABLE postac(
id_postaci INT NOT NULL AUTO_INCREMENT,  
nazwa VARCHAR(40),  
rodzaj ENUM('wiking', 'ptak', 'kobieta'),  
data_ur DATE,  
wiek INT UNSIGNED,
PRIMARY KEY (id_postaci)
);
```
2.
```sql
INSERT INTO postac (nazwa, rodzaj, data_ur, wiek) VALUES ("Bjorn", "wiking", "1500-03-20", 27);
INSERT INTO postac (nazwa, rodzaj, data_ur, wiek) VALUES ("drozd", "ptak", "1526-07-11", 1);
INSERT INTO postac (nazwa, rodzaj, data_ur, wiek) VALUES ("tesciowa", "kobieta", "1439-11-09", 87);
```
3.
```sql
UPDATE postac SET wiek = 88 WHERE wiek = 87;
```
# Zadanie 2
1.
```sql
CREATE TABLE walizka(
id_walizki INT AUTO_INCREMENT,
pojemnosc INT UNSIGNED,
kolor ENUM('rozowy', 'czerwony', 'teczowy', 'zolty'),
id_wlasciciela INT,
PRIMARY KEY (id_walizki),
FOREIGN KEY (id_wlasciciela) REFERENCES postac (id_postaci) ON DELETE CASCADE
);
```
2.
```sql
ALTER TABLE walizka MODIFY COLUMN kolor ENUM('rozowy', 'czerwony', 'teczowy', 'zolty') default 'rozowy';
```  
3.
```sql
INSERT INTO walizka (pojemnosc, kolor, id_wlasciciela) VALUES (55, "czerwony", 1);
INSERT INTO walizka (pojemnosc, id_wlasciciela) VALUES (40, 2);
```
# Zadanie 3
1.
```sql
CREATE TABLE izba(
adres_budynku VARCHAR(50),
nazwa_izby VARCHAR(50),
metraz INT UNSIGNED, wlasciciel INT,
CONSTRAINT adres PRIMARY KEY (adres_budynku, nazwa_izby),
FOREIGN KEY (wlasciciel) REFERENCES postac (id_postaci) ON DELETE SET NULL
);
```
2.
```sql
ALTER TABLE izba ADD COLUMN kolor_izby VARCHAR(40) DEFAULT 'czarny' AFTER metraz;
```

3.
```sql
INSERT INTO izba (adres_budynku, nazwa_izby, metraz, wlasciciel) VALUES ("Kolobrzeska 9", "Spizarnia", 300, 1);
```
# Zadanie 4
1.
typ year działa tylko od roku 1901 do 2155 razem z 0000
```sql
CREATE TABLE przetwory(
id_przetworu INT AUTO_INCREMENT,
rok_produkcji INT DEFAULT 1654, 
id_wykonawcy INT,
zawartosc VARCHAR(255),
dodatek VARCHAR(50) DEFAULT 'papryczka chilli',
id_konsumenta INT,
PRIMARY KEY (id_przetworu),
FOREIGN KEY (id_wykonawcy) REFERENCES postac (id_postaci),
FOREIGN KEY (id_konsumenta) REFERENCES postac (id_postaci)
);
```
2.
```sql
INSERT INTO przetwory (id_wykonawcy, zawartosc, id_konsumenta) VALUES (1, "bigos", 3);
```
# Zadanie 5
1.
```sql
INSERT INTO postac (nazwa, rodzaj, data_ur, wiek) VALUES
("Askellad", "wiking", "1487-05-17", 40),
("Thorfinn", "wiking", "1508-04-03", 19),
("Thorkell", "wiking", "1492-02-25", 35),
("Sigurd", "wiking", "1470-12-10", 56),
("Olaf", "wiking", "1502-07-21", 25);
```
2.
```sql
CREATE TABLE statek(
nazwa_statku VARCHAR(40),
rodzaj_statku ENUM("Knara", "Drakkar"),
data_wodowania DATE,
max_ladownosc INT UNSIGNED,
PRIMARY KEY (nazwa_statku)
);
```
3.
```sql
INSERT INTO statek (nazwa_statku, rodzaj_statku, data_wodowania, max_ladownosc) VALUES
("Odyn", "Knara", "1520-12-12", 700),
("Heimdall", "Drakkar", "1521-09-11", 900);
```
4.
```sql
ALTER TABLE postac ADD COLUMN funkcja VARCHAR(40);
```
5.
```sql
UPDATE postac SET funkcja = "kapitan" WHERE nazwa = "Bjorn";
```
6.
```sql
ALTER TABLE postac ADD COLUMN statek;
ALTER TABLE postac ADD FOREIGN KEY (statek) REFERENCES statek(nazwa_statku);
```
7.
```sql
UPDATE postac SET statek = "Heimdall" WHERE nazwa != "tesciowa";
```
8.
```sql
DELETE FROM izba WHERE nazwa_izby = "Spizarnia";
```
9.
```sql
DROP TABLE izba;
```
