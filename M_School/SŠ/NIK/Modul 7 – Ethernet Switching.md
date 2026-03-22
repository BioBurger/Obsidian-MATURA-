---
tags:
  - CCNA1
  - ethernet
  - switching
  - MAC-table
  - modul-7
aliases:
  - Modul 7
  - Ethernet Switching
---


> [!summary] Cilj modula
> Razložiti, kako Ethernet deluje v preklopnem omrežju – od zgradbe okvirja do odločitev stikala.

---

## 7.1 Ethernet okvir (Ethernet Frame)

Ethernet deluje na **Layer 1 in Layer 2** (fizična + podatkovna plast).

### Struktura Ethernet okvirja (IEEE 802.3)

| Polje | Velikost | Opis |
|-------|----------|------|
| **Preamble** | 7 bajtov | Sinhronizacija – vzorec 10101010 |
| **SFD** (Start Frame Delimiter) | 1 bajt | Označuje začetek okvirja (10101011) |
| **Destination MAC** | 6 bajtov | MAC naslov prejemnika |
| **Source MAC** | 6 bajtov | MAC naslov pošiljatelja |
| **Type/Length** | 2 bajta | Tip L3 protokola (0x0800=IPv4, 0x86DD=IPv6) ali dolžina |
| **Data** | 46–1500 bajtov | Enkapsuliran L3 paket (payload) |
| **FCS** | 4 bajti | Frame Check Sequence (CRC) – zaznavanje napak |

> [!important] Minimalna velikost Ethernet okvirja = **64 bajtov**  
> Maksimalna velikost = **1518 bajtov** (brez preamble/SFD)  
> Okvirji manjši od 64 bajtov = **runt frames** → zavrženi!

### Tri ključne lastnosti Ethernet okvirja

1. **Ethernet enkapsulacija** → ovije L3 paket v okvir za prenos po LAN-u
2. **Ethernet naslavljanje** → src in dst MAC naslov za dostavo znotraj LAN-a
3. **Ethernet zaznavanje napak** → FCS trailer z CRC vrednostjo

---

## 7.2 Ethernet MAC naslov

- **48-bitni** (6 bajtov) fizični naslov, zapisan v **heksadecimalno**
- Primer: `A0:B1:C2:D3:E4:F5`
- Vsak NIC ima **unikaten** MAC naslov, zapečen ob proizvodnji (**burned-in address – BIA**)
- MAC naslove shranjuje switch v **MAC Address Table** (= CAM tabela)

### Vrste Ethernet naslovov

| Tip | Primer MAC | Opis |
|-----|-----------|------|
| **Unicast** | `00:0A:1B:2C:3D:4E` | Točno en prejemnik |
| **Broadcast** | `FF:FF:FF:FF:FF:FF` | Vsi v LAN |
| **Multicast** | `01:00:5E:xx:xx:xx` | Skupina naprav (IPv4 multicast) |

> [!info] Broadcast okvir pošlje switch **na vse porte** razen vhodnega.

### OUI in Device ID

---

## 7.3 MAC Address Table (CAM tabela)

Switch gradi MAC tabelo **dinamično** s poslušanjem prometa.

### Kako switch gradi tabelo

1. Sprejme okvir → prebere **source MAC** + vhodni **port**
2. Vnese par `MAC → port` v tabelo (dinamičen vnos)
3. Vnos ostane dokler ne poteče **aging timer** (privzeto 5 min)

### Kako switch posreduje okvire

| Situacija | Akcija |
|-----------|--------|
| Dst MAC **znan** v tabeli | Pošlje samo na **točno določen port** (unicast) |
| Dst MAC **neznan** v tabeli | **Flooding** – pošlje na vse porte razen vhodnega |
| Dst MAC = `FF:FF:FF:FF:FF:FF` | **Flooding** – broadcast na vse porte |

> [!example] Primer učenja MAC tabele
> ```
> PCA (MAC: AA) → Port 1
> PCB (MAC: BB) → Port 2
> 
> 1. PCA pošlje okvir PCB-ju
> 2. Switch zabeleži: AA → Port1
> 3. BB ni v tabeli → flooding na Port2, Port3, ...
> 4. PCB odgovori → switch zabeleži: BB → Port2
> 5. Naslednjič PCA→PCB: direktno Port2 ✅
> ```

### Cisco IOS ukaz

```cisco
show mac address-table          → Prikaži MAC tabelo
show mac address-table dynamic  → Samo dinamični vnosi
clear mac address-table dynamic → Počisti tabelo
```

---

## 7.4 Switch: Hitrosti in metode posredovanja

### Duplex nastavitve

| Način | Opis | Trki |
|-------|------|------|
| **Half-duplex** | Oddaja ALI sprejema (ne hkrati) | Možni (CSMA/CD) |
| **Full-duplex** | Oddaja IN sprejema hkrati | Niso možni ✅ |

> [!important] Sodobni switchi delujejo **full-duplex** → CSMA/CD ni potreben!

### Auto-negotiation

- Naprave se **samodejno dogovorijo** za hitrost (10/100/1000 Mbps) in duplex
- Priporočeno: pusti na **auto** ali ročno nastavi oba konca enako

### Metode posredovanja okvirjev

#### 1. Store-and-Forward Switching ✅ (standard)
Sprejmi CELI okvir → preveri FCS (CRC) → posreduj
- **Prednost**: zavrže napačne okvirje (error detection)
- **Slabost**: višja zakasnitev (latency)

#### 2. Cut-Through Switching (nizka latenca)
Preberi samo DST MAC (prvih 6 bajtov) → takoj posreduj
- **Prednost**: zelo nizka latenca
- **Slabost**: posreduje tudi napačne okvirje!

| Varianta | Opis |
|----------|------|
| **Fast-Forward** | Posreduje takoj po branju dst MAC – najnižja latenca |
| **Fragment-Free** | Prebere prvih 64 bajtov (izogne se runt framom), nato posreduje |

> [!tip] Fragment-Free = kompromis med Store-and-Forward in Fast-Forward

### Pomnilnik za okvire (Buffering)

| Vrsta | Opis |
|-------|------|
| **Port-based memory** | Vsak port ima svojo vrsto (queue) |
| **Shared memory** | Skupni pomnilnik za vse porte → bolj fleksibilno |

---

## 🔗 Povezave

- [[Modul 6 - Data Link Layer]]
- [[Modul 8 - Network Layer]]

---

## ❓ Check Your Understanding

> [!question] Vprašanje 1
> Kaj je CAM tabela?
> > [!done]- Odgovor
> > **MAC Address Table** – stikalo jo gradi dinamično z učenjem source MAC naslovov in portov.

> [!question] Vprašanje 2
> Kaj naredi switch, ko prejme okvir z neznano destination MAC?
> > [!done]- Odgovor
> > **Flooding** – pošlje okvir na vse porte razen vhodnega.

> [!question] Vprašanje 3
> Kakšna je razlika med Store-and-Forward in Cut-Through?
> > [!done]- Odgovor
> > Store-and-Forward čaka na cel okvir in preveri CRC – zavrže napačne. Cut-Through posreduje takoj po branju dst MAC – nižja latenca, ne preverja napak.

> [!question] Vprašanje 4
> Katera minimalna velikost Ethernet okvirja je veljavna?
> > [!done]- Odgovor
> > **64 bajtov**. Manjši = runt frame → switch ga zavrže.

> [!question] Vprašanje 5
> Zakaj sodobni switchi ne potrebujejo CSMA/CD?
> > [!done]- Odgovor
> > Delujejo **full-duplex** – vsak port ima svojo kolizijsko domeno, trki niso možni.
|← OUI (3 bajti / 24 bitov) →|← Device ID (3 bajti / 24 bitov) →|
