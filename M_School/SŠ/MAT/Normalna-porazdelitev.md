- Normalna (Gaussova) porazdelitev je najpomembnejša zvezna porazdelitev — opisuje mnoge naravne pojave.

## Definicija
$$X\sim N(\mu,\sigma^2)$$
- $\mu$: **pričakovana vrednost** (srednja vrednost, sredina zvona)
- $\sigma$: **standardni odklon** (širina zvona)
- $\sigma^2$: **varianca**

## Lastnosti
- Graf je **Gaussova krivulja** (simetrična zvonasta krivulja)
- Simetrična okoli $\mu$: $P(X<\mu)=P(X>\mu)=0{,}5$
- Ploščina pod celotno krivuljo = 1

## Standardna normalna porazdelitev
$$Z\sim N(0,1) \quad (\mu=0,\ \sigma=1)$$

### Standardizacija
$$Z=\frac{X-\mu}{\sigma}$$
- Vsako normalno porazdelitev pretvorimo v standardno z zgornjo formulo.

## Pravilo $\sigma$
$$\begin{aligned}
P(\mu-\sigma < X < \mu+\sigma)&\approx 0{,}683 \quad (68{,}3\%)\\
P(\mu-2\sigma < X < \mu+2\sigma)&\approx 0{,}954 \quad (95{,}4\%)\\
P(\mu-3\sigma < X < \mu+3\sigma)&\approx 0{,}997 \quad (99{,}7\%)
\end{aligned}$$

## Branje tabel $\Phi(z)$
$$\Phi(z)=P(Z\leq z)$$
- Tabela dá $P(Z\leq z)$ za $z\geq 0$
- Za negativne vrednosti: $\Phi(-z)=1-\Phi(z)$
- $P(a<Z<b)=\Phi(b)-\Phi(a)$

## Primer
$$\begin{aligned}
&X\sim N(170, 100),\ \text{tj. }\mu=170,\ \sigma=10\\
&P(160<X<185)=?\\
&Z_1=\frac{160-170}{10}=-1,\quad Z_2=\frac{185-170}{10}=1{,}5\\
&P(-1<Z<1{,}5)=\Phi(1{,}5)-\Phi(-1)\\
&=\Phi(1{,}5)-(1-\Phi(1))=0{,}9332-(1-0{,}8413)=0{,}7745
\end{aligned}$$

> [!note] Za maturo — tipične naloge
> - Standardizacija in branje tabel
> - Izračun verjetnosti $P(a<X<b)$
> - Določi $\mu$ ali $\sigma$ iz dane verjetnosti
