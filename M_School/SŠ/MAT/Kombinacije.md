- n-elementov, izbiramo r elementov (r<n)
$$C_{n}^r=\binom{n}{r}=\frac{V_{n}^r}{r!}=\frac{n!}{r!(n-r!)}
$$
## Binomski simbol
$$\binom{12}{5}=\frac{12*11*10*9*8}{5!}=12C5=792
$$
$$\begin{aligned}
&\quad Lasnosti:\\
&\quad 1. \binom{n}{r}=\binom{n}{n-r}\\
&\quad 2. \binom{n}{1}=n\\
&\quad 3. \binom{n}{0}=\binom{n}{n}=1\\
&\quad 4. \binom{n}{r}+\binom{n}{r+1}=\binom{n+1}{r+1}
\end{aligned}$$
## Pascalov trikotnik/Binomski izrek

$$\begin{aligned}
&\quad (a + b)^n = \binom{n}{0} a^n b^0 + \binom{n}{1} a^{n-1} b^1 + \binom{n}{2} a^{n-2} b^2 + \dots + \binom{n}{n} a^0 b^n
\\
&\quad(a + b)^4 = a^4 + 4 a^3 b + 6 a^2 b^2 + 4 a b^3 + b^4
\\
&\quad\text{Vsak člen ima obliko:}\quad  \binom{n}{k} a^{n-k} b^k
\\
&\quad\text{pri čemer je}\quad \binom{n}{k} = \frac{n!}{k! (n-k)!}
\end{aligned}$$
$$\begin{aligned}
&\quad Primer:
\\
&\quad (cosx+sinx)^{12}
\\
&\quad \text{5 člen tega zaporedja}
\\
&\quad \binom{12}{4}a^8b^4=\frac{12*11*10*9}{4!}*(cosx)^8(sinx)^4=495(cosx)^8(sinx)^4
\\
&\quad Primer2:
\\
&\quad (3x^3+\sqrt{2})^{15}
\\
&\quad\text{Vsebuje: }x^9
\\
&\quad \binom{15}{3}(3x^3)^3(\sqrt{2})^{12}=455*27x^9*64=786240x^9
\end{aligned}$$
