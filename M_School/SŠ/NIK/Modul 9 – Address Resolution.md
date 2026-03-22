---
tags:
  - CCNA1
  - ARP
  - address-resolution
  - IPv6-ND
  - modul-9
aliases:
  - Modul 9
  - Address Resolution
  - ARP
---


> [!summary] Cilj modula
> Razložiti, kako ARP (IPv4) in Neighbor Discovery (IPv6) omogočata komunikacijo z razrešitvijo naslovov.

---

## 9.1 MAC in IP naslov – vlogi

Vsak okvir, ki potuje po omrežju, potrebuje **dva naslova**:

| Naslov | Plast | Namen | Se menja? |
|--------|-------|--------|-----------|
| **IP naslov** | Layer 3 | Identifikacija gosta v omrežju (end-to-end) | ❌ Ne (ostane isti skozi celotno pot) |
| **MAC naslov** | Layer 2 | Dostava v lokalnem segmentu (hop-to-hop) | ✅ Da (zamenja se na vsakem routerju) |

> [!example] Analogija
> IP naslov = poštna naslov (kjer živiš → cilj paketa)
> MAC naslov = ime voznika dostave (kdo ga fizično pripelje do vrat)

### Problem: IP znan, MAC neznan

Ko gost želi poslati paket:
1. **Pozna destination IP** (iz DNS ali ročno)
2. **Ne pozna destination MAC** → ne more sestaviti Ethernet okvirja!

→ Rešitev: **ARP** (za IPv4) ali **Neighbor Discovery** (za IPv6)

---

## 9.2 ARP – Address Resolution Protocol (IPv4)

> [!info] ARP = "Kdo ima ta IP naslov? Povej mi svojo MAC!"

### Dve funkciji ARP

1. **Razrešitev** IPv4 naslova v MAC naslov
2. **Vzdrževanje** ARP tabele (cache) z mapiranji IPv4 ↔ MAC

### ARP tabela

- Shranjena v **RAM** (začasno)
- Vsak vnos ima **timer** → vnosi brez uporabe se samodejno izbrišejo
- Pregled: `arp -a` (Windows/Linux)
arp -a  
Interface: 192.168.1.5  
Internet Address Physical Address Type  
192.168.1.1 a4-77-33-xx-xx-xx dynamic  
192.168.1.10 00-0a-1b-xx-xx-xx dynamic

---

## 9.3 Delovanje ARP – korak za korakom

### Korak 1: Pošiljatelj preveri ARP tabelo
Ali je destination IPv4 v moji ARP tabeli?  
├── DA → vzemi MAC iz tabele → sestavi okvir → pošlji  
└── NE → pošlji ARP Request (broadcast)

### Korak 2: ARP Request (broadcast)

| Polje | Vrednost |
|-------|---------|
| Dst MAC | `FF:FF:FF:FF:FF:FF` ← **broadcast** |
| Src MAC | MAC pošiljatelja |
| Vsebina | "Kdo ima IP 192.168.1.1? Jaz sem 192.168.1.5" |

[!important] ARP Request je **broadcast** → prejmejo VSE naprave v LAN!
Switch ga posreduje na **vse porte** (flooding).

### Korak 3: ARP Reply (unicast)

- Samo naprava z ujemajočim IP odgovori
- Odgovor je **unicast** nazaj k pošiljatelju
- Vsebina: "Jaz imam IP 192.168.1.1, moj MAC je XX:XX:XX:XX"

### Korak 4: Posodobitev ARP tabele

- Pošiljatelj doda vnos v ARP tabelo
- Sestavi Ethernet okvir z zdaj znano MAC
- Pošlje paket

---

## 9.4 ARP za default gateway

Ko je destination IP v **drugem omrežju** (remote host):
Gost ne pošlje ARP za remote IP!  
→ Pošlje ARP za IP default gateway-a  
→ Dobi MAC routerja  
→ Pošlje okvir routerju (ki ga naprej posreduje)

[!tip] Gost nikoli direktno pošlje ARP za IP naslov, ki je v drugem omrežju – to se vedno razreši prek default gateway-a!

---

## 9.5 ARP varnostne težave

| Napad | Opis |
|-------|------|
| **ARP Poisoning / ARP Spoofing** | Napadalec pošilja lažne ARP Reply-e → zastrupi ARP tabele → man-in-the-middle napad |
| **ARP Flood** | Množica ARP zahtev preplavi switch → denial of service |

[!warning] Zaščita: Dynamic ARP Inspection (DAI) na switchih – preveri ARP pakete glede na DHCP snooping tabelo.

---

## 9.6 IPv6 Neighbor Discovery (ND)

[!info] IPv6 **ne uporablja ARP**! Namesto njega je **ICMPv6 Neighbor Discovery (ND)** protokol.

### ND sporočila (ICMPv6)

| Sporočilo | Kratica | Namen | Analogija z ARP |
|-----------|---------|-------|----------------|
| **Neighbor Solicitation** | NS | "Kdo ima ta IPv6 naslov?" | ARP Request |
| **Neighbor Advertisement** | NA | "Jaz imam ta IPv6 naslov, tukaj je moj MAC" | ARP Reply |
| **Router Solicitation** | RS | Gost išče routerje v omrežju | — |
| **Router Advertisement** | RA | Router oglašuje svojo prisotnost + prefix | — |

### Ključne razlike ARP vs ND

| | ARP (IPv4) | ND / ICMPv6 (IPv6) |
|-|-----------|-------------------|
| Protokol | ARP | ICMPv6 (tip 135/136) |
| Request naslov | Broadcast (`FF:FF:FF:FF:FF:FF`) | Multicast (solicited-node) |
| Overhead | Višji (broadcast) | Nižji (multicast) ✅ |
| Tabela | ARP cache | Neighbor cache |
| Ukaz za pregled | `arp -a` | `netsh interface ipv6 show neighbors` |

[!info] Solicited-node multicast naslov
IPv6 NS se ne pošlje vsem (broadcast), ampak samo ciljni **solicited-node multicast skupini**:
`FF02::1:FF` + zadnji 24 bitov target IPv6 naslova
→ Manj naprav mora obdelati zahtevo!

### Router Advertisement (RA)

- Router periodično ali na zahtevo (RS) pošilja RA
- RA vsebuje: IPv6 **prefix omrežja**, dolžino prefiksa, default gateway info
- Gost si konfigurira IPv6 naslov samodejno → **SLAAC** (Stateless Address Autoconfiguration)

---

## 9.7 Cisco IOS ukazi za ARP

```cisco
show arp                         → Prikaži ARP tabelo routerja
show ip arp                      → Enako (alternativni ukaz)
clear arp-cache                  → Počisti ARP cache
debug arp                        → Live debug ARP prometa
```

Na PC (Windows):
arp -a → Prikaži ARP tabelo  
arp -d → Izbriši ARP tabelo

---

## 🔗 Povezave

- [[Modul 8 - Network Layer]]
- [[Modul 10 - Basic Router Configuration]]

---

## ❓ Check Your Understanding

[!question] Vprašanje 1
Kateri naslov se uporabi kot destination MAC v ARP Request?
> [!done]- Odgovor
> **FF:FF:FF:FF:FF:FF** – broadcast naslov → sprejmejo vse naprave v LAN.

[!question] Vprašanje 2
Kateri dve funkciji opravlja ARP?
> [!done]- Odgovor
> 1. Razrešitev IPv4 → MAC naslov
> 2. Vzdrževanje ARP tabele (cache) z mapiranji

[!question] Vprašanje 3
Kaj naredi gost, ko želi doseči IP v drugem omrežju?
> [!done]- Odgovor
> Pošlje ARP za **IP default gateway-a** (routerja) – ne za oddaljeni IP.

[!question] Vprašanje 4
Katera ICMPv6 sporočila nadomeščajo ARP pri IPv6?
> [!done]- Odgovor
> **Neighbor Solicitation (NS)** = ARP Request, **Neighbor Advertisement (NA)** = ARP Reply

[!question] Vprašanje 5
Zakaj je IPv6 ND učinkovitejši od ARP?
> [!done]- Odgovor
> NS se pošlje na **solicited-node multicast** (ne broadcast) → manj naprav mora procesirati zahtevo.

[!question] Vprašanje 6
Kaj je ARP Poisoning?
> [!done]- Odgovor
> Napad, kjer napadalec pošilja lažne ARP Reply-e in zastrupi ARP tabele → man-in-the-middle napad.