---
tags:
  - CCNA1
  - IPv6
  - naslavljanje
  - SLAAC
  - DHCPv6
  - modul-12
aliases:
  - Modul 12
  - IPv6 Addressing
  - IPv6 naslavljanje
---


> [!summary] Cilj modula
> Implementirati shemo IPv6 naslavljanja – statično in dinamično (SLAAC, DHCPv6).

---

## 12.1 Zakaj IPv6?

### Pomanjkljivosti IPv4

- IPv4 = 32 bitov → ~**4,3 milijarde** naslovov
- Naslovni prostor je **izčrpan** (IANA razdelil zadnje bloke že 2011)
- Rešitve kot NAT so le začasne in vnašajo kompleksnost

### Prednosti IPv6

- IPv6 = 128 bitov → **340 undecilijonov** naslovov (3,4 × 10³⁸)
- Poenostavljen header (fiksen, 40 bajtov)
- Brez broadcast (nadomeščen z multicast)
- Vgrajen IPsec (varnost)
- Brez NAT – vsaka naprava dobi javni naslov
- Boljši QoS (Flow Label polje)

### Prehod IPv4 → IPv6

| Metoda | Opis |
|--------|------|
| **Dual Stack** | IPv4 in IPv6 delujeta **hkrati** na isti napravi |
| **Tunneling** | IPv6 paket se **enkapsulira** v IPv4 paket za transport |
| **Translation (NAT64)** | IPv6 paketi se **pretvorijo** v IPv4 in obratno |

---

## 12.2 Zapis IPv6 naslovov

- 128 bitov = **8 skupin × 16 bitov**, vsaka v **heksadecimalno**
- Ločene z **dvopičjem** `:`
- Primer: `2001:0DB8:ACAD:0001:0000:0000:0000:0001`

### Pravila krajšanja

**Pravilo 1:** Vodilne ničle v skupini se **izpustijo**

0DB8 → DB8  
0001 → 1  
0000 → 0

**Pravilo 2:** Ena ali več zaporednih skupin samih ničel → zamenjaj z `::` (**samo enkrat!**)

2001:DB8:ACAD:1:0:0:0:1 → 2001:DB8:ACAD:1::1

> [!warning] `::` se lahko uporabi **samo enkrat** v naslovu!
> `2001::1::1` je NAPAČNO.

> [!example] Primeri krajšanja
> ```
> Polno:     2001:0DB8:0000:0000:0000:0000:0000:0001
> Korak 1:   2001:DB8:0:0:0:0:0:1
> Korak 2:   2001:DB8::1
> ```

---

## 12.3 Vrste IPv6 naslovov

| Vrsta | Prefix | Opis |
|-------|--------|------|
| **Global Unicast (GUA)** | `2000::/3` (začne z 2 ali 3) | Javno usmerljiv – ekvivalent public IPv4 |
| **Link-Local (LLA)** | `FE80::/10` | Samo v lokalnem segmentu, NI usmerljiv |
| **Unique Local** | `FC00::/7` | Zasebna raba (ekvivalent RFC1918) |
| **Loopback** | `::1/128` | Lokalno testiranje |
| **Unspecified** | `::/128` | Nedefiniran naslov (source pri boot) |
| **Multicast** | `FF00::/8` | Skupina naprav |

> [!important] Vsak IPv6 vmesnik **mora** imeti LLA!
> LLA se avtomatično generira ob zagonu vmesnika.

### Global Unicast Address (GUA) – struktura
Dodeli ISP/RIR Organizacija Naprava

- Skupaj: 48 + 16 + 64 = **128 bitov**
- Subnet ID = organizacija ima 2¹⁶ = **65536 podomrežij**!

---

## 12.4 Statična konfiguracija IPv6

### Na routerju

```cisco
R1(config)# ipv6 unicast-routing               → OBVEZNO za IPv6 routing!

R1(config)# interface gigabitethernet 0/0/0
R1(config-if)# ipv6 address 2001:DB8:ACAD:1::1/64   → GUA
R1(config-if)# ipv6 address FE80::1 link-local       → LLA (ročno)
R1(config-if)# no shutdown

R1(config)# interface gigabitethernet 0/0/1
R1(config-if)# ipv6 address 2001:DB8:ACAD:2::1/64
R1(config-if)# ipv6 address FE80::2 link-local
R1(config-if)# no shutdown
```

> [!tip] LLA nastavimo ročno za **predvidljivost** – enostavnejši debug in ND konfiguracija.

### Na gostem (PC)

- Statično: ročno vnesi IPv6, prefix dolžino, default gateway (LLA routerja)
- Dinamično: SLAAC ali DHCPv6

---

## 12.5 Dinamično naslavljanje IPv6

### SLAAC – Stateless Address Autoconfiguration

> [!info] SLAAC = naprava si **sama generira** GUA brez DHCP strežnika

**Postopek:**
1. Gost pošlje **Router Solicitation (RS)** na `FF02::2` (vsi routerji)
2. Router odgovori z **Router Advertisement (RA)**:
   - IPv6 prefix omrežja (npr. `2001:DB8:ACAD:1::/64`)
   - Default gateway (LLA routerja)
3. Gost vzame prefix + generira **Interface ID** (64 bitov)
4. Nastali naslov preveri z **DAD** (Duplicate Address Detection)

**Interface ID generiranje:**
- **EUI-64** metoda: iz MAC naslova (vstavi `FFFE` na sredino, invertira 7. bit)
- **Naključno** (privacy extensions) – danes privzeto v modernih OS

> [!example] EUI-64 iz MAC 00:1A:2B:3C:4D:5E
> ```
> MAC:    00:1A:2B : 3C:4D:5E
> Vstavi: 00:1A:2B:FF:FE:3C:4D:5E
> Invertaj 7. bit: 02:1A:2B:FF:FE:3C:4D:5E
> Interface ID: 021A:2BFF:FE3C:4D5E
> ```

### Tri metode dodelitve (iz RA)

| Metoda | RA sporočilo | Naslov | DNS/ostalo |
|--------|-------------|--------|-----------|
| **SLAAC** (Method 1) | A=1, O=0, M=0 | Gost sam (SLAAC) | Iz RA |
| **SLAAC + Stateless DHCPv6** (Method 2) | A=1, O=1, M=0 | Gost sam (SLAAC) | Iz DHCPv6 strežnika |
| **Stateful DHCPv6** (Method 3) | A=0, M=1 | Iz DHCPv6 strežnika | Iz DHCPv6 strežnika |

> [!tip] Flags v RA:
> - **A** = Autonomous (SLAAC)
> - **O** = Other (stateless DHCP za info)
> - **M** = Managed (stateful DHCP)

### DAD – Duplicate Address Detection

- Preden naprava začne uporabljati naslov, pošlje **NS** na ta naslov
- Če nihče ne odgovori → naslov je unikaten ✅
- Če kdo odgovori → **naslov je zaseden** ❌ → napaka!

---

## 12.6 Link-Local Address (LLA) – podrobno

- Prefix: `FE80::/10`
- **Obvezen** na vsakem IPv6 vmesniku
- **Ni usmerljiv** – router tega paketa ne bo posredoval naprej
- Uporablja se za: ND (NS/NA/RS/RA), routing protokoli (next-hop)

### Ročna konfiguracija LLA

```cisco
R1(config-if)# ipv6 address FE80::1 link-local
```

### Avtomatična generacija

Ko vklopiš vmesnik z IPv6, OS/IOS samodejno generira LLA z EUI-64 ali naključno.

---

## 12.7 IPv6 Multicast naslovi

| Naslov | Skupina | Namen |
|--------|---------|-------|
| `FF02::1` | Vsi IPv6 gosti | Broadcast ekvivalent |
| `FF02::2` | Vsi IPv6 routerji | RS sporočila |
| `FF02::5` | Vsi OSPF routerji | OSPF Hello |
| `FF02::1:FF00:0/104` | Solicited-node | ARP zamenjava (ND) |

> [!info] Solicited-node multicast
> `FF02::1:FF` + zadnji 24 bitov IPv6 naslova
> Primer: naslov `2001:DB8::A3B4:C5D6` → solicited-node: `FF02::1:FFB4:C5D6`

---

## 12.8 Subnetting IPv6

IPv6 subnetting je **bistveno enostavnejše** kot IPv4!

### Tipična shema: /48 → /64
Organizacija dobi: 2001:DB8:ACAD::/48  
Subnet ID = biti 49-64 = 16 bitov → 2¹⁶ = 65.536 podomrežij!  
Vsako podomrežje /64 → 2⁶⁴ naslovov za goste

> [!example] Podomrežja iz 2001:DB8:ACAD::/48
> ```
> Subnet 1: 2001:DB8:ACAD:0001::/64
> Subnet 2: 2001:DB8:ACAD:0002::/64
> Subnet 3: 2001:DB8:ACAD:0003::/64
> ...
> Zadnji:   2001:DB8:ACAD:FFFF::/64
> ```

---

## 12.9 Verify IPv6

```cisco
show ipv6 interface brief              → Kratek pregled IPv6 vmesnikov
show ipv6 interface [vmesnik]          → Detajli (GUA, LLA, multicast)
show ipv6 route                        → IPv6 routing tabela
show ipv6 neighbors                    → Neighbor cache (ekvivalent ARP tabele)
```

---

## 🔗 Povezave

- [[Modul 11 - IPv4 Addressing]]
- [[Modul 9 - Address Resolution]]

---

## ❓ Check Your Understanding

> [!question] Vprašanje 1
> Kateri prefix ima link-local IPv6 naslov?
> > [!done]- Odgovor
> > **FE80::/10** – ni usmerljiv, obvezen na vsakem vmesniku.

> [!question] Vprašanje 2
> Kako skrajšamo `2001:0DB8:0000:0000:0000:0000:0000:0001`?
> > [!done]- Odgovor
> > `2001:DB8::1` (izpustimo vodilne ničle + nadomestimo ničelne skupine z `::`)

> [!question] Vprašanje 3
> Kaj je SLAAC?
> > [!done]- Odgovor
> > Stateless Address Autoconfiguration – naprava si sama generira GUA iz RA prefiksa + Interface ID, brez DHCP strežnika.

> [!question] Vprašanje 4
> Katere 3 metode obstajajo za dinamično dodelitev IPv6 naslova?
> > [!done]- Odgovor
> > 1. **SLAAC** (samo), 2. **SLAAC + Stateless DHCPv6** (naslov SLAAC, DNS iz DHCP), 3. **Stateful DHCPv6** (vse iz DHCP)

> [!question] Vprašanje 5
> Kaj je DAD in zakaj se uporablja?
> > [!done]- Odgovor
> > Duplicate Address Detection – naprava preveri, ali je generirani IPv6 naslov že v uporabi, preden ga začne aktivno uporabljati.

> [!question] Vprašanje 6
> Koliko podomrežij /64 dobi organizacija, ki ima /48 blok?
> > [!done]- Odgovor
> > 2¹⁶ = **65.536 podomrežij**

> [!question] Vprašanje 7
> Kateri ukaz na routerju prikaže ekvivalent ARP tabele za IPv6?
> > [!done]- Odgovor
> > `show ipv6 neighbors` (neighbor cache)|← Global Routing Prefix (48 b) →|← Subnet ID (16 b) →|← Interface ID (64 b) →|