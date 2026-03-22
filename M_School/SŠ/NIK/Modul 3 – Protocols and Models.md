---
tags:
  - CCNA1
  - OSI
  - TCP-IP
  - protokoli
  - modul-3
aliases:
  - Modul 3
  - Protocols and Models
  - OSI model
---



> [!summary] Cilj modula
> Razložiti vlogo protokolov in modelov (OSI, TCP/IP) pri komunikaciji v omrežjih.

---

## 3.1 Komunikacijska pravila (osnove)

Vsaka komunikacija potrebuje:
1. **Vir (source)** → pošiljatelj
2. **Cilj (destination)** → prejemnik
3. **Kanal (channel/medium)** → pot prenosa

### Elementi protokola

- **Message encoding** → pretvorba sporočila v primerno obliko za prenos
- **Message formatting** → struktura sporočila
- **Message size** → razdelitev na pakete
- **Message timing** → flow control, response timeout
- **Message delivery options** → unicast, multicast, broadcast

---

## 3.2 Omrežni protokoli

> [!info] Protokol = dogovorjena pravila za komunikacijo med napravami

### Zakaj so protokoli pomembni

- Zagotavljajo **interoperabilnost** → naprave različnih proizvajalcev komunicirajo
- Definirani z **RFC** (Request for Comments) dokumenti pri IETF

### Kategorije protokolov

| Kategorija | Primeri |
|-----------|---------|
| **Network communications** | IP, TCP, UDP, HTTP |
| **Network security** | SSH, TLS/SSL, HTTPS |
| **Routing** | OSPF, EIGRP, BGP |
| **Service discovery** | DHCP, DNS |

---

## 3.3 Protokolni sklad (Protocol Suite)

- **Protocol suite** = skupina protokolov, ki skupaj zagotavljajo celotno komunikacijo
- Najpomembnejši: **TCP/IP suite** (internet standard)
- Zgodovinski: Novell IPX/SPX, Apple AppleTalk (zastareli)

### TCP/IP Suite – plasti

| Plast TCP/IP | Protokoli |
|-------------|-----------|
| **Application** | HTTP, HTTPS, DNS, DHCP, FTP, SMTP, POP3, IMAP |
| **Transport** | TCP, UDP |
| **Internet** | IP, ICMP, ARP |
| **Network Access** | Ethernet, Wi-Fi (802.11), PPP |

---

## 3.4 Standardizacijske organizacije

| Organizacija | Polno ime | Področje |
|-------------|-----------|----------|
| **IETF** | Internet Engineering Task Force | TCP/IP, RFC dokumenti |
| **IEEE** | Institute of Electrical and Electronics Engineers | Ethernet (802.3), Wi-Fi (802.11) |
| **ISO** | International Organization for Standardization | OSI model |
| **IANA** | Internet Assigned Numbers Authority | IP naslovi, port številke |
| **ICANN** | Internet Corporation for Assigned Names and Numbers | Domene, DNS |

---

## 3.5 Referenčni modeli

### OSI Model (7 plasti)

| #   | Plast          | Ang. naziv   | PDU     | Ključna funkcija                            |
| --- | -------------- | ------------ | ------- | ------------------------------------------- |
| 7   | Aplikacijska   | Application  | Data    | Vmesnik za aplikacije (HTTP, FTP, DNS)      |
| 6   | Predstavitvena | Presentation | Data    | Kodiranje, šifriranje, kompresija           |
| 5   | Seja           | Session      | Data    | Vzpostavljanje/zaključevanje sej            |
| 4   | Transportna    | Transport    | Segment | End-to-end zanesljivost (TCP/UDP)           |
| 3   | Omrežna        | Network      | Packet  | Logično naslavljanje, routing (IP)          |
| 2   | Podatkovna     | Data Link    | Frame   | Fizično naslavljanje, MAC, dostop do medija |
| 1   | Fizična        | Physical     | Bits    | Prenos bitov po mediju                      |

> [!tip] Mnemoehnika OSI 7→1
> **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing
> (Application, Presentation, Session, Transport, Network, Data Link, Physical)

### TCP/IP Model vs OSI Model

| TCP/IP | OSI plasti |
|--------|-----------|
| Application | 7 Application + 6 Presentation + 5 Session |
| Transport | 4 Transport |
| Internet | 3 Network |
| Network Access | 2 Data Link + 1 Physical |

> [!info] Zakaj dva modela?
> - **OSI** = teorijski referenčni model (troubleshooting, opis)
> - **TCP/IP** = praktični model (dejansko implementiran na internetu)

---

## 3.6 Data Encapsulation (Enkapsulacija)

> [!important] Enkapsulacija = dodajanje glav (headers) na vsaki plasti pri pošiljanju

### Proces (pošiljanje)
Aplikacija → Data  
Transport → Segment (doda TCP/UDP glavo)  
Omrežna → Packet (doda IP glavo)  
Podatkovna → Frame (doda MAC glavo + FCS)  
Fizična → Bits (pretvori v elektr./optični signal)


### De-enkapsulacija (sprejemanje) = obraten proces

| PDU | Plast | Vsebina |
|-----|-------|---------|
| **Data** | Application | Originalni podatki |
| **Segment** | Transport | Data + TCP/UDP header |
| **Packet** | Network | Segment + IP header |
| **Frame** | Data Link | Packet + MAC header + FCS trailer |
| **Bits** | Physical | Frame v binarni / električni obliki |

> [!example] Primer: HTTP zahteva
> Browser pošlje HTTP zahtevo →
> TCP doda port 80 header → Segment
> IP doda src/dst IP → Packet
> Ethernet doda src/dst MAC → Frame
> NIC pretvori v električne signale → Bits po žici

---

## 3.7 Naslovi na različnih plasteh

| Plast | Naslov | Namen |
|-------|--------|--------|
| **Transport (L4)** | Port number (0–65535) | Katera aplikacija? |
| **Network (L3)** | IP naslov (IPv4/IPv6) | Kateri host v omrežju? |
| **Data Link (L2)** | MAC naslov (48-bit, hex) | Katera naprava v LAN? |

### Pomembne port številke

| Port | Protokol |
|------|----------|
| 80 | HTTP |
| 443 | HTTPS |
| 22 | SSH |
| 23 | Telnet |
| 21 | FTP |
| 25 | SMTP |
| 53 | DNS |
| 67/68 | DHCP |

---

## 🔗 Povezave

- [[Modul 2 - Basic Switch and End Device Configuration]]
- [[Modul 4 - Physical Layer]]

---

## ❓ Check Your Understanding

> [!question] Vprašanje 1
> Naštej 7 plasti OSI modela od vrha navzdol.
> > [!done]- Odgovor
> > Application, Presentation, Session, Transport, Network, Data Link, Physical

> [!question] Vprašanje 2
> Kako se imenuje PDU na transportni plasti?
> > [!done]- Odgovor
> > **Segment**

> [!question] Vprašanje 3
> Kaj je enkapsulacija?
> > [!done]- Odgovor
> > Dodajanje glav na vsaki plasti pri pošiljanju podatkov navzdol po protokolnem skladu.

> [!question] Vprašanje 4
> Kakšna je razlika med OSI in TCP/IP modelom?
> > [!done]- Odgovor
> > OSI = 7-plastni teoretični model za opis in troubleshooting. TCP/IP = 4-plastni praktični model, ki se dejansko uporablja na internetu.
> >