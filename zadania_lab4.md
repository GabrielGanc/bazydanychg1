# Zadanie 1
1.  
```
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
```
INSERT INTO postac (nazwa, rodzaj, data_ur, wiek) VALUES ("Bjorn", "wiking", "1500-03-20", 27);
INSERT INTO postac (nazwa, rodzaj, data_ur, wiek) VALUES ("drozd", "ptak", "1526-07-11", 1);
INSERT INTO postac (nazwa, rodzaj, data_ur, wiek) VALUES ("tesciowa", "kobieta", "1439-11-09", 87);
```
3.
`UPDATE postac SET wiek = 88 WHERE wiek = 87;`
# Zadanie 2
1.
```
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
`ALTER TABLE walizka MODIFY COLUMN kolor ENUM('rozowy', 'czerwony', 'teczowy', 'zolty') default 'rozowy';`  
3.
```
INSERT INTO walizka (pojemnosc, kolor, id_wlasciciela) VALUES (55, "czerwony", 1);
INSERT INTO walizka (pojemnosc, id_wlasciciela) VALUES (40, 2);
```
# Zadanie 3
1.
```
CREATE TABLE izba(
adres_budynku VARCHAR(50),
nazwa_izby VARCHAR(50),
metraz INT UNSIGNED, wlasciciel INT,
CONSTRAINT adres PRIMARY KEY (adres_budynku, nazwa_izby),
FOREIGN KEY (wlasciciel) REFERENCES postac (id_postaci) ON DELETE SET NULL
);
```
2.
`ALTER TABLE izba ADD COLUMN kolor_izby VARCHAR(40) DEFAULT 'czarny' AFTER metraz;`
3.
`INSERT INTO izba (adres_budynku, nazwa_izby, metraz, wlasciciel) VALUES ("Kolobrzeska 9", "Spizarnia", 300, 1);`
# Zadanie 4
1.
```
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
`INSERT INTO przetwory (id_wykonawcy, zawartosc, id_konsumenta) VALUES (1, "bigos", 3);`
# Zadanie 5
1.
```
INSERT INTO postac (nazwa, rodzaj, data_ur, wiek) VALUES
("Askellad", "wiking", "1487-05-17", 40),
("Thorfinn", "wiking", "1508-04-03", 19),
("Thorkell", "wiking", "1492-02-25", 35),
("Sigurd", "wiking", "1470-12-10", 56),
("Olaf", "wiking", "1502-07-21", 25);
```
