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

* slide 38 - Operação de caracteres - Concatenação

```
ALGORITMO Strings
	//Procedimentos e funções
	//Declaração das variáveis
	var texto1, texto2, texto3: string;
INICIO
	texto1 = “Aprendendo ”;
	texto2 = “Pseudocodigo”;
	texto3 = texto1+texto2;
	ESCREVA texto3; //Irá escrever Aprendendo Pseudocodigo
	texto3 = texto2+texto1;
	ESCREVA texto3; //Irá escrever PseudocodigoAprendendo 
FIM       
```

* slide 39 - Operação de caracteres - Comparação

```
ALGORITMO Strings
	//Procedimentos e funções
	//Declaração das variáveis
	var texto1, texto2, texto3: string;
INICIO
	texto1 = “Aprendendo ”;
	texto2 = “Aprendendo”;
	texto3 = “Pseudocodigo”;
	ESCREVA COMPARE(texto1, texto3); //Irá escrever FALSO
	ESCREVA COMPARE(texto1, texto2); //Irá escrever FALSO
	ESCREVA COMPARE(texto1, texto1); //Irá escrever VERDADEIRO
FIM       
```

* slide 40 - Operação de caracteres - Substituir

```
ALGORITMO Strings
	//Procedimentos e funções
	//Declaração das variáveis
	var texto1, texto2, texto3: string;
INICIO
	texto1 = “Aprendendo ”;
	texto3 = “Pseudocodigo”;
	ESCREVA SUBSTITUIR(texto1, “A”, “a”);
	//Irá escrever aprendendo 
	ESCREVA SUBSTITUIR(texto1, “Y”, “a”);
	//Irá escrever aprendendo
FIM       
```

* slide 41 - Operação de caracteres - Localizar

```
ALGORITMO Strings
	//Procedimentos e funções
	//Declaração das variáveis
	var texto1, texto2, texto3: string;
INICIO
	texto1 = “Aprendendo ”;
	texto3 = “Pseudocodigo”;
	ESCREVA LOCALIZAR(texto1, “e”); 
	//Irá escrever [3,6]
FIM       
```

* slide 47 - Exemplo da criação de um programa

```
ALGORITMO Aminoácido
	var aminoacidos: array [0..2] of String;
	var apolares, polaresNeutros: Integer 
	var polaresAcidos, polaresBasicos: Integer
INICIO
FIM       
```

* slide 47
Crie um programa que receba uma sequência de aminoácidos e imprima a quantidade de aminoácidos apolares, polares neutros, polares ácidos, polares básicos. Neste exemplo usaremos somente 3

```
ALGORITMO Aminoácido
  var am: array [0..2] of String;
  var apolares, polaresNeutros: Integer 
  var polaresAcidos, polaresBasicos: Integer
INICIO
  ESCREVA “Digite um aminoácido (1 de 3)\n”;
  LEIA am[0];
  SE COMPARE(am[0],”G”) OU COMPARE(am[0],”C”) OU COMPARE(am[0],”A”) OU COMPARE(am[0],”L”) OU 
  COMPARE(am[0],”I”) OU COMPARE(am[0],”V”) OU COMPARE(am[0],”M”) OU COMPARE(am[0],”P”) OU
  COMPARE(am[0],”F”) OU COMPARE(am[0],”W”) ENTÃO
    apolares = apolares + 1;
  SENÃO
    SE COMPARE(am[0],”N”) OU COMPARE(am[0],”Q”) OU COMPARE(am[0],”S”) OU COMPARE(am[0],”T”) OU 
    COMPARE(am[0],”Y”) ENTÃO
      polaresNeutros = polaresNeutros + 1;
    SENÃO
      SE COMPARE(am[0],”D”) OU COMPARE(am[0],”E”) ENTÃO
        polaresAcidos = polaresAcidos + 1;
      SENÃO
        SE COMPARE(am[0],”R”) OU COMPARE(am[0],”H”) OU COMPARE(am[0],”K”) ENTÃO
          polaresBasicos = polaresBasicos + 1;
        SENÃO
          ESCREVA “Aminoácido invalido: ”;
          ESCREVA am[0];
        FIM-SENÃO
      FIM-SENÃO
    FIM-SENÃO
  FIM-SENÃO
  
  ESCREVA “Digite um aminoácido (2 de 3) \n”;
  LEIA am[1];
  SE COMPARE(am[1],”G”) OU COMPARE(am[0],”C”) OU COMPARE(am[1],”A”) OU COMPARE(am[1],”L”) OU 
  COMPARE(am[1],”I”) OU COMPARE(am[1],”V”) OU COMPARE(am[1],”M”) OU COMPARE(am[1],”P”) OU
  COMPARE(am[1],”F”) OU COMPARE(am[1],”W”) ENTÃO
    apolares = apolares + 1;
  SENÃO
    SE COMPARE(am[1],”N”) OU COMPARE(am[1],”Q”) OU COMPARE(am[1],”S”) OU COMPARE(am[1],”T”) OU 
    COMPARE(am[1],”Y”) ENTÃO
      polaresNeutros = polaresNeutros + 1;
    SENÃO
      SE COMPARE(am[1],”D”) OU COMPARE(am[1],”E”) ENTÃO
        polaresAcidos = polaresAcidos + 1;
      SENÃO
        SE COMPARE(am[1],”R”) OU COMPARE(am[1],”H”) OU COMPARE(am[1],”K”) ENTÃO
          polaresBasicos = polaresBasicos + 1;
        SENÃO
          ESCREVA “Aminoácido invalido: ”;
          ESCREVA am[1];
        FIM-SENÃO
      FIM-SENÃO
    FIM-SENÃO
  FIM-SENÃO

  ESCREVA “Digite um aminoácido (3 de 3) \n”;
  LEIA am[2];
  SE COMPARE(am[2],”G”) OU COMPARE(am[0],”C”) OU COMPARE(am[2],”A”) OU COMPARE(am[2],”L”) OU 
  COMPARE(am[2],”I”) OU COMPARE(am[2],”V”) OU COMPARE(am[2],”M”) OU COMPARE(am[2],”P”) OU
  COMPARE(am[2],”F”) OU COMPARE(am[2],”W”) ENTÃO
    apolares = apolares + 1;
  SENÃO
    SE COMPARE(am[2],”N”) OU COMPARE(am[2],”Q”) OU COMPARE(am[2],”S”) OU COMPARE(am[2],”T”) OU 
    COMPARE(am[2],”Y”) ENTÃO
      polaresNeutros = polaresNeutros + 1;
    SENÃO
      SE COMPARE(am[2],”D”) OU COMPARE(am[2],”E”) ENTÃO
        polaresAcidos = polaresAcidos + 1;
      SENÃO
        SE COMPARE(am[2],”R”) OU COMPARE(am[2],”H”) OU COMPARE(am[2],”K”) ENTÃO
          polaresBasicos = polaresBasicos + 1;
        SENÃO
          ESCREVA “Aminoácido invalido: ”;
          ESCREVA am[2];
        FIM-SENÃO
      FIM-SENÃO
    FIM-SENÃO
  FIM-SENÃO
  ESCREVA “Sequencia: ”+am[0]+” ”+ am[1]+” ”+ am[2]+“\n”
  ESCREVA “Apolares: ”+ apolares+“\n”
  ESCREVA “Polares neutros: ”+ polaresNeutros+“\n”
  ESCREVA “Polares acidos: ”+ polaresAcidos+“\n”
  ESCREVA “Polares basicos: ”+ polaresBasicos+“\n”
FIM

```	

* slide 53 - Estrutura de repetição - PARA (for)

```
PARA i = 0 ATÉ 99 PASSO 1 FAÇA
	ESCREVA vetor[i]+“\n”; 
FIM-PARA
```

```
PARA i = 99 ATÉ 0 PASSO -1 FAÇA
	ESCREVA vetor[i]+“\n”; 
FIM-PARA
```

* slide 55 - Estrutura de repetição - ENQUANTO

```
i = 0
ENQUANTO i <= 99 FAÇA
	 ESCREVA vetor[i]+“\n”;
	 i = i+1; 
FIM-ENQUANTO
```
```
i = 99
ENQUANTO i >= 0 FAÇA
	ESCREVA vetor[i]+“\n”;
	i = i-1; 
FIM-ENQUANTO
```

* slide 55 - Estrutura de repetição - REPITA

```
i = 0
REPITA
	ESCREVA vetor[i]+“\n”;
	i = i+1; 
ATÉ i == 99
```
```
i = 99
REPITA
	ESCREVA vetor[i]+“\n”;
	i = i-1; 
ATÉ i == 0
```

* slide 58
Crie um programa que receba uma sequência de aminoácidos e imprima a quantidade de aminoácidos apolares, polares neutros, polares ácidos, polares básicos. 

```
ALGORITMO Aminoácido
  var am: array [0..1000000] of String;
  var apolares, polaresNeutros, quantidade, i: Integer 
  var polaresAcidos, polaresBasicos: Integer
INICIO
  ESCREVA “Quantos aminoácidos você deseja digitar?”;
  LEIA quantidade;
  PARA i DE 1 ATÉ quantidade PASSO 1 FAÇA  
    ESCREVA “Digite o aminoácido (”+i+“ de ”+quantidade+“)”;
    LEIA am[i];
    SE COMPARE(am[i],”G”) OU COMPARE(am[i],”C”) OU COMPARE(am[i],”A”) OU COMPARE(am[i],”L”) OU 
    COMPARE(am[i],”I”) OU COMPARE(am[i],”V”) OU COMPARE(am[i],”M”) OU COMPARE(am[i],”P”) OU
    COMPARE(am[i],”F”) OU COMPARE(am[i],”W”) ENTÃO
      apolares = apolares + 1;
    SENÃO
      SE COMPARE(am[i],”N”) OU COMPARE(am[i],”Q”) OU COMPARE(am[i],”S”) OU COMPARE(am[i],”T”) OU 
      COMPARE(am[i],”Y”) ENTÃO
        polaresNeutros = polaresNeutros + 1;
      SENÃO
        SE COMPARE(am[i],”D”) OU COMPARE(am[i],”E”) ENTÃO
          polaresAcidos = polaresAcidos + 1;
        SENÃO
          SE COMPARE(am[i],”R”) OU COMPARE(am[i],”H”) OU COMPARE(am[i],”K”) ENTÃO
            polaresBasicos = polaresBasicos + 1;
          SENÃO
            ESCREVA “Aminoácido invalido: ”;
            ESCREVA am[i];
          FIM-SENÃO
        FIM-SENÃO
      FIM-SENÃO
    FIM-SENÃO
  FIM-PARA

  ESCREVA “Sequencia\n”
  PARA i DE 1 ATÉ quantidade PASSO 1 FAÇA  
    ESCREVA am[i]+“ ”;
  FIM-PARA

  ESCREVA “Apolares:”+ apolares+ “\n”
  ESCREVA “Polares neutros: ”+ polaresNeutros+“\n”
  ESCREVA “Polares acidos: ”+ polaresAcidos+“\n”
  ESCREVA “Polares basicos: ”+ polaresBasicos +“\n”
FIM
```

* slide 66 - Modularização

```
PROGRAMA NumeroPrimo 
	var numero: Integer;
	PROCEDIMENTO verificaSeEhPrimo (Integer numero)
		var i, metade: Integer;
		var ehPrimo: Boolean;
	INICIO
		metade = numero div 2;
		ehPrimo = TRUE;
	PARA i = 2 ATÉ metade INCREMENTO 1 FAÇA
		SE (numero % i) == 0 ENTÃO
			ehPrimo<-FALSE;
		FIM-SE
	FIM-PARA
	SE ehPrimo ENTÃO
		ESCREVA “O numero ”+numero+” e primo”;
	SENÃO
		ESCREVA “O numero ”+numero+” nao e primo”;
	FIM-SENÃO
FIM

INICIO
	ESCREVA “Digite um número”;
	LEIA numero;
	verificaSeEhPrimo(numero);
FIM
```

* slide 67
```
PROGRAMA NumeroPrimo 
	var numero: Integer;
	FUNÇÃO verificaSeEhPrimo (Integer numero): Boolean
		var i, metade: Integer;
		var ehPrimo: Boolean;
	INICIO
		metade = numero div 2;
		ehPrimo = VERDADEIRO;
	PARA i = 2 ATÉ metade INCREMENTO 1 FAÇA
		SE (numero % i) == 0 ENTÃO
			ehPrimo = FALSO;
		FIM-SE
	FIM-PARA
	RETORNE ehPrimo;
FIM

INICIO
	ESCREVA “Digite um número”
	LEIA numero
	SE verificaSeEhPrimo(numero) ENTÃO
		ESCREVA “O numero ”+numero+” e primo”
	SENÃO
		ESCREVA “O numero ”+numero+” nao e primo”
	FIM-SENÃO
FIM
```

* slide 69 - 

```
PROGRAMA Passagem 
	var numero, resultado: Real;
	FUNÇÃO exemplo (Integer numero): Real
		var resultado: Real;
	INICIO
		resultado = numero*numero; 			
		numero = numero+80;
		RETORNE resultado;
	FIM 
INICIO
	numero = 10;
	resultado = exemplo(numero);
	ESCREVA “O numero era ”+numero; 
	ESCREVA “o resultado era ”+resultado;
FIM
```

* slide 90 
Crie um programa que receba uma sequência de aminoácidos e imprima a quantidade de aminoácidos apolares, polares neutros, polares ácidos, polares básicos. 

```
ALGORITMO Aminoácido
  var am: array [0..1000000] of String;
  var apolares, polaresNeutros, quantidade, i: Integer 
  var polaresAcidos, polaresBasicos: Integer
  
  FUNÇÃO ehApolar(String am): Booleano
  INICIO
    SE COMPARE(am,”G”) OU COMPARE(am,”C”) OU COMPARE(am,”A”) OU COMPARE(am,”L”) OU COMPARE(am,”I”)       OU COMPARE(am,”V”) OU COMPARE(am,”M”) OU COMPARE(am,”P”) OU COMPARE(am,”F”) OU COMPARE(am,”W”) 
    ENTÃO
      RETORNE VERDADEIRO;
    FIM-SE
    RETORNE FALSO;
  FIM
  FUNÇÃO ehPolarNeutro(String am): Booleano
  INICIO
    SE COMPARE(am,”N”) OU COMPARE(am,”Q”) OU COMPARE(am,”S”) OU COMPARE(am,”T”) OU COMPARE(am,”Y”)   
    ENTÃO
      RETORNE VERDADEIRO;
    FIM-SE
    RETORNE FALSO;
  FIM

FUNÇÃO ehPolarAcido(String am): Booleano
  INICIO
    SE COMPARE(am,”D”) OU COMPARE(am,”E”) ENTÃO
      RETORNE VERDADEIRO;
    FIM-SE
    RETORNE FALSO;
  FIM
  FUNÇÃO ehPolarBasico(String am): Booleano
  INICIO
    SE COMPARE(am,”R”) OU COMPARE(am,”H”) OU COMPARE(am,”K”) ENTÃO
      RETORNE VERDADEIRO;
    FIM-SE
    RETORNE FALSO;
  FIM


INICIO
  ESCREVA “Quantos aminoácidos você deseja digitar?”;
  LEIA quantidade;
  PARA i DE 1 ATÉ quantidade PASSO 1 FAÇA  
    ESCREVA “Digite o aminoácido (”+i+“ de ”+quantidade+“)”;
    LEIA am[i];
    SE ehApolar(am[i]) ENTÃO
      apolares = apolares + 1;
    SENÃO
      SE ehPolarNeutro(am[i]) ENTÃO
        polaresNeutros = polaresNeutros + 1;
      SENÃO
        SE ehPolarAcido(am[i]) ENTÃO
          polaresAcidos = polaresAcidos + 1;
        SENÃO
          SE ehPolarBasico(am[i]) ENTÃO
            polaresBasicos = polaresBasicos + 1;
          SENÃO
            ESCREVA “Aminoácido invalido: ”;
            ESCREVA am[i];          
          FIM-SENÃO
        FIM-SENÃO
      FIM-SENÃO
    FIM-SENÃO
  FIM-PARA
  ESCREVA “Sequencia\n”
  PARA i DE 1 ATÉ quantidade PASSO 1 FAÇA  
    ESCREVA am[i]+“ ”;
  FIM-PARA
  ESCREVA “Apolares:”+ apolares+ “\n”
  ESCREVA “Polares neutros: ”+ polaresNeutros+“\n”
  ESCREVA “Polares acidos: ”+ polaresAcidos+“\n”
  ESCREVA “Polares basicos: ”+ polaresBasicos +“\n”
FIM
```











