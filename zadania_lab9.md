# Zadanie 1
1.
```sql
DELIMITER //
CREATE TRIGGER BEFORE_INSERT_kreatura
BEFORE INSERT
ON kreatura
FOR EACH ROW
BEGIN
  IF NEW.waga > 0
  THEN
    SET NEW.waga = 1;
  END IF;
END
//
DELIMITER ;
```
# Zadanie 2
1.
```sql
CREATE TABLE archiwum_wypraw (
id_wyprawy INT NOT NULL AUTO_INCREMENT,
nazwa VARCHAR(100),
data_rozpoczecia DATE,
data_zakonczenia DATE,
kierownik VARCHAR(40),
PRIMARY KEY(id_wyprawy)
);
DELIMITER //
CREATE TRIGGER BEFORE_DELETE_wyprawa
BEFORE DELETE
ON wyprawa
FOR EACH ROW
BEGIN
	INSERT INTO archiwum_wypraw
    SELECT w.id_wyprawy, w.nazwa, w.data_rozpoczecia, w.data_zakonczenia, k.nazwa
    FROM wyprawa AS w INNER JOIN kreatura AS k ON k.idKreatury = w.kierownik
    WHERE id_wyprawy = OLD.id_wyprawy;
END
//
DELIMITER ;
```
# Zadanie 3
1.
```sql
DELIMITER $$
CREATE PROCEDURE eliksir_sily(IN id int)
BEGIN
UPDATE kreatura SET udzwig = udzwig * 1.2 WHERE idKreatury = id;
END
$$
DELIMITER ;
```
2.
```sql
CREATE FUNCTION wielkie_litery (s CHAR(100))
RETURNS CHAR(100)
RETURN (UPPER(s));
```
# Zadanie 4
1.
```sql
CREATE TABLE system_alarmowy (
id_alarmu INT NOT NULL AUTO_INCREMENT,
wiadomosc VARCHAR(255),
PRIMARY KEY(id_alarmu)
);
```
2.
```sql

```
