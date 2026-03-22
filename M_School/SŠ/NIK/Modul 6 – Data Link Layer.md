---
tags:
  - CCNA1
  - data-link
  - Layer2
  - MAC
  - LLC
  - modul-6
aliases:
  - Modul 6
  - Data Link Layer
  - Podatkovna plast
---


> [!summary] Cilj modula
> Razložiti, kako nadzor dostopa do medija na podatkovni plasti podpira komunikacijo med omrežji.

---

## 6.1 Namen podatkovne plasti (Layer 2)

- **Data Link Layer** = OSI Layer 2
- Odgovorna za komunikacijo med **NIC karticami** (node-to-node)
- Skrbi za **dostop do medija** (kdo in kdaj sme oddajati)
- Enkapsulira Layer 3 pakete (IP) v **okvirje (frames)**
- Določa metodo enkapsulacije za specifični tip medija

### Ključne naloge

1. Enkapsulacija Layer 3 paketa v frame (doda header + trailer)
2. Nadzor dostopa do fizičnega medija (MAC)
3. Zaznavanje napak (FCS v trailerju)
4. Naslavljanje znotraj lokalnega omrežja (MAC naslovi)

---

## 6.2 Podplasti podatkovne plasti

IEEE 802 deli Layer 2 v dve podplasti:

### LLC (Logical Link Control) – IEEE 802.2

- Komunicira z **Layer 3** (omrežna plast)
- Identificira kateri L3 protokol je v okvirju (IPv4, IPv6)
- Omogoča, da **več L3 protokolov** deli isto NIC kartico

### MAC (Media Access Control)

- Komunicira z **Layer 1** (fizična plast)
- Definira procese dostopa do medija (hardware)
- Zagotavlja **MAC naslavljanje** (fizični naslovi)
- Upravlja dostop do deljenih medijev
- Dodaja **trailer z FCS** za zaznavanje napak

| Podplast | Povezava | Funkcija |
|----------|----------|----------|
| **LLC** (802.2) | ↔ Layer 3 | Identifikacija L3 protokola, multipleksiranje |
| **MAC** | ↔ Layer 1 | Fizično naslavljanje, dostop do medija, FCS |

---

## 6.3 Zagotavljanje dostopa do medija

Layer 2 mora preprečiti **trke (collisions)** pri deljenih medijih.

### CSMA/CD – za žično Ethernet (LAN)

**Carrier Sense Multiple Access / Collision Detection**

1. Posluša medij (Carrier Sense)
2. Če je prost → oddaj
3. Če zazna trk (Collision Detection) → ustavi, pošlji jam signal
4. Počaka naključen čas (backoff) → poskusi znova

> [!info] CSMA/CD se danes redko aktivira – full-duplex stikala trkov ne povzročajo!

### CSMA/CA – za brezžično (WLAN)

**Carrier Sense Multiple Access / Collision Avoidance**

1. Posluša medij
2. Če je prost → počaka naključen čas → oddaj
3. Prejemnik pošlje ACK (potrdilo)
4. Brez ACK → ponovi oddajanje

> [!tip] Razlika CD vs CA
> - **CD** = zaznaj in popravi trk (žičen)
> - **CA** = izogni se trku pred oddajanjem (brezžičen)

---

## 6.4 Topologije

> [!info] Dve vrsti topologij (isto kot pri L1, le drugačen kontekst)
> - **Fizična topologija** → fizične povezave med napravami
> - **Logična topologija** → kako podatki dejansko tečejo, definira MAC metodo

### WAN topologije

| Topologija | Opis | Prednosti |
|-----------|------|-----------|
| **Point-to-Point** | Direktna povezava 2 naprav | Preprosto, zanesljivo |
| **Hub and Spoke** | Centralno vozlišče + vejice | Ekonomično za zvezde |
| **Mesh** | Vsak z vsakim | Redundanca, odpornost |

### LAN topologije

| Topologija | Opis | Primer |
|-----------|------|--------|
| **Star** | Vse naprave → centralni switch | Moderno Ethernet omrežje ✅ |
| **Bus** | Vse naprave na isti žici | Stari 10BASE2 Ethernet |
| **Ring** | Naprave v zanki | Token Ring (zastarelو) |

> [!important] Danes je **Star topologija** (s switchem) standard za LAN!

---

## 6.5 Struktura okvirja (Frame)

Vsak Layer 2 okvir ima **3 dele**: Header, Data, Trailer
