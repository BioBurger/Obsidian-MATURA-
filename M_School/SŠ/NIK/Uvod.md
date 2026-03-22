---
tags:
  - CCNA1
  - index
  - MOC
aliases:
  - CCNA Index
  - CCNA1 MOC
---

# 🗺️ CCNA1 – Map of Content

> [!summary] O tem vault-u
> Zapiske za **Cisco Networking Academy – CCNA 1: Introduction to Networks (ITN v7)**
> Vsak modul je ločena datoteka z definicijami, tabelami, ukazi in CYU vprašanji.

---

## 📁 Moduli

| Modul | Tema | Status |
|-------|------|--------|
| [[Modul 1 - Networking Today]] | Komponente, topologije, varnost, trendi | ✅ |
| [[Modul 2 - Basic Switch and End Device Configuration]] | Cisco IOS, CLI, IP naslavljanje | ✅ |
| [[Modul 3 - Protocols and Models]] | OSI model, TCP/IP, enkapsulacija | ✅ |
| [[Modul 4 - Physical Layer]] | UTP, Fiber, Wireless, standardi | ✅ |

---

## 🔑 Ključni pojmi (hitri dostop)

- [[Modul 1 - Networking Today#1.6 Zanesljivo omrežje – 4 osnove|CIA triad + 4 karakteristike zanesljivega omrežja]]
- [[Modul 2 - Basic Switch and End Device Configuration#2.2 IOS Navigation – Načini (Modes)|IOS načini (User/Privileged/Config)]]
- [[Modul 3 - Protocols and Models#3.5 Referenčni modeli|OSI 7 plasti]]
- [[Modul 3 - Protocols and Models#3.6 Data Encapsulation (Enkapsulacija)|Enkapsulacija / PDU]]
- [[Modul 4 - Physical Layer#4.4 UTP kabling – podrobno|UTP kategorije in kabli]]
- [[Modul 4 - Physical Layer#4.5 Optični kabli (Fiber-Optic Cabling)|SMF vs MMF]]

---

## 📝 Hitri ukazi (Cisco IOS)

```cisco
enable                          → User → Privileged EXEC
configure terminal              → Privileged → Global Config
hostname IME                    → Nastavi ime naprave
enable secret GESLO             → Nastavi encrypted geslo
service password-encryption     → Šifriraj vsa gesla
banner motd # OPOZORILO #       → Banner sporočilo
copy running-config startup-config  → Shrani konfig!
show running-config             → Prikaži trenutno konfig
show ip interface brief         → Prikaži vmesnike
show version                    → Prikaži IOS verzijo
```

---

## 🧠 Mnemoehnika

| | |
|-|-|
| **OSI 7→1** | **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing |
| **CIA triad** | **C**onfidentiality, **I**ntegrity, **A**vailability |
| **4 reliab.** | **F**ault tolerance, **S**calability, **Q**oS, **S**ecurity |

---

> [!tip] Kako delati z zapisi
> - Odpri posamezni modul za podroben pregled
> - Callout bloki `> [!question]` skrijejo odgovore – klikni za razkritje
> - Označi naučene teme z ✅ v tabeli zgoraj