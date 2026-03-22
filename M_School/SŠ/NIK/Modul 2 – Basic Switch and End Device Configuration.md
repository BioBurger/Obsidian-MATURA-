---
tags:
  - CCNA1
  - switching
  - IOS
  - modul-2
aliases:
  - Modul 2
  - Switch Configuration
---



> [!summary] Cilj modula
> Konfigurirati osnovno nastavitev Cisco stikala in končnih naprav z uporabo Cisco IOS CLI.

---

## 2.1 Cisco IOS

- **IOS** = Internetwork Operating System → operacijski sistem na Cisco napravah
- Dostop do IOS: konzolni kabel, SSH, Telnet, AUX port
- IOS je **tekstovni (CLI)** vmesnik – ni GUI (razen CCP/Cisco CP)

### Dostopni načini

| Način                | Prompt                 | Namen                   |
| -------------------- | ---------------------- | ----------------------- |
| **User EXEC**        | `Switch>`              | Osnoven pregled, ping   |
| **Privileged EXEC**  | `Switch#`              | Diagnostika, show ukazi |
| **Global Config**    | `Switch(config)#`      | Splošne nastavitve      |
| **Interface Config** | `Switch(config-if)#`   | Nastavitev vmesnika     |
| **Line Config**      | `Switch(config-line)#` | Nastavitev konzole/VTY  |

---

## 2.2 IOS Navigation – Načini (Modes)

```cisco
Switch> enable                     → User → Privileged EXEC
Switch# configure terminal         → Privileged → Global Config
Switch(config)# interface vlan 1   → Global → Interface Config
Switch(config-if)# exit            → korak nazaj
Switch(config-if)# end             → takoj nazaj v Privileged EXEC
Switch# disable                    → Privileged → User EXEC
```

> [!tip] Bližnjice
> - `Ctrl+Z` = isto kot `end`
> - `Tab` = autocomplete ukaza
> - `?` = pomoč / seznam ukazov
> - `Ctrl+C` = prekini ukaz

---

## 2.3 Osnovna konfiguracija naprave

### Korak za korakom – celotna osnovna konfiguracija

```cisco
Switch> enable
Switch# configure terminal

Switch(config)# hostname S1                        → Nastavi ime
Switch(config)# enable secret cisco123             → Encrypted privileged geslo
Switch(config)# service password-encryption        → Šifrira vsa plain-text gesla

Switch(config)# banner motd # Nepooblascen dostop prepovedan! #

Switch(config)# line console 0
Switch(config-line)# password con123
Switch(config-line)# login
Switch(config-line)# exit

Switch(config)# line vty 0 15
Switch(config-line)# password vty123
Switch(config-line)# login
Switch(config-line)# exit

Switch(config)# interface vlan 1
Switch(config-if)# ip address 192.168.1.2 255.255.255.0
Switch(config-if)# no shutdown
Switch(config-if)# exit

Switch(config)# ip default-gateway 192.168.1.1

Switch(config)# end
Switch# copy running-config startup-config
```

---

## 2.4 Gesla – vrste in razlika

| Geslo | Ukaz | Shranjeno |
|-------|------|-----------|
| **enable password** | `enable password GESLO` | Plain text ❌ |
| **enable secret** | `enable secret GESLO` | MD5 hash ✅ |
| **console** | `line con 0` → `password` + `login` | Plain text (šifrira se s `service password-encryption`) |
| **VTY (Telnet/SSH)** | `line vty 0 15` → `password` + `login` | Plain text (enako) |

> [!important] Vedno uporabljaj `enable secret` namesto `enable password`!
> Če sta oba nastavljena, ima `enable secret` prednost.

---

## 2.5 Konfiguracija IP naslova

### Na stikalu (Layer 2) – prek SVI (VLAN vmesnik)

```cisco
Switch(config)# interface vlan 1
Switch(config-if)# ip address 192.168.1.10 255.255.255.0
Switch(config-if)# no shutdown
```

### Na PC (Windows)
- **Static**: Nastavi IP, Subnet, Gateway ročno
- **DHCP**: Avtomatsko pridobi IP

---

## 2.6 Verify (preverjanje konfiguracije)

```cisco
show running-config              → Prikaži aktivno konfiguracijo
show startup-config              → Prikaži shranjeno konfiguracijo
show ip interface brief          → Kratek pregled vmesnikov (IP, status)
show interfaces                  → Detajlni pregled vmesnikov
show version                     → IOS verzija, uptime, HW info
show mac address-table           → MAC tabela stikala
```

> [!example] Izhod show ip interface brief
> ```
> Interface    IP-Address    OK?  Method  Status  Protocol
> Vlan1        192.168.1.10  YES  manual  up      up
> ```

---

## 2.7 Shranjevanje in brisanje konfiguracije

```cisco
copy running-config startup-config    → Shrani (RAM → NVRAM)
copy startup-config running-config    → Naloži shranjeno
erase startup-config                  → Izbriši shranjeno konfig
reload                                → Ponovni zagon
```

> [!warning] `erase startup-config` + `reload` = tovarniške nastavitve!

---

## 2.8 Sintaksa IOS ukazov

| Element | Opis | Primer |
|---------|------|--------|
| **Keyword** | Fiksen del ukaza | `show`, `interface` |
| **Argument** | Spremenljiv del | `vlan 1`, `192.168.1.1` |
| **Bold** | Vtipkaj točno tako | **show** |
| **Italic** | Zamenjaj z vrednostjo | *ip-address* |
| `[x]` | Neobvezno | `[no]` shutdown |
| `{x\|y}` | Izberi eno | `{in\|out}` |

---

## 🔗 Povezave

- [[Modul 1 - Networking Today]]
- [[Modul 3 - Protocols and Models]]

---

## ❓ Check Your Understanding

> [!question] Vprašanje 1
> Kateri ukaz te postavi v Global Configuration mode?
> > [!done]- Odgovor
> > `configure terminal` (iz Privileged EXEC mode)

> [!question] Vprašanje 2
> Kakšna je razlika med `enable password` in `enable secret`?
> > [!done]- Odgovor
> > `enable secret` shrani geslo kot MD5 hash – varnejše. `enable password` je plain text.

> [!question] Vprašanje 3
> Kateri ukaz shrani running-config v NVRAM?
> > [!done]- Odgovor
> > `copy running-config startup-config`

> [!question] Vprašanje 4
> Zakaj stikalu nastavimo IP naslov prek `interface vlan 1`?
> > [!done]- Odgovor
> > Ker je stikalo Layer 2 naprava – nima fizičnega IP vmesnika. SVI (VLAN1) služi za management dostop.