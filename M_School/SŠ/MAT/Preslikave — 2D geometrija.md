

- Preslikava je funkcija, ki vsaki točki ravnine priredi natanko eno točko ravnine
- Označimo: $f: T \mapsto T'$, kjer je $T$ **originalna točka** in $T'$ **slika**

## Vrste preslikav

| Preslikava | Ohranja razdalje | Ohranja kote | Ohranja orientacijo |
|---|---|---|---|
| Zrcaljenje | ✓ | ✓ | ✗ |
| Rotacija | ✓ | ✓ | ✓ |
| Translacija | ✓ | ✓ | ✓ |
| Homotetija | ✗ | ✓ | ✓ / ✗ |

- **Izometrija**: preslikava, ki ohranja razdalje (zrcaljenje, rotacija, translacija)
- **Podobnostna preslikava**: ohranja kote, razdalje le sorazmerno (homotetija)

---

## 1. Zrcaljenje (simetrija)

### Čez koordinatni osi in premici $y=x$

| Premica | $T(x,y) \to T'$ |
|---|---|
| $x$-os | $(x,\ -y)$ |
| $y$-os | $(-x,\ y)$ |
| $y=x$ | $(y,\ x)$ |
| $y=-x$ | $(-y,\ -x)$ |

### Čez navpično premico $x=a$
$$T'(2a-x,\ y)$$

### Čez vodoravno premico $y=b$
$$T'(x,\ 2b-y)$$

### Čez splošno premico $y=kx+n$ oz. $ax+by+c=0$
$$x'=x-\frac{2a(ax+by+c)}{a^2+b^2}$$
$$y'=y-\frac{2b(ax+by+c)}{a^2+b^2}$$

### Zrcaljenje čez točko $S(s_1, s_2)$ — centralna simetrija
$$T'(2s_1-x,\ 2s_2-y)$$
- Sredina $TT'$ je točka $S$

> [!tip] Preizkus zrcaljenja
> 1. Razdalja $|TS| = |T'S|$ (pri zrcaljenju čez točko)
> 2. Razdalja $T$ do premice $=$ razdalja $T'$ do premice
> 3. Premica $TT'$ je pravokotna na os zrcaljenja

---

## 2. Rotacija (zasuk)

### Rotacija okoli izhodišča za kot $\varphi$
$$x' = x\cos\varphi - y\sin\varphi$$
$$y' = x\sin\varphi + y\cos\varphi$$

### Pogosti koti

| $\varphi$ | $T(x,y) \to T'$ |
|---|---|
| $90°$ | $(-y,\ x)$ |
| $180°$ | $(-x,\ -y)$ |
| $270°$ | $(y,\ -x)$ |
| $-90°$ | $(y,\ -x)$ |

### Rotacija okoli točke $S(a,b)$ za kot $\varphi$
$$\text{1. Premakni koordinatni sistem: } x_0=x-a,\ y_0=y-b$$
$$\text{2. Zavrti: } x_0'=x_0\cos\varphi-y_0\sin\varphi,\ y_0'=x_0\sin\varphi+y_0\cos\varphi$$
$$\text{3. Vrni nazaj: } x'=x_0'+a,\ y'=y_0'+b$$

> [!tip] Primer: zasukaj $T(3,1)$ za $90°$ okoli $S(1,1)$
> $x_0=3-1=2,\ y_0=1-1=0$
> $x_0'=-0=-0,\ y_0'=2$
> $T'=(0+1,\ 2+1)=(1,\ 3)$

---

## 3. Translacija (premik)

### Za vektor $\vec{v}=(a,b)$
$$T'(x+a,\ y+b)$$
- Translacija ohranja velikost, obliko in orientacijo lika
- Vsaka točka se premakne za enak vektor

---

## 4. Homotetija (razteg)

### Homotetija s centrom $O(0,0)$ in koeficientom $k$
$$T'(kx,\ ky)$$

### Homotetija s centrom $S(a,b)$ in koeficientom $k$
$$x'=a+k(x-a)$$
$$y'=b+k(y-b)$$

- $k>0$: slika je na isti strani centra kot original
- $k<0$: slika je na nasprotni strani centra
- $|k|>1$: povečava; $|k|<1$: pomanjšava; $k=-1$: centralna simetrija

> [!tip] Razmerja pri homotetiji
> $$\frac{|T'S|}{|TS|}=|k|$$
> Ploščine se povečajo za faktor $k^2$, prostornine za $k^3$.

---

## 5. Kompozitum preslikav

- Zaporedna uporaba dveh preslikav: najprej $f$, potem $g$
$$T \xrightarrow{f} T'' \xrightarrow{g} T'$$

> [!note] Pomembno
> Kompozitum **ni komutativen** — vrstni red je pomemben!

### Dve zrcaljenji čez vzporedni premici = translacija
- Razdalja premikov $= 2 \times$ razdalja med premicama

### Dve zrcaljenji čez sekajoči premici = rotacija
- Kot zasuka $= 2 \times$ kot med premicama

---

## Invariantne točke
- Točka $T$ je **invariantna (negibna)**, če velja $T'=T$
- Pri zrcaljenju čez premico: vse točke na premici so invariantne
- Pri rotaciji za $\varphi \neq 0°$: samo center rotacije
- Pri translaciji za $\vec{v}\neq\vec{0}$: nobena točka ni invariantna

> [!note] Za maturo — tipične naloge
> - Določi sliko točke/lika pri dani preslikavi
> - Najdi os zrcaljenja iz para $T, T'$
> - Kompozitum dveh preslikav
> - Določi invariantne točke
> - Homotetija — razmerja ploščin in prostornin
