# Bem vindos ao curso de programação da Mosaico

Nesta seção, vocês encontrarão os pseudocódigos utilizados durantes as aulas.


***

# Pseudocódigos

* slide 31
```
ALGORITMO Exemplo
	//Procedimentos e funções
	//Declaração das variáveis
	var x: array [0..2] of real;
	var Y: real;
INICIO
	ESCREVA “Digite um numero [0]”;
	LEIA x[0];
	ESCREVA “Digite um numero [1]”;
	LEIA x[1];
	ESCREVA “Digite um numero [2]” ;
	LEIA x[2] ;
	Y = x[0]+x[1]+x[2] ;
	Y = Y/3;
	ESCREVA Y;
FIM!
```

* slide 32
```
ALGORITMO CalculaMedia
	//Procedimentos e funções
	//Declaração das variáveis
	var numeros: array [0..2] of real;
	var media, somatorio: real;
INICIO
	ESCREVA “Digite um numero [0] \n”;
	LEIA numeros[0];
	ESCREVA “Digite um numero [1] \n”;
	LEIA numeros[1];
	ESCREVA “Digite um numero [2] \n”;
	LEIA numeros[2];
	somatorio = numeros[0]+ numeros[1]+ numeros[2];
	media = somatorio/3;
	ESCREVA media;
FIM!
```


