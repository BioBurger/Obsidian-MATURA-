- Odvod funkcije $f$ v točki $a$ je trenutna hitrost spremembe — naklon tangente na graf v tej točki.

## Definicija
$$f'(a)=\lim_{h\to 0}\frac{f(a+h)-f(a)}{h}$$
- Če ta limita obstaja, je $f$ **odvedljiva** v točki $a$
- Odvedljivost $\Rightarrow$ zveznost (obratno ne velja)

## Oznake
$$f'(x)=\frac{df}{dx}=\frac{d}{dx}f(x)=\dot{f}(x)$$

## Tabela osnovnih odvodov

| Funkcija | Odvod |
|---|---|
| $c$ (konstanta) | $0$ |
| $x^n$ | $nx^{n-1}$ |
| $\sqrt{x}$ | $\dfrac{1}{2\sqrt{x}}$ |
| $e^x$ | $e^x$ |
| $a^x$ | $a^x \ln a$ |
| $\ln x$ | $\dfrac{1}{x}$ |
| $\log_a x$ | $\dfrac{1}{x \ln a}$ |
| $\sin x$ | $\cos x$ |
| $\cos x$ | $-\sin x$ |
| $\tan x$ | $\dfrac{1}{\cos^2 x}$ |
| $\cot x$ | $-\dfrac{1}{\sin^2 x}$ |
| $\arcsin x$ | $\dfrac{1}{\sqrt{1-x^2}}$ |
| $\arccos x$ | $-\dfrac{1}{\sqrt{1-x^2}}$ |
| $\arctan x$ | $\dfrac{1}{1+x^2}$ |

## Pravila odvajanja

### Vsota / razlika
$$(f \pm g)'= f' \pm g'$$

### Produkt
$$(f \cdot g)'= f'g + fg'$$

### Količnik
$$\left(\frac{f}{g}\right)'=\frac{f'g - fg'}{g^2}, \quad g\neq 0$$

### Kompozitum — verižno pravilo
$$(f(g(x)))'=f'(g(x))\cdot g'(x)$$
$$\begin{aligned}
&\quad \text{Primer: } (\sin(x^2))'=\cos(x^2)\cdot 2x
\end{aligned}$$

### Potenca kompozituma
$$\bigl(f(x)^n\bigr)'=n\cdot f(x)^{n-1}\cdot f'(x)$$

## Enačba tangente in normale

### Tangenta na $f$ v točki $x_0$
$$y = f'(x_0)(x-x_0)+f(x_0)$$

### Normala (pravokotnica na tangento)
$$y = -\frac{1}{f'(x_0)}(x-x_0)+f(x_0), \quad f'(x_0)\neq 0$$

> [!tip] Primer
> $f(x)=x^2$, tangenta v $x_0=2$:
> $f'(x)=2x \Rightarrow f'(2)=4$
> $y=4(x-2)+4=4x-4$

## Drugi odvod
$$f''(x)=(f'(x))'$$
- $f''(x)>0$: funkcija je **konveksna** (konkavna navzgor ∪)
- $f''(x)<0$: funkcija je **konkavna** (konkavna navzdol ∩)

### Prevoj
- Točka $x_0$ je **prevoj**, če se v njej konveksnost zamenja:
$$f''(x_0)=0 \quad \text{in } f'' \text{ zamenja predznak v } x_0$$

## Analiza funkcije z odvodom

### Naraščanje in padanje
- $f'(x)>0$ na intervalu $\Rightarrow f$ **narašča**
- $f'(x)<0$ na intervalu $\Rightarrow f$ **pada**
- $f'(x)=0$ v točki $\Rightarrow$ kandidat za **lokalni ekstrem**

### Lokalni ekstremi
$$f'(x_0)=0 \text{ in:}$$
- $f'$ gre iz $+$ v $-$ $\Rightarrow$ **lokalni maksimum**
- $f'$ gre iz $-$ v $+$ $\Rightarrow$ **lokalni minimum**
- z drugim odvodom:
  - $f''(x_0)<0 \Rightarrow$ **lokalni maksimum**
  - $f''(x_0)>0 \Rightarrow$ **lokalni minimum**

### Postopek analize funkcije
1. Domena $D_f$
2. Ničle ($f(x)=0$) in začetna vrednost ($f(0)$)
3. Asimptote (navpična, vodoravna, poševna)
4. $f'(x)=0$ — kandidati za ekstreme, naraščanje/padanje
5. $f''(x)=0$ — kandidati za prevoje, konveksnost/konkavnost
6. Skica grafa

## Ekstremi na zaprtem intervalu $[a,b]$
- Izračunaj $f'(x)=0$ na $(a,b)$ — to so **stacionarne točke**
- Primerjaj vrednosti $f$ v stacionarnih točkah in na robovih $f(a), f(b)$
- **Globalni maksimum/minimum** je največja/najmanjša vrednost med vsemi

> [!note] Za maturo — tipične naloge
> - Enačba tangente v točki
> - Iskanje ekstremov in prevojnih točk
> - Ekstremalni problemi (npr. največja/najmanjša ploščina/prostornina)
> - Analiza poteka funkcije
