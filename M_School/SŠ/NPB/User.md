# Kaj so Uporabniki (Users)?

Uporabnik v MariaDB je identiteta, ki se lahko poveže na strežnik in izvaja SQL ukaze. Vsak uporabnik je sestavljen iz **imena** in **hosta** (od kod se povezuje).

---

## 1. Ustvarjanje uporabnika

```sql
-- Osnovna sintaksa
CREATE USER 'ime'@'host' IDENTIFIED BY 'geslo';

-- Primeri:
CREATE USER 'janez'@'localhost' IDENTIFIED BY 'geslo123';   -- samo lokalno
CREATE USER 'ana'@'%' IDENTIFIED BY 'geslo456';             -- od kjerkoli
CREATE USER 'miha'@'192.168.1.10' IDENTIFIED BY 'geslo789'; -- specifičen IP
```

### Razlaga hostov

| Host | Pomen |
|---|---|
| `localhost` | Samo lokalna povezava |
| `%` | Vse povezave (wildcard) |
| `192.168.1.%` | Subnet |
| `192.168.1.10` | Točen IP |

---

## 2. Pregled uporabnikov

```sql
-- Prikaži vse uporabnike
SELECT User, Host FROM mysql.user;

-- Prikaži trenutnega uporabnika
SELECT CURRENT_USER();

-- Prikaži privilege uporabnika
SHOW GRANTS FOR 'janez'@'localhost';
```

---

## 3. Sprememba gesla

```sql
-- Novo geslo
ALTER USER 'janez'@'localhost' IDENTIFIED BY 'novoGeslo';

-- Alternativno (stari način)
SET PASSWORD FOR 'janez'@'localhost' = PASSWORD('novoGeslo');
```

---

## 4. Brisanje uporabnika

```sql
DROP USER 'janez'@'localhost';

-- Brisanje, če obstaja (brez napake)
DROP USER IF EXISTS 'janez'@'localhost';
```

---

## 5. Primer – celoten potek

```sql
-- 1. Ustvari uporabnika
CREATE USER 'webuser'@'localhost' IDENTIFIED BY 'varnoGeslo!';

-- 2. Dodeli pravice
GRANT SELECT, INSERT, UPDATE ON mydb.* TO 'webuser'@'localhost';

-- 3. Osveži pravice
FLUSH PRIVILEGES;

-- 4. Preveri
SHOW GRANTS FOR 'webuser'@'localhost';

-- 5. Izbriši (ko ni več potreben)
DROP USER 'webuser'@'localhost';
```

---

## Značilnosti

- **User = ime + host** — `'janez'@'localhost'` ≠ `'janez'@'%'`
- **FLUSH PRIVILEGES** — potreben po ročnem urejanju `mysql.user`
- **Varnost** — nikoli ne uporabljaj `%` za admin račune
- **mysql.user** — sistemska tabela z vsemi uporabniki