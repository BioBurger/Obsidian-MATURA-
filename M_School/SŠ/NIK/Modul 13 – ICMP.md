---
tags:
  - CCNA1
  - ICMP
  - ping
  - traceroute
  - diagnostika
  - modul-13
aliases:
  - Modul 13
  - ICMP
  - ping traceroute
---


> [!summary] Cilj modula
> Testirati omrežno povezljivost z orodji ping in traceroute, ki temeljijo na ICMP.

---

## 13.1 ICMP – Internet Control Message Protocol

- **ICMP** = Internet Control Message Protocol
- Deluje na **Layer 3** (omrežna plast), uporablja IP
- Namen: povratne informacije o **napakah pri obdelavi IP paketov**
- ICMP sam po sebi **ne zagotavlja zanesljivosti** – je samo diagnostično orodje
- Dve verziji: **ICMPv4** (za IPv4) in **ICMPv6** (za IPv6)

> [!info] ICMPv6 je razširjen – poleg diagnostike vsebuje tudi **Neighbor Discovery (ND)** protokol (RS, RA, NS, NA).

---

## 13.2 ICMP sporočila – skupna ICMPv4 in ICMPv6

### Host Reachability (Echo Request / Echo Reply)

| Sporočilo | Namen |
|-----------|-------|
| **Echo Request** | Pošiljatelj prosi: "Ali si živ?" |
| **Echo Reply** | Prejemnik odgovori: "Da, sem!" |

→ To je osnova ukaza **ping**!

### Destination Unreachable

Router pošlje to sporočilo, ko **ne more dostavi paketa**.

| Koda | Opis |
|------|------|
| **0** | Network Unreachable |
| **1** | Host Unreachable |
| **2** | Protocol Unreachable |
| **3** | Port Unreachable |

### Time Exceeded

- Pošlje **router**, ko paket doseže **TTL = 0** (IPv4) ali **Hop Limit = 0** (IPv6)
- Router paket zavrže in pošlje "Time Exceeded" nazaj k viru
- → Osnova ukaza **traceroute**!

---

## 13.3 ICMPv6 dodatna sporočila (Neighbor Discovery)

| Sporočilo | Kratica | Namen |
|-----------|---------|-------|
| **Router Solicitation** | RS | Gost išče router: "Je kdo tu?" |
| **Router Advertisement** | RA | Router oglašuje: "Tukaj sem, prefix je X" |
| **Neighbor Solicitation** | NS | "Kdo ima ta IPv6 naslov?" (= ARP Request) |
| **Neighbor Advertisement** | NA | "Jaz imam ta naslov, moj MAC je X" (= ARP Reply) |

> [!tip] Vsa ND sporočila so del **ICMPv6** – ne ARP! IPv6 nima ARP protokola.

---

## 13.4 Ping – testiranje povezljivosti

**Ping** = pošlje **ICMP Echo Request** in čaka **ICMP Echo Reply**

### Sintaksa
ping [ip-naslov ali hostname] → osnovno (Windows/Linux/IOS)  
ping -c 5 192.168.1.1 → Linux (5 paketov)  
ping 192.168.1.1 repeat 10 → Cisco IOS  
ping ipv6 2001:DB8::1 → IPv6 ping (IOS)


### Interpretacija rezultatov

| Simbol | Cisco IOS | Opis |
|--------|-----------|------|
| `!` | Uspeh | Echo Reply prejet |
| `.` | Timeout | Ni odgovora v času |
| `U` | Unreachable | ICMP Dest. Unreachable prejet |
| `M` | MTU exceeded | Paket prevelik |

> [!example] Tipičen ping izhod (Windows)
> ```
> Pinging 192.168.1.1 with 32 bytes of data:
> Reply from 192.168.1.1: bytes=32 time=1ms TTL=64
> Reply from 192.168.1.1: bytes=32 time=1ms TTL=64
>
> Ping statistics: Sent = 4, Received = 4, Lost = 0 (0% loss)
> Average = 1ms
> ```

### 3 vrste ping testov

| Test | Ukaz | Preveri |
|------|------|---------|
| **Loopback test** | `ping 127.0.0.1` (IPv4) / `ping ::1` (IPv6) | TCP/IP sklad na napravi |
| **Default gateway** | `ping [gateway IP]` | Povezava v lokalnem omrežju |
| **Remote host** | `ping [remote IP]` | End-to-end komunikacija |

> [!important] Uspešen `ping 127.0.0.1` **ne dokazuje**, da je NIC kabel priključen!
> Samo potrdi, da TCP/IP sklad na napravi deluje.

> [!tip] Zakaj prvi ping pogosto zapade (timeout)?
> Ker naprava najprej izvede **ARP** (ali ND za IPv6) za resolucijo MAC naslova – to vzame čas. Drugi ping je že uspešen.

---

## 13.5 Traceroute – sledenje poti

**Traceroute** (Windows: `tracert`) = prikaže **vsak skok (hop)** na poti do cilja

### Princip delovanja
1. Pošlji paket z TTL=1 → prvi router ga zavrže → pošlje Time Exceeded  
    → zabeleži IP prvega routerja
    
2. Pošlji paket z TTL=2 → drugi router ga zavrže → pošlje Time Exceeded  
    → zabeleži IP drugega routerja
    
3. Ponavljaj (TTL++) dokler paket ne doseže cilja  
    → Cilj odgovori z Echo Reply



### Sintaksa
tracert 8.8.8.8 → Windows  
traceroute 8.8.8.8 → Linux/Mac  
traceroute 192.168.1.1 → Cisco IOS

> [!example] Primer izhoda tracert
> ```
>  1    1ms   1ms   1ms  192.168.1.1    ← Default gateway
>  2   10ms  10ms  10ms  10.0.0.1       ← ISP router
>  3   20ms  20ms  21ms  8.8.8.8        ← Google DNS (cilj)
> ```

### Razlaga izhoda

| Simbol | Opis |
|--------|------|
| `ms ms ms` | 3 meritve zakasnitvne (za vsak hop) |
| `* * *` | Hop ne odgovori (firewall blokira ICMP) |
| `!H` | Host unreachable |
| `!N` | Network unreachable |

> [!info] Vsak hop prikaže **RTT** (Round Trip Time) v milisekundah.
> Visoke vrednosti = visoka latenca = morebitna ozko grlo!

---

## 13.6 Ping vs Traceroute

| | Ping | Traceroute |
|-|------|-----------|
| Protokol | ICMP Echo Request/Reply | ICMP Time Exceeded + Echo Reply |
| Namen | Preveri **dostopnost** cilja | Prikaže **pot** do cilja (vsak hop) |
| Informacije | RTT, % izgube | IP vsakega routerja, RTT na hop |
| Ukaz (Win) | `ping` | `tracert` |
| Ukaz (Linux/Mac) | `ping` | `traceroute` |
| Ukaz (Cisco IOS) | `ping` | `traceroute` |

---

## 13.7 Extended ping (Cisco IOS)

```cisco
R1# ping
Protocol [ip]: ip
Target IP address: 192.168.2.1
Repeat count: 100[1]
Datagram size : 1500
Timeout in seconds: 5[2]
```

> [!tip] Extended ping omogoča: spremembo izvora, velikosti paketa, ponavljanj, timeout-a.

---

## 🔗 Povezave

- [[Modul 8 - Network Layer]]
- [[Modul 14 - Transport Layer]]

---

## ❓ Check Your Understanding

> [!question] Vprašanje 1
> Kateri dve ICMP sporočili sta osnova ukaza ping?
> > [!done]- Odgovor
> > **Echo Request** in **Echo Reply**

> [!question] Vprašanje 2
> Kako traceroute izve IP naslov vsakega hopa?
> > [!done]- Odgovor
> > Pošlje pakete z rastočim TTL (1, 2, 3...). Ko TTL = 0, router paket zavrže in pošlje **ICMP Time Exceeded** sporočilo nazaj – v njem je IP routerja.

> [!question] Vprašanje 3
> Kaj pomeni `* * *` v izhodu traceroute?
> > [!done]- Odgovor
> > Hop **ne odgovarja** – verjetno firewall blokira ICMP. Ne pomeni nujno, da je pot prekinjena.

> [!question] Vprašanje 4
> Zakaj je prvi ping pogosto timeout?
> > [!done]- Odgovor
> > Naprava mora najprej razrešiti MAC naslov prek **ARP** (ali ND za IPv6). To vzame dodaten čas pri prvem paketu.

> [!question] Vprašanje 5
> Kaj preveri `ping 127.0.0.1`?
> > [!done]- Odgovor
> > Delovanje **TCP/IP sklada** na lokalni napravi. Ne preverja kabla, NIC-a ali omrežne povezave!

> [!question] Vprašanje 6
> Katera 4 ND sporočila so del ICMPv6?
> > [!done]- Odgovor
> > **RS** (Router Solicitation), **RA** (Router Advertisement), **NS** (Neighbor Solicitation), **NA** (Neighbor Advertisement)