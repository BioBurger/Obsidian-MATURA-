---
tags:
  - CCNA1
  - network-layer
  - IPv4
  - IPv6
  - routing
  - modul-8
aliases:
  - Modul 8
  - Network Layer
  - Omrežna plast
---



> [!summary] Cilj modula
> Razložiti, kako omrežna plast (Layer 3) zagotavlja komunikacijo med omrežji z IP protokolom in usmerjanjem.

---

## 8.1 Karakteristike omrežne plasti

**Network Layer = OSI Layer 3** → prenos paketov med gosti (end-to-end)

### Štiri procese omrežne plasti

1. **Naslavljanje** (Addressing) → vsak gost dobi unikaten IP naslov
2. **Enkapsulacija** → L4 segment se ovije v IP paket (doda IP header)
3. **Usmerjanje** (Routing) → router izbere najboljšo pot do cilja
4. **De-enkapsulacija** → cilj odstrani IP header, preda L4 segmentu

### Lastnosti IP protokola

| Lastnost | Opis |
|----------|------|
| **Connectionless** | Ni vzpostavljene povezave pred pošiljanjem |
| **Best Effort (Unreliable)** | Ni garancije dostave – brez potrdil (ACK) |
| **Media Independent** | Ne zanima ga fizični medij – deluje na UTP, fiber, wireless |

> [!info] Zanesljivost zagotavlja Layer 4 (TCP) – ne IP!

---

## 8.2 IPv4 paket – struktura

### IPv4 header polja

| Polje | Velikost | Opis |
|-------|----------|------|
| **Version** | 4 biti | IP verzija → `0100` = IPv4 |
| **IHL** (Header Length) | 4 biti | Dolžina headerja v 32-bitnih besedah |
| **DSCP** | 6 bitov | QoS prioritizacija |
| **Total Length** | 16 bitov | Celotna velikost paketa (header + data) |
| **Identification** | 16 bitov | ID za fragmentacijo |
| **Flags** | 3 biti | Nadzor fragmentacije (DF, MF biti) |
| **Fragment Offset** | 13 bitov | Položaj fragmenta |
| **TTL** (Time to Live) | 8 bitov | Maks. število hopov – zmanjša se za 1 pri vsakem routerju |
| **Protocol** | 8 bitov | Tip L4 protokola: TCP=6, UDP=17, ICMP=1 |
| **Header Checksum** | 16 bitov | Preverjanje napak v headerju |
| **Source IP** | 32 bitov | IP naslov pošiljatelja |
| **Destination IP** | 32 bitov | IP naslov prejemnika |

> [!important] Ko TTL doseže 0 → router paket zavrže in pošlje ICMP "Time Exceeded" naprej!

### Fragmentacija

- IPv4 paket se **razdeli** (fragmentira), če je večji od MTU naslednjega medija
- **MTU** (Maximum Transmission Unit) = maks. velikost okvirja, privzeto **1500 bajtov** na Ethernetu
- Fragmentirane pakete **sestavi cilj** (destination host)
- **IPv6 ne fragmentira** na routerjih – za to poskrbi pošiljatelj!

---

## 8.3 IPv6 paket – struktura

### Zakaj IPv6?

- IPv4 naslovni prostor izčrpan (~4,3 milijarde naslovov)
- IPv6 = **128-bitni** naslovi → 340 undecilijonov naslovov

### IPv6 header (poenostavljen!)

| Polje | Velikost | Opis |
|-------|----------|------|
| **Version** | 4 biti | `0110` = IPv6 |
| **Traffic Class** | 8 bitov | QoS (ekvivalent DSCP pri IPv4) |
| **Flow Label** | 20 bitov | Označuje tok paketov za QoS |
| **Payload Length** | 16 bitov | Dolžina podatkov za headerjem |
| **Next Header** | 8 bitov | Tip naslednjega headerja (TCP=6, UDP=17, ICMPv6=58) |
| **Hop Limit** | 8 bitov | Enako kot TTL pri IPv4 |
| **Source IPv6** | 128 bitov | IPv6 naslov pošiljatelja |
| **Destination IPv6** | 128 bitov | IPv6 naslov prejemnika |

### IPv4 vs IPv6 primerjava

| | IPv4 | IPv6 |
|-|------|------|
| Dolžina naslova | 32 bitov | 128 bitov |
| Header velikost | 20–60 bajtov (spremenljiv) | 40 bajtov (fiksen) |
| Fragmentacija | Router ali host | Samo host |
| Broadcast | ✅ Da | ❌ Ne (nadomeščen z multicast) |
| Checksum v headerju | ✅ Da | ❌ Ne |
| TTL / Hop Limit | TTL | Hop Limit |
| Polje za QoS | DSCP | Traffic Class + Flow Label |

---

## 8.4 Kako gost pošlje paket (Host Routing)

Vsak gost se odloči: je destinacija **lokalna** ali **oddaljena**?
Pošiljatelj:  
IP_src & Subnet_mask → Moja omrežna addr  
IP_dst & Subnet_mask → Destinacijska omrežna addr

Če sta enaki → LOCAL (pošlji direktno v LAN)  
Če sta različni → REMOTE (pošlji na default gateway)

### Posebni naslovi

| Naslov | Opis |
|--------|------|
| `127.0.0.1` | **Loopback** IPv4 – testiranje TCP/IP sklada |
| `::1` | **Loopback** IPv6 |
| Default Gateway | Router v lokalnem omrežju → vrata v svet |

### Routing tabela na gostem
route print (Windows)  
netstat -r (Windows/Linux)

Tabela vsebuje:
- **Direktno povezano** omrežje (own IP / own interface)
- **Lokalno omrežje** (LAN segment)
- **Default route** `0.0.0.0/0` → vse ostalo gre na default gateway

---

## 8.5 Delovanje routerja

Router posreduje pakete med **različnimi omrežji**.

### Routing tabela routerja

```cisco
show ip route        → Prikaži routing tabelo (IPv4)
show ipv6 route      → Prikaži routing tabelo (IPv6)
```

### Viri route vnosov (oznake v `show ip route`)

| Koda | Vir | Opis |
|------|-----|------|
| **C** | Connected | Direktno priključeno omrežje |
| **L** | Local | IP naslov routerjevega vmesnika |
| **S** | Static | Ročno konfigurirana statična pot |
| **O** | OSPF | Dinamično – OSPF protokol |
| **D** | EIGRP | Dinamično – EIGRP protokol |
| **R** | RIP | Dinamično – RIP protokol |
| **\*** | Default | Default route (kandidat) |

[!example] Primer izhoda show ip route
Destinacija: 192.168.1.55  
Tabela:  
192.168.0.0/16 → manj specifično  
192.168.1.0/24 → bolj specifično ← IZBERE TO  
192.168.1.0/25 → še bolj specifično ← ali to, če obstaja

### Statično vs dinamično usmerjanje

| | Statično | Dinamično |
|-|----------|-----------|
| Konfiguracija | Ročno | Samodejno (protokol) |
| Primerno za | Majhna omrežja | Velika, kompleksna omrežja |
| Overhead | Brez | Porabi pasovno širino |
| Odziv na spremembe | Manuel update | Samodejno |
| Primeri | `ip route` ukaz | OSPF, EIGRP, RIP, BGP |

---

## 8.6 Administrativna razdalja (AD) in metrika

| Pojem | Opis |
|-------|------|
| **Administrative Distance** | Zaupljivost vira route (nižje = boljše) |
| **Metric** | Cena poti znotraj protokola (nižje = boljše) |

### Administrativna razdalja – pogosti protokoli

| Protokol | AD |
|----------|-----|
| Connected | 0 |
| Static | 1 |
| EIGRP | 90 |
| OSPF | 110 |
| RIP | 120 |
| External BGP | 20 |

---

## 🔗 Povezave

- [[Modul 7 - Ethernet Switching]]
- [[Modul 9 - Address Resolution]]

---

## ❓ Check Your Understanding

[!question] Vprašanje 1
Kateri tri lastnosti ima IP protokol?
> [!done]- Odgovor
> **Connectionless**, **Best Effort (Unreliable)**, **Media Independent**

[!question] Vprašanje 2
Kaj pomeni TTL polje v IPv4 paketu?
> [!done]- Odgovor
> Time to Live – zmanjša se za 1 na vsakem routerju. Ko doseže 0, router paket zavrže in pošlje ICMP "Time Exceeded" sporočilo.

[!question] Vprašanje 3
Kakšna je razlika med IPv4 in IPv6 glede fragmentacije?
> [!done]- Odgovor
> IPv4: router ali host fragmentira. IPv6: **samo host** fragmentira – routerji tega ne počno.

[!question] Vprašanje 4
Kaj je Longest Prefix Match?
> [!done]- Odgovor
> Router izbere **najbolj specifično** (najdaljšo) ujemajočo pot v routing tabeli.

[!question] Vprašanje 5
Katera koda v `show ip route` označuje direktno priključeno omrežje?
> [!done]- Odgovor
> **C** (Connected)

[!question] Vprašanje 6
Kdaj gost pošlje paket na default gateway?
> [!done]- Odgovor
> Ko je destinacija v **drugem omrežju** (remote host) – torej ko se omrežni del src in dst IP razlikuje.