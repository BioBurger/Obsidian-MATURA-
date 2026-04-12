# Kaj so Pravice (Privileges)?

Pravice določajo, kaj sme posamezen uporabnik početi v bazi. MariaDB ima hierarhičen sistem pravic: **globalne → baza → tabela → stolpec**.

---

## 1. GRANT – dodelitev pravic

```sql
-- Sintaksa
GRANT pravica ON baza.tabela TO 'user'@'host';

-- Vse pravice na vseh bazah
GRANT ALL PRIVILEGES ON *.* TO 'janez'@'localhost';

-- Samo branje na eni bazi
GRANT SELECT ON mydb.* TO 'ana'@'localhost';

-- Specifične pravice na tabeli
GRANT SELECT, INSERT, UPDATE ON mydb.users TO 'miha'@'localhost';

-- Pravice na stolpcu
GRANT SELECT (ime, priimek) ON mydb.users TO 'bralec'@'localhost';

-- Z možnostjo nadaljnje podelitve
GRANT SELECT ON mydb.* TO 'manager'@'localhost' WITH GRANT OPTION;
```

---

## 2. Vrste pravic

| Pravica | Opis |
|---|---|
| `SELECT` | Branje podatkov |
| `INSERT` | Dodajanje vrstic |
| `UPDATE` | Posodabljanje vrstic |
| `DELETE` | Brisanje vrstic |
| `CREATE` | Ustvarjanje tabel/baz |
| `DROP` | Brisanje tabel/baz |
| `ALTER` | Sprememba strukture |
| `INDEX` | Ustvarjanje indeksov |
| `EXECUTE` | Izvajanje procedur/funkcij |
| `ALL PRIVILEGES` | Vse pravice |
| `GRANT OPTION` | Podeljevanje pravic naprej |

---

## 3. REVOKE – odvzem pravic

```sql
-- Sintaksa
REVOKE pravica ON baza.tabela FROM 'user'@'host';

-- Odvzemi SELECT
REVOKE SELECT ON mydb.* FROM 'ana'@'localhost';

-- Odvzemi vse
REVOKE ALL PRIVILEGES ON *.* FROM 'janez'@'localhost';

-- Odvzemi GRANT OPTION
REVOKE GRANT OPTION ON mydb.* FROM 'manager'@'localhost';
```

---

## 4. Pregled pravic

```sql
-- Pravice za določenega uporabnika
SHOW GRANTS FOR 'ana'@'localhost';

-- Pravice za trenutnega uporabnika
SHOW GRANTS;
SHOW GRANTS FOR CURRENT_USER();
```

---

## 5. Hierarhija pravic
Globalne (_._)  
└── Baza (mydb.*)  
└── Tabela (mydb.users)  
└── Stolpec (mydb.users.ime)

```sql
-- Globalna raven
GRANT SELECT ON *.* TO 'user'@'localhost';

-- Baza raven
GRANT SELECT ON mydb.* TO 'user'@'localhost';

-- Tabela raven
GRANT SELECT ON mydb.users TO 'user'@'localhost';

-- Stolpec raven
GRANT SELECT (ime) ON mydb.users TO 'user'@'localhost';
```

---

## Značilnosti

- **Specifičnejše zmaga** — tabela pravica preglasi globalno
- **FLUSH PRIVILEGES** — po ročnem urejanju `mysql.user`
- **Varnostno načelo** — dodeli samo potrebne pravice (Principle of Least Privilege)
- **WITH GRANT OPTION** — uporabnik lahko pravice prenaša naprej