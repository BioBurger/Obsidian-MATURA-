## COLLATE v MariaDB - Popolna razlaga

### Kaj je COLLATE?

**COLLATE** (kolacijski red) je **набор правил za sortiranje in primerjavo znakov** (character strings) v bazi podatkov. Collation ni isto kot character set - character set определава **kako se znaki shranjujejo**, collation pa определава **kako se primerjajo in sortirajo**.[](https://mariadb.com/docs/server/reference/data-types/string-data-types/character-sets/setting-character-sets-and-collations)​
```sql
-- Character set UTF8MB4 bi lahko shranil: "Miha", "Mïha", "Míha"
-- Collation utf8mb4_slovenian_ci določa kako se primerjajo
SELECT * FROM employees WHERE name = 'Mika';  -- Ali vključi 'Míka'?
```
```text
utf8mb4_slovenian_ci
│       │         │
│       │         └─→ Case-Insensitive (malo/velika črka enako)
│       │
│       └──────────→ Jezikovno specifični pravila (slovenščina)
│
└─────────────────→ Character set
```
### 2. **Database level** (privzeto za novo bazo)
```sql
-- Pri kreiranju nove baze
CREATE DATABASE my_slovenian_db
CHARACTER SET 'utf8mb4'
COLLATE 'utf8mb4_slovenian_ci';

-- Ali s priporočenim UCA 14.0.0
CREATE DATABASE my_slovenian_db
COLLATE 'uca1400_slovenian_as_ci';

-- Sprememba obstoječe baze
ALTER DATABASE my_slovenian_db
COLLATE 'utf8mb4_slovenian_ci';

-- Preverjanje
SHOW CREATE DATABASE my_slovenian_db;
```
### 3. **Table level** (privzeto za tabelo)
```sql
-- Pri kreiranju tabele
CREATE TABLE slovenian_employees (
    id INT PRIMARY KEY,
    name VARCHAR(100)
)
CHARACTER SET 'utf8mb4'
COLLATE 'utf8mb4_slovenian_ci';

-- Sprememba obstoječe tabele
ALTER TABLE slovenian_employees
CONVERT TO CHARACTER SET utf8mb4 COLLATE utf8mb4_slovenian_ci;
```
## 1. BINARY Operator

**BINARY** je **operator, ki prisili primerjavo na osnovi binarnih vrednosti (byte-by-byte), namesto karakternih vrednosti (character-by-character)**.[](https://www.sqliz.com/posts/how-binary-operator-works-in-mariadb/)​

### Kako deluje BINARY

- **Brez Collation** - ignorira collation nastavitve in primerjava **natančne byte vrednosti**[](https://mariadb.com/docs/server/reference/sql-functions/string-functions/binary-operator)​
    
- **Case-sensitive** - razlika med malo in veliko črko je **bistvena**[](https://www.sqliz.com/posts/how-binary-operator-works-in-mariadb/)​
    
- **Accent-sensitive** - diakritični znaki so **bistveni** (č ≠ c)[](https://stackoverflow.com/questions/5629111/how-can-i-make-sql-case-sensitive-string-comparison-on-mysql)​
    
- **Trailing spaces** - **prazni prostor na koncu je biten** (razlika od normalnih primerjav)[](https://database.guide/how-the-binary-operator-works-in-mariadb/)​
    

### Sintaksa
```sql
BINARY expression
-- ali
column COLLATE {charset}_bin
```
### Primer
```sql
-- Tabela z utf8mb4_slovenian_ci (case-insensitive collation)
CREATE TABLE users (
    id INT,
    username VARCHAR(100) COLLATE utf8mb4_slovenian_ci
);

INSERT INTO users VALUES 
(1, 'janez'),
(2, 'Janez'),
(3, 'JANEZ');

-- Brez BINARY - case-insensitive (default collation)
SELECT * FROM users WHERE username = 'janez';
-- Rezultat: 3 vrstice (janez, Janez, JANEZ) - vse se ujemajo

-- S BINARY - case-sensitive
SELECT * FROM users WHERE BINARY username = 'janez';
-- Rezultat: 1 vrstica (samo janez)
```
### Razlika med collation
```sql
-- Privzeta collation je case-insensitive
SELECT 'cat' = 'CAT';          -- TRUE (1)
SELECT BINARY 'cat' = 'CAT';   -- FALSE (0)

-- Diakritični znaki (accents)
SELECT 'cas' = 'čas';          -- TRUE (CI collation ignora accent)
SELECT BINARY 'cas' = 'čas';   -- FALSE (BINARY je accent-sensitive)
```
### Trailing spaces - KLJUČNA razlika
```sql
-- Privzeta collation ignora trailing spaces
SELECT 'cat ' = 'cat';           -- TRUE (1) - spaces se ignoriraj
SELECT BINARY 'cat ' = 'cat';    -- FALSE (0) - spaces so bistveni

-- Oboje z BINARY
SELECT BINARY 'cat ' = BINARY 'cat ';  -- TRUE - oba imata 1 space
SELECT BINARY 'cat  ' = BINARY 'cat ';  -- FALSE - različno število spaces
```
### Značilnosti BINARY

- **Byte-by-byte primerjava** - primerjava binarnih vrednosti, ne znakov[](https://mariadb.com/docs/server/reference/sql-functions/string-functions/binary-operator)​
    
- **Case-sensitive IN Accent-sensitive** - hkrati oba[](https://stackoverflow.com/questions/5629111/how-can-i-make-sql-case-sensitive-string-comparison-on-mysql)​
    
- **Trailing spaces so bitni** - razlika od normalnih primerjav[](https://database.guide/how-the-binary-operator-works-in-mariadb/)​
    
- **Performance** - malo hitrejši (ni potrebna collation logika)[](https://www.sqliz.com/posts/how-binary-operator-works-in-mariadb/)​
    
- **Kombinacija s collation** - BINARY = `_bin` collation[](https://database.guide/how-the-binary-operator-works-in-mariadb/)


## 2. Razlika med = in LIKE
### Ključna razlika

|Operator|Namen|Wildcard|Hitrost|Case-sensitive|Trailing spaces|
|---|---|---|---|---|---|
|**=**|Točna primerjava|Ne|**Hitro**|Odvisno od collation|Ignorirani|
|**LIKE**|Pattern matching|Da (%, _)|**Počasno**|Odvisno od collation|**VEDNO bitni**|

### Operator =

**= je operator za TOČNO primerjavo**:[](https://stackoverflow.com/questions/543580/equals-vs-like)
```sql
-- Točna primerjava - ne sprašuje po paternih
SELECT * FROM employees WHERE name = 'Janez';
-- Rezultat: samo Janez (ne janez, ne JANEZ - odvisno od collation)

-- Wildcard znaki so dobesedni
SELECT * FROM employees WHERE name = 'Jan%';
-- Rezultat: samo osebe s pravim imenom "Jan%", ne "Janez"

-- Case-insensitive (privzeto)
SELECT 'janez' = 'JANEZ';        -- TRUE
```
### Operator LIKE

**LIKE je operator za PATTERN MATCHING** z wildcard znaki:[](https://mariadb.com/docs/server/reference/sql-functions/string-functions/like)
```sql
-- Pattern matching - wildcard znaki so obravnavani posebno
SELECT * FROM employees WHERE name LIKE 'Jan%';
-- Rezultat: Janez, Jana, Jan (VSI ki se začnejo z "Jan")

-- Wildcards:
-- % = katero koli število znakov (0 ali več)
-- _ = točno 1 znak

SELECT * FROM employees WHERE name LIKE '_anez';
-- Rezultat: janez, Janez, JANEZ (1. znak je koli kaj, ostalo je "anez")

-- Kombinacija
SELECT * FROM employees WHERE name LIKE 'J_n%';
-- Rezultat: Janez, Jonez, Jani (J + 1 znak + n + ostalo)
```
#### Primerjava - Primeri
```sql
-- Tabela
CREATE TABLE people (ime VARCHAR(100));
INSERT INTO people VALUES ('Janez'), ('Jana'), ('Miha'), ('Jan'), ('Jani');

-- 1. = operator - točna primerjava
SELECT * FROM people WHERE ime = 'Janez';
-- Rezultat: Janez (samo ta)

-- 2. = s Case-insensitive
SELECT * FROM people WHERE ime = 'janez';
-- Rezultat: Janez (collation je case-insensitive)

-- 3. = s Wildcard (dobesedno!)
SELECT * FROM people WHERE ime = 'Jan%';
-- Rezultat: nič (ni osebe z natančnim imenom "Jan%")

-- 4. LIKE - pattern matching
SELECT * FROM people WHERE ime LIKE 'Jan%';
-- Rezultat: Janez, Jana, Jan (vsi ki se začnejo z "Jan")

-- 5. LIKE s podčrtajem
SELECT * FROM people WHERE ime LIKE 'J_n%';
-- Rezultat: Janez, Jana, Jani (J + 1 znak + n + ostalo)

-- 6. LIKE - nič ne vrne
SELECT * FROM people WHERE ime LIKE 'X%';
-- Rezultat: nič (noben se ne začne z X)
```
#### Trailing spaces - RAZLIKA
```sql
-- Privzeto s = operator: trailing spaces se ignoriraj
SELECT 'Janez ' = 'Janez';       -- TRUE (1) - spaces se ignoriraj

-- S LIKE: trailing spaces so VEDNO bitni!
SELECT 'Janez ' LIKE 'Janez';    -- FALSE (0) - space je biten!
SELECT 'Janez ' LIKE 'Janez %';  -- TRUE (1) - space je del patterna

-- S BINARY in =: trailing spaces so bitni
SELECT BINARY 'Janez ' = BINARY 'Janez';  -- FALSE (0)
```

#### Wildcard znaki v LIKE
```sql
-- % = katero koli število znakov (0 ali več)
'Janez' LIKE 'Jan%'       -- TRUE (1)
'Jan' LIKE 'Jan%'         -- TRUE (1) - 0 znakov
'Jani' LIKE 'Jan%'        -- FALSE (0) - 'i' se ne ujema

-- _ = točno 1 znak
'Janez' LIKE 'Ja_ez'      -- TRUE (1) - 'n' je 1 znak
'Jabez' LIKE 'Ja_ez'      -- TRUE (1) - 'b' je 1 znak
'Jaez' LIKE 'Ja_ez'       -- FALSE (0) - manjka 1 znak

-- Kombinacija
'Janez' LIKE 'J%z'        -- TRUE (1) - J + katero koli + z
'test' LIKE 't_s_'        -- TRUE (1) - t + e + s + t = 4 znaki
```
#### LIKE s BINARY - Case-sensitive pattern
```sql
-- Case-insensitive LIKE
SELECT * FROM employees WHERE name LIKE 'jan%';
-- Rezultat: Janez, Jana, Jan (case se ignora)

-- Case-sensitive LIKE
SELECT * FROM employees WHERE BINARY name LIKE 'jan%';
-- Rezultat: nič (malih črk se ne ujema)

SELECT * FROM employees WHERE BINARY name LIKE 'Jan%';
-- Rezultat: Janez, Jana, Jan (samo ti z veliko črko J)
```

## 3. Razlika med CHAR in VARCHAR

### Ključna razlika

|Aspekt|CHAR|VARCHAR|
|---|---|---|
|**Tip**|Fiksna dolžina|Spremenljiva dolžina|
|**Storage**|Vedno N bytov|Do N bytov + 1-2 bytov (length)|
|**Padding**|**Trailing spaces** (zapolnjeno)|Brez paddinga|
|**Hitrost**|**Hitreja** (fixed size)|Počasnejša (variable size)|
|**Disk prostor**|**Več** (vaak je zapravljenega)|**Manj** (samo potrebno)|
|**Index**|**Hitrejši** (predictable)|Počasnejši (fragmentation)|
|**Uporaba**|Fiksne vrednosti|Spremenljive vrednosti|

### CHAR - Fixed Length

**CHAR je fiksne dolžine - vedno zavzame N bytov**:[](https://www.pingcap.com/article/optimizing-database-performance-char-vs-varchar-tips/)
```sql
-- CHAR(5) - vedno 5 znakov
CREATE TABLE test_char (
    id INT,
    status CHAR(5)
);

INSERT INTO test_char VALUES 
(1, 'YES'),    -- Shranjeno kot: 'YES  ' (3 + 2 prazni prostori)
(2, 'NO'),     -- Shranjeno kot: 'NO   ' (2 + 3 prazni prostori)
(3, 'MAYBE');  -- Shranjeno kot: 'MAYBE' (5 znakov)

-- Ko bremo:
SELECT * FROM test_char WHERE id = 1;
-- Rezultat: 'YES  ' (trailing spaces so del vrednosti v memory)

-- LENGTH() ignora trailing spaces
SELECT LENGTH(status) FROM test_char WHERE id = 1;
-- Rezultat: 3 (YES, brez spaces)

-- CHAR_LENGTH() in konkatencija vključuja trailing spaces
SELECT CONCAT('*', status, '*') FROM test_char WHERE id = 1;
-- Rezultat: '*YES  *' (spaces so vidni)
```
### VARCHAR - Variable Length

**VARCHAR je spremenljive dolžine - zavzame samo toliko, kolikor je potrebno**:[](https://www.pingcap.com/article/maximize-storage-with-char-and-varchar-in-tidb/)​
```sql
-- VARCHAR(5) - do 5 znakov
CREATE TABLE test_varchar (
    id INT,
    status VARCHAR(5)
);

INSERT INTO test_varchar VALUES 
(1, 'YES'),    -- Shranjeno kot: 'YES' (3 bytova + 1 length byte = 4)
(2, 'NO'),     -- Shranjeno kot: 'NO' (2 bytova + 1 length byte = 3)
(3, 'MAYBE');  -- Shranjeno kot: 'MAYBE' (5 bytov + 1 length byte = 6)

-- Ko bremo:
SELECT * FROM test_varchar WHERE id = 1;
-- Rezultat: 'YES' (brez trailing spaces)

-- LENGTH() in CHAR_LENGTH() sta enaka
SELECT LENGTH(status) FROM test_varchar WHERE id = 1;
-- Rezultat: 3
```
#### Praktičen primer
```sql
-- Primeri WHERE CHAR je BOLJŠI:
-- Države ISO kode (natančno 2 znaka)
CREATE TABLE countries (
    country_code CHAR(2),    -- ✅ Vedno 2 znaka
    country_name VARCHAR(100) -- ✅ Različne dolžine imen
);

-- Primeri WHERE VARCHAR je BOLJŠI:
-- E-mail naslovi
CREATE TABLE emails (
    email VARCHAR(255)  -- ✅ Različne dolžine
);

-- Opisi produktov
CREATE TABLE products (
    description VARCHAR(1000)  -- ✅ Različne dolžine
);
```

#### Padding in trailing spaces
```sql
-- CHAR avtomatično polni s trailing spaces
CHAR(5) s 'YES' = 'YES  ' (2 spaces)

-- VARCHAR NE polni
VARCHAR(5) s 'YES' = 'YES' (brez spaces)

-- Primerjava:
'YES' = 'YES  '      -- TRUE (collation ignora trailing)
BINARY 'YES' = BINARY 'YES  '  -- FALSE (BINARY je biten)
```
### Nasveti za izbiro

#### Kateri operator uporabiti?

1. **Uporabi =** - ko potrebuješ **točno primerjavo**[](https://www.baeldung.com/sql/queries-equals-vs-like)​
    
    - Večja hitrost
        
    - Boljši indexing
        
    - Bolj jasno
        
2. **Uporabi LIKE** - ko potrebuješ **pattern matching**[](https://www.mariadbtutorial.com/mariadb-basics/mariadb-like/)​
    
    - Iskanje delnih ujemanj
        
    - Wildcard znaki (%, _)
        
    - Fleksibilnejše
        
3. **Uporabi BINARY** - ko potrebuješ **case-sensitive primerjavo**[](https://www.sqliz.com/posts/how-binary-operator-works-in-mariadb/)​
    
    - Passwords
        
    - Identifikatorji s case-sensitive
        
    - Strict data integrity
        

#### Kateri tip uporabiti?

1. **CHAR** - **fiksne vrednosti**[](https://chat2db.ai/resources/blog/key-differences-between-char-and-varchar)​
    
    - Državne kode (ISO): 'US', 'SI', 'DE'
        
    - Spol: 'M', 'F'
        
    - Tip vrednosti s stalno dolžino
        
2. **VARCHAR** - **spremenljive vrednosti**[](https://www.pingcap.com/article/optimizing-database-performance-char-vs-varchar-tips/)​
    
    - Imena: 'Janez', 'Ana', 'Miha'
        
    - Naslovi: različne dolžine
        
    - E-mail: različne dolžine
        
    - Opisi: različne dolžine
## Kaj je generated stolpec

Generated stolpec je posebni stolpec, katerega vrednost se vedno izračuna iz drugih stolpcev v isti vrstici z danim izrazom.[](https://www.postgresql.org/docs/current/ddl-generated-columns.html)​  
To se uporablja za stvari kot so: vsota dveh stolpcev, normalizirane vrednosti, izpeljani podatki (npr. `cena_z_ddv = cena * 1.22`).[](https://www.mysqltutorial.net/mysql-generated-columns/)​

### Sintaksa (MariaDB/MySQL)

Tipičen primer v MariaDB/MySQL:
```sql
CREATE TABLE artikli (
    id          INT PRIMARY KEY,
    cena        DECIMAL(10,2),
    ddv         DECIMAL(10,2)
        GENERATED ALWAYS AS (cena * 0.22)
        STORED,
    cena_z_ddv  DECIMAL(10,2)
        GENERATED ALWAYS AS (cena + ddv)
        VIRTUAL
);
```
- `GENERATED ALWAYS` označi, da je to generiran stolpec.[](https://dev.mysql.com/doc/en/create-table-generated-columns.html)​
    
- `AS (expression)` določi izraz, iz katerega se vrednost izračuna.[](https://dev.mysql.com/doc/en/create-table-generated-columns.html)​
    
- `STORED` (ali `PERSISTENT`) pomeni, da se vrednost izračuna ob `INSERT/UPDATE` in se fizično shrani.[](https://sqlite.org/gencol.html)​
    
- `VIRTUAL` pomeni, da se vrednost ne shranjuje, ampak se izračuna ob branju.[](https://mariadb.com/docs/server/reference/sql-statements/data-definition/create/generated-columns)​
    

### Lastnosti in omejitve

- Generated stolpca ne smeš nastavljati v `INSERT`/`UPDATE`; baza vedno sama izračuna vrednost.[](https://modern-sql.com/caniuse/generated-always-as)​
    
- Izraz mora biti determinističen (brez funkcij tipa `NOW()`, `RAND()` v nekaterih sistemih) in sme uporabljati samo stolpce iste tabele.[](https://dev.to/antozanini/a-complete-guide-to-generated-columns-in-mysql-3n26)​
    

Če želiš, lahko skupaj napiševa konkreten primer za tvojo tabelo (npr. iz dveh stolpcev izračunan tretji).