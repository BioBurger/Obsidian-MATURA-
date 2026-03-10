- Selektori služijo izbiri določenega elementa v HTML datoteki
Primer:
```html
h1{
	color: purple;
}
p{
	font-size: 14pt;
	color: grey;
}
```
## ID
- Za izbiro določenega elementa(unikatnega)
```html
<html>

<head>

  <link rel="stylesheet" href="styles.css">
  
  <style>
  
  #rdece {

    color: red;

  }
  </style>
  
</head>

<body>

  <p id="rdece">To je odstavek.</p>

</body>

</html>
```
## CLASS
- Uporabimo ko bo imelo več elementov take lasnosti
```html
<html>

<head>
	
  <style>
  
  .rdece{
	  color: red;
  }
  
  </style>
  
  <link rel="stylesheet" href="styles.css">

</head>

<body>

     <p class="rdece">To je odstavek.</p>

</body>

</html>
```
- Elementu lahko dodamo več classov
```html
<html>

<head>

  <style>
  
  .rdece {

    color: red;

}

  
.sredina {

    text-align: center;

}

  
.povecano {

    font-size: xx-large;

}
  
  </style>
  
  <link rel="stylesheet" href="styles.css">

</head>

<body>

   <p class="rdece sredina povecano">To je odstavek.</p>

</body>

</html>
```
- Če za selektor damo * izberemo vse elemene v datoteki
- Lahko združimo selektorje
```html
h1,h2,h3{
	color: brown;
}
```

| Selektor        | Primer    | Pomen                                                               |
| --------------- | --------- | ------------------------------------------------------------------- |
| #id             | #naslov   | Izbere element z id="naslov".                                       |
| .class          | .sredina  | Izbere vse elemente s class="sredina".                              |
| element.class   | p.sredina | Izbere samo elemente <p.> s class="sredina".                        |
| *               | *         | Izbere vse elemente.                                                |
| element         | p         | Izbere vse elemente <p.>.                                           |
| element,element | div,p,h1  | Izbere vse elemente <div.>, vse elemente <p.> in vse elemente <h1.> |
## Komentarji
- Komentar označimo s /* in končamo s */