Spodaj imaš en sam, zgoščen »A3 cheat‑sheet« iz modulov 1–14, optimiziran za CCNA1 ITN final (teme se lepo ujemajo z vprašanjih s tvojega linka in podobnih verzij iz InfraExam/Scribd).infraexam+2  
Predlagam tisk v dveh stolpcih, font 9–10 pt.

---

# CCNA1 – ITN v7 (Moduli 1–14) – A3 povzetek

---

## 1. Omrežja, zanesljivost, varnost

**Značilnosti omrežja**

- Povezuje: ljudi, naprave, storitve, podatke (komunikacija, delo na daljavo, e‑trgovina, cloud).[[infraexam](https://infraexam.com/ccna1-v7/)]​
    
- Vrste omrežij: PAN, LAN, WLAN, MAN, WAN, intranet, extranet, internet.
    

**Zanesljivo omrežje – 4 stebri (CIA + 4R)**

- CIA: Confidentiality, Integrity, Availability.
    
- 4 karakteristike: Fault tolerance, Scalability, QoS, Security.[[infraexam](https://infraexam.com/ccna1-v7/ccna1-v7-itnv7-final-exam-answers/)]​
    

**Grožnje in zaščita**

- Grožnje: virus, worm (samoreplikacija po omrežju), trojan, spyware, adware, DDoS, phishing, ARP poisoning.
    
- Zaščita: antivirus, firewall, ACL, strong gesla/2FA, VPN, IDS/IPS.
    

---

## 2. Naprave, topologije, mediji

**Vrste naprav**

- Končne: PC, laptop, telefon, strežniki (web, DNS, e‑mail).
    
- Vmesne: switch (LAN, MAC tabele), router (L3, usmerjanje), WAP, firewall, modem.
    

**Topologije**

- Fizične: star (današnji Ethernet), bus (zastarelo), ring (zastarelo), point‑to‑point, hub‑and‑spoke, mesh.[[scribd](https://www.scribd.com/document/464000442/CCNA-1-v7-0-Final-Exam-Answers-Full-Introduction-to-Networks)]​
    
- Logične: kako teče promet (broadcast domena, collision domena).
    

**Mediji**

- Baker UTP/STP: cenejši, max 100 m, občutljiv na EMI.
    
- Optika (SMF/MMF): veliko hitrosti, dolge razdalje, imun na EMI.
    
- Brezžično (802.11): mobilnost, občutljivo na motnje in varnost.
    

---

## 3. OSI in TCP/IP model, enkapsulacija

**OSI (7 → 1)**

- Application, Presentation, Session, Transport, Network, Data Link, Physical.
    
- PDU po plasteh: Data, Segment, Packet, Frame, Bits.
    

**TCP/IP (4)**

- Application, Transport, Internet, Network Access.[[studocu](https://www.studocu.com/en-us/document/emporia-state-university/computer-networks-internets/ccna-1-v70-final-exam-answers-full-introduction-to-networks/22652598)]​
    
- Preslikava:
    
    - TCP/IP Application ↔ OSI 7–5
        
    - Transport ↔ OSI 4
        
    - Internet ↔ OSI 3
        
    - Network Access ↔ OSI 2–1
        

**Enkapsulacija / de‑enkapsulacija**

- Pošiljatelj: Data → Segment (TCP/UDP) → Packet (IP) → Frame (MAC) → Bits.
    
- Prejemnik: nasprotna smer; router na vsakem skoku zamenja **L2 header (MAC)**, **IP naslov ostane isti**.[[scribd](https://www.scribd.com/document/464000442/CCNA-1-v7-0-Final-Exam-Answers-Full-Introduction-to-Networks)]​
    

---

## 4. Fizična plast, UTP, optika, Wi‑Fi

**Pojmi**

- Bandwidth (teoretična kapaciteta), Throughput (dejanski), Latency (zakasnitev), Goodput (koristni podatki/s).
    
- Funkcije L1: kodiranje, signalizacija, konektorji, standardi.[[infraexam](https://infraexam.com/ccna1-v7/)]​
    

**UTP kategorije (pomni)**

- Cat5e: 1 Gbps / 100 MHz.
    
- Cat6: 1–10 Gbps (do ~55 m).
    
- Cat6a: 10 Gbps / 100 m.
    
- RJ‑45, max 100 m segment.
    

**Vrste UTP kablov**

- Straight‑through: PC ↔ switch, switch ↔ router.
    
- Crossover: PC ↔ PC, switch ↔ switch (Auto‑MDIX to danes sam rešuje).
    

**Optika**

- SMF: majhno jedro, laser, dolge razdalje (WAN).
    
- MMF: večje jedro, LED/VCSEL, kratke razdalje (LAN, DC).[[infraexam](https://infraexam.com/ccna1-v7/ccna1-v7-itnv7-final-exam-answers/)]​
    

**802.11 standardi (hitro)**

- b/g: 2,4 GHz, 11/54 Mb/s.
    
- n: 2,4/5 GHz, do 600 Mb/s.
    
- ac: 5 GHz, do več Gbps (Wi‑Fi 5).
    
- ax: 2,4/5/6 GHz, Wi‑Fi 6.
    

---

## 5. Številski sistemi in »magične« vrednosti

**Oktet (8 bitov)**

- Teže: 128, 64, 32, 16, 8, 4, 2, 1 → vsota = 255.
    
- Bin ↔ dec: 11000000₂ = 192, 11110000₂ = 240 itd.
    

**Hex ↔ bin**

- En hex znak = 4 biti (nibble).
    
- Hex 0–F = 0000–1111₂. Uporaba: MAC, IPv6.
    

**IPv4 maske in host biti**

- /24 → 255.255.255.0 → 8 host bitov → 2⁸−2 = 254 hostov.
    
- /25 → 255.255.255.128 → 7 bitov → 126 hostov.
    
- /26 → 255.255.255.192 → 6 bitov → 62 hostov.
    
- /27 → 255.255.255.224 → 5 bitov → 30 hostov.
    
- /28 → 255.255.255.240 → 4 bitov → 14 hostov.
    
- /29 → 255.255.255.248 → 3 bitov → 6 hostov.
    
- /30 → 255.255.255.252 → 2 bita → 2 hosta (P2P link).[[infraexam](https://infraexam.com/ccna1-v7/ccna1-v7-itnv7-practice-final-itn-answers/)]​
    

---

## 6. Data Link, Ethernet, MAC, switchi

**Podatkovna plast (L2)**

- LLC: “pogovarja se” z L3 (kateri L3 protokol).
    
- MAC: dostop do medija, MAC naslavljanje, FCS.[[infraexam](https://infraexam.com/ccna1-v7/)]​
    

**MAC naslov**

- 48 bitov, zapis v hex, npr. 00‑1A‑2B‑3C‑4D‑5E.
    
- Struktura: OUI (proizvajalec) + Device ID (unikaten).
    
- Tipi: unicast, broadcast FF:FF:FF:FF:FF:FF, multicast (npr. 01:00:5E:…).
    

**Ethernet frame**

- Src MAC, Dst MAC, Type/Length, Data (46–1500 B), FCS.
    
- Min 64 B, max 1518 B (brez preamble/SFD); manjše = runt → drop.[[infraexam](https://infraexam.com/ccna1-v7/ccna1-v7-itnv7-final-exam-answers/)]​
    

**Switch in MAC tabela (CAM)**

- Učenje: bere **source MAC** + port → zapiše v tabelo.
    
- Posredovanje:
    
    - Dst MAC znan → unicast na en port.
        
    - Dst MAC neznan ali broadcast → flooding na vse porte razen vhodnega.
        

**Duplex in načini posredovanja**

- Half‑duplex + CSMA/CD (zastarelo, hubi).
    
- Full‑duplex (ni trkov, standard danes).
    
- Store‑and‑forward: prebere cel frame, preveri FCS (varno).
    
- Cut‑through: prebere samo dst MAC, nižja latenca, lahko posreduje pokvarjene frame.
    

---

## 7. Network Layer, IPv4/IPv6 osnovni koncepti

**Funkcije L3 (IP)**

- Logično naslavljanje, enkapsulacija L4 segmentov, usmerjanje med omrežji, de‑enkapsulacija.[[scribd](https://www.scribd.com/document/464000442/CCNA-1-v7-0-Final-Exam-Answers-Full-Introduction-to-Networks)]​
    
- IP je connectionless, best effort, media‑independent.
    

**IPv4 header – pomembna polja**

- Src IP, Dst IP, TTL (dekrement na vsakem routerju; TTL=0 → ICMP Time Exceeded), Protocol (TCP=6, UDP=17, ICMP=1).[[infraexam](https://infraexam.com/ccna1-v7/ccna1-v7-itnv7-final-exam-answers/)]​
    
- Fragmentacija: če je paket > MTU (tipično 1500 B), IPv4 lahko fragmentira.
    

**IPv6 header – razlike**

- 128‑bit naslovi, fiksen header 40 B, brez header checksum, brez L3 broadcast (uporablja multicast), fragmentira samo host, ne routerji.[[studocu](https://www.studocu.com/en-us/document/emporia-state-university/computer-networks-internets/ccna-1-v70-final-exam-answers-full-introduction-to-networks/22652598)]​
    

**Usmerjanje (routing)**

- Router gleda destinacijski IP in **najdaljši ujemajoči prefix (Longest Prefix Match)** v routing tabeli.[[scribd](https://www.scribd.com/document/464000442/CCNA-1-v7-0-Final-Exam-Answers-Full-Introduction-to-Networks)]​
    
- Viri vnosov (`show ip route`): C (connected), L (local), S (static), O (OSPF), D (EIGRP), R (RIP).
    
- Administrative Distance: Connected 0, Static 1, EIGRP 90, OSPF 110, RIP 120.
    

---

## 8. ARP (IPv4) in Neighbor Discovery (IPv6)

**Zakaj potrebujemo ARP/ND**

- Za vsak L3 paket moraš poznati **L2 (MAC) cilj** na trenutnem segmentu.
    
- IP naslovi ostanejo enaki od izvora do cilja; MAC naslovi se spreminjajo na vsakem hopu.[[scribd](https://www.scribd.com/document/464000442/CCNA-1-v7-0-Final-Exam-Answers-Full-Introduction-to-Networks)]​
    

**ARP (IPv4)**

- ARP Request: L2 broadcast (FF:FF:FF:FF:FF:FF) z vprašanjem »Kdo ima IP X?«.
    
- ARP Reply: unicast odgovor z MAC naslovom.
    
- ARP tabela (cache): `arp -a`, na routerju `show arp`.
    

**Pomembno za izpit**

- Gost za **remote IP** _ne_ pošlje ARP – pošlje ARP za **default gateway**, potem router reši naprej.[[scribd](https://www.scribd.com/document/464000442/CCNA-1-v7-0-Final-Exam-Answers-Full-Introduction-to-Networks)]​
    
- ARP poisoning: napadalec pošilja lažne Reply → MITM.
    

**IPv6 Neighbor Discovery (ND, del ICMPv6)**

- NS (Neighbor Solicitation) / NA (Neighbor Advertisement) = ARP zamenjava, uporabljata **solicited‑node multicast**, ne broadcast.[[infraexam](https://infraexam.com/ccna1-v7/ccna1-v7-itnv7-final-exam-answers/)]​
    
- RS/RA (Router Solicitation / Advertisement) za prefixe, DGW, SLAAC/DHCPv6 informacije.
    

---

## 9. Basic router/switch config in show ukazi

**Boot proces routerja**

1. POST + bootstrap iz ROM.
    
2. Naloži IOS iz flash (ali TFTP).
    
3. Naloži startup‑config iz NVRAM; če ga ni → setup dialog.[[elktech](https://elktech.org/CCNA/Semester1/ModuleReviews/ITN10.pdf)]​
    

**Spomin**

- RAM: running‑config, routing tabele, ARP, bufferji.
    
- NVRAM: startup‑config.
    
- Flash: IOS image, dodatne datoteke.
    
- ROM: bootstrap, ROMmon.
    

**Osnovni konfiguracijski pattern**

text

`enable configure terminal hostname R1 no ip domain-lookup enable secret <geslo> service password-encryption banner motd # ... # line console 0  password <...> login logging synchronous line vty 0 4  password <...> login ! interface g0/0/0  description LAN 192.168.10.0/24 ip address 192.168.10.1 255.255.255.0 no shutdown ! copy running-config startup-config`

**Show ukazi (klasični v vprašanji)**

- `show ip interface brief` → IP naslovi, L1/L2 status vmesnikov.[[scribd](https://www.scribd.com/document/464000442/CCNA-1-v7-0-Final-Exam-Answers-Full-Introduction-to-Networks)]​
    
- `show running-config`, `show startup-config`, `show interfaces`, `show ip route`, `show version`, `show mac address-table`.
    

---

## 10. IPv4 naslavljanje in subnetting

**Struktura in posebni naslovi**

- Network address (vsi host biti = 0), Broadcast (vsi host biti = 1), usable hosti vmes.
    
- Zasebni bloki: 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16.[[infraexam](https://infraexam.com/ccna1-v7/)]​
    

**Formule**

- Št. hostov: 2n−22^n - 22n−2, n = št. host bitov.
    
- Št. podomrežij: 2s2^s2s, s = izposojeni biti iz host dela.
    

**Tipične naloge**

- »LAN potrebuje 25/50/90 hostov – najmanjša maska?«
    
    - Najdi najmanjši n, da 2n−2≥2^n - 2 ≥2n−2≥ št. hostov → n → maska.
        
    - 25 hostov → 25−2=302^5 - 2 = 3025−2=30 → /27 → 255.255.255.224.infraexam+1
        

**Primer: 192.168.1.0/24 na 4 enaka subnet‑a**

- Potrebuješ 4 subnet‑e → 2² → izposodiš 2 bita → /26.
    
- Blok = 64 naslovov:
    
    - 0–63, 64–127, 128–191, 192–255.
        

---

## 11. IPv6 naslavljanje

**Zapis in krajšanje**

- 128 bitov, 8 skupin po 16 bitov v hex, ločene z `:`.
    
- Pravila krajšanja: odstrani vodilne ničle; eno zaporedje samih 0 nadomesti z `::` (samo enkrat).[[studocu](https://www.studocu.com/en-us/document/emporia-state-university/computer-networks-internets/ccna-1-v70-final-exam-answers-full-introduction-to-networks/22652598)]​
    

**Vrste naslovov**

- GUA: `2000::/3` (2/3 na začetku), globalno usmerljiv.
    
- Link‑local: `FE80::/10`, avtomatsko na vsakem vmesniku, ne‑usmerljiv.
    
- Unique Local: `FC00::/7`, zasebni obseg.
    
- Loopback: `::1`, Unspecified: `::`.[[studocu](https://www.studocu.com/en-us/document/emporia-state-university/computer-networks-internets/ccna-1-v70-final-exam-answers-full-introduction-to-networks/22652598)]​
    

**Samodejna konfiguracija**

- SLAAC: host dobi prefix iz RA in sam generira Interface ID; uporablja DAD (Duplicate Address Detection).[[studocu](https://www.studocu.com/en-us/document/emporia-state-university/computer-networks-internets/ccna-1-v70-final-exam-answers-full-introduction-to-networks/22652598)]​
    
- Kombinacije RA flagov:
    
    - SLAAC only (A=1, M=0, O=0),
        
    - SLAAC + stateless DHCPv6 (A=1, O=1),
        
    - Stateful DHCPv6 (M=1).
        

**IPv6 subnetting**

- Tipično: organizacija dobi /48 → /64 za posamezen LAN (16 bitov za subnet ID → 65.536 subnetov).[[studocu](https://www.studocu.com/en-us/document/emporia-state-university/computer-networks-internets/ccna-1-v70-final-exam-answers-full-introduction-to-networks/22652598)]​
    

---

## 12. ICMP, ping, traceroute

**ICMPv4/v6 osnovna sporočila**

- Echo Request / Echo Reply → ping.
    
- Destination Unreachable (različne kode).
    
- Time Exceeded → TTL/Hop limit = 0 (osnova traceroute).[[infraexam](https://infraexam.com/ccna1-v7/ccna1-v7-itnv7-final-exam-answers/)]​
    

**Ping**

- Test loopback (`127.0.0.1` ali `::1`), lokalni GW, remote host.
    
- Prvi ping lahko pade zaradi ARP/ND.
    

**Traceroute / tracert**

- Pošilja pakete z TTL=1,2,3…; vsak router, kjer TTL poteče, vrne ICMP Time Exceeded → vidiš vsak hop in RTT.[[infraexam](https://infraexam.com/ccna1-v7/ccna1-v7-itnv7-final-exam-answers/)]​
    

---

## 13. Transport Layer, TCP vs UDP, porti

**TCP**

- Connection‑oriented (3‑way handshake), zanesljiv (ACK + retransmisija), ohrani vrstni red (sequence numbers), flow control (window size), congestion control.[[youtube](https://www.youtube.com/watch?v=0VtGnhUze6Y)]​
    
- Uporaba: HTTP/HTTPS, FTP, SMTP, POP3, IMAP, SSH, Telnet.
    

**UDP**

- Connectionless, best effort, brez ACK, brez vrstnega reda, minimalen header (8 B) → manj overheada.[[studocu](https://www.studocu.com/en-us/document/emporia-state-university/computer-networks-internets/ccna-1-v70-final-exam-answers-full-introduction-to-networks/22652598)]​
    
- Uporaba: DNS, DHCP, VoIP, video streaming, TFTP, SNMP, gaming.
    

**3‑way handshake (kratko)**

- SYN → SYN‑ACK → ACK.
    

**Porti – nujni za CCNA**

- 20/21 FTP, 22 SSH, 23 Telnet, 25 SMTP, 53 DNS (TCP/UDP), 67/68 DHCP, 69 TFTP, 80 HTTP, 110 POP3, 143 IMAP, 161 SNMP, 443 HTTPS.scribd+1
    
- Well‑known: 0–1023, registered: 1024–49151, ephemeral: 49152–65535.
    

**Socket par**

- (Src IP:Src port, Dst IP:Dst port) unikatno identificira sejo.
    

---

## 14. Ključni ukazi za troubleshooting (Windows & Cisco)

**Windows**

- `ipconfig /all` – IP, maska, DGW, DNS.[[infraexam](https://infraexam.com/ccna1-v7/ccna1-v7-itnv7-final-exam-answers/)]​
    
- `ping` – povezljivost.
    
- `tracert` – pot do cilja.
    
- `arp -a` – ARP tabela.
    
- `nslookup` – DNS resolve.
    

**Cisco IOS**

- `show ip interface brief`, `show ipv6 interface brief`.
    
- `show running-config`, `show startup-config`, `show ip route`, `show ipv6 route`, `show arp`, `show ipv6 neighbors`.
    
- `copy running-config startup-config`, `erase startup-config`, `reload`.
    

---

To je “en list za vse”: če si to dobro ponotranjiš (posebej maske/hoste, port številke, ARP vs ND, TCP/UDP lastnosti, strukture frame/paketa), bi moral biti večino final vprašanj sposoben rešiti brez direktnega prepoznavanja vprašanja z neta.scribd+1