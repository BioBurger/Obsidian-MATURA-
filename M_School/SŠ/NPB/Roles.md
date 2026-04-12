# Kaj so Vloge (Roles)?

Vloga (role) je **poimenovana skupek pravic**, ki jo dodelimo uporabnikom. Namesto da vsakemu uporabniku nastavljaš pravice ročno, jih enkrat definiraš v vlogi in vlogo dodeljaš naprej.

---

## 1. Ustvarjanje vloge

```sql
-- Ustvari vlogo
CREATE ROLE 'bralec';
CREATE ROLE 'pisalec';
CREATE ROLE 'admin_vloga';
```

---

## 2. Dodelitev pravic vlogi

```sql
-- Bralec: samo branje
GRANT SELECT ON mydb.* TO 'bralec';

-- Pisalec: branje in pisanje
GRANT SELECT, INSERT, UPDATE, DELETE ON mydb.* TO 'pisalec';

-- Admin: vse
GRANT ALL PRIVILEGES ON mydb.* TO 'admin_vloga';
```

---

## 3. Dodelitev vloge uporabniku

```sql
-- Ustvari uporabnika
CREATE USER 'janez'@'localhost' IDENTIFIED BY 'geslo';
CREATE USER 'ana'@'localhost' IDENTIFIED BY 'geslo';

-- Dodeli vlogo
GRANT 'bralec' TO 'janez'@'localhost';
GRANT 'pisalec' TO 'ana'@'localhost';

-- Dodeli več vlog
GRANT 'bralec', 'pisalec' TO 'janez'@'localhost';
```

---

## 4. Aktivacija vloge

```sql
-- Aktiviraj vlogo v trenutni seji
SET ROLE 'bralec';

-- Aktiviraj vse vloge
SET ROLE ALL;

-- Deaktiviraj vloge
SET ROLE NONE;

-- Nastavi privzeto vlogo (ob prijavi)
SET DEFAULT ROLE 'bralec' FOR 'janez'@'localhost';
```

---

## 5. Pregled in brisanje

```sql
-- Prikaži vse vloge
SELECT * FROM mysql.roles_mapping;

-- Prikaži pravice vloge
SHOW GRANTS FOR 'bralec';

-- Odvzemi vlogo uporabniku
REVOKE 'bralec' FROM 'janez'@'localhost';

-- Izbriši vlogo
DROP ROLE 'bralec';
DROP ROLE IF EXISTS 'bralec';
```

---

## 6. Primer – celoten potek

```sql
-- 1. Ustvari vloge
CREATE ROLE 'app_read';
CREATE ROLE 'app_write';

-- 2. Nastavi pravice
GRANT SELECT ON appdb.* TO 'app_read';
GRANT SELECT, INSERT, UPDATE, DELETE ON appdb.* TO 'app_write';

-- 3. Ustvari uporabnike
CREATE USER 'bralec1'@'localhost' IDENTIFIED BY 'geslo1';
CREATE USER 'pisalec1'@'localhost' IDENTIFIED BY 'geslo2';

-- 4. Dodeli vloge
GRANT 'app_read' TO 'bralec1'@'localhost';
GRANT 'app_write' TO 'pisalec1'@'localhost';

-- 5. Nastavi privzeto vlogo
SET DEFAULT ROLE 'app_read' FOR 'bralec1'@'localhost';
SET DEFAULT ROLE 'app_write' FOR 'pisalec1'@'localhost';
```

---

## Značilnosti

- **Skupinska dodelitev** — ena vloga, veliko uporabnikov
- **Lažje upravljanje** — sprememba vloge vpliva na vse njene člane
- **Aktivacija potrebna** — vloga ni aktivna samodejno brez `SET DEFAULT ROLE`
- **Vloga ≠ uporabnik** — vloga nima gesla, ne more se prijaviti