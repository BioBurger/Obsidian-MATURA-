## InnoDB

InnoDB je **privzet storage engine** v MariaDB/MySQL od verzije 5.5 in predstavlja najbolj vsestranski engine za večino aplikacij.[](https://mariadb.com/docs/server/server-usage/storage-engines/choosing-the-right-storage-engine)​

**Glavne lastnosti:**

- **ACID transakcije** - popolna podpora za transakcije s COMMIT, ROLLBACK in crash recovery mehanizmi[](https://www.datacamp.com/blog/acid-transactions)​
    
- **Row-level locking** - zaklepa posamezne vrstice namesto celotnih tabel, kar omogoča visoko konkurenčnost in zmogljivost pri write-heavy obremenitvah[](https://blog.devart.com/myisam-vs-innodb.html)​
    
- **Foreign key constraints** - edini engine, ki podpira referenčno integriteto med tabelami[](https://mariadb.org/per-table-unique-foreign-key-constraint-names-new-feature-in-mariadb-12-1/)​
    
- **MVCC (Multi-Version Concurrency Control)** - omogoča nekaterih branj brez zaklepanja, kar izboljša konkurenčnost[](https://stackoverflow.com/questions/6321647/innodbs-row-locking-the-same-as-mvcc-non-blocking-reads)​
    
- **Crash-safe** - podatki so vedno konsistentni po sesutju sistema[](https://blog.devart.com/myisam-vs-innodb.html)​
    
- **Clustered indexes** - podatki so shranjeni v istem vrstnem redu kot primarni ključ, kar optimizira poizvedbe[](https://tecadmin.net/choosing-between-innodb-myisam-and-memory-storage-engines/)​
    
- **Buffer pool** - učinkovit memory caching za podatke in indekse[](https://blog.devart.com/myisam-vs-innodb.html)​
    
- **Full-text search** - podprt od MySQL 5.6 naprej[](https://typesense.org/learn/full-text-search-mysql/)​
    

**Kdaj uporabiti:**

- Aplikacije, ki potrebujejo transakcije in ACID skladnost[](https://tecadmin.net/choosing-between-innodb-myisam-and-memory-storage-engines/)​
    
- Visoka konkurenčnost (veliko sočasnih uporabnikov)[](https://blog.devart.com/myisam-vs-innodb.html)​
    
- Write-heavy obremenitve[](https://tecadmin.net/choosing-between-innodb-myisam-and-memory-storage-engines/)​
    
- Potrebna referenčna integriteta (foreign keys)[](https://200oksolutions.com/blog/mysql-innodb-vs-myisam/)​
    
- Kritični podatki, kjer je crash recovery pomemben[](https://200oksolutions.com/blog/mysql-innodb-vs-myisam/)​
    

**Slabosti:**

- Počasnejši pri preprostih read operacijah kot MyISAM[](https://phoenixnap.com/kb/myisam-vs-innodb)​
    
- Večja poraba disknega prostora[](https://blog.devart.com/myisam-vs-innodb.html)​
    
- Kompleksnejša konfiguracija[](https://blog.devart.com/myisam-vs-innodb.html)​

## MyISAM

MyISAM je **najstarejši storage engine** v MySQL/MariaDB, ki je bil privzet pred verzijo 5.5.[](https://vettabase.com/mariadb-and-mysql-storage-engines-an-overview/)​

**Glavne lastnosti:**

- **Table-level locking** - zaklepa celotno tabelo pri write operacijah, kar omejuje konkurenčnost[](https://www.liquidweb.com/blog/mysql-performance-myisam/)​
    
- **Brez transakcij** - ne podpira COMMIT/ROLLBACK[](https://200oksolutions.com/blog/mysql-innodb-vs-myisam/)​
    
- **Brez crash-safe** - podatki se lahko poškodujejo pri sesutju[](https://vettabase.com/mariadb-and-mysql-storage-engines-an-overview/)​
    
- **Hitra read operacija** - optimiziran za SELECT poizvedbe[](https://phoenixnap.com/kb/myisam-vs-innodb)​
    
- **Full-text indexing** - izvirna podpora za full-text search[](https://typesense.org/learn/full-text-search-mysql/)​
    
- **Majhen footprint** - manjša poraba prostora kot InnoDB[](https://mariadb.com/docs/server/server-usage/storage-engines)​
    
- **Table compression** - myisampack omogoča 40-70% kompresijo tabel za read-only uporabo[](https://dev.mysql.com/doc/refman/8.3/en/myisampack.html)​
    
- **Enostavno kopiranje** - tabele lahko preprosto kopiraš med sistemi[](https://mariadb.com/docs/server/server-usage/storage-engines/choosing-the-right-storage-engine)​
    

**Kdaj uporabiti:**

- Read-heavy aplikacije z malo ali brez write operacij[](https://tecadmin.net/choosing-between-innodb-myisam-and-memory-storage-engines/)​
    
- Data warehousing in analitika[](https://tecadmin.net/choosing-between-innodb-myisam-and-memory-storage-engines/)​
    
- Legacy sistemi[](https://mariadb.com/docs/server/server-usage/storage-engines/choosing-the-right-storage-engine)​
    
- Okolja z omejenimi resursi[](https://blog.devart.com/myisam-vs-innodb.html)​
    
- Potreba po table compression za read-only podatke[](https://dev.mysql.com/doc/refman/8.3/en/myisampack.html)​
    

**Slabosti:**

- Table-level locking povzroča bottlenecke pri write operacijah[](https://www.catalyst2.com/knowledgebase/server-management/advantages-of-innodb-over-myisam/)​
    
- Brez transakcij in ACID skladnosti[](https://200oksolutions.com/blog/mysql-innodb-vs-myisam/)​
    
- Ni crash-safe - tabele se lahko poškodujejo[](https://vettabase.com/mariadb-and-mysql-storage-engines-an-overview/)​
    
- Brez foreign key support[](https://200oksolutions.com/blog/mysql-innodb-vs-myisam/)​
    
- Ni več v aktivnem razvoju[](https://en.wikipedia.org/wiki/Comparison_of_MySQL_database_engines)​

## Aria

Aria je **crash-safe nadomestek MyISAM**, razvit s strani MariaDB ekipe od 2007 naprej.[](https://severalnines.com/blog/using-aria-storage-engine-mariadb-server/)​

**Glavne lastnosti:**

- **Crash-safe** - recovery vseh tabel na stanje začetka stavka ali zadnjega LOCK TABLES[](https://mariadb.com/docs/server/server-usage/storage-engines/aria/aria-storage-engine)​
    
- **PAGE row format** - privzet format, nujen za crash-safe funkcionalnost[](https://subscription.packtpub.com/book/data/9781783284399/3/ch03lvl1sec35/configuring-the-aria-pagecache)​
    
- **8K page size** (vs 1K pri MyISAM) - hitrejše pri fixed-size keys, počasnejše pri variabilnih[](https://severalnines.com/blog/using-aria-storage-engine-mariadb-server/)​
    
- **Boljši caching** - stran-based caching daje boljšo zmogljivost[](https://mariadb.com/resources/blog/storage-engine-choice-aria/)​
    
- **Optimizirano za GROUP BY in DISTINCT** - do 4x hitrejše kot InnoDB pri agregacijah[](https://mariadb.com/resources/blog/storage-engine-choice-aria/)​
    
- **Večja max key length** - 2000 bytes od MariaDB 10.5 (vs 1000 pri MyISAM)[](https://severalnines.com/blog/using-aria-storage-engine-mariadb-server/)​
    
- **Concurrent inserts** - podpira več sočasnih vstavitev[](https://www.datavail.com/blog/exploring-mariadbs-storage-engine-options/)​
    
- **Večji log files** - privzeto 1GB[](https://severalnines.com/blog/using-aria-storage-engine-mariadb-server/)​
    
- **Brez transakcij** - ni ACID-compliant kot InnoDB[](https://en.wikipedia.org/wiki/Aria_\(storage_engine\))​
    

**Kdaj uporabiti:**

- Read-heavy obremenitve brez potrebe po transakcijah[](https://mariadb.com/resources/blog/storage-engine-choice-aria/)​
    
- Interne temporary tabele - MariaDB uporablja Aria za on-disk temporary tables[](https://mariadb.com/docs/server/server-usage/storage-engines/aria/aria-storage-engine)​
    
- System tabele - MariaDB uporablja Aria za vse system tables od verzije 10.4[](https://mariadb.com/resources/blog/storage-engine-choice-aria/)​
    
- Agregacijske poizvedbe (GROUP BY, ORDER BY)[](https://mariadb.com/resources/blog/storage-engine-choice-aria/)​
    
- Kjer potrebuješ crash-safe alternativo MyISAM[](https://www.datavail.com/blog/exploring-mariadbs-storage-engine-options/)​
    

**Slabosti:**

- Ni transakcijski engine[](https://en.wikipedia.org/wiki/Aria_\(storage_engine\))​
    
- Table-level locking kot MyISAM[](https://severalnines.com/blog/using-aria-storage-engine-mariadb-server/)​
    
- Večji log files zasedejo več prostora[](https://severalnines.com/blog/using-aria-storage-engine-mariadb-server/)​

## MEMORY (HEAP)

MEMORY engine shranjuje **vse podatke v RAM-u** za izjemno hiter dostop.[](https://dev.mysql.com/doc/refman/8.4/en/memory-storage-engine.html)​

**Glavne lastnosti:**

- **Shranjeno v RAM** - vsi podatki so v pomnilniku[](https://www.w3resource.com/mysql/mysql-storage-engines.php)​
    
- **Podatki izgubljeni po restartu** - samo table definition ostane[](https://mariadb.com/docs/server/server-usage/storage-engines/memory-storage-engine)​
    
- **Table-level locking** - kot MyISAM[](https://www.w3resource.com/mysql/mysql-storage-engines.php)​
    
- **Podpira HASH in BTREE indekse** - HASH je privzet[](https://www.w3resource.com/mysql/mysql-storage-engines.php)​
    
- **max_heap_table_size** - omejuje velikost tabel (privzeto 16MB)[](https://www.wiserfirst.com/blog/increase-mysql-table-size-for-memory-storage-engine/)​
    
- **Brez BLOB/TEXT** - ne podpira teh tipov stolpcev[](https://mariadb.com/docs/server/server-usage/storage-engines/memory-storage-engine)​
    
- **Brez transakcij** - ni ACID-compliant[](https://www.w3resource.com/mysql/mysql-storage-engines.php)​
    
- **Dynamic hashing** - 100% za inserte[](https://dev.mysql.com/doc/refman/8.4/en/memory-storage-engine.html)​
    

**Kdaj uporabiti:**

- Session data za spletne aplikacije[](https://www.mysqltutorial.org/mysql-administration/mysql-memory-storage-engine/)​
    
- Temporary data za vmesne rezultate[](https://dev.mysql.com/doc/refman/8.2/en/storage-engines.html)​
    
- Caching pogosto dostopanih podatkov, ki se redko spreminjajo[](https://www.mysqltutorial.org/mysql-administration/mysql-memory-storage-engine/)​
    
- Real-time analytics dashboards[](https://www.baeldung.com/sql/mysql-storage-engine-types)​
    
- Lookup tabele za hitre searches[](https://labex.io/questions/when-should-i-use-memory-engine-843564)​
    

**Slabosti:**

- Podatki izgubljeni po restartu serverja[](https://dev.mysql.com/doc/refman/8.4/en/memory-storage-engine.html)​
    
- Omejena velikost tabel (max_heap_table_size)[](https://www.wiserfirst.com/blog/increase-mysql-table-size-for-memory-storage-engine/)​
    
- Table-level locking omejuje konkurenčnost[](https://tecadmin.net/choosing-between-innodb-myisam-and-memory-storage-engines/)​
    
- Ne podpira BLOB/TEXT stolpcev[](https://mariadb.com/docs/server/server-usage/storage-engines/memory-storage-engine)​
    
- Večja poraba RAM-a[](https://tecadmin.net/choosing-between-innodb-myisam-and-memory-storage-engines/)​

## MERGE (MRG_MyISAM)

MERGE engine omogoča **združevanje več identičnih MyISAM tabel** v eno logično tabelo.[](https://www.mysqltutorial.org/mysql-administration/mysql-merge-storage-engine/)​

**Glavne lastnosti:**

- **Kolekcija MyISAM tabel** - združuje več MyISAM tabel z identično strukturo[](https://dev.mysql.com/doc/refman/8.4/en/merge-storage-engine.html)​
    
- **UNION parameter** - določa, katere tabele so vključene[](https://www.mysqltutorial.org/mysql-administration/mysql-merge-storage-engine/)​
    
- **INSERT_METHOD** - določa, kam gredo INSERT stavki (FIRST/LAST/NO)[](http://dev.cs.ovgu.de/db/mysql/MERGE.html)​
    
- **Samo .MRG file** - vsebuje seznam tabel, ne podatkov[](http://dev.cs.ovgu.de/db/mysql/MERGE.html)​
    
- **Podpira SELECT, INSERT, UPDATE, DELETE** - na združeni tabeli[](https://www.mysqltutorial.org/mysql-administration/mysql-merge-storage-engine/)​
    
- **Ni partitioning support** - ne more biti particionirana[](https://docs.oracle.com/cd/E17952_01/mysql-5.7-en/partitioning-limitations-storage-engines.html)​
    
- **MyISAM značilnosti** - table-level locking, brez transakcij[](https://www.baeldung.com/sql/mysql-storage-engine-types)​
    

**Kdaj uporabiti:**

- Distribucija podatkov med več fajli za boljšo organizacijo[](https://www.baeldung.com/sql/mysql-storage-engine-types)​
    
- Logging sistemi z rotacijo tabel[](https://severalnines.com/blog/exploring-storage-engine-options-mariadb/)​
    
- Data warehousing z velikimi dataseti[](https://www.baeldung.com/sql/mysql-storage-engine-types)​
    
- Paralelizacija myisamchk za repair po crash-u[](https://www.flamingspork.com/blog/2013/04/19/the-merge-storage-engine-not-dead-just-resting-or-forgotten/)​
    
- Premagovanje omejitev file system size[](https://www.flamingspork.com/blog/2013/04/19/the-merge-storage-engine-not-dead-just-resting-or-forgotten/)​
    

**Slabosti:**

- **Deprecated funkcionalnost** - PARTITIONING je boljša alternativa[](https://www.flamingspork.com/blog/2013/04/19/the-merge-storage-engine-not-dead-just-resting-or-forgotten/)​
    
- Samo za MyISAM tabele[](https://mariadb.com/docs/server/server-usage/storage-engines/choosing-the-right-storage-engine)​
    
- Brez paralelizacije poizvedb[](https://www.flamingspork.com/blog/2013/04/19/the-merge-storage-engine-not-dead-just-resting-or-forgotten/)​
    
- **Varnostna luknja** - uporabniki lahko dostopajo do tabel preko MERGE tudi po preklicu pravic[](https://www.flamingspork.com/blog/2013/04/19/the-merge-storage-engine-not-dead-just-resting-or-forgotten/)​
    
- Ne podpira partitioninga[](https://docs.oracle.com/cd/E17952_01/mysql-5.7-en/partitioning-limitations-storage-engines.html)​
    
- Omejene use case scenario - večinoma nadomeščen s PARTITIONING[](https://www.flamingspork.com/blog/2013/04/19/the-merge-storage-engine-not-dead-just-resting-or-forgotten/)​

## CSV

CSV engine shranjuje podatke v **text files v comma-separated-values formatu**.[](https://mariadb.com/docs/server/server-usage/storage-engines/csv/csv-overview)​

**Glavne lastnosti:**

- **Plain text files** - podatki shranjeni kot CSV datoteke[](https://fromdual.com/csv-storage-engine)​
    
- **Trije fajli**: .frm (table format), .CSV (podatki), .CSM (metadata)[](https://mariadb.com/docs/server/server-usage/storage-engines/csv/csv-overview)​
    
- **Brez indexov** - ne podpira indeksov[](https://www.mysqltutorial.org/mysql-administration/mysql-csv-storage-engine/)​
    
- **Brez transakcij** - ni ACID-compliant[](https://www.mysqltutorial.org/mysql-administration/mysql-csv-storage-engine/)​
    
- **Brez partitioning** - ni mogoče particionirati CSV tabel[](https://docs.oracle.com/cd/E17952_01/mysql-5.7-en/partitioning-limitations-storage-engines.html)​
    
- **Enostaven data exchange** - enostavna izmenjava podatkov z drugimi aplikacijami[](https://mariadb.com/docs/server/server-usage/storage-engines/csv/csv-overview)​
    
- **Privzet za logging** - uporabljen za SQL query logging to tables[](https://mariadb.com/docs/server/server-usage/storage-engines/csv/csv-overview)​
    

**Kdaj uporabiti:**

- Hiter data import/export[](https://www.baeldung.com/sql/mysql-storage-engine-types)​
    
- Izmenjava podatkov med aplikacijami[](https://stackoverflow.com/questions/26491823/when-to-use-csv-storage-engine-for-mysql)​
    
- Temporary data storage pri system migrations[](https://www.baeldung.com/sql/mysql-storage-engine-types)​
    
- Logging tabel (general_log, slow_query_log)[](https://mariadb.com/docs/server/server-usage/storage-engines/csv/csv-overview)​
    

**Slabosti:**

- **Brez indexov** - slaba query performance na velikih datasetih[](https://www.mysqltutorial.org/mysql-administration/mysql-csv-storage-engine/)​
    
- Brez transakcij[](https://www.mysqltutorial.org/mysql-administration/mysql-csv-storage-engine/)​
    
- Omejene funkcionalnosti[](https://www.mysqltutorial.org/mysql-administration/mysql-csv-storage-engine/)​
    
- **CONNECT engine je boljša alternativa** od MariaDB 10.0[](https://mariadb.com/docs/server/server-usage/storage-engines/csv/csv-overview)​
    
- Ne podpira partitioninga[](https://docs.oracle.com/cd/E17952_01/mysql-5.7-en/partitioning-limitations-storage-engines.html)

## Primerjava storage engines - ključne razlike

| Feature               | InnoDB            | MyISAM                   | Aria                      | MEMORY           | MERGE           | CSV            |
| --------------------- | ----------------- | ------------------------ | ------------------------- | ---------------- | --------------- | -------------- |
| **Transakcije**       | Da (ACID)         | Ne                       | Ne                        | Ne               | Ne              | Ne             |
| **Locking**           | Row-level         | Table-level              | Table-level               | Table-level      | Table-level     | Table-level    |
| **Foreign Keys**      | Da                | Ne                       | Ne                        | Ne               | Ne              | Ne             |
| **Crash-safe**        | Da                | Ne                       | Da                        | Ne               | Ne              | Ne             |
| **Full-text**         | Da (5.6+)         | Da                       | Da                        | Ne               | Da              | Ne             |
| **Compression**       | Da                | Da (myisampack)          | Ne                        | Ne               | Ne              | Ne             |
| **Indexes**           | B-tree, Full-text | B-tree, Full-text        | B-tree                    | HASH, B-tree     | B-tree          | Brez           |
| **Data Location**     | Disk              | Disk                     | Disk                      | RAM              | Disk (multiple) | Disk (CSV)     |
| **Best for**          | OLTP, Mixed       | Read-heavy               | Read-heavy, System tables | Temporary, Cache | Large datasets  | Data exchange  |
| **Zmogljivost Read**  | Dobra             | Odlična                  | Odlična                   | Izjemna          | Dobra           | Slaba          |
| **Zmogljivost Write** | Odlična           | Slaba (high concurrency) | Slaba                     | Dobra            | Slaba           | Dobra (append) |
| **Disk space**        | Večji             | Manjši                   | Srednji                   | RAM              | Manjši          | Majhen         |
| **Max key length**    | 3072 bytes        | 1000 bytes               | 2000 bytes                | 3072 bytes       | 1000 bytes      | N/A            |

**Ključni predlogi za uporabo:**

- **InnoDB** - standard za večino aplikacij, OLTP, transakcije[](https://severalnines.com/blog/exploring-storage-engine-options-mariadb/)​
    
- **MyISAM** - legacy sistemi, read-only arhivi, compressed tables[](https://blog.devart.com/myisam-vs-innodb.html)​
    
- **Aria** - system tables, temporary tables, read-heavy analytics[](https://mariadb.com/docs/server/server-usage/storage-engines/aria/aria-storage-engine)​
    
- **MEMORY** - session data, caching, temporary calculations[](https://www.mysqltutorial.org/mysql-administration/mysql-memory-storage-engine/)​
    
- **MERGE** - deprecated, zamenjaj s PARTITIONING[](https://www.flamingspork.com/blog/2013/04/19/the-merge-storage-engine-not-dead-just-resting-or-forgotten/)​
    
- **CSV** - data exchange, zamenjaj s CONNECT engineom[](https://mariadb.com/docs/server/server-usage/storage-engines/csv/csv-overview)​