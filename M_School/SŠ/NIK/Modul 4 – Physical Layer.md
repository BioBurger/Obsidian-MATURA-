---
tags:
  - CCNA1
  - physical-layer
  - UTP
  - fiber
  - modul-4
aliases:
  - Modul 4
  - Physical Layer
  - Fizična plast
---


> [!summary] Cilj modula
> Opisati namen in funkcijo fizične plasti ter različne vrste medijev (baker, optika, brezžično).

---

## 4.1 Namen fizične plasti

- Fizična plast (OSI Layer 1) = **prenos bitov** po prenosnem mediju
- Ne zanima jo pomen podatkov – samo zanesljiv prenos surovih bitov
- Definira: električne/optične signale, priključke, kable, hitrosti

### Tri funkcije fizične plasti

1. **Fizične komponente** → kabli, priključki, NIC-i
2. **Kodiranje** → kako so biti predstavljeni (NRZ, Manchester, 4B/5B…)
3. **Signalizacija** → električna napetost, svetloba, radijski valovi

---

## 4.2 Pasovna širina in propustnost

| Pojem | Definicija | Primer |
|-------|-----------|--------|
| **Bandwidth** | Max. teoretična zmogljivost | 1 Gbps Ethernet |
| **Throughput** | Dejanska izmerjena hitrost | ~800 Mbps v praksi |
| **Latency** | Zamuda pri prenosu | 5 ms |
| **Goodput** | Throughput – overhead | Koristni podatki / sekundo |

> [!info] Bandwidth ≠ Throughput
> Bandwidth = cesta s 4 pasovi. Throughput = koliko avtomobilov dejansko pelje.

---

## 4.3 Vrste prenosnih medijev

| Medij | Signal | Prednosti | Slabosti |
|-------|--------|-----------|---------|
| **Baker (UTP/STP)** | Električni | Poceni, enostaven | EMI motnje, omejena razdalja |
| **Optični kabel** | Svetloba | Visoka hitrost, velika razdalja | Drag, krhek |
| **Brezžično** | Radio valovi | Mobilnost, brez kablov | Varnost, motnje, deljeni medij |

---

## 4.4 UTP kabling – podrobno

**UTP** = Unshielded Twisted Pair  
**STP** = Shielded Twisted Pair (oklopljen, boljša zaščita pred EMI)

### Kategorije UTP

| Kategorija | Max. hitrost | Bandwidth | Uporaba |
|-----------|-------------|-----------|---------|
| **Cat 3** | 10 Mbps | 16 MHz | Stari telefoni |
| **Cat 5** | 100 Mbps | 100 MHz | Fast Ethernet |
| **Cat 5e** | 1 Gbps | 100 MHz | Gigabit Ethernet ✅ |
| **Cat 6** | 1 Gbps / 10 Gbps (55m) | 250 MHz | Gigabit / 10G kratke razdalje |
| **Cat 6a** | 10 Gbps | 500 MHz | 10G Ethernet do 100m |
| **Cat 7** | 10 Gbps | 600 MHz | Data centri |

### Priključki

- **RJ-45** → standardni Ethernet priključek
- Max. razdalja UTP segmenta: **100 m**

### Vrste UTP kablov

| Kabel | Barve (T568B) | Uporaba |
|-------|--------------|---------|
| **Straight-through** | Oba konca T568B | PC → Switch, Switch → Router |
| **Crossover** | En konec T568A, drug T568B | PC → PC, Switch → Switch |
| **Rollover / Console** | Obrnjeni pini | PC → Cisco naprava (konzola) |

> [!tip] Danes večina naprav podpira **Auto-MDIX** → samodejno zazna tip kabla, crossover ni več nujen!

### T568B standard (za zapomniti)
