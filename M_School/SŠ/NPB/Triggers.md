# Kaj so Sprožilci (Triggers)?

Sprožilec je SQL blok, ki se **avtomatično izvede** ob določenem dogodku na tabeli (INSERT, UPDATE, DELETE). Ne klicemo ga ročno — sproži se sam.

---

## 1. Sintaksa

```sql
CREATE TRIGGER ime_triggerja
    {BEFORE | AFTER} {INSERT | UPDATE | DELETE}
    ON ime_tabele
    FOR EACH ROW
BEGIN
    -- logika
END;
```

### Kombinacije

| Čas | Dogodek | Opis |
|---|---|---|
| `BEFORE INSERT` | Pred vstavljanjem | Validacija, sprememba vrednosti |
| `AFTER INSERT` | Po vstavljanju | Logiranje, posodobitev druge tabele |
| `BEFORE UPDATE` | Pred posodobitvijo | Validacija spremembe |
| `AFTER UPDATE` | Po posodobitvi | Revizija, kaskadne posodobitve |
| `BEFORE DELETE` | Pred brisanjem | Preprečitev brisanja |
| `AFTER DELETE` | Po brisanju | Čiščenje, logiranje |

---

## 2. NEW in OLD

```sql
-- NEW = nova vrednost (INSERT, UPDATE)
-- OLD = stara vrednost (UPDATE, DELETE)

BEFORE INSERT:  NEW.stolpec  (OLD ni na voljo)
AFTER INSERT:   NEW.stolpec  (OLD ni na voljo)
BEFORE UPDATE:  OLD.stolpec, NEW.stolpec
AFTER UPDATE:   OLD.stolpec, NEW.stolpec
BEFORE DELETE:  OLD.stolpec  (NEW ni na voljo)
AFTER DELETE:   OLD.stolpec  (NEW ni na voljo)
```

---

## 3. Primer – AFTER INSERT (logiranje)

```sql
DELIMITER //

CREATE TRIGGER log_nov_user
    AFTER INSERT ON users
    FOR EACH ROW
BEGIN
    INSERT INTO audit_log (akcija, user_id, cas)
    VALUES ('DODAN', NEW.id, NOW());
END //

DELIMITER ;

-- Test
INSERT INTO users (ime, email) VALUES ('Janez', 'janez@email.si');
-- Trigger se sproži avtomatično!
SELECT * FROM audit_log;
```

---

## 4. Primer – BEFORE INSERT (validacija)

```sql
DELIMITER //

CREATE TRIGGER preveri_starost
    BEFORE INSERT ON osebe
    FOR EACH ROW
BEGIN
    IF NEW.starost < 0 OR NEW.starost > 150 THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Neveljavna starost!';
    END IF;
END //

DELIMITER ;

-- Test
INSERT INTO osebe (ime, starost) VALUES ('Ana', -5);
-- Napaka: Neveljavna starost!
```

---

## 5. Primer – BEFORE UPDATE (revizija)

```sql
DELIMITER //

CREATE TRIGGER belezi_spremembo_place
    BEFORE UPDATE ON zaposleni
    FOR EACH ROW
BEGIN
    IF OLD.placa <> NEW.placa THEN
        INSERT INTO placa_log (zaposleni_id, stara_placa, nova_placa, datum)
        VALUES (OLD.id, OLD.placa, NEW.placa, NOW());
    END IF;
END //

DELIMITER ;
```

---

## 6. Primer – BEFORE DELETE (preprečitev)

```sql
DELIMITER //

CREATE TRIGGER preprecitev_brisanja_admina
    BEFORE DELETE ON users
    FOR EACH ROW
BEGIN
    IF OLD.vloga = 'admin' THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Adminov ni mogoče brisati!';
    END IF;
END //

DELIMITER ;
```

---

## 7. Upravljanje triggerjev

```sql
-- Prikaži vse triggerje
SHOW TRIGGERS;
SHOW TRIGGERS FROM mydb;

-- Prikaži kodo triggerja
SHOW CREATE TRIGGER ime_triggerja;

-- Izbriši trigger
DROP TRIGGER IF EXISTS ime_triggerja;
```

---

## Značilnosti

- **Avtomatični** — ni potreben ročni klic
- **FOR EACH ROW** — izvede se za vsako vrstico posebej
- **SIGNAL** — sproži napako in prekine akcijo
- **Ne moremo klicati direktno** — samo prek INSERT/UPDATE/DELETE
- **Previdno z zmogljivostjo** — preveč triggerjev upočasni DML operacije