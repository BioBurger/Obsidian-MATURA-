---
tags:
  - CCNA1
  - security
  - network-security
  - modul-16
aliases:
  - Modul 16
  - Network Security Fundamentals
  - Osnove varnosti omrežja
---


> [!summary] Cilj modula
> Razumeti vrste groženj in napadov, principe **layered security** in osnovno utrjevanje (hardening) usmerjevalnikov in stikal.

---

## 16.1 Zakaj sploh varnost?

- Današnja omrežja povezujejo **kritične podatke, storitve in naprave** – napad lahko pomeni finančno škodo, izpad storitev ali izgubo ugleda.
- Grožnje prihajajo od **zunanjih napadalcev**, notranjih uporabnikov (malomarnih ali zlonamernih) in avtomatizirane zlonamerne kode (malware).[web:78]
- Varnost nikoli ni 100 % – cilj je **zmanjšanje tveganja** z več sloji zaščite (defense-in-depth).[web:78]

### Tri vrste posledic napadov

- **Information theft** → kraja podatkov (osebni podatki, poslovne skrivnosti).[web:82]
- **Data loss / manipulation** → brisanje ali spreminjanje podatkov (npr. baze, konfiguracije).[web:82]
- **Disruption of service** → DoS/DDoS, izpadi storitev (email, web, VoIP).[web:78][web:82]

---

## 16.2 Ranljivosti in grožnje

### Tri glavne skupine ranljivosti

| Vrsta | Primeri |
|-------|---------|
| **Technological** | Stara IOS verzija, znane CVE ranljivosti, nezaščiteni protokoli (Telnet, HTTP).[web:78] |
| **Configuration** | Privzeta gesla, odprti vsi porti, napačne ACL, nezaščiteni VTY.[web:78] |
| **Security policy / procedural** | Ni politike gesel, brez varnostnih kopij, brez izobraževanja uporabnikov.[web:78] |

### Malware

- **Virus** → potrebuje gostiteljsko datoteko, razširi se z njeno uporabo.[web:78]
- **Worm** → se širi samostojno prek omrežja, brez uporabnika.[web:78]
- **Trojan horse** → navidez legitimen program, v ozadju izvaja zlonamerne akcije.[web:78]
- Drugi: **spyware, adware, ransomware, rootkit**.[web:78]

### Omrežni napadi (po kategorijah)

| Kategorija | Opis | Primeri |
|-----------|------|---------|
| **Reconnaissance** | Zbiranje informacij, iskanje ranljivosti | port scan, ping sweep, packet sniffer.[web:78][web:82] |
| **Access attacks** | Neavtoriziran dostop do sistemov/podatkov | password attack (dictionary, brute-force), man-in-the-middle, port redirection.[web:78][web:82] |
| **Denial of Service (DoS/DDoS)** | Onemogočanje storitve z veliko količino prometa | SYN flood, ICMP flood, ping of death.[web:78][web:82] |

---

## 16.3 Fizične grožnje

> [!info] Štiri kategorije fizičnih groženj[web:78]
> 1. **Hardware threats** – kraja/poškodba naprav.
> 2. **Environmental threats** – temperatura, vlaga, prah.
> 3. **Electrical threats** – izpad napajanja, prenapetost, špice.
> 4. **Maintenance threats** – slabo vzdrževanje, kabli po tleh, odprti racki.

Primeri zaščite:
- Zaklenjene sobe/racki, video nadzor, pristopne kartice.
- UPS, prenapetostne zaščite, generatorji.
- Urejena kabelska infrastruktura, označevanje, redni pregledi.[web:78]

---

## 16.4 Defense-in-Depth – slojevita zaščita

> [!important] Ideja: ne zanašaš se na **en** varnostni mehanizem, ampak na **več slojev**.[web:78]

### Tipične komponente

- **Perimeter firewall / ASA** – filtriranje prometa med notranjim in zunanjim omrežjem.[web:78]
- **VPN** – šifriran dostop na daljavo (site-to-site, remote access).[web:78]
- **IPS/IDS** – zaznava in/ali blokira znane vzorce napadov.[web:78]
- **Email Security Appliance (ESA)** – filtriranje spama, malware v emailu.[web:78]
- **Web Security Appliance (WSA)** – filtriranje HTTP/HTTPS prometa, kategorije strani.[web:78]
- **AAA strežnik** (RADIUS/TACACS+) – centralno preverjanje identitete in avtorizacija.[web:78][web:82]
- **Endpoint security** – antivirus/EDR, host-based firewall, NAC rešitve.[web:78]

---

## 16.5 AAA – Authentication, Authorization, Accounting

| Funkcija | Vloga |
|----------|------|
| **Authentication** | Uporabnik dokaže, kdo je (username/geslo, certifikat, MFA).[web:82] |
| **Authorization** | Določi, kaj uporabnik LAHKO počne (pravice, privilegiji).[web:82] |
| **Accounting** | Beleži, kaj je uporabnik delal (logi, audit).[web:82] |

- Skupaj = **AAA** – tipično implementirano prek RADIUS ali TACACS+ strežnika.[web:78][web:82]
- Na routerju/switchu lahko AAA uporabljaš za VTY, konzolo, SSH dostop.[web:78]

---

## 16.6 Utrjevanje (hardening) usmerjevalnikov in stikal

### Osnovni koraki

```cisco
hostname R1
no ip domain-lookup                  ! brez nadležnega DNS lookupa pri tipkarski napaki
service password-encryption          ! šifriraj vsa plain-text gesla[1]

enable secret MoCnoGeslo123          ! močno, hashirano geslo[1]

line console 0
 password konzola123
 login
 logging synchronous
 exec-timeout 5 0                    ! 5 min neaktivnosti[1]
 exit

line vty 0 4
 transport input ssh                 ! dovoli samo SSH, onemogoči Telnet[3][1]
 login local
 exec-timeout 10 0
 exit
```
Drugo:

- Nastavi **minimalno dolžino gesel** (`security passwords min-length 10`).[web:78]
    
- Uporabi `login block-for ...` za omejitev brute-force poizkusov.[web:78]
    
- Onemogoči neuporabljene servise (npr. `no cdp run` kjer ni potreben, `no ip http server`).[web:78][web:86]
    
- Redno posodabljaj IOS na verzije z zaprtimi ranljivostmi.[web:78]

## 16.7 Konfiguracija SSH

Koraki za omogočanje **varnega oddaljenega dostopa** (namesto Telnet):
R1(config)# hostname R1
R1(config)# ip domain-name example.local       ! potreben za RSA ključ[1]

R1(config)# crypto key generate rsa modulus 1024
R1(config)# username admin secret MoCnoGeslo   ! lokalna baza uporabnikov[1]

R1(config)# line vty 0 4
R1(config-line)# transport input ssh           ! samo SSH
R1(config-line)# login local                   ! uporabi lokalne uporabnike
R1(config-line)# exec-timeout 10 0
R1(config-line)# exit

R1(config)# ip ssh version 2                   ! uporabi SSH v2[3][1]
[!tip] Preverjanje:


show ip ssh → ali je SSH omogočen.


show control-plane host open-ports → kateri management porti so odprti.[web:86]
## 🔗 Povezave
- [[Modul 8 - Network Layer]]
    
- [[Modul 10 - Basic Router Configuration]]
    
- [[Modul 17 - Build a Small Network]]

## ❓ Check Your Understanding

> [!question] Vprašanje 1  
> Katere tri glavne kategorije omrežnih napadov ločimo?
> 
> > [!done]- Odgovor  
> > **Reconnaissance**, **access attacks** in **denial of service (DoS/DDoS)**.

> [!question] Vprašanje 2  
> Kaj pomenijo črke v AAA?
> 
> > [!done]- Odgovor  
> > **Authentication** (preverjanje identitete), **Authorization** (dovoljenja), **Accounting** (beleženje aktivnosti).

> [!question] Vprašanje 3  
> Zakaj je Telnet slab in kaj uporabiš namesto njega?
> 
> > [!done]- Odgovor  
> > Telnet pošilja vse v **clear-text** (tudi gesla). Namesto njega uporabiš **SSH**, ki promet šifrira.

> [!question] Vprašanje 4  
> Naštej vsaj 3 korake za hardening routerja.
> 
> > [!done]- Odgovor  
> > Močna gesla (`enable secret`), šifriranje gesel (`service password-encryption`), onemogočanje Telnet-a (`transport input ssh`), nastavitve `exec-timeout`, onemogočanje neuporabljenih servisov.

> [!question] Vprašanje 5  
> Kaj je defense-in-depth?
> 
> > [!done]- Odgovor  
> > Slojevita zaščita – uporaba več varnostnih mehanizmov (firewall, IPS, VPN, AAA, endpoint security) hkrati, da en sam neuspeh ne zruši celotne varnosti.

