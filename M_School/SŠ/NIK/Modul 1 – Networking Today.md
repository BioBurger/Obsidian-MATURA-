---
tags:
  - CCNA1
  - networking
  - modul-1
aliases:
  - Networking Today
  - Modul 1
---



> [!summary] Cilj modula
> Razložiti napredek sodobnih omrežnih tehnologij in kako omrežja vplivajo na naše vsakdanje življenje.

---

## 1.1 Kako omrežja vplivajo na naše življenje

- Omrežja povezujejo **ljudi, naprave in informacije** po vsem svetu
- Omogočajo: komunikacijo, zabavo, e-commerce, zdravstvene storitve, izobraževanje
- Sodobna omrežja so **konvergirana** → glas, video, podatki tečejo po istem omrežju

> [!example] Primer
> Ko pošlješ Snapchat, podatki potujejo skozi tvoj router → ISP → internet → strežnik Snapchata → prejemnik. Vse to v milisekundah.

---

## 1.2 Komponente omrežja

Omrežje sestavljajo **hosts**, **intermediary devices** in **media**.

### Hosts (končne naprave)

| Vrsta | Opis | Primeri |
|-------|------|---------|
| **Client** | Zahteva storitve | PC, telefon, tablica |
| **Server** | Nudi storitve | Web server, mail server, file server |
| **Peer** | Hkrati client in server | V P2P omrežjih |

### Intermediary Devices (vmesne naprave)

- **Switch** → poveže naprave v LAN, posreduje okvirje (frames)
- **Router** → poveže različna omrežja, posreduje pakete (packets)
- **Wireless Access Point (WAP)** → brezžičen dostop
- **Firewall** → varnostni filter prometa
- **Modem** → pretvori signal za WAN (DSL, kabel)

### Network Media (mediji)

| Medij | Opis | Hitrost |
|-------|------|---------|
| **Copper (UTP/STP)** | Električni signal | do 10 Gbps |
| **Fiber-optic** | Svetlobni signal | do 100+ Gbps |
| **Wireless** | Radio valovi | odvisno od standarda |

---

## 1.3 Omrežne reprezentacije in topologije

> [!info] Dve vrsti topologij
> - **Physical topology** → kako so naprave fizično povezane
> - **Logical topology** → kako podatki tečejo skozi omrežje

### Simboli za diagrame

| Simbol | Naprava |
|--------|---------|
| Trikotnik s puščicami | Router |
| Kvadrat z linijami | Switch |
| Oblak | Internet / WAN |
| Računalnik | Host / PC |
| Antena | Wireless AP |

---

## 1.4 Vrste omrežij

### Glede na velikost

| Tip | Polno ime | Pokritost |
|-----|-----------|-----------|
| **PAN** | Personal Area Network | ~meter (Bluetooth) |
| **LAN** | Local Area Network | stavba, kampus |
| **MAN** | Metropolitan Area Network | mesto |
| **WAN** | Wide Area Network | država, kontinent, svet |
| **WLAN** | Wireless LAN | brezžičen LAN |

### LAN vs WAN

| | LAN | WAN |
|--|-----|-----|
| Lastništvo | Zasebno (podjetje, dom) | ISP / Telekom |
| Hitrost | Visoka (1–10 Gbps) | Nižja (odvisno od ISP) |
| Napake | Redkejše | Pogostejše |
| Primer | Domače omrežje | Internet |

### Internet, Intranet, Extranet

- **Internet** → javno globalno omrežje omrežij
- **Intranet** → zasebno omrežje znotraj organizacije
- **Extranet** → omejen dostop zunanjim partnerjem (dobaviteljem, strankam)

---

## 1.5 Internetne povezave

### Za domače / SOHO uporabnike

- **DSL** (Digital Subscriber Line) → skozi telefonsko linijo, do 100 Mbps
- **Cable** → skozi kabelsko TV infrastrukturo, do 1 Gbps
- **Fiber** → najhitrejši, direktno optičen kabel
- **Cellular (4G/5G)** → mobilno omrežje
- **Satellite** → oddaljene lokacije (Starlink!)

### Za podjetja

- **Dedicated Leased Lines** → zagotovljena pasovna širina (T1, T3)
- **Metro Ethernet** → visoka hitrost v mestih
- **Business DSL / Cable**

---

## 1.6 Zanesljivo omrežje – 4 osnove

> [!important] 4 karakteristike zanesljivega omrežja
> 1. **Fault Tolerance** (odpornost na napake)
> 2. **Scalability** (razširljivost)
> 3. **Quality of Service – QoS** (prioritizacija prometa)
> 4. **Security** (varnost)

### Fault Tolerance

- Omrežje deluje kljub napakam → **redundantne** poti in naprave
- Packet-switched omrežja: podatki se razdelijo na **pakete**, ki gredo po različnih poteh

### Scalability

- Omrežje se da razširiti **brez degradacije** obstoječe storitve
- Dosežemo z modularnima dizajnom in standardiziranimi protokoli

### QoS

- Nekateri tipi prometa imajo **prednost** (VoIP > file download)
- Brez QoS: vid. klic se zamrzne, ko nekdo prenaša film

### Security

- **Confidentiality** → podatki vidni samo pooblaščenim
- **Integrity** → podatki se niso spremenili med prenosom
- **Availability** → storitve dostopne pooblaščenim ob pravem času
- → **CIA triad** !

---

## 1.7 Trendi v omrežjih

| Trend | Opis |
|-------|------|
| **BYOD** | Bring Your Own Device – zaposleni/učenci prinašajo svoje naprave |
| **Online Collaboration** | Skupno delo v realnem času (Teams, Google Docs) |
| **Video Communication** | Zoom, Meet, WebEx |
| **Cloud Computing** | IaaS, SaaS, PaaS – storitve v oblaku |
| **IoT** | Internet of Things – pametni dom, industrija |
| **Powerline Networking** | Omrežje po električnih vodih (HomePlug) |

---

## 1.8 Osnove varnosti omrežja

### Grožnje

- **Virusi, worms, trojanci** → škodljiva programska oprema
- **Spyware, adware** → zbiranje podatkov
- **Zero-day attacks** → napadi na neznane ranljivosti
- **DDoS** → preplavitev z zahtevami
- **Identity theft** → kraja identitete
- **Data interception** → prisluškovanje

### Osnovna zaščita

- **Antivirus / Antimalware** software
- **Firewall** → filtrira promet
- **Access control** → gesla, 2FA
- **VPN** → šifriran tunel

---

## 1.9 IT poklici v omrežju

- Network Engineer / Administrator
- Security Analyst
- Cloud Architect
- NOC Technician (Network Operations Center)

---

## 🔗 Povezave

- [[Modul 2 - Basic Switch and End Device Configuration]]
- [[Modul 3 - Protocols and Models]]
- [[Modul 4 - Physical Layer]]

---

## ❓ Check Your Understanding

> [!question] Vprašanje 1
> Kateri dve vrsti naprav sta "intermediary devices"?
> > [!done]- Odgovor
> > **Router** in **Switch** (ter AP, Firewall, Modem)

> [!question] Vprašanje 2
> Kateri 4 stebri gradijo zanesljivo omrežje?
> > [!done]- Odgovor
> > Fault Tolerance, Scalability, QoS, Security

> [!question] Vprašanje 3
> Kakšna je razlika med intranet in extranet?
> > [!done]- Odgovor
> > Intranet = zasebno, samo za interno. Extranet = delno odprt za zunanje partnerje.