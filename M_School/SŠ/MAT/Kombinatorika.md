$$\begin{aligned}
\text{Odločevanje v več neodvisnih fazah, v vsaki je }k_{i}\text{ možnosti vseh možnosti je }k_{1}*k_{2}*....k_{n}
\end{aligned}$$


## Osnovni izrek kombinatorike:
### Pravilo produkta
- Kadar je povedamo IN (npr. 3 juhe in 2 solati)
$$k_{1}*k_{2}*....k_{n}$$
```mermaid
%%{init: {"themeVariables": {"fontSize": "10px"}} }%%
graph TD  
Start((Start))  
Start --> A1  
Start --> B1
Start --> C1 
A1 --> AB 
A1 --> AC 
B1 --> BA
B1 --> BC 
C1 --> CA 
C1 --> CB
```
$$\text{Izberemo 1 juho in 1 solato : }\rightarrow3*2=6\text{ možnosti}$$

### Pravilo vsote
- Kadar je povedano ALI (npr. 3 juhe ali 2 solati)
$$k_{1}+k_{2}+....k_{n}$$
$$\text{Izberemo 1 juho ali 1 solato : }\rightarrow3juhe+2solati=5$$
