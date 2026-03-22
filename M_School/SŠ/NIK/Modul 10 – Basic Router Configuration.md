---
tags:
  - CCNA1
  - router
  - IOS
  - konfiguracija
  - modul-10
aliases:
  - Modul 10
  - Basic Router Configuration
  - Router Config
---


> [!summary] Cilj modula
> Implementirati začetne nastavitve na Cisco routerju in konfigurirati vmesnike ter default gateway.

---

## 10.1 Router – osnove

### Fizične komponente routerja

| Komponenta | Opis |
|-----------|------|
| **CPU** | Izvaja IOS in procesira pakete |
| **RAM** | Delovno pomnilnik – running-config, routing tabela, ARP cache |
| **NVRAM** | Trajna hramba – startup-config |
| **Flash** | Hramba IOS image datoteke |
| **ROM** | Bootstrap program, POST, mini-IOS (ROMmon) |
| **Interfaces** | LAN (GigabitEthernet), WAN (Serial), Management (Console, AUX) |

### Boot proces routerja (3 faze)
1. POST (Power-On Self-Test) + naloži bootstrap iz ROM
    
2. Poišče in naloži IOS image:  
    Flash → TFTP strežnik → ROM (mini-IOS)
    
3. Poišče in naloži startup-config:  
    NVRAM → TFTP → Setup mode (če ni najdeno)
    
> [!warning] RAM se ob ponovnem zagonu **izbriše** (running-config, routing tabela, ARP cache)!
> NVRAM in Flash sta **neizgubni** (non-volatile).

---

## 10.2 Osnovna konfiguracija routerja – korak za korakom

### Korak 1: Začetne nastavitve

```cisco
Router> enable
Router# configure terminal

R1(config)# hostname R1
R1(config)# no ip domain-lookup          → Onemogoči DNS lookup pri typo-jih
R1(config)# enable secret cisco123       → Encrypted privileged geslo
R1(config)# service password-encryption  → Šifrira plain-text gesla

R1(config)# banner motd #
*** POZOR: Nepooblascen dostop je prepovedan! ***
#
```

### Korak 2: Gesla za konzolo in VTY

```cisco
R1(config)# line console 0
R1(config-line)# password con123
R1(config-line)# login
R1(config-line)# logging synchronous     → Prepreči prekinitev ukazov z log sporočili
R1(config-line)# exit

R1(config)# line vty 0 4
R1(config-line)# password vty123
R1(config-line)# login
R1(config-line)# exit
```

### Korak 3: Konfiguracija vmesnikov

```cisco
R1(config)# interface gigabitethernet 0/0/0
R1(config-if)# description Povezava na LAN 192.168.10.0
R1(config-if)# ip address 192.168.10.1 255.255.255.0
R1(config-if)# ipv6 address 2001:DB8:ACAD:10::1/64
R1(config-if)# ipv6 address FE80::1 link-local
R1(config-if)# no shutdown               → OBVEZNO – vmesnik je privzeto izklopljen!
R1(config-if)# exit

R1(config)# interface gigabitethernet 0/0/1
R1(config-if)# description Povezava na LAN 192.168.20.0
R1(config-if)# ip address 192.168.20.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit
```

> [!important] Router vmesniki so privzeto **administratively down**!
> Vedno zaključi z `no shutdown` da aktiviraš vmesnik.

### Korak 4: Shrani konfiguracijo

```cisco
R1# copy running-config startup-config
```

---

## 10.3 Konfiguracija IPv6 na routerju

IPv6 usmerjanje mora biti posebej **vklopljeno**:

```cisco
R1(config)# ipv6 unicast-routing         → OBVEZNO za IPv6 routing!

R1(config)# interface gigabitethernet 0/0/0
R1(config-if)# ipv6 address 2001:DB8:ACAD:1::1/64    → Global unicast
R1(config-if)# ipv6 address FE80::1 link-local        → Link-local
R1(config-if)# no shutdown
```

### IPv6 naslovne vrste na vmesniku

| Vrsta | Primer | Opis |
|-------|--------|------|
| **Global Unicast** | `2001:DB8::/32` | Javno usmerljiv (ekvivalent public IPv4) |
| **Link-Local** | `FE80::/10` | Samo v lokalnem segmentu, ni usmerljiv |
| **Loopback** | `::1/128` | Lokalno testiranje |

---

## 10.4 Verify – preverjanje konfiguracije routerja

```cisco
show running-config                    → Celotna aktivna konfiguracija
show ip interface brief                → Hiter pregled vseh vmesnikov (IPv4)
show ipv6 interface brief              → Hiter pregled vseh vmesnikov (IPv6)
show interfaces                        → Detajlni status vmesnikov
show ip route                          → IPv4 routing tabela
show ipv6 route                        → IPv6 routing tabela
show ip interface [vmesnik]            → Detajlni IPv4 info za vmesnik
show version                           → IOS verzija, hardware info, uptime
```

### Razlaga statusov `show ip interface brief`

| Status | Protocol | Razlaga |
|--------|----------|---------|
| `up` | `up` | ✅ Vmesnik deluje normalno |
| `up` | `down` | ⚠️ L1 ok, L2 problem (keepalive, encapsulation) |
| `administratively down` | `down` | ❌ Izklopljen z `shutdown` ukazom |
| `down` | `down` | ❌ Ni kabla / fizična napaka |

> [!example] Primer izhoda
> ```
> Interface          IP-Address      OK? Method Status    Protocol
> GigabitEthernet0/0/0  192.168.10.1  YES manual up      up
> GigabitEthernet0/0/1  192.168.20.1  YES manual up      up
> GigabitEthernet0/0/2  unassigned    YES unset  admin down down
> ```

---

## 10.5 Default Gateway konfiguracija

### Na end device (PC)

- PC **mora** imeti: IP naslov, subnet maska, default gateway
- Default gateway = **IP routerjevega vmesnika** v istem omrežju
- Brez default gateway → komunikacija samo znotraj lokalnega omrežja!

### Na switchu (za remote management)

```cisco
Switch(config)# interface vlan 1
Switch(config-if)# ip address 192.168.10.254 255.255.255.0
Switch(config-if)# no shutdown
Switch(config-if)# exit

Switch(config)# ip default-gateway 192.168.10.1   → IP routerjevega vmesnika!
```

> [!info] Zakaj switch potrebuje default gateway?
> Switch je Layer 2 naprava. Brez default gateway-a ga ne moreš konfigurirati iz drugega omrežja (npr. prek SSH z oddaljenega PC-ja).

---

## 10.6 Loopback vmesnik

```cisco
R1(config)# interface loopback 0
R1(config-if)# ip address 1.1.1.1 255.255.255.255
R1(config-if)# description Loopback za testiranje
```

- **Loopback** = virtualni vmesnik, vedno je `up/up`
- Uporablja se za: testiranje, router ID pri OSPF, management
- Ne potrebuje `no shutdown` – je vedno aktiven

---

## 10.7 Router IOS načini – primerjava z switchem

Enako kot pri switchu (Modul 2), samo drugačen prompt:

| Način | Prompt | Dostop |
|-------|--------|--------|
| User EXEC | `Router>` | `enable` |
| Privileged EXEC | `Router#` | `configure terminal` |
| Global Config | `Router(config)#` | `interface`, `line`... |
| Interface Config | `Router(config-if)#` | `interface GigX` |
| Line Config | `Router(config-line)#` | `line console 0` |
| Routing Protocol | `Router(config-router)#` | `router ospf 1` |

---

## 🔗 Povezave

- [[Modul 9 - Address Resolution]]
- [[Modul 2 - Basic Switch and End Device Configuration]]

---

## ❓ Check Your Understanding

> [!question] Vprašanje 1
> Zakaj je potreben ukaz `no shutdown` na router vmesniku?
> > [!done]- Odgovor
> > Router vmesniki so privzeto **administratively down** – `no shutdown` jih aktivira.

> [!question] Vprašanje 2
> Kje je shranjen IOS image? Kje running-config? Kje startup-config?
> > [!done]- Odgovor
> > IOS image → **Flash**, running-config → **RAM**, startup-config → **NVRAM**

> [!question] Vprašanje 3
> Kateri ukaz aktivira IPv6 usmerjanje na routerju?
> > [!done]- Odgovor
> > `ipv6 unicast-routing` (v Global Config mode)

> [!question] Vprašanje 4
> Kaj pomeni status `administratively down` pri `show ip interface brief`?
> > [!done]- Odgovor
> > Vmesnik je **ročno izklopljen** z ukazom `shutdown`. Popravi z `no shutdown`.

> [!question] Vprašanje 5
> Zakaj switchu nastavimo default gateway?
> > [!done]- Odgovor
> > Da ga lahko upravljamo (SSH/Telnet) **iz drugega omrežja** – brez njega switch ne more komunicirati izven svojega LAN segmenta.

> [!question] Vprašanje 6
> Kateri ukaz preveri stanje vmesnikov in IP naslove v kratki obliki?
> > [!done]- Odgovor
> > `show ip interface brief`
