- Metoda dokazovanja trditev, ki veljajo za vsa naravna števila $n\geq n_0$

## Postopek

### Korak 1 — Osnova indukcije
Dokaži, da trditev velja za $n=n_0$ (ponavadi $n_0=1$).

### Korak 2 — Indukcijska hipoteza
Predpostavi, da trditev velja za nek $n=k$:
$$\text{Predpostavimo: }P(k)\text{ velja.}$$

### Korak 3 — Indukcijski korak
Dokaži, da iz $P(k)$ sledi $P(k+1)$:
$$P(k) \Rightarrow P(k+1)$$

> [!tip] Logika
> Indukcija je kot neskončna vrsta domin — če podremo prvo (osnova) in vsaka podre naslednjo (korak), padejo vse.

## Primer — vsota prvih $n$ naravnih števil
$$\text{Trditev: } S_n=1+2+\ldots+n=\frac{n(n+1)}{2}$$

**Osnova** ($n=1$):
$$S_1=1=\frac{1\cdot 2}{2}=1 \checkmark$$

**Hipoteza**: Predpostavimo $S_k=\dfrac{k(k+1)}{2}$.

**Korak** ($n=k+1$):
$$\begin{aligned}
S_{k+1}&=S_k+(k+1)=\frac{k(k+1)}{2}+(k+1)\\
&=(k+1)\left(\frac{k}{2}+1\right)=(k+1)\cdot\frac{k+2}{2}\\
&=\frac{(k+1)(k+2)}{2} \checkmark
\end{aligned}$$

## Primer — deljivost
$$\text{Trditev: } 3\mid (4^n-1) \text{ za vse } n\geq 1$$

**Osnova** ($n=1$): $4^1-1=3$, $3\mid 3$ ✓

**Hipoteza**: $3\mid(4^k-1)$, torej $4^k-1=3m$ za nek $m\in\mathbb{Z}$.

**Korak**:
$$\begin{aligned}
4^{k+1}-1&=4\cdot 4^k-1=4(3m+1)-1\\
&=12m+4-1=12m+3=3(4m+1)
\end{aligned}$$
$$\Rightarrow 3\mid(4^{k+1}-1) \checkmark$$

> [!note] Za maturo — tipične naloge
> - Dokaz formule za vsoto zaporedja
> - Dokaz deljivosti
> - Dokaz neenačbe z indukcijo
