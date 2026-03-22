---
tags:
  - CCNA1
  - application-layer
  - modul-15
aliases:
  - Modul 15
  - Application Layer
  - Aplikacijska plast
---


> [!summary] Cilj modula
> Razložiti delovanje **aplikacijske, predstavitvene in sejne plasti** ter osnovne aplikacijske protokole: HTTP/HTTPS, e‑pošta, DNS, DHCP in protokoli za deljenje datotek.[web:89][web:93]

---

## 15.1 Application, Presentation, Session

### Application Layer (OSI 7 / TCP-IP Application)

- Nudi **vmesnik med aplikacijami** (browser, mail client, FTP client) in omrežjem.[web:89]
- Uporablja **aplikacijske protokole**: HTTP, HTTPS, FTP, TFTP, SMTP, POP3, IMAP, DNS, DHCP, SMB …[web:89][web:92]
- Ne izvaja samega prenosa podatkov – to delajo nižje plasti (L4–L1), ampak **določi format zahtev/odgovorov**.[web:89]

### Presentation Layer (OSI 6)

Tri glavne funkcije:[web:89][web:92]

1. **Formatting** – pretvorba podatkov v skupen format (tekst, slike, zvok, video).
2. **Compression** – stiskanje in razširjanje podatkov.
3. **Encryption** – šifriranje pri pošiljanju, dešifriranje pri prejemu.

Primeri:
- Kodiranje znakov (**ASCII, UTF-8**),
- slike (JPEG, PNG), video (H.264),
- šifriranje (TLS pri HTTPS).[web:89][web:92]

### Session Layer (OSI 5)

- Ustvarja in vzdržuje **seje (dialogs)** med aplikacijami vira in cilja.[web:89]
- Skrbi za:
  - vzpostavitev, vzdrževanje in zaključek seje,
  - **ponovni zagon** seje, če je bila prekinjena ali predolgo neaktivna.[web:89][web:92]

> [!info] V TCP/IP modelu so **Application, Presentation, Session** združene v **Application layer**.

---

## 15.2 Client–Server in Peer‑to‑Peer

### Client–Server model

| Vloga | Opis |
|-------|------|
| **Client** | Zahteva storitve (brskalnik, mail odjemalec).[web:89] |
| **Server** | Odziva se na zahteve, nudi storitve (web, mail, DNS …).[web:89] |

- Protokol definira **format zahteve in odgovora** (npr. HTTP GET/response).[web:92]
- Strežniki so pogosto **centralizirani**, z varnostnimi in backup politikami.[web:89]

### Peer‑to‑Peer (P2P)

- Dve ali več naprav (peers) si **delita vire brez namenskega strežnika**.[web:92][web:89]
- Vsaka naprava je lahko **hkrati client in server**, odvisno od trenutne transakcije.[web:92]
- Primeri:
  - Windows file sharing med dvema PC-jema v domačem omrežju,
  - P2P aplikacije (torrent odjemalci ipd.).[web:92]

> [!important] P2P je fleksibilen in poceni, a slabše skalira in je težje varovati/upravljati kot centraliziran client–server.

---

## 15.3 Web in e‑mail protokoli

### HTTP in HTTPS

- **HTTP (Hypertext Transfer Protocol)** – aplikacijski protokol za prenos spletnih strani.[web:92][web:94]
- Teče nad TCP, tipično **port 80**.[web:94]
- **HTTPS** = HTTP + TLS/SSL šifriranje (tipično **port 443**).[web:94]

Osnovne metode:
- **GET** – klient zahteva vir (npr. `index.html`).[web:92][web:94]
- **POST** – klient pošlje podatke na strežnik (npr. obrazci).[web:94]
- **PUT/DELETE** – posodobitev/brisanje virov (REST API).[web:94]

> [!example] Tipičen tok:
> 1. Browser (client) vzpostavi TCP povezavo na `server:80` ali `server:443`.
> 2. Pošlje HTTP **GET** za `/index.html`.
> 3. Strežnik vrne HTML.
> 4. Browser prikaže stran.[web:89][web:94]

### E‑pošta: SMTP, POP3, IMAP

| Protokol | Namen | Porti (tipično) |
|----------|-------|-----------------|
| **SMTP** | Pošiljanje e‑pošte **od odjemalca na strežnik** ali **med strežniki**.[web:89][web:94] | TCP 25 (ali 587, 465) |
| **POP3** | Prenos sporočil z strežnika na klienta (običajno jih pobriše s strežnika).[web:89][web:94] | TCP 110 (995 TLS) |
| **IMAP** | Sinhronizirano branje pošte – sporočila ostanejo na strežniku, mapice itd.[web:89][web:94] | TCP 143 (993 TLS) |

- SMTP → “**push**” sporočil,
- POP3/IMAP → “**pull**” sporočil na odjemalca.[web:94]

---

## 15.4 IP Addressing Services: DNS in DHCP

### DNS – Domain Name System

- Pretvarja **domena → IP naslov** (npr. `www.cisco.com → 72.163.x.x`).[web:89][web:92]
- Uporablja **UDP in TCP port 53** (UDP za večino vprašanj, TCP za cone/večje odgovore).[web:89][web:94]
- DNS hierarhija: **root**, TLD (.com, .org, .si …), avtoritativni strežniki, rekurzivni resolverji.[web:89]

Osnovni potek:
1. Klient pošlje DNS query (navadno rekurzivnemu resolverju, npr. ISP‑ju).[web:89]
2. Resolver po potrebi sprašuje višje ravni (root → TLD → avtoritativni).
3. Odgovor (A, AAAA, MX zapis …) vrne klientu in ga **cacha**.[web:89]

Uporaben ukaz:
- `nslookup domena` (Windows/Linux) – ročna DNS poizvedba.[web:94]

### DHCP – Dynamic Host Configuration Protocol

- Dodeli **IPv4/IPv6 konfiguracijo**: IP naslov, maska, gateway, DNS …[web:89][web:94]
- **DHCPv4:** klient UDP **68**, strežnik UDP **67**.[web:94]
- Zmanjša ročno konfiguracijo, omogoča **ponovno uporabo** naslovov (lease).[web:89]

Osnovni DORA postopek (DHCPv4):[web:94]

1. **D**iscover – klient pošlje broadcast, da najde DHCP strežnik.
2. **O**ffer – strežnik ponudi naslov (DHCPOFFER).
3. **R**equest – klient izbere in zahteva določen offer.
4. **A**ck – strežnik potrdi (DHCPACK) in dodeli lease.

---

## 15.5 File Sharing Services: FTP, TFTP, SMB

### FTP – File Transfer Protocol

- Klasičen protokol za prenos datotek, uporablja **TCP** port **21 (control)** in **20 (data)**.[web:89][web:94]
- **Control connection (21)** – ukazi in odgovori (USER, PASS, LIST, RETR, STOR …).[web:94]
- **Data connection (20)** – dejanski prenos datotek, ustvarjen vsakič, ko se prenašajo podatki.[web:94]

> [!example] FTP tok:
> 1. Client vzpostavi TCP povezavo na **21** (ukazi).
> 2. Po loginu client zahteva seznam/datoteko.
> 3. Ustvari se nova TCP povezava na **20** za data.
> 4. Prenos v eno ali drugo smer (download/upload).[web:94]

### TFTP – Trivial File Transfer Protocol

- Enostaven protokol, uporablja **UDP 69**.[web:89][web:94]
- Brez autentikacije/zapisovanja seje – uporablja se za:
  - prenos konfiguracij,
  - prenos IOS slik v lab/test okoljih.[web:89]
- Zaradi varnosti se v produkciji uporablja previdno ali z izolacijo.[web:89]

### SMB – Server Message Block

- **SMB** (Windows file sharing) je client–server protokol za:[web:94]
  - deljenje datotek, map, tiskalnikov,
  - “Windows share” (`\\SERVER\share`).
- Deluje preko TCP (tipično **port 445**).[web:94]
- Uporablja se v Windows domenah, NAS napravah, Samba na Linuxu.

---

## 🔗 Povezave

- [[Modul 14 - Transport Layer]]
- [[Modul 11 - IPv4 Addressing]]
- [[Modul 12 - IPv6 Addressing]]

---

## ❓ Check Your Understanding

> [!question] Vprašanje 1  
> Katere tri OSI plasti združuje Application layer v TCP/IP modelu?
> > [!done]- Odgovor  
> > **Application, Presentation, Session** – vse tri tvorijo Application layer v TCP/IP modelu.

> [!question] Vprašanje 2  
> Naštej 3 funkcije predstavitvene (Presentation) plasti.
> > [!done]- Odgovor  
> > Formatiranje/predstavitev podatkov, kompresija/dekompresija, šifriranje/dešifriranje.[web:89][web:92]

> [!question] Vprašanje 3  
> Katera protokola se tipično uporabljata za web promet in na katerih portih?
> > [!done]- Odgovor  
> > **HTTP** na TCP **80** in **HTTPS** (HTTP + TLS) na TCP **443**.[web:94]

> [!question] Vprašanje 4  
> Kakšna je vloga DNS in kateri port uporablja?
> > [!done]- Odgovor  
> > DNS pretvarja domenska imena v IP naslove in obratno, uporablja **UDP/TCP port 53**.[web:89][web:94]

> [!question] Vprašanje 5  
> Opiši DORA postopek pri DHCPv4.
> > [!done]- Odgovor  
> > **Discover → Offer → Request → Acknowledgment (ACK)** – klient odkrije strežnik, dobi ponudbo, izbere ponudbo, strežnik jo potrdi.[web:94]

> [!question] Vprašanje 6  
> Kakšna je razlika med FTP in TFTP?
> > [!done]- Odgovor  
> > FTP uporablja **TCP, porta 21/20**, podpira prijavo in kontrolno povezavo; TFTP uporablja **UDP 69**, je preprost, brez avtentikacije in se uporablja predvsem za tehnični prenos konfiguracij/IOS datotek.[web:89][web:94]
