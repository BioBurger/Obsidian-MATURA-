# Kaj so Indeksi (Indexes)?

Indeks je podatkovna struktura, ki **pospeši iskanje** podatkov v tabeli. Podoben je kazalu v knjigi — namesto da pregleduješ vse strani, greš direktno na pravo stran.

---

## 1. Vrste indeksov

| Vrsta | Opis | Unikatnost |
|---|---|---|
| `PRIMARY KEY` | Primarni ključ, ena na tabelo | ✅ Unikaten + NOT NULL |
| `UNIQUE` | Unikaten indeks | ✅ Unikaten, NULL možen |
| `INDEX` (KEY) | Navaden indeks | ❌ Duplikati OK |
| `FULLTEXT` | Besedilno iskanje | ❌ Za TEXT stolpce |

---

## 2. Ustvarjanje indeksov

```sql
-- Med ustvarjanjem tabele
CREATE TABLE users (
    id      INT         PRIMARY KEY AUTO_INCREMENT,
    email   VARCHAR(100) UNIQUE,
    ime     VARCHAR(50)  NOT NULL,
    priimek VARCHAR(50),
    INDEX idx_priimek (priimek)     -- navaden indeks
);

-- Po ustvarjanju tabele
CREATE INDEX idx_ime ON users (ime);
CREATE UNIQUE INDEX idx_email ON users (email);

-- ALTER TABLE način
ALTER TABLE users ADD INDEX idx_priimek (priimek);
ALTER TABLE users ADD UNIQUE INDEX idx_email (email);
ALTER TABLE users ADD PRIMARY KEY (id);
```

---

## 3. Sestavljeni indeksi (Composite)

```sql
-- Indeks na več stolpcih
CREATE INDEX idx_ime_priimek ON users (priimek, ime);

-- Učinkovit za:
SELECT * FROM users WHERE priimek = 'Novak';          -- ✅
SELECT * FROM users WHERE priimek = 'Novak' AND ime = 'Janez'; -- ✅

-- Neučinkovit za:
SELECT * FROM users WHERE ime = 'Janez';              -- ❌ (brez levega stolpca)
```

> 💡 **Pravilo levega prefiksa** — sestavljeni indeks deluje samo, če poizvedba začne z levim(i) stolpcem.

---

## 4. FULLTEXT indeks

```sql
-- Ustvari
CREATE TABLE clanki (
    id      INT PRIMARY KEY AUTO_INCREMENT,
    naslov  VARCHAR(200),
    vsebina TEXT,
    FULLTEXT ft_vsebina (naslov, vsebina)
);

-- Iskanje z MATCH ... AGAINST
SELECT * FROM clanki
WHERE MATCH(naslov, vsebina) AGAINST('MariaDB indeksi' IN BOOLEAN MODE);
```

---

## 5. Pregled indeksov

```sql
-- Prikaži indekse tabele
SHOW INDEX FROM users;
SHOW KEYS FROM users;

-- V EXPLAIN preveri, ali se indeks uporablja
EXPLAIN SELECT * FROM users WHERE email = 'janez@email.si';
```

### Razlaga EXPLAIN izpisa

| Stolpec | Dobro | Slabo |
|---|---|---|
| `type` | `ref`, `range`, `const` | `ALL` (full scan) |
| `key` | Ime indeksa | `NULL` (indeks se ne uporablja) |
| `rows` | Malo vrstic | Veliko vrstic |

---

## 6. Brisanje indeksov

```sql
-- Izbriši navaden indeks
DROP INDEX idx_ime ON users;
ALTER TABLE users DROP INDEX idx_ime;

-- Izbriši PRIMARY KEY
ALTER TABLE users DROP PRIMARY KEY;
```

---

## 7. Kdaj uporabiti indeks?

```sql
-- ✅ Dobri kandidati za indeks:
-- Stolpci v WHERE pogojih
SELECT * FROM orders WHERE status = 'aktiven';

-- Stolpci v JOIN pogojih
SELECT * FROM orders JOIN users ON orders.user_id = users.id;

-- Stolpci v ORDER BY
SELECT * FROM orders ORDER BY datum_narocila;

-- ❌ Slabi kandidati za indeks:
-- Stolpci z malo unikatnimi vrednostmi (npr. spol: M/Ž)
-- Tabele z malo vrsticami (< 1000)
-- Stolpci, ki se pogosto posodabljajo
```

---

## Značilnosti

- **Pospeši SELECT** — iskanje je O(log n) namesto O(n)
- **Upočasni DML** — vsak INSERT/UPDATE/DELETE posodobi tudi indeks
- **Samodejno za PK** — MariaDB samodejno ustvari indeks za PRIMARY KEY in UNIQUE
- **EXPLAIN je tvoj prijatelj** — vedno preveri z EXPLAIN, ali se indeks dejansko uporablja
- **Ne pretiravaj** — preveč indeksov škodi pisanju, ne koristi branju