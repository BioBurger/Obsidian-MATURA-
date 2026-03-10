**View** (pogled) je **virtualna tabela**, ki ne vsebuje podatkov sama, ampak je definirana s SELECT poizvedbo. View-i predstavljajo shranjene poizvedbe, ki jih lahko uporabljaš kot navadne tabele.

## Osnovni CREATE VIEW sintaksa
```sql
CREATE [OR REPLACE]
[ALGORITHM = {UNDEFINED | MERGE | TEMPTABLE}]
[DEFINER = { user | CURRENT_USER | role | CURRENT_ROLE }]
[SQL SECURITY { DEFINER | INVOKER }]
VIEW [IF NOT EXISTS] view_name [(column_list)]
AS select_statement
[WITH [CASCADED | LOCAL] CHECK OPTION]
```

## ALGORITHM - Načini procesiranja view-ov

Algorithm določa, kako MariaDB procesira view.[](https://mariadb.com/docs/server/server-usage/views/view-algorithms)​

### 1. **MERGE** (privzeto prednostno)

- **Princip delovanja**: View definicija in poizvedba, ki uporablja view, se **združita (merge) v eno poizvedbo**[](https://dev.mysql.com/doc/refman/8.1/en/view-algorithms.html)​
    
- **Prednosti**:
    
    - Bolj učinkovito - omogoča uporabo indexov iz osnovnih tabel[](https://stackoverflow.com/questions/42513839/mysql-view-performance-temptable-or-merge)​
        
    - Omogoča UPDATE/INSERT operacije na view-u[](https://www.mysqltutorial.org/mysql-views/mysql-view-processing-algorithms/)​
        
    - Filtri iz glavne poizvedbe se lahko "potisnejo" v view[](https://www.percona.com/blog/a-workaround-for-the-performance-problems-of-temptable-views/)​
        
- **Kdaj se NE more uporabiti MERGE**:[](https://mariadb.com/docs/server/server-usage/views/view-algorithms)​
    
    - Agregacijske funkcije (SUM, COUNT, MAX, MIN, AVG)
        
    - Subquery v SELECT listi
        
    - GROUP BY ali HAVING
        
    - DISTINCT ali UNION
        
    - Samo literalne vrednosti brez osnovnih tabel
    
**Primer MERGE delovanja**:
```sql
-- View definicija
CREATE ALGORITHM=MERGE VIEW v_merge AS 
SELECT * FROM employees WHERE department_id = 1;

-- Tvoja poizvedba
SELECT * FROM v_merge WHERE salary > 3000;

-- MariaDB združi v:
SELECT * FROM employees 
WHERE department_id = 1 AND salary > 3000;
```
### 2. **TEMPTABLE**

- **Princip delovanja**: View **najprej izvrši svojo SELECT poizvedbo in rezultate shrani v začasno tabelo**, šele nato se izvede glavna poizvedba nad to začasno tabelo[](https://dev.mysql.com/doc/refman/8.1/en/view-algorithms.html)​
    
- **Prednosti**:
    
    - Lock-i na osnovnih tabelah se sprostijo prej[](https://mariadb.com/docs/server/server-usage/views/view-algorithms)​
        
    - Uporabno pri kompleksnih view-ih, kjer MERGE ni mogoč[](https://mariadb.com/docs/server/server-usage/views/view-algorithms)​
        
- **Slabosti**:
    
    - **Manj učinkovito** - mora kreirati začasno tabelo in prenesti vse podatke[](https://www.navicat.com/en/company/aboutus/blog/1046-understanding-views-in-relational-databases.html)​
        
    - **NE omogoča UPDATE/INSERT** - view ni updatable[](https://www.mysqltutorial.org/mysql-views/mysql-view-processing-algorithms/)​
        
    - Ne more uporabljati indexov iz osnovnih tabel[](https://stackoverflow.com/questions/42513839/mysql-view-performance-temptable-or-merge)​
        
    - Filtri se ne morejo "potisniti" v view[](https://www.percona.com/blog/a-workaround-for-the-performance-problems-of-temptable-views/)​
        

**Primer TEMPTABLE delovanja**:
```sql
CREATE ALGORITHM=TEMPTABLE VIEW v_temp AS 
SELECT department_id, AVG(salary) as avg_salary 
FROM employees 
GROUP BY department_id;

-- MariaDB najprej kreira temp table z vsemi rezultati,
-- šele nato aplicira dodatne filtre
```
### 3. **UNDEFINED** (privzeto)

- **Princip delovanja**: MariaDB **avtomatično izbere** MERGE ali TEMPTABLE[](https://dev.mysql.com/doc/refman/8.1/en/view-algorithms.html)​
    
- MariaDB preferira MERGE, če je mogoč, sicer uporabi TEMPTABLE[](https://stackoverflow.com/questions/42513839/mysql-view-performance-temptable-or-merge)​
    
- Če definiraš ALGORITHM=MERGE, a view zahteva temporary table, MariaDB avtomatično nastavi UNDEFINED in generira warning[](https://www.mysqltutorial.org/mysql-views/mysql-view-processing-algorithms/)​
    

## SQL SECURITY - Pravice izvajanja

SQL SECURITY določa, **s katerimi pravicami se view izvaja**.[](https://mariadb.com/docs/server/server-usage/stored-routines/stored-functions/stored-routine-privileges)​

### **DEFINER** (privzeto)

- View se izvaja s **pravicami uporabnika, ki je kreiral view** (definer)[](https://dev.mysql.com/doc/refman/8.2/en/create-view.html)​
    
- Vsi uporabniki, ki lahko dostopajo do view-a, lahko izvršijo operacije **ne glede na svoje lastne pravice**[](https://www.getgalaxy.io/learn/keywords/sql-security)
- **Use case**: Dovoli uporabnikom dostop do podatkov brez dajanja direktnih pravic na tabele​
```sql
-- Superuser kreira view
CREATE DEFINER = 'admin'@'localhost'
SQL SECURITY DEFINER
VIEW sensitive_data AS 
SELECT employee_id, name FROM employees;

-- Navaden uporabnik brez pravic na 'employees' lahko vidi podatke preko view-a
```
### **INVOKER**

- View se izvaja s **pravicami uporabnika, ki kliče view** (trenutni uporabnik)[](https://dev.mysql.com/doc/refman/8.2/en/create-view.html)​
    
- Uporabnik mora imeti potrebne pravice na osnovnih tabelah[](https://www.getgalaxy.io/learn/keywords/sql-security)​
    
- **Bolj varno** - preprečuje privilege escalation[](https://dev.mysql.com/doc/refman/8.4/en/stored-objects-security.html)​
```sql
CREATE SQL SECURITY INVOKER
VIEW public_employees AS 
SELECT name, department FROM employees;

-- Vsak uporabnik lahko vidi samo toliko, kolikor mu dovoljujejo njegove pravice
```
## WITH CHECK OPTION - Varovanje konsistentnosti

WITH CHECK OPTION **preprečuje INSERT/UPDATE operacije**, ki bi ustvarile vrstice, ki **ne ustrezajo WHERE pogojem view-a**.[](https://mariadb.com/docs/server/server-usage/views/inserting-and-updating-with-views)
### Osnovna uporaba​
```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    department VARCHAR(50),
    salary INT
);

-- View za IT oddelek
CREATE VIEW it_employees AS 
SELECT * FROM employees 
WHERE department = 'IT'
WITH CHECK OPTION;

-- To bo delovalo
INSERT INTO it_employees VALUES (1, 'Janez', 'IT', 3000);

-- To bo ZAVRNILO - department ni 'IT'
INSERT INTO it_employees VALUES (2, 'Ana', 'HR', 2500);
-- ERROR 1369 (HY000): CHECK OPTION failed
```
### **LOCAL** vs **CASCADED**

Pri view-ih, ki so kreirani na osnovi drugih view-ov, se razlikujeta dva načina preverjanja.[](https://www.mysqltutorial.org/mysql-views/mysql-view-with-local-check-option-vs-with-cascaded-check-option/)​

#### **CASCADED** (privzeto)

- Preverja pogoje **trenutnega view-a IN VSEH podrejenih view-ov rekurzivno**[](https://mariadb.com/docs/server/server-usage/views/inserting-and-updating-with-views)​
    
- Dodaja WITH CASCADED CHECK OPTION vsem underlying view-om (samo za namen preverjanja)[](https://docs.oracle.com/cd/E17952_01/mysql-5.7-en/view-check-option.html)
​
```sql
CREATE TABLE t1 (c INT);

-- v1: c < 20 (brez CHECK OPTION)
CREATE VIEW v1 AS SELECT * FROM t1 WHERE c < 20;

-- v2: c > 10 (WITH CASCADED CHECK OPTION)
CREATE VIEW v2 AS SELECT * FROM v1 WHERE c > 10 
WITH CASCADED CHECK OPTION;

-- v3: c < 15 (WITH CASCADED CHECK OPTION)
CREATE VIEW v3 AS SELECT * FROM v2 WHERE c < 15 
WITH CASCADED CHECK OPTION;

-- INSERT preko v3:
INSERT INTO v3 VALUES (12);  -- OK: 12 < 15 (v3), 12 > 10 (v2), 12 < 20 (v1)
INSERT INTO v3 VALUES (8);   -- ZAVRNJENO: 8 < 10 (ne ustreza v2)
INSERT INTO v3 VALUES (16);  -- ZAVRNJENO: 16 >= 15 (ne ustreza v3)
INSERT INTO v3 VALUES (25);  -- ZAVRNJENO: 25 >= 20 (ne ustreza v1)
```

#### **LOCAL**

- Preverja pogoje **samo tistih view-ov, ki imajo WITH CHECK OPTION** (LOCAL ali CASCADED)[](https://www.mysqltutorial.org/mysql-views/mysql-view-with-local-check-option-vs-with-cascaded-check-option/)​
    
- NE preverja view-ov brez CHECK OPTION[](https://www.ibm.com/docs/en/i/7.5.0?topic=view-local-check-option)​
```sql
CREATE TABLE t1 (c INT);

-- v1: c < 20 (brez CHECK OPTION)
CREATE VIEW v1 AS SELECT * FROM t1 WHERE c < 20;

-- v2: c > 10 (WITH LOCAL CHECK OPTION)
CREATE VIEW v2 AS SELECT * FROM v1 WHERE c > 10 
WITH LOCAL CHECK OPTION;

-- v3: c < 15 (WITH LOCAL CHECK OPTION)
CREATE VIEW v3 AS SELECT * FROM v2 WHERE c < 15 
WITH LOCAL CHECK OPTION;

-- INSERT preko v3:
INSERT INTO v3 VALUES (12);  -- OK: 12 < 15 (v3), 12 > 10 (v2)
INSERT INTO v3 VALUES (8);   -- ZAVRNJENO: 8 < 10 (ne ustreza v2)
INSERT INTO v3 VALUES (16);  -- ZAVRNJENO: 16 >= 15 (ne ustreza v3)
INSERT INTO v3 VALUES (25);  -- OK!: v1 nima CHECK OPTION, zato se ne preverja c < 20
```

**Glavna razlika**: CASCADED preverja VSE underlying view-e, LOCAL preverja samo tiste z CHECK OPTION.[](https://stackoverflow.com/questions/74338342/what-is-the-difference-between-local-and-cascaded-with-check-option-clause-in-my)​

## Updatable View-i

View je **updatable** (omogoča INSERT/UPDATE/DELETE), če izpolnjuje določene pogoje.[](https://www.docs4dev.com/docs/mariadb/10.6.4/inserting-and-updating-with-views/index.html)​

### Pogoji za updatable view

View **NI updatable**, če uporablja:[](https://runebook.dev/en/docs/mariadb/inserting-and-updating-with-views/index)​

- ALGORITHM=TEMPTABLE
    
- Agregacijske funkcije (COUNT, SUM, MAX, MIN, AVG)
    
- GROUP BY ali HAVING
    
- DISTINCT
    
- UNION ali UNION ALL
    
- Subquery v SELECT listi
    
- Subquery v WHERE, ki referenca tabelo iz FROM
    
- Outer join
    
- Samo literalne vrednosti brez osnovnih tabel
    
- Več referenc na isti base table stolpec
    

## Dodatni pogoji za INSERT

Za INSERT operacije view mora dodatno:[](https://www.docs4dev.com/docs/mariadb/10.6.4/inserting-and-updating-with-views/index.html)​

- Vsebovati **vse stolpce brez default vrednosti** iz osnovne tabele
    
- Nimeti dupliciranih imen stolpcev
    
- Vsi view stolpci morajo biti **enostavni stolpci** (ne izvedeni):
    
    - ✅ `column_name`
        
    - ❌ `column_name + 25`
        
    - ❌ `LOWER(column_name)`
        
    - ❌ `column1 / column2`

## Koristni ukazi
```sql
-- Prikaži vse view-e
SHOW FULL TABLES WHERE Table_type = 'VIEW';

-- Prikaži CREATE VIEW statement
SHOW CREATE VIEW view_name;

-- Preveri updatable status
SELECT TABLE_NAME, IS_UPDATABLE, CHECK_OPTION, SECURITY_TYPE
FROM INFORMATION_SCHEMA.VIEWS
WHERE TABLE_SCHEMA = 'your_database';

-- Spremeni view
ALTER VIEW view_name AS SELECT ...;

-- Izbriši view
DROP VIEW IF EXISTS view_name;
```
## Performance napotki

1. **Preferiraj MERGE** - hitrejši, omogoča uporabo indexov[](https://www.percona.com/blog/a-workaround-for-the-performance-problems-of-temptable-views/)​
    
2. **Izogibaj se TEMPTABLE** - uporablja začasne tabele in ne more biti updatable[](https://www.percona.com/blog/a-workaround-for-the-performance-problems-of-temptable-views/)​
    
3. **Uporabi WITH CHECK OPTION** - preprečuje neveljaven INSERT/UPDATE in ohranja integriteto[](https://www.mysqltutorial.org/mysql-views/mysql-view-with-check-option/)​
    
4. **SQL SECURITY INVOKER** - varnejše za production[](https://dev.mysql.com/doc/refman/8.4/en/stored-objects-security.html)​
    
5. **Materializirani view-i** - če potrebuješ cache, implementiraj svoje materialized views, ker MariaDB nima native support[](https://stackoverflow.com/questions/42513839/mysql-view-performance-temptable-or-merge)​
    

View-i so močno orodje za abstrakcijo podatkov, varnost in poenostavitev kompleksnih poizvedb v MariaDB.[](https://www.mariadbtutorial.com/mariadb-views/mariadb-create-view/)​