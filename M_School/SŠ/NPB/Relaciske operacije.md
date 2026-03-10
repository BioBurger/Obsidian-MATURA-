## Relacijska Algebra - Presek, Unija, Razlika in Deljenje

Relacijska algebra je **matematični sistem za manipulacijo podatkov v tabelah (relacijah)**. Te štiri operacije spadajo v **operacije teorije množic** (set operations), ki obravnavajo rezultate SELECT stavkov kot **množice vrstic**.[](https://studentski.net/get/ulj_fri_ri3_pbz_vaj_prosojnice_2007_2008_01.pdf)​
## 1. UNIJA (UNION)

**UNIJA kombinira rezultate DVEH poizvedb in vrne VSE vrstice iz ene ALI druge poizvedbe**.[](https://dijaski.net/get/mat_ref_relacijska_algebra_01.pdf)​

### Sintaksa
```sql
SELECT column1, column2 FROM table1
UNION [ALL | DISTINCT]
SELECT column1, column2 FROM table2;
```
### Kako deluje

- **Kombinira rezultate** - vrstice iz prve in druge SELECT poizvedbe se povežejo[](https://mariadb.com/docs/server/reference/sql-statements/data-manipulation/selecting-data/joins-subqueries/union)​
    
- **Odstrani duplikate** - UNION (bez ALL) avtomatično odstrani enake vrstice[](https://stackoverflow.com/questions/49925/what-is-the-difference-between-union-and-union-all)​
    
- **Rezultat je sortiiran** - UNION privzeto sortira rezultate[](https://stackoverflow.com/questions/49925/what-is-the-difference-between-union-and-union-all)​
    
- **Pogoj**: Obe SELECT morata biti **union-kompatibilni**:[](http://osebje.famnit.upr.si/~savnik/predmeti/OPB/Algebra.pdf)​
    
    - Isto število stolpcev
        
    - Istoležni stolpci enake ali kompatibilne tipe
### Razlika: UNION vs UNION ALL
```sql
-- Tabela A: (1, 2, 2, 3)
-- Tabela B: (3, 4, 4, 5)

-- UNION - odstrani duplikate (počasnejše)
SELECT val FROM tableA
UNION
SELECT val FROM tableB;
-- Rezultat: 1, 2, 3, 4, 5  ← duplikati so odstrajeni

-- UNION ALL - obdrži duplikate (hitrejše)
SELECT val FROM tableA
UNION ALL
SELECT val FROM tableB;
-- Rezultat: 1, 2, 2, 3, 3, 4, 4, 5  ← duplikati ostanejo
```
### Primer praktičen
```sql
-- Tabeli
CREATE TABLE java_studenti (id INT, ime VARCHAR(100));
CREATE TABLE delphi_studenti (id INT, ime VARCHAR(100));

INSERT INTO java_studenti VALUES (1, 'Janez'), (2, 'Ana'), (3, 'Miha');
INSERT INTO delphi_studenti VALUES (2, 'Ana'), (3, 'Miha'), (4, 'Eva');

-- UNION - študenti, ki učijo JAVA ALI DELPHI
SELECT ime FROM java_studenti
UNION
SELECT ime FROM delphi_studenti;

-- Rezultat:
-- Ana
-- Eva
-- Janez
-- Miha  (Ana in Miha se pojavita samo enkrat)
```
### Značilnosti

- **Komutativna** - A ∪ B = B ∪ A[](http://osebje.famnit.upr.si/~savnik/predmeti/OPB/Algebra.pdf)​
    
- **Asocijativna** - (A ∪ B) ∪ C = A ∪ (B ∪ C)[](http://osebje.famnit.upr.si/~savnik/predmeti/OPB/Algebra.pdf)​
    
- **Počasnejša UNION** - ker mora sortirati in odstraniti duplikate[](https://stackoverflow.com/questions/49925/what-is-the-difference-between-union-and-union-all)​
    
- **Hitrejša UNION ALL** - če vidiš, da so rezultati že unikatni[](https://stackoverflow.com/questions/49925/what-is-the-difference-between-union-and-union-all)​
    

### Pravila za union-kompatibilnost
```sql
-- ✅ OK - enako število in tip stolpcev
SELECT id, ime FROM zaposleni
UNION
SELECT id, ime FROM upokojenci;

-- ❌ NAPAKA - različni tipski ali red
SELECT ime, id FROM zaposleni
UNION
SELECT id, ime FROM upokojenci;  -- Stolpca sta obrnjena!

-- ✅ OK - različna imena stolpcev (ime je vseeno)
SELECT e_id AS id, e_name AS ime FROM employees
UNION
SELECT c_id, c_name FROM customers;
```
## 2. PRESEK (INTERSECT)

**PRESEK vrne samo vrstice, ki se nahajajo V OBEH poizvedbah**.[](https://mariadb.com/docs/server/reference/sql-statements/data-manipulation/selecting-data/joins-subqueries/intersect)​

### Sintaksa
```sql
SELECT column1, column2 FROM table1
INTERSECT [ALL | DISTINCT]
SELECT column1, column2 FROM table2;
```
### Kako deluje

- **Skupne vrstice** - vrstice, ki se pojavljajo v obeh rezultatih[](https://mariadb.com/docs/server/reference/sql-statements/data-manipulation/selecting-data/joins-subqueries/intersect)​
    
- **Avtomatičen DISTINCT** - INTERSECT privzeto odstrani duplikate[](https://mariadb.com/docs/server/reference/sql-statements/data-manipulation/selecting-data/joins-subqueries/intersect)​
    
- **Samo vrstice v OBEH** - vrstice, ki se pojavljajo samo v eni, so izključene[](https://mariadb.com/docs/server/reference/sql-statements/data-manipulation/selecting-data/joins-subqueries/intersect)​
    

### Primer
```sql
-- Tabeli
CREATE TABLE java_studenti (ime VARCHAR(100));
CREATE TABLE delphi_studenti (ime VARCHAR(100));

INSERT INTO java_studenti VALUES ('Janez'), ('Ana'), ('Miha');
INSERT INTO delphi_studenti VALUES ('Ana'), ('Miha'), ('Eva');

-- INTERSECT - študenti, ki učijo Java IN DELPHI
SELECT ime FROM java_studenti
INTERSECT
SELECT ime FROM delphi_studenti;

-- Rezultat:
-- Ana      ← pojavljata se v obeh
-- Miha
-- (Janez in Eva sta samo v eni tabeli, zato se ne pojavita)
```
### INTERSECT vs INTERSECT ALL
```sql
-- Tabela A: (1, 2, 2, 3)
-- Tabela B: (2, 2, 3, 4)

-- INTERSECT - odstrani duplikate
SELECT val FROM tableA
INTERSECT
SELECT val FROM tableB;
-- Rezultat: 2, 3

-- INTERSECT ALL - obdrži duplikate
SELECT val FROM tableA
INTERSECT ALL
SELECT val FROM tableB;
-- Rezultat: 2, 2, 3  ← duplikati ostanejo
```
## 3. RAZLIKA (EXCEPT / MINUS)

**RAZLIKA vrne vrstice, ki se nahajajo V PRVI poizvedbi, NI PA V DRUGI**.[](https://mariadb.com/docs/server/reference/sql-statements/data-manipulation/selecting-data/joins-subqueries/except)​

### Sintaksa
```sql
SELECT column1, column2 FROM table1
EXCEPT [ALL | DISTINCT]
SELECT column1, column2 FROM table2;

-- ali (v Oracle mode)
SELECT column1, column2 FROM table1
MINUS [ALL | DISTINCT]
SELECT column1, column2 FROM table2;
```
### Kako deluje

- **Vrstice samo v prvi** - A - B = vrstice v A, ki NISO v B[](https://www.ibm.com/docs/en/netezza?topic=except-operation)​
    
- **Avtomatičen DISTINCT** - EXCEPT privzeto odstrani duplikate[](https://mariadb.com/docs/server/reference/sql-statements/data-manipulation/selecting-data/joins-subqueries/except)​
    
- **Asimetrična operacija** - A EXCEPT B ≠ B EXCEPT A[](https://www.waitingforcode.com/sql/minus-except-operator-sql/read)​
    

### Primer
```sql
-- Tabeli
CREATE TABLE java_studenti (ime VARCHAR(100));
CREATE TABLE delphi_studenti (ime VARCHAR(100));

INSERT INTO java_studenti VALUES ('Janez'), ('Ana'), ('Miha');
INSERT INTO delphi_studenti VALUES ('Ana'), ('Miha'), ('Eva');

-- EXCEPT - študenti, ki učijo SAMO JAVA (ne DELPHI)
SELECT ime FROM java_studenti
EXCEPT
SELECT ime FROM delphi_studenti;

-- Rezultat:
-- Janez  ← je samo v java_studenti, ne v delphi_studenti
-- (Ana in Miha se pojavita v obeh, zato sta izključeni)
```
### EXCEPT vs MINUS

**EXCEPT in MINUS sta sinonima** - oba delujeta enako:[](https://mariadb.com/docs/server/reference/sql-statements/data-manipulation/selecting-data/joins-subqueries/minus)
```sql
-- MariaDB - podpira EXCEPT (od verzije 10.6.1)
SELECT i FROM seqs WHERE i <= 3
EXCEPT
SELECT i FROM seqs WHERE i >= 3;

-- Oracle mode - podpira MINUS
SET SQL_MODE='ORACLE';
SELECT i FROM seqs WHERE i <= 3
MINUS
SELECT i FROM seqs WHERE i >= 3;
```
### EXCEPT ALL
```sql
-- Tabela A: (1, 2, 2, 3)
-- Tabela B: (2, 3, 4)

-- EXCEPT - odstrani duplikate
SELECT val FROM tableA
EXCEPT
SELECT val FROM tableB;
-- Rezultat: 1

-- EXCEPT ALL - obdrži duplikate
SELECT val FROM tableA
EXCEPT ALL
SELECT val FROM tableB;
-- Rezultat: 1, 2  ← drugega 2 se ohrani, ker se pojavljata po enkrat
```
## 4. DELJENJE (DIVISION)

**DELJENJE vrne vse vrednosti iz prvega stolpca, ki se kombinirajo Z VSEMI vrednostmi drugega stolpca**.[](https://wwwlovre.appspot.com/resources/students/material/auditorium_practice.pdf)​

### Kako deluje

- **Iskanje "VSE" kombinacij** - kateri X-i se kombinirajo z VSEMI Y-ji[](https://nsuniv.ac.in/wp-content/uploads/2025/03/bca-3rd-sem-relational-algebra.pdf)​
    
- **Kompleksna operacija** - matematično: R ÷ S = vrstice X, ki se kombinirajo z vsemi Y-ji[](https://wwwlovre.appspot.com/resources/students/material/auditorium_practice.pdf)​
    
- **Relacija 1 ÷ Relacija 2 = Rezultat**[](https://www.tutorialspoint.com/explain-division-operation-in-relational-algebra-dbms)​
    

### Primer
```sql
-- Tabela: Študenti_Predmeti (Študent, Predmet)
CREATE TABLE student_course (
    student VARCHAR(100),
    course VARCHAR(100)
);

INSERT INTO student_course VALUES 
('Ana', 'DBMS'),
('Ana', 'OS'),
('Janez', 'DBMS'),
('Janez', 'OS'),
('Miha', 'DBMS');

-- Vprašanje: Kateri študenti obiskujejo VSE predmete?
-- Najprej: Koliko predmetov je skupno?
-- Odgovor: 2 (DBMS in OS)

-- DELJENJE - kateri študenti obiskujejo OBA predmeta?
-- Rezultat: Ana, Janez (Miha ne, ker obiskuje samo DBMS)
```
### SQL implementacija brez native DELJENJA

MariaDB direktno **NE podpira deljenje**, zato se implementira s **NOT IN**:[](https://nsuniv.ac.in/wp-content/uploads/2025/03/bca-3rd-sem-relational-algebra.pdf)​
```sql
-- Deljenje simulacija
SELECT DISTINCT student
FROM student_course s
WHERE NOT EXISTS (
    -- Preveri, ali student obiskuje VSE predmete
    SELECT course FROM (
        SELECT DISTINCT course FROM student_course
    ) all_courses
    WHERE NOT EXISTS (
        SELECT 1 FROM student_course
        WHERE student = s.student
        AND course = all_courses.course
    )
);

-- Enostavnejša formula:
SELECT DISTINCT student
FROM student_course
GROUP BY student
HAVING COUNT(DISTINCT course) = (
    SELECT COUNT(DISTINCT course) FROM student_course
);
```
### Primer: Zaposleni na VSE projektih
```sql
-- Tabela: Zaposleni_Projekti
CREATE TABLE emp_project (
    emp_name VARCHAR(100),
    project_name VARCHAR(100)
);

INSERT INTO emp_project VALUES 
('John', 'P1'),
('John', 'P2'),
('John', 'P3'),
('Alice', 'P1'),
('Alice', 'P2'),
('Bob', 'P1');

-- Vprašanje: Kateri zaposleni delajo na VSE projektih?
-- Skupaj je 3 projektov (P1, P2, P3)

-- Odgovor: John (deluje na P1, P2, P3)

-- SQL:
SELECT DISTINCT emp_name
FROM emp_project
GROUP BY emp_name
HAVING COUNT(DISTINCT project_name) = (
    SELECT COUNT(DISTINCT project_name) FROM emp_project
);

-- Rezultat: John
```
