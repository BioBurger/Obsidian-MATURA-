
## Kaj je JOIN?

**JOIN** je **mehanizem za kombiniranje podatkov iz dveh ali več tabel na osnovi skupne vrednosti**. JOIN povezuje vrstice iz različnih tabel, kar omogoča kompleksne poizvedbe na povezanih podatkih.[](https://www.mariadbtutorial.com/mariadb-basics/mariadb-join/)​
## 1. INNER JOIN

**INNER JOIN vrne samo vrstice, ki imajo ujemanje v OBEH tabelah**.[](https://mariadb.com/docs/server/mariadb-quickstart-guides/mariadb-join-guide)​

### Sintaksa
```sql
SELECT column_name
FROM table1
INNER JOIN table2
ON table1.column_name = table2.column_name;

-- Kratica (INNER je privzeto)
SELECT column_name
FROM table1
JOIN table2
ON table1.column_name = table2.column_name;
```
### Kako deluje

- **Pregleda vsako vrstico iz table1**
    
- **Za vsako vrstico preveri, ali obstaja ujemanje v table2**
    
- **Vključi samo vrstice, ki imajo ujemanje v OBEH tabelah**[](https://stackoverflow.com/questions/5706437/whats-the-difference-between-inner-join-left-join-right-join-and-full-join)​
### Primer
```sql
-- Tabele
CREATE TABLE employees (id INT, name VARCHAR(100), dept_id INT);
CREATE TABLE departments (id INT, dept_name VARCHAR(100));

INSERT INTO employees VALUES (1, 'Janez', 1), (2, 'Ana', 2), (3, 'Miha', NULL);
INSERT INTO departments VALUES (1, 'IT'), (2, 'HR'), (3, 'Finance');

-- INNER JOIN - samo zaposleni z oddelkom
SELECT employees.name, departments.dept_name
FROM employees
INNER JOIN departments ON employees.dept_id = departments.id;

-- Rezultat:
-- Janez    | IT
-- Ana      | HR
-- (Miha ni vključen, ker dept_id = NULL)
```
### Značilnosti

- **Samo ujemanja** - vrne samo vrstice z ujemanjem v obeh tabelah[](https://mariadb.com/docs/server/mariadb-quickstart-guides/mariadb-join-guide)​
    
- **Brez NULL vrednosti** - vrstice brez ujemanja se zavrnejo[](https://stackoverflow.com/questions/5706437/whats-the-difference-between-inner-join-left-join-right-join-and-full-join)​
    
- **Simetrična operacija** - vrstni red tabel ne vpliva na rezultat (A JOIN B = B JOIN A)[](https://mariadb.com/docs/server/mariadb-quickstart-guides/mariadb-join-guide)​
    
- **Hitro** - se pogosto optimizira s posebnimi algoritmi[](https://mariadb.com/docs/server/mariadb-quickstart-guides/mariadb-join-guide)​

## 2. LEFT JOIN (LEFT OUTER JOIN)

**LEFT JOIN vrne VSE vrstice iz LEVE tabele in ujemanja iz desne tabele**.[](https://stackoverflow.com/questions/5706437/whats-the-difference-between-inner-join-left-join-right-join-and-full-join)​

### Sintaksa
```sql
SELECT column_name
FROM table1
LEFT JOIN table2
ON table1.column_name = table2.column_name;

-- Ekvivalentno
SELECT column_name
FROM table1
LEFT OUTER JOIN table2
ON table1.column_name = table2.column_name;
```
### Kako deluje

- **Pregleda vsako vrstico iz table1 (leva tabela)**
    
- **Isče ujemanje v table2**
    
- **Če je ujemanje - vključi podatke iz table2**
    
- **Če NI ujemanja - vključi vrstico s NULL vrednostmi za table2**[](https://stackoverflow.com/questions/5706437/whats-the-difference-between-inner-join-left-join-right-join-and-full-join)

### Primer​
```sql
-- LEFT JOIN - vsi zaposleni in njihovi oddelki (ali NULL)
SELECT employees.name, departments.dept_name
FROM employees
LEFT JOIN departments ON employees.dept_id = departments.id;

-- Rezultat:
-- Janez    | IT
-- Ana      | HR
-- Miha     | NULL      ← Miha je vključen, kljub NULL dept_id
```
### Značilnosti

- **Vsi iz leve tabele** - nobena vrstica iz table1 se ne zavrne[](https://stackoverflow.com/questions/5706437/whats-the-difference-between-inner-join-left-join-right-join-and-full-join)​
    
- **NULL za brez ujemanja** - desna tabela ima NULL, če ni ujemanja[](https://mariadb.com/docs/server/mariadb-quickstart-guides/mariadb-join-guide)​
    
- **Asimetrična operacija** - A LEFT JOIN B ≠ B LEFT JOIN A[](https://mariadb.com/docs/server/mariadb-quickstart-guides/mariadb-join-guide)​
    
- **Primerna za reports** - dobiš vse vrstice, tudi brez povezav[](https://www.mariadbtutorial.com/mariadb-basics/mariadb-join/)​

## 3. RIGHT JOIN (RIGHT OUTER JOIN)

**RIGHT JOIN vrne VSE vrstice iz DESNE tabele in ujemanja iz leve tabele**.[](https://stackoverflow.com/questions/5706437/whats-the-difference-between-inner-join-left-join-right-join-and-full-join)​

### Sintaksa
```sql
SELECT column_name
FROM table1
RIGHT JOIN table2
ON table1.column_name = table2.column_name;

-- Ekvivalentno
SELECT column_name
FROM table1
RIGHT OUTER JOIN table2
ON table1.column_name = table2.column_name;
```
### Kako deluje

- **Pregleda vsako vrstico iz table2 (desna tabela)**
    
- **Isče ujemanje v table1**
    
- **Če je ujemanje - vključi podatke iz table1**
    
- **Če NI ujemanja - vključi vrstico s NULL vrednostmi za table1**[](https://www.ionos.com/digitalguide/hosting/technical-matters/mariadb-join/)​
    
### Primer
```sql
-- RIGHT JOIN - vsi oddelki in njihovi zaposleni (ali NULL)
SELECT employees.name, departments.dept_name
FROM employees
RIGHT JOIN departments ON employees.dept_id = departments.id;

-- Rezultat:
-- Janez      | IT
-- Ana        | HR
-- NULL       | Finance    ← Finance je vključen, čeprav ga nihče ne opravlja
```
### Značilnosti

- **Vsi iz desne tabele** - nobena vrstica iz table2 se ne zavrne[](https://www.ionos.com/digitalguide/hosting/technical-matters/mariadb-join/)​
    
- **NULL za brez ujemanja** - leva tabela ima NULL, če ni ujemanja[](https://mariadb.com/docs/server/mariadb-quickstart-guides/mariadb-join-guide)​
    
- **Asimetrična operacija** - A RIGHT JOIN B ≠ B RIGHT JOIN A[](https://mariadb.com/docs/server/mariadb-quickstart-guides/mariadb-join-guide)​
    
- **Redkeje se koristi** - RIGHT JOIN A je ekvivalenten LEFT JOIN A (obrnjena vrstna red)[](https://mariadb.com/docs/server/mariadb-quickstart-guides/mariadb-join-guide)​
    
### RIGHT JOIN kot alternativa
```sql
-- To je enako:
SELECT * FROM employees RIGHT JOIN departments ON employees.dept_id = departments.id;

-- Bi bilo isto kot:
SELECT * FROM departments LEFT JOIN employees ON employees.dept_id = departments.id;
```
## 4. FULL JOIN (FULL OUTER JOIN)

**MariaDB DIREKTNO NE PODPIRA FULL JOIN!** Nadomestiti ga je treba s kombinacijo LEFT in RIGHT JOIN-a z UNION.[](https://www.devart.com/dbforge/mysql/studio/mysql-joins.html)​

### Kako se implementira v MariaDB

**FULL JOIN = LEFT JOIN UNION RIGHT JOIN**[](https://databasefaqs.com/mariadb-full-outer-join/)
```sql
SELECT *
FROM table1
LEFT JOIN table2 ON table1.id = table2.id

UNION

SELECT *
FROM table1
RIGHT JOIN table2 ON table1.id = table2.id;
```

### Razlika med UNION in UNION ALL
```sql
-- UNION - odstrani duplikate
SELECT * FROM employees LEFT JOIN departments ON ...
UNION
SELECT * FROM employees RIGHT JOIN departments ON ...;

-- UNION ALL - obdrži duplikate (bolj pravilno za FULL JOIN!)
SELECT * FROM employees LEFT JOIN departments ON ...
UNION ALL
SELECT * FROM employees RIGHT JOIN departments ON ...;
```
### Primer
```sql
CREATE TABLE users (id INT, name VARCHAR(100));
CREATE TABLE hobbies (id INT, hobby VARCHAR(100));

INSERT INTO users VALUES (1, 'Janez'), (2, 'Ana'), (3, 'Miha');
INSERT INTO hobbies VALUES (1, 'Plezanje'), (2, 'Plavanje'), (4, 'Čitanje');

-- FULL OUTER JOIN simulacija
SELECT users.name, hobbies.hobby
FROM users
LEFT JOIN hobbies ON users.id = hobbies.id

UNION ALL

SELECT users.name, hobbies.hobby
FROM users
RIGHT JOIN hobbies ON users.id = hobbies.id;

-- Rezultat:
-- Janez    | Plezanje
-- Ana      | Plavanje
-- Miha     | NULL
-- NULL     | Čitanje     ← Čitanje nima lastnika (id=4)
```
### Značilnosti

- **Vsi iz OBEH tabel** - nobena vrstica se ne zavrne[](https://www.devart.com/dbforge/mysql/studio/mysql-joins.html)​
    
- **NULL za brez ujemanja** - obstransko NULL[](https://www.devart.com/dbforge/mysql/studio/mysql-joins.html)​
    
- **UNION ALL je pravilno** - UNION odstrani duplikate, kar je napačno za FULL JOIN[](https://databasefaqs.com/mariadb-full-outer-join/)​
    
- **Kompleksna** - potrebna sta dva JOIN-a in UNION[](https://databasefaqs.com/mariadb-full-outer-join/)

## 5. CROSS JOIN (Cartesian Product)

**CROSS JOIN vrne KARTEZIČNI PRODUKT - vsaka vrstica iz table1 se kombinira z VSAKO vrstico iz table2**.[](https://www.alphacodingskills.com/mariadb/mariadb-cross-join.php)​

### Sintaksa
```sql
SELECT column_name
FROM table1
CROSS JOIN table2;

-- Enako (brez ON pogoja):
SELECT column_name
FROM table1, table2;
```
### Kako deluje

- **Brez ON pogoja!** - samo nastopi med tabelama[](https://www.geeksforgeeks.org/sql/sql-join-cartesian-join-self-join/)​
    
- **m × n vrstic** - če je table1 5 vrstic in table2 3 vrstice, rezultat ima 5 × 3 = 15 vrstic[](https://www.alphacodingskills.com/mariadb/mariadb-cross-join.php)​
    
- **Vse kombinacije** - vsaka vrstica z vsako[](https://www.geeksforgeeks.org/sql/sql-join-cartesian-join-self-join/)​
### Primer
```sql
CREATE TABLE colors (name VARCHAR(50));
CREATE TABLE sizes (size VARCHAR(10));

INSERT INTO colors VALUES ('Rdeča'), ('Modra'), ('Zelena');
INSERT INTO sizes VALUES ('S'), ('M'), ('L');

-- CROSS JOIN - vse kombinacije barv in velikosti
SELECT colors.name, sizes.size
FROM colors
CROSS JOIN sizes;

-- Rezultat (3 × 3 = 9 vrstic):
-- Rdeča    | S
-- Rdeča    | M
-- Rdeča    | L
-- Modra    | S
-- Modra    | M
-- Modra    | L
-- Zelena   | S
-- Zelena   | M
-- Zelena   | L
```
### Značilnosti

- **Brez ON pogoja** - samo CROSS JOIN nastopiš[](https://www.alphacodingskills.com/mariadb/mariadb-cross-join.php)​
    
- **Kartezični produkt** - eksponentna rast vrstic[](https://www.geeksforgeeks.org/sql/sql-join-cartesian-join-self-join/)​
    
- **Redko se koristi** - naročilo se stvari nemenljive podmnožice[](https://www.alphacodingskills.com/mariadb/mariadb-cross-join.php)​
    
- **ON pogoj = INNER JOIN** - CROSS JOIN s WHERE je enak INNER JOIN-u[](https://www.alphacodingskills.com/mariadb/mariadb-cross-join.php)​
```sql
-- To je enako INNER JOIN:
SELECT * FROM colors CROSS JOIN sizes WHERE colors.id = sizes.color_id;
```
## 6. NATURAL JOIN

**NATURAL JOIN avtomatično ujema VSE stolpce z ENAKIMI IMENI**.[](https://www.w3resource.com/mysql/advance-query-in-mysql/mysql-natural-join.php)​

### Sintaksa
```sql
SELECT column_name
FROM table1
NATURAL JOIN table2;

-- S LEFT:
SELECT column_name
FROM table1
NATURAL LEFT JOIN table2;

-- S RIGHT:
SELECT column_name
FROM table1
NATURAL RIGHT JOIN table2;
```
### Kako deluje

- **Avtomatični pogoj** - poiščeš vse stolpce z istim imenom[](https://www.datacamp.com/doc/mysql/mysql-natural-join)​
    
- **Brez ON pogoja** - ON se NE piše[](https://www.w3resource.com/mysql/advance-query-in-mysql/mysql-natural-join.php)​
    
- **Redundantni stolpci se izpustijo** - skupni stolpec se pojavi samo enkrat[](https://dev.mysql.com/doc/en/join.html)​
    

### Primer
```sql
CREATE TABLE orders (order_id INT, customer_id INT, amount INT);
CREATE TABLE customers (customer_id INT, name VARCHAR(100));

INSERT INTO orders VALUES (1, 101, 500), (2, 102, 300);
INSERT INTO customers VALUES (101, 'Janez'), (102, 'Ana'), (103, 'Miha');

-- NATURAL JOIN - avtomatično ujema customer_id
SELECT *
FROM orders
NATURAL JOIN customers;

-- Rezultat (customer_id se pojavi samo enkrat):
-- customer_id | order_id | amount | name
-- 101         | 1        | 500    | Janez
-- 102         | 2        | 300    | Ana

-- Ekvivalentno je:
SELECT *
FROM orders
INNER JOIN customers USING (customer_id);
```
### Značilnosti

- **Avtomatičen** - ni potreben ON pogoj[](https://www.datacamp.com/doc/mysql/mysql-natural-join)​
    
- **Redundančnost odpravljena** - skupni stolpec se pojavi samo enkrat[](https://dev.mysql.com/doc/en/join.html)​
    
- **Nevarno** - skrit JOIN pogoj, težko za debugging[](https://www.w3resource.com/mysql/advance-query-in-mysql/mysql-natural-join.php)​
    
- **Ne priporočam** - v praksi se izogne (eksplicitne USING je boljša)[](https://www.datacamp.com/doc/mysql/mysql-natural-join)​
## 7. STRAIGHT_JOIN

**STRAIGHT_JOIN prisili MariaDB, da ujema tabele v TOČNO NAVEDENIM VRSTNEM REDU (brez optimizacije)**.[](https://quantum5.ca/2018/11/04/optimize-mysql-mariadb-query-straight-join/)​

### Sintaksa
```sql
SELECT column_name
FROM table1
STRAIGHT_JOIN table2 ON table1.id = table2.id;

-- Rezultat je enak INNER JOIN, razlika je samo v vrstnem redu procesiranja
```
### Kako deluje

- **Prisila vrstni red** - table1 se VEDNO procesira pred table2[](https://www.alibabacloud.com/help/en/analyticdb/analyticdb-for-mysql/user-guide/straight-join)​
    
- **Brez optimizacije** - MariaDB optimizer se NE izvedeće[](https://www.alibabacloud.com/help/en/analyticdb/analyticdb-for-mysql/user-guide/straight-join)​
    
- **Enak rezultat kot INNER JOIN** - samo drugačen načrt izvajanja[](https://www.alibabacloud.com/help/en/analyticdb/analyticdb-for-mysql/user-guide/straight-join)​
    

### Primer
```sql
-- Slaba query (neoptimalna poDefault):
SELECT COUNT(*)
FROM big_table (1M vrstic)
JOIN small_table (100 vrstic)
ON big_table.id = small_table.id
WHERE small_table.filter = 'important';

-- STRAIGHT_JOIN - prisili pravilni vrstni red
SELECT COUNT(*)
FROM small_table (100 vrstic)
STRAIGHT_JOIN big_table (1M vrstic)
ON small_table.id = big_table.id
WHERE small_table.filter = 'important';
```
### Zakaj se koristi

Včasih je MariaDB optimizer izbere **neoptimalno** vrstni red (zlasti z WHERE pogoji). STRAIGHT_JOIN forsira željeni vrstni red.[](https://quantum5.ca/2018/11/04/optimize-mysql-mariadb-query-straight-join/)​
### Značilnosti

- **Performančen tuning** - uporabi samo, ko je potrebno[](https://quantum5.ca/2018/11/04/optimize-mysql-mariadb-query-straight-join/)​
    
- **Primoramarani vrstni red** - MariaDB ga ne smatra za optimizacijo[](https://www.alibabacloud.com/help/en/analyticdb/analyticdb-for-mysql/user-guide/straight-join)​
    
- **Enak rezultat kot INNER JOIN** - razlika je samo v performanci[](https://www.alibabacloud.com/help/en/analyticdb/analyticdb-for-mysql/user-guide/straight-join)​
    
- **Redko** - uporabljaj samo v posebnih primerih[](https://quantum5.ca/2018/11/04/optimize-mysql-mariadb-query-straight-join/)​
## Nasveti za izbiro JOIN vrste

1. **INNER JOIN** - ko te zanima samo ujemanja[](https://mariadb.com/docs/server/mariadb-quickstart-guides/mariadb-join-guide)​
    
2. **LEFT JOIN** - ko potrebuješ vse iz leve tabele (reports)[](https://www.mariadbtutorial.com/mariadb-basics/mariadb-join/)​
    
3. **RIGHT JOIN** - redko, zavrtni tabeli in koristi LEFT[](https://mariadb.com/docs/server/mariadb-quickstart-guides/mariadb-join-guide)​
    
4. **FULL JOIN** - ko potrebuješ vse iz obeh tabel[](https://www.devart.com/dbforge/mysql/studio/mysql-joins.html)​
    
5. **CROSS JOIN** - samo za kartezične produkte (permutacije)[](https://www.alphacodingskills.com/mariadb/mariadb-cross-join.php)​
    
6. **NATURAL JOIN** - izogni se v produkciji[](https://www.w3resource.com/mysql/advance-query-in-mysql/mysql-natural-join.php)​
    
7. **STRAIGHT_JOIN** - samo za performance tuning[](https://quantum5.ca/2018/11/04/optimize-mysql-mariadb-query-straight-join/)​
    

**Za 99% primerov uporabite INNER, LEFT ali RIGHT JOIN!**[](https://www.mariadbtutorial.com/mariadb-basics/mariadb-join/)​