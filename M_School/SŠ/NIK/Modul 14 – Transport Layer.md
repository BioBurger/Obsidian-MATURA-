---
tags:
  - CCNA1
  - transport-layer
  - TCP
  - UDP
  - port-numbers
  - modul-14
aliases:
  - Modul 14
  - Transport Layer
  - Transportna plast
  - TCP UDP
---

> [!summary] Cilj modula
> Primerjati delovanje TCP in UDP protokolov ter razložiti vlogo portnih številk pri transportu podatkov.

---

## 14.1 Namen transportne plasti

- **Transport Layer = OSI Layer 4**
- Je vez med **aplikacijsko plastjo** (Layer 7) in **nižjimi plastmi** (L3/L2/L1)
- Zagotavlja **logično komunikacijo med aplikacijami** na različnih gostih (end-to-end)

### 4 ključne naloge transportne plasti

1. **Sledenje pogovorov** → loči komunikacije med različnimi aplikacijami
2. **Segmentacija in sestavitev** → razdeli data na segmente, sestavi na drugem koncu
3. **Prepoznavanje aplikacij** → prek port številk
4. **Multipleksiranje** → več aplikacij hkrati prek istega omrežja

### Dva protokola

| Protokol | Ime | Karakteristika |
|---------|-----|---------------|
| **TCP** | Transmission Control Protocol | Zanesljiv, orientiran na sejo |
| **UDP** | User Datagram Protocol | Hiter, brez zanesljivosti |

---

## 14.2 TCP – Transmission Control Protocol

### Karakteristike TCP

| Lastnost | Opis |
|----------|------|
| **Connection-oriented** | Vzpostavi sejo pred pošiljanjem (3-way handshake) |
| **Reliable delivery** | Zagotovi dostavo – manjkajoče ponovni pošlje |
| **Same-order delivery** | Sequence numbers → pravilni vrstni red |
| **Flow control** | Prilagodi hitrost glede na zmogljivost prejemnika |
| **Full duplex** | Hkratna komunikacija v obe smeri |

### TCP header

| Polje | Velikost | Opis |
|-------|----------|------|
| **Source Port** | 16 bitov | Portna številka pošiljatelja |
| **Destination Port** | 16 bitov | Portna številka prejemnika |
| **Sequence Number** | 32 bitov | Zaporedna številka prvega bajta |
| **Acknowledgment Number** | 32 bitov | Naslednji pričakovani bajt |
| **Header Length** | 4 biti | Dolžina TCP headerja |
| **Control Bits (Flags)** | 6 bitov | SYN, ACK, FIN, RST, PSH, URG |
| **Window Size** | 16 bitov | Velikost okna za flow control |
| **Checksum** | 16 bitov | Preverjanje napak |

> [!info] TCP header = **20 bajtov** (minimalno) – večji kot UDP (8 bajtov)!

### TCP Control Flags

| Flag | Opis |
|------|------|
| **SYN** | Synchronize – začetek seje |
| **ACK** | Acknowledgment – potrditev |
| **FIN** | Finish – konec seje |
| **RST** | Reset – takojšnja prekinitev |
| **PSH** | Push – takoj posreduj aplikaciji |
| **URG** | Urgent – nujno sporočilo |

---

## 14.3 TCP – 3-Way Handshake (vzpostavitev seje)
Odjemalec Router/Server  
│ │  
│──── SYN ──────────>│ Korak 1: "Hočem se povezati" (SYN=1, SEQ=x)  
│ │  
│<─── SYN-ACK ───────│ Korak 2: "OK, sprejemam" (SYN=1, ACK=x+1, SEQ=y)  
│ │  
│──── ACK ──────────>│ Korak 3: "Potrjujem" (ACK=y+1)  
│ │  
│ [Prenos podatkov]│


> [!important] Po uspešnem 3-way handshake se začne prenos podatkov. TCP sejo vzpostavi **vsak** TCP prenos!

### TCP – Zaključek seje (4-Way)
Odjemalec Server  
│──── FIN ──────────>│ Korak 1: "Zaključujem pošiljanje"  
│<─── ACK ───────────│ Korak 2: "Razumem"  
│<─── FIN ───────────│ Korak 3: "Tudi jaz zaključujem"  
│──── ACK ──────────>│ Korak 4: "Potrjujem"

---

## 14.4 TCP – Zanesljivost in Flow Control

### Sequence Numbers in ACK
Pošiljatelj pošlje: SEQ=1 (1000 bajtov)  
Prejemnik odgovori: ACK=1001 ("pošlji mi od bajta 1001 naprej")  
Pošiljatelj pošlje: SEQ=1001 (1000 bajtov)  
Prejemnik odgovori: ACK=2001

### Retransmission (ponoven prenos)

- Če ACK ni prejet v določenem času (**RTO** – Retransmission Timeout) → pošlje segment **znova**
- TCP sam zazna izgubo in popravi brez intervencije aplikacije

### Flow Control – Window Size

- **Window** = koliko podatkov sme pošiljatelj poslati preden čaka ACK
- Prejemnik nadzoruje okno glede na razpoložljiv pomnilnik
- **Sliding window**: okno se samodejno prilagaja
Majhno okno → pošiljatelj počaka pogosteje → manjša hitrost  
Veliko okno → pošiljatelj pošlje več naenkrat → višja hitrost

### Congestion Avoidance

- TCP prepozna preobremenitev omrežja → **zmanjša window** → manj podatkov naenkrat
- Osnova za TCP Slow Start algoritem

---

## 14.5 UDP – User Datagram Protocol

### Karakteristike UDP

| Lastnost | Opis |
|----------|------|
| **Connectionless** | Ni vzpostavljene seje – pošlji in pozabi |
| **Unreliable** | Ni potrdil (ACK), ni retransmisije |
| **No ordering** | Paketi se sestavijo v vrstnem redu prihoda |
| **Low overhead** | Majhen header (8 bajtov), hiter |
| **No flow control** | Pošilja s polno hitrostjo |

### UDP header (samo 4 polja!)

| Polje | Velikost | Opis |
|-------|----------|------|
| **Source Port** | 16 bitov | Portna številka pošiljatelja |
| **Destination Port** | 16 bitov | Portna številka prejemnika |
| **Length** | 16 bitov | Dolžina UDP headerja + podatkov |
| **Checksum** | 16 bitov | Opcijsko preverjanje napak |

> [!info] UDP header = samo **8 bajtov** → minimalni overhead!

### Kdaj použiti UDP?

| Aplikacija | Razlog za UDP |
|-----------|--------------|
| **DNS** | Kratki zahtevi/odgovori – hiter, majhen overhead |
| **DHCP** | Kratke izmenjave za dodelitev IP |
| **TFTP** | Prenos brez seje |
| **VoIP** | Nizka latenca > zanesljivost (en spuščeni paket ni katastrofa) |
| **Video streaming** | Hitrost > popolna zanesljivost |
| **SNMP** | Kratka sporočila za upravljanje |
| **Online gaming** | Nizka latenca |

---

## 14.6 TCP vs UDP – primerjava

| | TCP | UDP |
|-|-----|-----|
| Vzpostavitev seje | ✅ 3-way handshake | ❌ Connectionless |
| Zanesljivost | ✅ ACK + retransmission | ❌ Best effort |
| Vrstni red | ✅ Sequence numbers | ❌ Vrstni red prihoda |
| Flow control | ✅ Window size | ❌ Brez |
| Header | 20 bajtov | 8 bajtov |
| Hitrost | Počasnejši | Hitrejši ✅ |
| Aplikacije | HTTP, HTTPS, FTP, SMTP, SSH | DNS, DHCP, VoIP, Video, TFTP |

> [!tip] Mnemoehnika: **TCP = Telefon** (vzpostaviš klic, pogovor je zanesljiv), **UDP = Pismo** (pošlješ in ne veš ali je prispelo)

---

## 14.7 Port številke

Port številke omogočajo **multipleksiranje** – več aplikacij hkrati prek istega IP naslova.

### Kategorije portov

| Kategorija | Obseg | Opis |
|-----------|-------|------|
| **Well-known ports** | 0–1023 | Rezervirani za standardne storitve |
| **Registered ports** | 1024–49151 | Registrirane aplikacije |
| **Dynamic/Private ports** | 49152–65535 | Začasni (ephemeral) porti odjemalca |

### Ključni well-known porti

| Port | Protokol | Storitev |
|------|----------|---------|
| **20** | TCP | FTP – prenos podatkov |
| **21** | TCP | FTP – upravljanje |
| **22** | TCP | SSH |
| **23** | TCP | Telnet |
| **25** | TCP | SMTP (pošiljanje e-pošte) |
| **53** | TCP/UDP | DNS |
| **67** | UDP | DHCP Server |
| **68** | UDP | DHCP Client |
| **69** | UDP | TFTP |
| **80** | TCP | HTTP |
| **110** | TCP | POP3 |
| **143** | TCP | IMAP |
| **161** | UDP | SNMP |
| **443** | TCP | HTTPS |
| **514** | UDP | Syslog |

### Socket par

Kombinacija **IP naslov + port** = **socket**
Socket odjemalca: 192.168.1.10:49152  
Socket strežnika: 93.184.216.34:80

Socket par = 192.168.1.10:49152 ↔ 93.184.216.34:80  
→ identificira točno eno TCP/UDP sejo!

> [!example] Primer: brskalnik odpre 3 zavihke
> ```
> Tab 1: 192.168.1.5:49200 → 93.184.216.34:443  (HTTPS)
> Tab 2: 192.168.1.5:49201 → 172.217.16.14:443  (Google)
> Tab 3: 192.168.1.5:49202 → 151.101.1.69:80   (HTTP)
> ```
> Vsak zavihek = drug ephemeral port → switch/router loči promet!

---

## 14.8 Cisco IOS – pregled TCP/UDP

```cisco
show ip sockets              → Aktivni TCP/UDP sockets
show tcp brief               → Aktivne TCP seje
netstat -an                  → Windows/Linux – aktivne povezave
```

---

## 🔗 Povezave

- [[Modul 13 - ICMP]]
- [[Modul 15 - Application Layer]]

---

## ❓ Check Your Understanding

> [!question] Vprašanje 1
> Opiši 3-way handshake.
> > [!done]- Odgovor
> > 1. Odjemalec → SYN → strežnik
> > 2. Strežnik → SYN-ACK → odjemalec
> > 3. Odjemalec → ACK → strežnik

> [!question] Vprašanje 2
> Kateri dve karakteristiki ločita TCP od UDP?
> > [!done]- Odgovor
> > TCP: **zanesljiv** (ACK + retransmission) in **connection-oriented** (3-way handshake).
> > UDP: **connectionless** in **best effort** (brez ACK).

> [!question] Vprašanje 3
> Zakaj je UDP boljši za VoIP?
> > [!done]- Odgovor
> > Nizka latenca je pomembnejša kot zanesljivost – en spuščeni paket pri govoru je manj moteč kot zamuda ob retransmisiji.

> [!question] Vprašanje 4
> Kaj je socket par?
> > [!done]- Odgovor
> > Kombinacija **src IP:src port ↔ dst IP:dst port** – unikatno identificira eno TCP/UDP sejo.

> [!question] Vprašanje 5
> Katero orodje (TCP ali UDP) uporablja DNS in zakaj?
> > [!done]- Odgovor
> > **UDP** za odjemalec–strežnik (hiter, majhen overhead). **TCP** za strežnik–strežnik (zanesljiv prenos večjih podatkov med DNS strežniki).

> [!question] Vprašanje 6
> Kaj je window size pri TCP?
> > [!done]- Odgovor
> > Količina podatkov, ki jo pošiljatelj sme poslati preden čaka ACK. Prejemnik ga nadzoruje za **flow control**.