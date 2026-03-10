
|            | SIMENS    | ARDUINO     |
| ---------- | --------- | ----------- |
| PRETVORNIK | 10 bit-n  | 10bit-n     |
| DOSEG      | 0V -> 10V | 0V -> 5V    |
| NAPAJANJE  | 24V DC    | 7V ->12V DC |

## REZULTATI AD PRETVORNIKA V OUTPUT BYTE-IH

### ARDUINO — DESNO PORAVNANO (~5mV)

- **Rezultat je poravnan desno:** Najmanj pomembni biti (LSB) so vedno na desni strani, višji biti pa (če je širina registra večja od ločljivosti ADC) so nastavljeni na ničle.
    
- **Primer (10 bitov v 16-bit register):**
    
    - ADH (high byte) vsebuje dva najvišja bita, ADL (low byte) preostalih 8 bitov.
        
    - Primer vrednosti 940: `00000011 10101100` (ADH vsebuje 2 najvišja bita, ADL ostalih 8).
        
- **Uporaba:** Poenostavi uporabnost rezultata — neposredno združevanje (>>8 in |) brez dodatnega zamikanja.
    
- **Najpogostejša izbira v mikrokontrolerjih** zaradi enostavnosti in robustnosti.
    

#### ADH (High — Arduino, desna poravnava)

|0|0|0|0|0|0|X|X|
|---|---|---|---|---|---|---|---|

- ADH vsebuje **2 najvišja bita** rezultata (od skupaj 10).

```vega-lite
{
  "width": 600,
  "height": 320,
  "data": {
    "values": [
      {"x": 0, "adh": 0},
      {"x": 1.25, "adh": 1},
      {"x": 2.5, "adh": 2},
      {"x": 3.75, "adh": 3}
    ]
  },
  "mark": {"type": "bar", "color": "#4f81bd"},
  "encoding": {
    "x": {"field": "x", "type": "ordinal", "title": "Napetost (V)"},
    "y": {"field": "adh", "type": "quantitative", "title": "ADH (2 bita)"}
  }
}

```


Ko se **napetost preminja od 0V -> 5V** vhoda se pa na ADH-ju spreminja **vrednost od** **0 -> 255**.

#### ADL (Low — Arduino, desna poravnava)

|  X  |  X  |  X  |  X  |  X  |  X  |  X  |  X  |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |

- ADL vsebuje vseh 8 nizkih bitov iz 10-bitnega rezultata.
```vega-lite
{
  "width":600,
  "data": {
    "values": [
      {"analog": 0.00, "adl": 0},
      {"analog": 0.25, "adl": 51},
      {"analog": 0.5, "adl": 102},
      {"analog": 0.75, "adl": 153},
      {"analog": 1.0, "adl": 204},
      {"analog": 1.249999, "adl": 255},
      {"analog": 1.25, "adl": 0},
      {"analog": 1.5, "adl": 51},
      {"analog": 1.75, "adl": 102},
      {"analog": 2.0, "adl": 153},
      {"analog": 2.25, "adl": 204},
      {"analog": 2.49999, "adl": 255},
      {"analog": 2.5, "adl": 0},
      {"analog": 2.75, "adl": 51},
      {"analog": 3.0, "adl": 102},
      {"analog": 3.25, "adl": 153},
      {"analog": 3.5, "adl": 204},
      {"analog": 3.749999, "adl": 255},
      {"analog": 3.75, "adl": 0},
      {"analog": 4.0, "adl": 51},
      {"analog": 4.25, "adl": 102},
      {"analog": 4.5, "adl": 153},
      {"analog": 4.75, "adl": 204},
      {"analog": 4.9999, "adl": 255},
      {"analog": 5.0, "adl": 0}
    ]
  },
  "layer": [
    {
      "mark": {"type": "line", "interpolate": "linear", "point": true, "color": "#e76f8a"},
      "encoding": {
        "x": {"field": "analog", "type": "quantitative", "title": "Analog Input (V)"},
        "y": {"field": "adl", "type": "quantitative", "title": "ADL (Desno poravnano)"}
      }
    },
    {
      "data": {
        "values": [
          {"x": 1.25}, {"x": 2.5}, {"x": 3.75}, {"x": 5.0}
        ]
      },
      "mark": {"type": "rule", "color": "#e76f8a", "size": 2},
      "encoding": {
        "x": {"field": "x", "type": "quantitative"}
      }
    }
  ]
}

```

- **ADL** se spreminja od 0 → 255 z napetostjo 0V → 5V, resetira pri vsakem koraku.

### SIEMENS — LEVO PORAVNANO

- **Rezultat je poravnan levo:** Najbolj pomembni biti (MSB) so na levi strani registra, preostali (LSB) so ničle ali prazni.
    
- **Primer (10 bitov v 16):**
    
    - ADH vsebuje 8 najvišjih bitov, ADL le spodnja dva.
        
    - Primer vrednosti 940: `11101001 10000000` (vrednost zamaknjena levo).
        
- **Uporaba:** Uporabno za hiter ogled najpomembnejših bitov (npr. za grobo primerjavo ali izpis).
    
- **Zahteva dodatno premikanje ali maskiranje** za pridobitev polne 10-bitne vrednosti.
    

#### ADH (High — Siemens, leva poravnava)

|  X  |  X  |  X  |  X  |  X  |  X  |  X  |  X  |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |

- ADH vsebuje **8 najvišjih bitov** rezultata.
```vega-lite
{
  "width": 600,
  "height": 320,
  "data": {
    "values": [
      {"x": 0, "adh": 0},
      {"x": 5, "adh": 255}
    ]
  },
  "mark": {"type": "line", "point": true, "color": "#4f81bd"},
  "encoding": {
    "x": {"field": "x", "type": "quantitative", "title": "Napetost (V)"},
    "y": {"field": "adh", "type": "quantitative", "title": "ADH (Leva poravnava)"}
  }
}

```


- Od 0V do 5V se vrednost na ADH spreminja od 0 do 255 (za prikaz, dejansko je le 8 bitov pomembnih).

#### ADL (Low — Siemens, leva poravnava)

|X|X|0|0|0|0|0|0|
|---|---|---|---|---|---|---|---|

- ADL vsebuje samo **dva najvišja bita**, ostalo ničle.
```vega-lite
{
  "width": 600,
  "height": 320,
  "data": {
    "values": [
      {"x": 0, "adl": 0},
      {"x": 10, "adl": 64},
      {"x": 20, "adl": 128},
      {"x": 30, "adl": 192},
      {"x": 40, "adl": 0},
      {"x": 50, "adl": 64},
      {"x": 60, "adl": 128},
      {"x": 70, "adl": 192}
    ]
  },
  "mark": {"type": "bar", "color": "#e76f8a"},
  "encoding": {
    "x": {"field": "x", "type": "ordinal", "title": "Napetost (mV)"},
    "y": {"field": "adl", "type": "quantitative", "title": "ADL (2 bita)"}
  }
}

```




- Pri levi poravnavi se vrednost ADL ponavlja od 0 → 192 (ker imata LSB le 2 bita).

### Kapaciteta
Farat -> Amper sekunda nad volt 
$$
F=\frac{\mathrm{A} \cdot \mathrm{s}}{\mathrm{V}}
$$
Kapaciteta Q
$$
Q=C\cdot U 
$$
Ali
$$
Q=I\cdot t
$$
Torej iz tega dobimo:
$$
C\cdot U = I \cdot t
$$
$$U=\frac I C \cdot t$$
Dobimo konstanto k:
$$k=\frac I C$$
$$\frac{1 \cdot 10^{-3} \cdot A \cdot V}{1 \cdot 10^{-6} \cdot A \cdot s} = 1k\frac V s$$
S tem da je Tok: $$I=1mA$$
In
Kapacitetivnost $$C=1\mu F$$
Poznamo tudi upornost C:$$X_{c}=\frac 1{j \cdot \omega \cdot C}$$
$$-\frac j {\omega \cdot C}$$
Ali neskončna upornost.
