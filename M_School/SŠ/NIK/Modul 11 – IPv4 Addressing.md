---
tags:
  - CCNA1
  - IPv4
  - subnetting
  - naslavljanje
  - modul-11
aliases:
  - Modul 11
  - IPv4 Addressing
  - Subnetting
---

> [!summary] Cilj modula
> Implementirati shemo IPv4 naslavljanja, vključno z deljenjem omrežij na podomrežja (subnetting).

---

## 11.1 Struktura IPv4 naslova

- IPv4 naslov = **32 bitov** = 4 okteti (decimalno, ločeni s pikam)
- Primer: `192.168.1.10`
- Sestavljen iz dveh delov:
192.168.1 .10  
(določa omrežje) (določa gosta)

### Subnet maska

- 32-bitno število, ki pove kje se **network** konča in **host** začne
- Tam kjer so **1-ji** → network portion
- Tam kjer so **0-ji** → host portion
- Zapis: decimalno (`255.255.255.0`) ali **prefix/CIDR** (`/24`)

| Subnet maska | CIDR | Binarno |
|-------------|------|---------|
| 255.0.0.0 | /8 | 11111111.00000000.00000000.00000000 |
| 255.255.0.0 | /16 | 11111111.11111111.00000000.00000000 |
| 255.255.255.0 | /24 | 11111111.11111111.11111111.00000000 |
| 255.255.255.128 | /25 | 11111111.11111111.11111111.10000000 |
| 255.255.255.192 | /26 | 11111111.11111111.11111111.11000000 |
| 255.255.255.224 | /27 | 11111111.11111111.11111111.11100000 |
| 255.255.255.240 | /28 | 11111111.11111111.11111111.11110000 |
| 255.255.255.248 | /29 | 11111111.11111111.11111111.11111000 |
| 255.255.255.252 | /30 | 11111111.11111111.11111111.11111100 |

---

## 11.2 Naslovi v omrežju

Za vsako podomrežje obstajajo **3 posebni naslovi**:

| Naslov | Opis | Primer (/24) |
|--------|------|--------------|
| **Network address** | Naslov omrežja – ne dodeli se hostu (vse host bite = 0) | 192.168.1.**0** |
| **Usable hosts** | Naslovi za naprave | 192.168.1.**1–254** |
| **Broadcast address** | Dosežejo vse hoste v omrežju (vse host bite = 1) | 192.168.1.**255** |

### Formula za število gostov

\[
\text{Število gostov} = 2^n - 2
\]

kjer je \(n\) = število **host bitov** (bitov z vrednostjo 0 v subnet maski)

> [!example] /24 → host biti = 8 → 2⁸ - 2 = **254 gostov**
> [!example] /26 → host biti = 6 → 2⁶ - 2 = **62 gostov**
> [!example] /30 → host biti = 2 → 2² - 2 = **2 gosta** (point-to-point!)

---

## 11.3 Vrste IPv4 naslovov

### Unicast, Broadcast, Multicast

| Tip | Pošiljatelj | Prejemnik | Primer |
|-----|------------|-----------|--------|
| **Unicast** | 1 | 1 | 192.168.1.5 → 192.168.1.10 |
| **Broadcast** | 1 | Vsi v omrežju | 192.168.1.255 |
| **Multicast** | 1 | Skupina | 224.0.0.5 (OSPF routerji) |

### Javni (public) vs zasebni (private) naslovi

| Razred | Zasebni obseg | Subnet maska |
|--------|--------------|--------------|
| **A** | 10.0.0.0 – 10.255.255.255 | /8 |
| **B** | 172.16.0.0 – 172.31.255.255 | /12 |
| **C** | 192.168.0.0 – 192.168.255.255 | /16 |

> [!important] Zasebni naslovi **niso usmerljivi** na internetu!
> Za internet dostop se potrebuje **NAT** (Network Address Translation).

### Posebni IPv4 naslovi

| Naslov | Namen |
|--------|-------|
| `127.0.0.1` | Loopback – testiranje TCP/IP |
| `169.254.0.0/16` | APIPA – ko DHCP ne odgovori (link-local) |
| `0.0.0.0/0` | Default route – vse destinacije |
| `255.255.255.255` | Limited broadcast |

---

## 11.4 Subnetting – osnove

> [!info] Subnetting = razdelitev enega večjega omrežja na **manjša podomrežja**

### Zakaj subnetting?

- Zmanjša broadcast domene → manj nepotrebnega prometa
- Izboljša varnost (ločeni segmenti)
- Boljša organizacija (po oddelkih, lokacijah)
- Bolj učinkovita izraba naslovnega prostora

### Subnetting na mejah oktetov

| Omrežje | Prefix | Opis |
|---------|--------|------|
| 192.168.1.0/24 | /24 | 1 omrežje, 254 gostov |
| 192.168.1.0/25 | /25 | 2 podomrežji, 126 gostov vsako |
| 192.168.1.0/26 | /26 | 4 podomrežja, 62 gostov vsako |
| 192.168.1.0/27 | /27 | 8 podomrežij, 30 gostov vsako |
| 192.168.1.0/28 | /28 | 16 podomrežij, 14 gostov vsako |
| 192.168.1.0/29 | /29 | 32 podomrežij, 6 gostov vsako |
| 192.168.1.0/30 | /30 | 64 podomrežij, 2 gosta vsako |

### Formula za število podomrežij

\[
\text{Število podomrežij} = 2^s
\]

kjer je \(s\) = število **izposojenih bitov** (bitov dodanih k network delu)

> [!example] /24 → /26: izposodili smo 2 bita → 2² = **4 podomrežja**

---

## 11.5 Subnetting – primer postopka

> [!example] Naloga: Razdeli 192.168.1.0/24 na 4 enaka podomrežja

**Korak 1:** Koliko bitov izposoditi?  
4 podomrežja = 2² → izposodi **2 bita** → nov prefix = /24 + 2 = **/26**

**Korak 2:** Nova subnet maska?  
/26 = `255.255.255.192`

**Korak 3:** Velikost bloka?  
Host biti = 32 - 26 = 6 → 2⁶ = 64 naslovov na podomrežje

**Korak 4:** Podomrežja:

| Podomrežje | Network addr | Usable hosts | Broadcast |
|-----------|-------------|--------------|-----------|
| 1. | 192.168.1.**0**/26 | .1 – .62 | .63 |
| 2. | 192.168.1.**64**/26 | .65 – .126 | .127 |
| 3. | 192.168.1.**128**/26 | .129 – .190 | .191 |
| 4. | 192.168.1.**192**/26 | .193 – .254 | .255 |

> [!tip] Korak med podomrežji = velikost bloka = 2^(host biti)
> /26 → blok = 2⁶ = 64

---

## 11.6 VLSM – Variable Length Subnet Masking

> [!info] VLSM = vsako podomrežje ima **svojo** velikost (subnet masko) glede na potrebe

### Zakaj VLSM?

- Klasično subnetting: vsa podomrežja enako velika → izguba naslovov
- VLSM: vsako podomrežje točno takšno, kot potrebuje

### Postopek VLSM

1. Razvrsti podomrežja od **največjega** do **najmanjšega**
2. Začni z največjim – dodeli ustrezen prefix
3. Nadaljuj z naslednjim iz preostalega naslovnega prostora

> [!example] Scenarij: LAN A (50 gostov), LAN B (20 gostov), WAN link (2 gosta)
> ```
> LAN A: 50 gostov → /26 (62 use.) → 192.168.1.0/26
> LAN B: 20 gostov → /27 (30 use.) → 192.168.1.64/27
> WAN:    2 gosta  → /30  (2 use.) → 192.168.1.96/30
> ```

---

## 11.7 Cisco IOS ukazi za subnetting/IP

```cisco
show ip interface brief          → Pregled IP naslovov vmesnikov
show interfaces                  → Detajli vmesnikov
show ip route                    → Routing tabela
```

Na PC:
ipconfig /all → Windows – IP, maska, gateway, DNS  
ip addr show → Linux

---

## 🔗 Povezave

- [[Modul 8 - Network Layer]]
- [[Modul 12 - IPv6 Addressing]]

---

## ❓ Check Your Understanding

> [!question] Vprašanje 1
> Koliko gostov sprejme podomrežje /27?
> > [!done]- Odgovor
> > Host biti = 32-27 = 5 → 2⁵ - 2 = **30 gostov**

> [!question] Vprašanje 2
> Kateri 3 zasebni obsegi obstajajo pri IPv4?
> > [!done]- Odgovor
> > 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16

> [!question] Vprašanje 3
> Kakšna je broadcast adresa omrežja 192.168.5.0/24?
> > [!done]- Odgovor
> > **192.168.5.255** (vse host bite = 1)

> [!question] Vprašanje 4
> Razdeli 10.0.0.0/24 na 8 podomrežij. Kateri prefix dobiš?
> > [!done]- Odgovor
> > 8 = 2³ → izposodi 3 bite → /24+3 = **/27**

> [!question] Vprašanje 5
> Kaj je VLSM in zakaj ga uporabljamo?
> > [!done]- Odgovor
> > Variable Length Subnet Masking – različna podomrežja imajo različne maske glede na dejansko potrebo → preprečuje izgubo naslovov.

> [!question] Vprašanje 6
> Koliko podomrežij dobimo, če iz /24 izposodimo 4 bite?
> > [!done]- Odgovor
> > 2⁴ = **16 podomrežij** (vsako /28 z 14 gosti)