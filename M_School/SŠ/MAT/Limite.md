## Definicija
$$\begin{flalign*}
& \text{Zapis: } \lim_{x \to a} f(x) = L \text{ Pomeni: ko se } x \text{ približuje } a,
  \text{ se } f(x) \text{ približuje } L &
\\
& \text{(ni nujno, da je } f(a) \text{ sploh definiran).} &
\\
\\
&\text{Leva/desna limita: }\lim_{x\to a^{-}}f(x)\text{ in }\lim_{x\to a^{+}}f(x);\text{ limita obstaja natanko, ko sta enaki.} &
\end{flalign*}$$

### 1. Vrste limit
$$\begin{flalign*}
& \text{Limita v točki }a:{ }\lim_{x \to a}f(x). &
\\
&\text{Limita v neskončnosti: }\lim_{x \to \infty}f(x)\text{ ali }\lim_{x \to -\infty}f(x).&
\\
&\text{Neskončna limita: }\lim_{x \to a}f(x)=\pm\infty\text{ (tipično pri racionalnih funkcijah).}&
\end{flalign*}$$

### 2. Pravila za računanje
$$\begin{flalign*}
& \text{Če } \lim_{x \to a} f(x)=L \text{ in } \lim_{x\to a} g(x)=M \text{ potem:} &\\
& \text{1. Vsota/razlika: } \lim (f \pm g)=L \pm M &\\
& \text{2. Produkt: } \lim (fg)=LM &\\
& \text{3. Količnik: } \lim \left(\frac{f}{g}\right)=\frac{L}{M},\ \text{če } M\neq 0 &\\
& \text{4. Potence/koren: } \lim_{x\to a}\bigl(f(x)\bigr)^{n}=L^{n} &\\
& \text{5. Zvezna funkcija v } a: \lim_{x\to a} f(x)=f(a) &
\end{flalign*}$$

## Reševanje
$$\begin{flalign*}
& \text{1. Korak: poskusimo neposredno vstaviti } x=a. &\\
& \text{Če dobimo končno število, je to vrednost limite.} &\\[4pt]
& \text{2. Korak: če dobimo nedoločeno obliko (npr. } 0/0,\ \infty/\infty\text{),} &\\
& \text{moramo izraz preoblikovati (krajšanje, racionalizacija, deljenje z najvišjo potenco).} &\\[4pt]
& \text{3. Korak: po poenostavitvi ponovno vstavimo } x=a \text{ in izračunamo limito.} &
\end{flalign*}$$

## Nedoločene oblike
$$\frac{0}{0},\quad \frac{\infty}{\infty},\quad 0\cdot\infty,\quad \infty-\infty,\quad 0^{0},\quad 1^{\infty},\quad \infty^{0}$$

## Tehnike

### 1. Faktorizacija in krajšenje
$$\begin{flalign*}
& \text{Uporabimo, ko dobimo } \frac{0}{0} \text{ pri polinomih.} &\\
& \text{Primer: } \lim_{x\to 2}\frac{x^{2}-4}{x-2}. &\\
& x^{2}-4=(x-2)(x+2) &\\
& \Rightarrow \lim_{x\to 2}\frac{(x-2)(x+2)}{x-2} = \lim_{x\to 2}(x+2) = 4. &
\end{flalign*}$$

### 2. Racionalizacija
$$\begin{flalign*}
& \text{Uporabimo, ko imamo korene v števcu ali imenovalcu.} &\\
& \text{Primer: } \lim_{x\to 0}\frac{\sqrt{1+x}-1}{x}. &\\
& \frac{\sqrt{1+x}-1}{x}\cdot\frac{\sqrt{1+x}+1}{\sqrt{1+x}+1} = \frac{x}{x(\sqrt{1+x}+1)} = \frac{1}{\sqrt{1+x}+1}. &\\
& \Rightarrow \lim_{x\to 0}\frac{\sqrt{1+x}-1}{x} = \frac{1}{2}. &
\end{flalign*}$$

### 3. Limite v neskončnosti
$$\begin{flalign*}
& \text{Pri } \lim_{x\to\infty} \frac{P_n(x)}{Q_m(x)} \text{ delimo z najvišjo potenco } x. &\\[4pt]
& n<m \Rightarrow \text{limita } = 0. &\\
& n=m \Rightarrow \text{limita = razmerje vodilnih koeficientov.} &\\
& n>m \Rightarrow \text{limita } = \pm\infty. &\\[4pt]
& \text{Primer: } \lim_{x\to\infty}\frac{3x^{2}+2x-1}{5x^{2}-7} = \frac{3}{5}. &
\end{flalign*}$$

## Posebne limite

### 1. Trigonometrična limita
$$\begin{flalign*}
& \lim_{x\to 0}\frac{\sin x}{x}=1. &\\
& \lim_{x\to 0}\frac{\sin(kx)}{x}=k. &\\
& \text{Primer: } \lim_{x\to 0}\frac{\sin(4x)}{3x} = \frac{4}{3}. &
\end{flalign*}$$

### 2. Eulerjeva limita
$$\begin{flalign*}
& \lim_{n\to\infty}\left(1+\frac{1}{n}\right)^{n}=e. &\\
& \lim_{x\to\infty}\left(1+\frac{k}{x}\right)^{x}=e^{k}. &\\
& \text{Primer: } \lim_{x\to\infty}\left(1+\frac{3}{x}\right)^{x}=e^{3}. &
\end{flalign*}$$

## Zveznost funkcije
$$\begin{flalign*}
& f \text{ je zvezna v točki } a \text{ natanko tedaj, ko:} &\\
& \text{1. } f(a) \text{ je definirana.} &\\
& \text{2. } \lim_{x\to a} f(x) \text{ obstaja.} &\\
& \text{3. } \lim_{x\to a} f(x)=f(a). &
\end{flalign*}$$

## Asimptote

### 1. Navpična asimptota
$$\lim_{x\to a^-} f(x)=\pm\infty \text{ ali } \lim_{x\to a^+} f(x)=\pm\infty$$

### 2. Vodoravna asimptota
$$\lim_{x\to \infty} f(x)=L \text{ ali } \lim_{x\to -\infty} f(x)=L$$

### 3. Poševna asimptota
$$k=\lim_{x\to\infty}\frac{f(x)}{x}, \qquad n=\lim_{x\to\infty}\bigl(f(x)-kx\bigr)$$
$$\text{Premica: } y=kx+n$$
