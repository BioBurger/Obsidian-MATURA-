- Opisuje verjetnost **točno $k$ uspehov** v $n$ **neodvisnih** ponovitvah poskusa, kjer ima vsak poskus verjetnost uspeha $p$.

## Formula
$$P(X=k)=\binom{n}{k}p^k(1-p)^{n-k}, \quad k=0,1,\ldots,n$$

- $n$: število ponovitev
- $k$: željeno število uspehov
- $p$: verjetnost uspeha pri enem poskusu
- $1-p=q$: verjetnost neuspeha

## Primer
$$\begin{aligned}
&\text{Kovanec vržemo 6-krat. Kolikšna je verjetnost točno 4 grbov?}\\
&n=6,\ k=4,\ p=\frac{1}{2}\\
&P(X=4)=\binom{6}{4}\left(\frac{1}{2}\right)^4\left(\frac{1}{2}\right)^2=15\cdot\frac{1}{16}\cdot\frac{1}{4}=\frac{15}{64}\approx 0{,}234
\end{aligned}$$

## Pričakovana vrednost in varianca
$$E(X)=np$$
$$D(X)=np(1-p)=npq$$

> [!tip] Kdaj uporabiti?
> Bernoullijeva formula velja, ko:
> 1. Število poskusov $n$ je **fiksno**
> 2. Vsak poskus je **neodvisen**
> 3. Verjetnost uspeha $p$ je pri vsakem poskusu **enaka**

## Verjetnost vsaj $k$ uspehov
$$P(X\geq k)=1-P(X<k)=1-\sum_{i=0}^{k-1}\binom{n}{i}p^i q^{n-i}$$
