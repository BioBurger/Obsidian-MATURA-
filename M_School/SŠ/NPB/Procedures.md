# Kaj so Procedure (Stored Procedures)?

Procedura je shranjeni SQL blok, ki izvede **zaporedje ukazov**. Za razliko od funkcij ne vrača vrednosti neposredno — namesto tega lahko vrne rezultate prek **OUT parametrov** ali **SELECT stavkov**.

---

## 1. Sintaksa

```sql
DELIMITER //

CREATE PROCEDURE ime_procedure(
    IN  vhodni_param  TIP,
    OUT izhodni_param TIP,
    INOUT dvosmerni   TIP
)
BEGIN
    -- SQL logika
END //

DELIMITER ;

-- Klic
CALL ime_procedure(vrednost, @spremenljivka, @obe);
```

### Vrste parametrov

| Tip | Smer | Opis |
|---|---|---|
| `IN` | Vhod | Vrednost se pošlje v proceduro |
| `OUT` | Izhod | Procedura vrne vrednost |
| `INOUT` | Obe smeri | Pošlje se in vrne nazaj |

---

## 2. Primer – osnovna procedura

```sql
DELIMITER //

CREATE PROCEDURE pozdravi(IN ime VARCHAR(50))
BEGIN
    SELECT CONCAT('Pozdravljeni, ', ime, '!') AS pozdrav;
END //

DELIMITER ;

-- Klic
CALL pozdravi('Janez');
-- Rezultat: Pozdravljeni, Janez!
```

---

## 3. Primer – OUT parameter

```sql
DELIMITER //

CREATE PROCEDURE stevilo_uporabnikov(OUT stevilo INT)
BEGIN
    SELECT COUNT(*) INTO stevilo FROM users;
END //

DELIMITER ;

-- Klic
CALL stevilo_uporabnikov(@rezultat);
SELECT @rezultat;
-- Rezultat: 42 (odvisno od tabele)
```

---

## 4. Primer – pogoji in zanka

```sql
DELIMITER //

CREATE PROCEDURE bonusi(IN min_placa DECIMAL(10,2))
BEGIN
    DECLARE konec INT DEFAULT 0;
    DECLARE id_dela INT;
    DECLARE placa_dela DECIMAL(10,2);
    
    -- Deklaracija kurzorja
    DECLARE cur CURSOR FOR
        SELECT id, placa FROM zaposleni WHERE placa >= min_placa;
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET konec = 1;
    
    OPEN cur;
    
    zanka: LOOP
        FETCH cur INTO id_dela, placa_dela;
        IF konec = 1 THEN LEAVE zanka; END IF;
        
        UPDATE zaposleni
        SET placa = placa_dela * 1.10
        WHERE id = id_dela;
    END LOOP;
    
    CLOSE cur;
END //

DELIMITER ;

-- Klic
CALL bonusi(1000.00);
```

---

## 5. IF / CASE v proceduri

```sql
DELIMITER //

CREATE PROCEDURE ocena_studenta(IN tocke INT, OUT ocena VARCHAR(10))
BEGIN
    IF tocke >= 90 THEN
        SET ocena = 'Odlično';
    ELSEIF tocke >= 75 THEN
        SET ocena = 'Prav dobro';
    ELSEIF tocke >= 60 THEN
        SET ocena = 'Dobro';
    ELSEIF tocke >= 50 THEN
        SET ocena = 'Zadostno';
    ELSE
        SET ocena = 'Nezadostno';
    END IF;
END //

DELIMITER ;

CALL ocena_studenta(82, @oc);
SELECT @oc;
-- Rezultat: Prav dobro
```

---

## 6. Zanke (Loops)

```sql
-- WHILE zanka
WHILE pogoj DO
    -- koda
END WHILE;

-- REPEAT zanka (do-while)
REPEAT
    -- koda
UNTIL pogoj END REPEAT;

-- LOOP (neskončna, z LEAVE)
ime_zanke: LOOP
    IF pogoj THEN LEAVE ime_zanke; END IF;
    -- koda
END LOOP;
```

---

## 7. Upravljanje procedur

```sql
-- Prikaži vse procedure
SHOW PROCEDURE STATUS WHERE Db = 'mydb';

-- Prikaži kodo procedure
SHOW CREATE PROCEDURE ime_procedure;

-- Izbriši proceduro
DROP PROCEDURE IF EXISTS ime_procedure;
```

---

## Primerjava: Funkcija vs Procedura

| | Funkcija | Procedura |
|---|---|---|
| Vrne vrednost | Da (RETURN) | Prek OUT ali SELECT |
| Klic | SELECT func() | CALL proc() |
| V SELECT | ✅ Da | ❌ Ne |
| Sprememba podatkov | Omejena | ✅ Da |
| Več rezultatov | ❌ Ne | ✅ Da |