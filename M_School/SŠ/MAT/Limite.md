## **Definicaija**
$$\begin{flalign*}
& \text{Zapis: } \lim_{x \to a} f(x) = L \text{ Pomeni: ko se } x \text{ približuje } a,
  \text{ se } f(x) \text{ približuje } L &
\\
& \text{(ni nujno, da je } f(a) \text{ sploh definiran).} &
\\
\\
&\text{Leva/desna limta: }\lim_{x\to a^{-}}f(x)\text{ in }lim_{x\to a^{+}}f(x);\text{ limita obstaja natanko,ko sta enaki.} &
\end{flalign*}
$$

### **1. Vrste limit**
$$\begin{flalign*}
& \text{Limita v točki }a:{ }\lim_{x \to a}f(x). &
\\
&\text{Limita v neskončnosti: }\lim_{x \to \infty}f(x)\text{ ali }\lim_{x \to -\infty}f(x).&
\\
&\text{Neskončna limita: }\lim_{x \to a}f(x)=\pm\infty\text{ (tipično pri poljih racionalnih funkcij).}&
\end{flalign*}$$
### **2. Pravila za računanje**
$$\begin{flalign*}
& \text{Če } \lim_{x \to a} f(x)=L \text{ in } \lim_{x\to a} g(x)=M \text{ potem:} &\\
& \text{1. Vsota/razlika: } \lim (f \pm g)=L \pm M &\\
& \text{2. Produkt: } \lim (fg)=LM &\\
& \text{3. Količnik: } \lim \left(\frac{f}{g}\right)=\frac{L}{M},\ \text{če } M\neq 0 &\\
& \text{4. Potence/koren: } \lim_{x\to a}\bigl(f(x)\bigr)^{n}=L^{n} &\\
& (\text{če je smiselno v realnih številih}) &\\
& \text{5. Če je funkcija zvezna v } a,\ \text{potem } \lim_{x\to a} f(x)=f(a) &\\
& (\text{npr. polinomi povsod; racionalne tam, kjer imenovalec ni } 0). &
\end{flalign*}
$$
## **Reševanje**
$$\begin{flalign*} & \text{1. Korak: poskusimo neposredno vstaviti } x=a. &\\ & \text{Če dobimo končno število, je to vrednost limite.} &\\[4pt] & \text{2. Korak: če dobimo nedoločeno obliko (npr. } 0/0,\ \infty/\infty\text{),} &\\ & \text{moramo izraz preoblikovati (krajšanje, racionalizacija, deljenje z najvišjo potenco).} &\\[4pt] & \text{3. Korak: po poenostavitvi ponovno vstavimo } x=a \text{ in izračunamo limito.} & \end{flalign*}$$
## **Nedoločene oblike**
$$\begin{flalign*} & \text{Tipične nedoločene oblike pri limitah:} &\\ & \frac{0}{0},\quad \frac{\infty}{\infty},\quad 0\cdot\infty,\quad \infty-\infty, 0^{0},\quad 1^{\infty},\quad \infty^{0}. & \end{flalign*}$$
## **Tehnike**
### **1. Faktorizacija in krajšenje**
$$\begin{flalign*} & \text{Uporabimo, ko dobimo } \frac{0}{0} \text{ pri polinomih.} &\\ & \text{Postopek: razstavi števec in imenovalec na faktorje,} &\\ & \text{krajšaj skupni faktor in šele nato vstavimo } x=a. & \end{flalign*}$$
$$\begin{flalign*} & \text{Primer: } \lim_{x\to 2}\frac{x^{2}-4}{x-2}. &\\ & x^{2}-4=(x-2)(x+2) &\\ & \Rightarrow \lim_{x\to 2}\frac{(x-2)(x+2)}{x-2} = \lim_{x\to 2}(x+2) = 4. & \end{flalign*}$$

### **2. Racionalizacija**
$$\begin{flalign*} & \text{Uporabimo, ko imamo korene v števcu ali imenovalcu.} &\\ & \text{Postopek: izraz pomnožimo s konjugiranim izrazom} &\\ & \text{(npr. } \sqrt{1+x}-1 \Rightarrow \sqrt{1+x}+1\text{) in poenostavimo.} & \end{flalign*}$$$$\begin{flalign*} & \text{Primer: } \lim_{x\to 0}\frac{\sqrt{1+x}-1}{x}. &\\ & \text{Pomnožimo s konjugiranim: } \frac{\sqrt{1+x}-1}{x}\cdot\frac{\sqrt{1+x}+1}{\sqrt{1+x}+1} &\\ & = \frac{(1+x)-1}{x(\sqrt{1+x}+1)} = \frac{x}{x(\sqrt{1+x}+1)} = \frac{1}{\sqrt{1+x}+1}. &\\ & \Rightarrow \lim_{x\to 0}\frac{\sqrt{1+x}-1}{x} = \frac{1}{\sqrt{1+0}+1} = \frac12. & \end{flalign*}$$
### **3. Limite v neskončnosti**
$$\begin{flalign*} & \text{Pri } \lim_{x\to\infty} \frac{P_n(x)}{Q_m(x)} \text{ delimo števec in imenovalec} &\\ & \text{z najvišjo potenco } x. &\\[4pt] & \text{Če je stopnja števca manjša od stopnje imenovalca } (n<m),\ \text{je limita } 0. &\\ & \text{Če je } n=m,\ \text{je limita razmerje vodilnih koeficientov.} &\\ & \text{Če je } n>m,\ \text{je limita } \pm\infty \text{ (odvisno od predznaka).} & \end{flalign*}$$$$\begin{flalign*} & \text{Primer: } \lim_{x\to\infty}\frac{3x^{2}+2x-1}{5x^{2}-7}. &\\ & \text{Delimo števec in imenovalec z } x^{2}: &\\ & \lim_{x\to\infty}\frac{3+\frac{2}{x}-\frac{1}{x^{2}}}{5-\frac{7}{x^{2}}} = \frac{3}{5}. & \end{flalign*}$$

##  **Posebne limite**
### **1. Trigonometrična limita**
$$\begin{flalign*} & \text{Osnovna limita: } \lim_{x\to 0}\frac{\sin x}{x}=1. &\\ & \text{Posledica: } \lim_{x\to 0}\frac{\sin(kx)}{kx}=1 \Rightarrow \lim_{x\to 0}\frac{\sin(kx)}{x}=k. & \end{flalign*}$$$$\begin{flalign*} & \text{Osnovna limita: } \lim_{x\to 0}\frac{\sin x}{x}=1. &\\ & \text{Primer: } \lim_{x\to 0}\frac{\sin(4x)}{3x}. &\\ & \frac{\sin(4x)}{3x} = \frac{4}{3}\cdot\frac{\sin(4x)}{4x} &\\ & \Rightarrow \lim_{x\to 0}\frac{\sin(4x)}{3x} = \frac{4}{3}\cdot 1 = \frac{4}{3}. & \end{flalign*}$$

### **2. Eulerjeva limita**
$$\begin{flalign*} & \text{Definicija števila } e:\ \lim_{n\to\infty}\left(1+\frac{1}{n}\right)^{n}=e. &\\ & \text{Splošna oblika: } \lim_{x\to\infty}\left(1+\frac{k}{x}\right)^{x}=e^{k}. & \end{flalign*}$$$$\begin{flalign*} & \text{Osnovna: } \lim_{n\to\infty}\left(1+\frac{1}{n}\right)^{n}=e. &\\ & \text{Splošna: } \lim_{x\to\infty}\left(1+\frac{k}{x}\right)^{x}=e^{k}. &\\ & \text{Primer: } \lim_{x\to\infty}\left(1+\frac{3}{x}\right)^{x}=e^{3}. & \end{flalign*}$$
##  **Zveznost funkcije**
$$\begin{flalign*} & \text{Funkcija } f \text{ je zvezna v točki } a \text{ natanko tedaj, ko velja:} &\\ & \text{1. } f(a) \text{ je definirana.} &\\ & \text{2. } \lim_{x\to a} f(x) \text{ obstaja.} &\\ & \text{3. } \lim_{x\to a} f(x)=f(a). &\\[4pt] & \text{Krajši zapis zveznosti: } \lim_{x\to a} f(x)=f(a). & \end{flalign*}$$
## **Asimptote**
### **1. Navpična asimptota**
$$\begin{flalign*} & \text{Premica } x=a \text{ je navpična asimptota funkcije } f, \text{ če velja:} &\\ & \lim_{x\to a^-} f(x)=\pm\infty \ \text{ali}\ \lim_{x\to a^+} f(x)=\pm\infty. & \end{flalign*}$$
### **2. Vodoravna asimptota**
$$\begin{flalign*} & \text{Premica } y=L \text{ je vodoravna asimptota, če velja:} &\\ & \lim_{x\to \infty} f(x)=L \ \text{ali}\ \lim_{x\to -\infty} f(x)=L. & \end{flalign*}$$
### **3 Poševna asimptota**
$$\begin{flalign*} & \text{Premica } y=kx+n \text{ je poševna asimptota, če velja:} &\\ & k=\lim_{x\to\infty}\frac{f(x)}{x}, \qquad n=\lim_{x\to\infty}\bigl(f(x)-kx\bigr). & \end{flalign*}$$
