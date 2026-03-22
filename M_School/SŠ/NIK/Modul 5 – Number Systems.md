---
tags:
  - CCNA1
  - number-systems
  - binary
  - hexadecimal
  - modul-5
aliases:
  - Modul 5
  - Number Systems
  - Številski sistemi
---


> [!summary] Cilj modula
> Pretvarjati števila med decimalnim, binarnim in heksadecimalnim sistemom.

---

## 5.1 Binarni številski sistem

- **Binarni** = osnova 2 → samo cifri **0** in **1** (bits)
- Računalniki in omrežne naprave interno delujejo **izključno v binarnem**
- IPv4 naslov = 32 bitov = 4x **oktet** (8 bitov)

### Vrednosti bitov v oktetu

| Bit pozicija | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|-------------|---|---|---|---|---|---|---|---|
| Potenca 2ⁿ | 2⁷ | 2⁶ | 2⁵ | 2⁴ | 2³ | 2² | 2¹ | 2⁰ |
| Vrednost | **128** | **64** | **32** | **16** | **8** | **4** | **2** | **1** |

> [!tip] Zapomni si: 128 – 64 – 32 – 16 – 8 – 4 – 2 – 1  
> Vsak bit je polovica prejšnjega. Vsota vseh = 255.

---

## 5.2 Pretvorba: Decimalno → Binarno

### Metoda odštevanja (greedy)

Pojdi od leve (128) proti desni (1). Če je vrednost ≤ preostanku → napiši **1** in odštej. Sicer → napiši **0**.

> [!example] Primer: 192 → binarno
> ```
> 192 ≥ 128 → 1  (192 - 128 = 64)
>  64 ≥ 64  → 1  (64 - 64 = 0)
>   0 < 32  → 0
>   0 < 16  → 0
>   0 < 8   → 0
>   0 < 4   → 0
>   0 < 2   → 0
>   0 < 1   → 0
> Rezultat: 11000000 = 192
> ```

> [!example] Primer: 173 → binarno
> ```
> 173 ≥ 128 → 1  (173-128=45)
>  45 < 64  → 0
>  45 ≥ 32  → 1  (45-32=13)
>  13 < 16  → 0
>  13 ≥ 8   → 1  (13-8=5)
>   5 ≥ 4   → 1  (5-4=1)
>   1 < 2   → 0
>   1 ≥ 1   → 1
> Rezultat: 10101101 = 173
> ```

---

## 5.3 Pretvorba: Binarno → Decimalno

Seštej vrednosti vseh pozicij kjer je bit **1**.

> [!example] Primer: 10110110 → decimalno
> ```
> 1×128 + 0×64 + 1×32 + 1×16 + 0×8 + 1×4 + 1×2 + 0×1
> = 128 + 32 + 16 + 4 + 2 = 182
> ```

### Pogosti binarni okteti (za hitro referenco)

| Decimalno | Binarno |
|-----------|---------|
| 0 | 00000000 |
| 1 | 00000001 |
| 127 | 01111111 |
| 128 | 10000000 |
| 192 | 11000000 |
| 224 | 11100000 |
| 240 | 11110000 |
| 248 | 11111000 |
| 252 | 11111100 |
| 254 | 11111110 |
| 255 | 11111111 |

> [!tip] Te vrednosti se pojavljajo kot **subnet maske** – jih je vredno zapomniti!

---

## 5.4 Heksadecimalni številski sistem

- **Heksadecimalni (hex)** = osnova 16
- Cifre: **0–9** in **A–F** (A=10, B=11, C=12, D=13, E=14, F=15)
- Uporablja se za: **MAC naslove** (Ethernet) in **IPv6 naslove**

### Hex tabela

| Decimalno | Hex | Binarno |
|-----------|-----|---------|
| 0 | 0 | 0000 |
| 1 | 1 | 0001 |
| 2 | 2 | 0010 |
| 3 | 3 | 0011 |
| 4 | 4 | 0100 |
| 5 | 5 | 0101 |
| 6 | 6 | 0110 |
| 7 | 7 | 0111 |
| 8 | 8 | 1000 |
| 9 | 9 | 1001 |
| 10 | A | 1010 |
| 11 | B | 1011 |
| 12 | C | 1100 |
| 13 | D | 1101 |
| 14 | E | 1110 |
| 15 | F | 1111 |

> [!tip] En hex znak = 4 biti (nibble). Dva hex znaka = 1 bajt (oktet).

---

## 5.5 Pretvorba: Decimalno ↔ Hex

### Decimalno → Hex

Deli z 16, zapiši ostanke od spodaj navzgor.

> [!example] Primer: 255 → hex
> ```
> 255 ÷ 16 = 15, ostanek 15 → F
>  15 ÷ 16 = 0,  ostanek 15 → F
> Beri od spodaj: FF
> 255 = 0xFF
> ```

> [!example] Primer: 192 → hex
> ```
> 192 ÷ 16 = 12, ostanek 0 → 0
>  12 ÷ 16 = 0,  ostanek 12 → C
> Beri od spodaj: C0
> 192 = 0xC0
> ```

### Hex → Decimalno

Vsako hex cifro pomnoži z ustrezno potenco 16.

> [!example] Primer: 0xC9 → decimalno
> ```
> C = 12 → 12 × 16¹ = 192
> 9 = 9  →  9 × 16⁰ = 9
> Skupaj: 192 + 9 = 201
> ```

---

## 5.6 Binarno ↔ Hex (direktna pretvorba)

Ker je 16 = 2⁴, vsak **hex znak točno ustreza 4 bitom**!

> [!example] Primer: 10101100 → hex
> ```
> 1010 = A
> 1100 = C
> Rezultat: AC
> ```

> [!example] Primer: 0x2B → binarno
> ```
> 2 = 0010
> B = 1011
> Rezultat: 00101011
> ```

---

## 5.7 IPv4 in IPv6 – povezava z številskimi sistemi

| | IPv4 | IPv6 |
|-|------|------|
| Dolžina | 32 bitov | 128 bitov |
| Zapis | Decimalno (4 okteti) | Heksadecimalno (8 skupin po 16 bitov) |
| Primer | 192.168.1.1 | 2001:0DB8:ACAD:0001::1 |
| Ločilo | `.` | `:` |

> [!info] IPv6 zapis
> - 8 skupin × 4 hex znaki = 32 hex znakov = 128 bitov
> - Vodilne ničle v skupini se lahko izpustijo: `0001` → `1`
> - Ena skupina zaporednih ničelnih skupin se zamenja z `::` (samo enkrat!)

---

## 🔗 Povezave

- [[Modul 4 - Physical Layer]]
- [[Modul 6 - Data Link Layer]]

---

## ❓ Check Your Understanding

> [!question] Vprašanje 1
> Koliko bitov ima en IPv4 oktet?
> > [!done]- Odgovor
> > **8 bitov**. IPv4 naslov ima 4 oktete = 32 bitov skupaj.

> [!question] Vprašanje 2
> Pretvori 255 v binarno.
> > [!done]- Odgovor
> > **11111111** (vsi biti so 1 → 128+64+32+16+8+4+2+1 = 255)

> [!question] Vprašanje 3
> Koliko desetiških vrednost predstavlja en hex znak?
> > [!done]- Odgovor
> > En hex znak = 4 biti (nibble) → vrednosti 0–15.

> [!question] Vprašanje 4
> Pretvori 0xFF v decimalno.
> > [!done]- Odgovor
> > F=15 → 15×16 + 15×1 = 240+15 = **255**

> [!question] Vprašanje 5
> Kateri zapis se uporablja za IPv6 naslove?
> > [!done]- Odgovor
> > **Heksadecimalni**, 8 skupin po 4 hex znake, ločene z `:`.