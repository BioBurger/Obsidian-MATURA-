# Kaj so Funkcije (Functions)?

Funkcija je shranjeni SQL blok, ki **vedno vrne eno vrednost**. Razlikuje se od procedure po tem, da jo kličemo znotraj SQL izrazov (npr. SELECT).

---

## 1. Sintaksa

```sql
DELIMITER //

CREATE FUNCTION ime_funkcije(parameter TIP)
RETURNS povratni_tip
DETERMINISTIC   -- ali NOT DETERMINISTIC
BEGIN
    -- logika
    RETURN vrednost;
END //

DELIMITER ;
```

### DETERMINISTIC vs NOT DETERMINISTIC

| Ključna beseda | Pomen |
|---|---|
| `DETERMINISTIC` | Enaki vhodi → vedno enak izhod |
| `NOT DETERMINISTIC` | Izhod se lahko razlikuje (npr. RAND(), NOW()) |

---

## 2. Primer – osnovna funkcija

```sql
DELIMITER //

CREATE FUNCTION pozdrav(ime VARCHAR(50))
RETURNS VARCHAR(100)
DETERMINISTIC
BEGIN
    RETURN CONCAT('Pozdravljeni, ', ime, '!');
END //

DELIMITER ;

-- Klic
SELECT pozdrav('Janez');
-- Rezultat: Pozdravljeni, Janez!
```

---

## 3. Primer – funkcija z logiko

```sql
DELIMITER //

CREATE FUNCTION starost_kategorija(starost INT)
RETURNS VARCHAR(20)
DETERMINISTIC
BEGIN
    DECLARE kategorija VARCHAR(20);
    
    IF starost < 18 THEN
        SET kategorija = 'Mladoletnik';
    ELSEIF starost < 65 THEN
        SET kategorija = 'Odrasli';
    ELSE
        SET kategorija = 'Upokojenec';
    END IF;
    
    RETURN kategorija;
END //

DELIMITER ;

-- Klic v SELECT
SELECT ime, starost, starost_kategorija(starost) AS kategorija
FROM osebe;
```

---

## 4. Primer – funkcija z izračunom

```sql
DELIMITER //

CREATE FUNCTION ddv_cena(cena DECIMAL(10,2), ddv_procent DECIMAL(5,2))
RETURNS DECIMAL(10,2)
DETERMINISTIC
BEGIN
    RETURN cena * (1 + ddv_procent / 100);
END //

DELIMITER ;

-- Klic
SELECT ime_produkta, cena, ddv_cena(cena, 22) AS cena_z_ddv
FROM produkti;
```

---

## 5. Upravljanje funkcij

```sql
-- Prikaži vse funkcije v bazi
SHOW FUNCTION STATUS WHERE Db = 'mydb';

-- Prikaži kodo funkcije
SHOW CREATE FUNCTION ime_funkcije;

-- Izbriši funkcijo
DROP FUNCTION IF EXISTS ime_funkcije;

-- Posodobitev (izbriši + ustvari)
DROP FUNCTION IF EXISTS ime_funkcije;
CREATE FUNCTION ime_funkcije(...) ...
```

---

## Značilnosti

- **Vrne EN rezultat** — ne more vrniti tabele ali več vrednosti
- **Klic v SELECT** — `SELECT moja_funkcija(stolpec) FROM tabela`
- **Ne more spremeniti podatkov** — brez INSERT/UPDATE/DELETE (v striktnem načinu)
- **DELIMITER** — potreben, ker telo vsebuje `;`