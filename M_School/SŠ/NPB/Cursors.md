# Kaj so Kurzorji (Cursors)?

Kurzor je mehanizem za **vrstično obdelavo rezultatov poizvedbe** znotraj procedure ali funkcije. Namesto da obdelaš vse vrstice naenkrat, jih obdeluješ eno za drugo.

---

## 1. Življenjski cikel kurzorja
DECLARE → OPEN → FETCH (zanka) → CLOSE

---

## 2. Sintaksa

```sql
-- 1. Deklariraj kurzor
DECLARE ime_kurzorja CURSOR FOR
    SELECT stolpec1, stolpec2 FROM tabela WHERE pogoj;

-- 2. Deklariraj handler za konec
DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = 1;

-- 3. Odpri kurzor
OPEN ime_kurzorja;

-- 4. Beri vrstice
FETCH ime_kurzorja INTO spremenljivka1, spremenljivka2;

-- 5. Zapri kurzor
CLOSE ime_kurzorja;
```

---

## 3. Osnoven primer

```sql
DELIMITER //

CREATE PROCEDURE izpisi_uporabnike()
BEGIN
    DECLARE done INT DEFAULT 0;
    DECLARE v_ime VARCHAR(100);
    DECLARE v_email VARCHAR(100);
    
    -- Deklariraj kurzor
    DECLARE cur CURSOR FOR
        SELECT ime, email FROM users;
    
    -- Handler za NOT FOUND (konec kurzorja)
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = 1;
    
    OPEN cur;
    
    beri: LOOP
        FETCH cur INTO v_ime, v_email;
        IF done = 1 THEN
            LEAVE beri;
        END IF;
        
        -- Obdelaj vrstico
        SELECT CONCAT(v_ime, ' - ', v_email) AS podatki;
    END LOOP;
    
    CLOSE cur;
END //

DELIMITER ;

CALL izpisi_uporabnike();
```

---

## 4. Primer – posodobitev z kurzorjem

```sql
DELIMITER //

CREATE PROCEDURE dodaj_ddv()
BEGIN
    DECLARE done INT DEFAULT 0;
    DECLARE v_id INT;
    DECLARE v_cena DECIMAL(10,2);
    
    DECLARE cur CURSOR FOR
        SELECT id, cena FROM produkti WHERE ddv_vkljucen = 0;
    
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = 1;
    
    OPEN cur;
    
    zanka: LOOP
        FETCH cur INTO v_id, v_cena;
        IF done = 1 THEN LEAVE zanka; END IF;
        
        UPDATE produkti
        SET cena = v_cena * 1.22,
            ddv_vkljucen = 1
        WHERE id = v_id;
    END LOOP;
    
    CLOSE cur;
END //

DELIMITER ;
```

---

## 5. Vrstni red deklaracij (POMEMBNO!)

```sql
BEGIN
    -- 1. Najprej spremenljivke
    DECLARE done INT DEFAULT 0;
    DECLARE v_ime VARCHAR(100);
    
    -- 2. Potem kurzorji
    DECLARE cur CURSOR FOR SELECT ...;
    
    -- 3. Na koncu handlerji
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = 1;
    
    -- 4. Logika
    OPEN cur;
    ...
    CLOSE cur;
END
```

> ⚠️ **Napačen vrstni red deklaracij povzroči napako!**

---

## Značilnosti

- **Vrstično procesiranje** — ena vrstica naenkrat
- **Samo za branje** — kurzor ne more posodabljati (posodobiš z UPDATE WHERE id)
- **Zapri po uporabi** — `CLOSE` sprosti pomnilnik
- **Počasno** — za velike množice raje uporabi množičen UPDATE/INSERT
- **CONTINUE HANDLER** — zazna konec rezultatov (NOT FOUND)