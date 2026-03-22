---
tags:
  - CCNA1
  - small-network
  - troubleshooting
  - modul-17
aliases:
  - Modul 17
  - Build a Small Network
  - Malo omrežje
---


> [!summary] Cilj modula
> Prepoznati komponente malega omrežja, razumeti tipične protokole, naslovno shemo, osnovno preverjanje povezljivosti in postopke za odpravljanje napak.

---

## 17.1 Devices in a Small Network

> [!info] Večina podjetij je **majhnih**, zato so tudi njihova omrežja relativno preprosta.

### Tipične naprave

- Končne naprave (hosts) – PC-ji, prenosniki, IP telefoni, tiskalniki, IP kamere, IoT.
- Stikala (switches) – povezujejo naprave v LAN, lahko več VLAN-ov.
- Usmerjevalnik / SOHO router – povezava v WAN/internet, NAT, DHCP, osnovni firewall.
- Wireless router / AP – brezžični dostop za mobilne naprave.
- Strežniki – datotečni, aplikacijski, web, DNS, DHCP, VoIP.
- Security naprave – firewall, IPS/IDS, VPN terminator (lahko integrirano v router/ASA).[web:79]

### Majhna omrežja – topologija

- Običajno ena WAN povezava (DSL, kabel, Ethernet uplink).
- LAN del v star topologiji: en ali več stikal, nanje priklopljene končne naprave.
- Upravljanje omrežja pogosto pokriva lokalni IT ali zunanji izvajalec, ne ločen IT oddelek.[web:79]

---

## 17.2 Small Network Applications and Protocols

> [!summary] Katere storitve tipično tečejo v malem omrežju?

| Storitev | Protokol(i) | Kratek opis |
|----------|-------------|-------------|
| Web | HTTP, HTTPS | Brskanje, web aplikacije. |
| E‑pošta | SMTP, POP3, IMAP | Pošiljanje/prejemanje e‑pošte. |
| Imena | DNS | Pretvorba imena v IP naslov. |
| Konfiguracija IP | DHCP | Dinamična dodelitev IPv4/IPv6 nastavitev. |
| Datoteke | FTP, SFTP, SMB | Deljenje datotek, upload/download. |
| Upravljanje | SSH, SNMP | Upravljanje in monitoring naprav. |
| Real-time | RTP/RTCP, VoIP | Govor, video klici. |

> [!tip] V malih omrežjih prevladuje promet HTTP(S), DNS, SMB (datoteke) in e‑pošta.[web:79]

---

## 17.3 IP Addressing for a Small Network

Pri implementaciji malega omrežja je ključno dobra IP shema:

- Vsaka naprava v internetworku potrebuje unikaten naslov.
- V shemo moraš vključiti:
  - končne naprave (uporabniki, Wi‑Fi klienti),
  - strežnike in periferne naprave (tiskalniki, kamere),
  - vmesnike na usmerjevalnikih/switchih (gateway, management).[web:79]

> [!tip] Priporočilo: naslavljanje po tipu naprave (npr. strežniki 192.168.10.50–100, printers 192.168.10.200+) olajša troubleshooting in filtriranje v logih.[web:79]

### VLAN-i in VLSM

- Loči promet po VLAN-ih (npr. Users, Servers, Management, Guest Wi‑Fi).
- Vsak VLAN dobi svoje podomrežje z ustrezno masko (VLSM).[web:79]

> [!example] Primer:
> - VLAN 10 – Users: 50 hostov → 192.168.10.0/26
> - VLAN 20 – Servers: 20 hostov → 192.168.20.0/27
> - VLAN 30 – Management: 10 hostov → 192.168.30.0/28
> - VLAN 40 – Guest: 50 hostov → 192.168.40.0/26

---

## 17.4 Scale to Larger Networks

> [!info] Velika omrežja so zgrajena iz več malih omrežij – isti principi, samo več naprav/povezav.[web:78]

Za skaliranje iz malega v večje omrežje potrebuješ:

- Network documentation – fizična in logična topologija.
- Device inventory – seznam vseh naprav v omrežju.
- Budget – plan nabave opreme, licenc, podpore.
- Traffic analysis – kateri protokoli in aplikacije obstajajo, kakšne so njihove potrebe (bandwidth, latency).[web:78]

Koncepti:
- Redundanca – dvojni uplinki, dva switcha, failover WAN, HA firewalli.
- Hierarhija – Access / Distribution / Core plasti za preglednost in skaliranje.
- QoS – prioritetizacija real-time prometa (voice, video) pred “bulk” (FTP).[web:112]

---

## 17.5 Verify Connectivity

### Orodja na hostu

- ipconfig /all (Windows) / ip addr (Linux) – preveri IP, masko, gateway, DNS.
- ping – osnovni test dosegljivosti (RTT, packet loss).
- tracert / traceroute – pokaže vsak hop na poti do cilja.
- netstat -r ali route print – lokalna routing tabela.[web:79]

### Cisco IOS – must know ukazi

(show bloke si mirno obdelaš kot navadno besedilo ali jih po želji ročno daš v kodo)

show ip interface brief      – IP naslovi in status vmesnikov  
show ipv6 interface brief    – IPv6 naslovi in status  
show ip route                – Routing tabela IPv4  
show ipv6 route              – Routing tabela IPv6  
show arp                     – ARP tabela  
show cdp neighbors           – sosednje Cisco naprave, porti, platforma  
show version                 – IOS verzija, strojna oprema  

> [!tip] show cdp neighbors detail pokaže tudi IP naslov sosednje naprave – super za odkrivanje topologije.[web:79][web:109]

---

## 17.6 Host and IOS Commands

Na hostu (Windows):

- ipconfig /release / /renew – osvoboditev in ponovna pridobitev DHCP konfiguracije.
- ipconfig /displaydns – lokalni DNS cache.
- nslookup ime – ročno testiranje DNS.[web:105]

Na Cisco napravah (dopuna):

show interfaces               – detajli o vmesnikih (errors, collisions, duplex, speed)  
show protocols                – kateri L3 protokoli tečejo na katerih vmesnikih  
show ip interface             – IPv4 info, ACL, helperji  
show cdp neighbors detail     – sosedi + IP info  

---

## 17.7 Troubleshooting Methodologies

Cisco definira 6 korakov reševanja težav:[web:79]

1. Identify the problem – zberi informacije (uporabnik, logi, show ukazi, ping, traceroute).
2. Establish a theory of probable causes – sestavi seznam možnih vzrokov (IP napaka, kabel, VLAN, gateway, DNS …).
3. Test the theory to determine cause – z dodatnimi testi (zamenjaj kabel/port, preveri konfiguracijo, izloči dele omrežja).
4. Establish a plan of action and implement the solution – spremembe uvajaj premišljeno, če je možno izven produkcijskega časa.
5. Verify full system functionality and implement preventive measures – preveri, da vse spet dela, ne le en primer (ping, aplikacije, logi), razmisli o preventivi.
6. Document findings, actions, and outcomes – zapiši problem in rešitev – prihrani čas pri naslednjem podobnem incidentu.[web:79]

> [!tip] Delaj si baseline (normalne RTT, utilization, top talkers). Tako takoj opaziš nenormalna odstopanja.[web:79]

---

## 17.8 Troubleshooting Scenarios – tipični primeri

### 1) Uporabnik nima povezave v LAN

- ipconfig – napačen IP/maska/gateway? DHCP lease potekel?
- ping 127.0.0.1 – preveri TCP/IP stack.
- ping [lastni IP] – preveri NIC driver.
- ping [gateway] – preveri povezavo do switcha/routerja.[web:79]

Če ping do gateway-a ne dela:
- Preveri kabel, port status (show ip interface brief), ali je host v pravem VLAN-u.[web:79]

### 2) LAN deluje, ni interneta

- Ping do gateway-a OK, ping do zunanje IP (npr. 8.8.8.8) FAIL → problem na routerju, WAN linku ali pri ISP (routing, ACL, NAT).
- Ping do IP OK, do domenskega imena FAIL → verjetno DNS problem (napačen DNS server, nedelujoč DNS).[web:79]

---

## 🔗 Povezave

- [[Modul 16 - Network Security Fundamentals]]
- [[Modul 13 - ICMP]]
- [[Modul 14 - Transport Layer]]

---

## ❓ Check Your Understanding

> [!question] Vprašanje 1  
> Naštej tri tipične naprave v malem poslovnem omrežju.
> > [!done]- Odgovor  
> > Končne naprave (PC, laptop, IP telefon), stikalo(e), usmerjevalnik ali SOHO router (pogosto z brezžičnim AP-jem).

> [!question] Vprašanje 2  
> Katera orodja uporabiš za preverjanje povezljivosti med dvema hostoma?
> > [!done]- Odgovor  
> > ping za osnovni reachability in RTT, tracert/traceroute za pot in latenco po hopih.

> [!question] Vprašanje 3  
> Naštej 6 korakov strukturiranega odpravljanja napak.
> > [!done]- Odgovor  
> > 1) Identify the problem, 2) Establish a theory of probable causes, 3) Test the theory, 4) Establish a plan & implement, 5) Verify full functionality, 6) Document findings.

> [!question] Vprašanje 4  
> Zakaj v malem omrežju pogosto uporabljaš več VLAN-ov?
> > [!done]- Odgovor  
> > Zaradi segmentacije (varnost), manjših broadcast domen in boljše organizacije (Users, Servers, Management, Guest).

> [!question] Vprašanje 5  
> Kateri ukaz na Cisco napravi ti prikaže sosednje Cisco naprave?
> > [!done]- Odgovor  
> > show cdp neighbors (in show cdp neighbors detail za IP naslove in platformo).

> [!question] Vprašanje 6  
> Če ping do gateway-a dela, ping do zunanjega IP pa ne – kje iščeš napako?
> > [!done]- Odgovor  
> > Lokalni segment je OK, problem je verjetno na routerju, WAN povezavi ali pri ISP (routing, firewall, NAT).
