# Bem vindos ao curso de programação da Mosaico

Nesta seção, vocês encontrarão os codigos de python utilizados durantes as aulas.

***
Instalar anaconda
<p>Abrir anaconda
  
***

# Códigos Python


* slide 112
```
print("ola mundo")
```
Executar script:
```
python olamundo.py
```

* slide 118 - Tipos de variáveis
```
import numpy as np

texto =“”
lista = []
matrix = np.zeros((3,4))

texto =“Ola”
lista.append(10)
matrix[0][1] = 0.68

```

* slide 119 - Tipos de variáveis 

```
import numpy as np

texto =“”
vector = np.zeros((3))
matrix = np.zeros((3,4))

texto =“Ola”
vector[0] = 10
matrix[0][1] = 0.68
```

* slide 121 - Operadores de string - Concatenação

```
texto1 = “Aprendendo ”
texto2 = “Pseudocodigo”
texto3 = texto1+texto2
print(texto3)
```

* slide 122 - Operadores de string - Concatenação 

```
texto1 = “Aprendendo ”
texto2 = “Pseudocodigo”
print(texto1.replace(“A”, “a”))
print(texto1.replace(“Y”, “a”))
```

* slide 123 - Mudando tipo do dado

```
texto1 = “Aprender ”
texto2 = “Pseudocodigo é ”
numero = 10
texto3 = texto1+texto2+ str(numero)
texto3 = f”{texto1}{texto2} {numero}”
print(texto3)
```

* slide 124 - Operadores de string - Comparação

```
texto1 = “Aprendendo ”
texto2 = “Aprendendo”
texto3 = “Python”
print(texto1 == texto3)
print(texto1 == texto2)
```

* slide 125 - Expressões mistas

```
nota = float(input())
if nota >= 6:
    print(“Aprovado”)
else:
    if nota >= 5 and nota < 6:
        print(“Recuperação”)
    else:
        print(“Reprovado”)
```

* slide 127 - Recebendo o input do teclado

```
numero = input(“Digite um numero”)
```

* slide 131 - Preenchendo um vetor – Inserindo valores no final

```
vetor=[]
for i in range(0,5,1):
    var= input(“Insira um valor”)
    vetor.append(var)
```

* slide 150 - Preenchendo um vetor – Removendo valores

```
x=2
removed= vetor.pop(x)
```

* slide 156 - Estrutura de repetição com vetores
``` 
for var in vetor:
    print (var)
#OU
for i in range(len(vetor)):
    print (vetor[i])
#OU
while i< len(vetor):
    print (vetor[i])
    i=i+1
```

* slide 165 - Exemplo de um if dentro de um laço: quantos pares?

```
contador = 0
for i in range(len(vetor)):
    if vetor[i] % 2 == 0:
        contador=contador+1
print (contador)
```

* slide 178 - Funções e procedimentos – Passagem por valor

```
def quadrado(numero):
    quadrado=numero*numero
    return quadrado
num = input()
elevado=quadrado(num)
```

* slide 182 - Manipulação de arquivos

```
#Leitura
FILE = open(“arquivo.txt”, “r”)
```

* slide 183 - Manipulação de arquivos

```
#Escrita
FILE = open(“arquivo2.txt”, “w”)
```

* slide 184 - Manipulação de arquivos - Lendo

```
FILE = open(“arquivo.txt”, “r”)
for line in FILE:
    print(line)
```

* slide 191 - Manipulação de arquivos – Armazenando um arquivo em um vetor

```
vetor = []
FILE = open(“arquivo.txt”, “r”)
for line in FILE:
    vetor.append(line)
```

* slide 197 - Manipulação de arquivos – Escrevendo em um arquivo
```
string = “Texto aleatorio”
fileOut = open(“arquivo.txt”, “w”)
fileOut.write(string)
```

* slide 212 - Tipos de variáveis - Dicionários

```
dicionario = {}
dicionario[“nome”] = “Thiago P Leal”
dicionario[“professor”] = True
dicionario[“monitor”] = True
```

* slide 213 - Tipos de variáveis  

```
dict = {}
dict[“nome”] = “Thiago P Leal”
dict[“professor”] = True
dict[“monitor”] = True

print (dict)
```

* slide 214 - Tipos de variáveis  

```
dict = {}
dict[“nome”] = “Thiago P Leal”
dict[“professor”] = True
dict[“monitor”] = True

print (dict[“professor”])
```

* slide 215 - Tipos de variáveis  

```
dict = {}
dict[“nome”] = “Thiago P Leal”
dict[“professor”] = True
dict[“monitor”] = True

dict[“nome”] = “Thiago Peixoto Leal”
print (dict[“nome”])
```

* slide 220 - Tipos de variáveis  

```
dict = {}
dict[“Thiago P Leal”] = {}
dict[“Thiago P Leal”][“professor”] = True
dict[“Thiago P Leal”][“monitor”] = True

dict[“Carolina S de Carvalho”] = {}
dict[“Carolina S de Carvalho”][“professor”] = False
dict[“Carolina S de Carvalho”][“monitor”] = True
dict[“Carolina S de Carvalho”][“organizador”] = True

dict[“Camila Zolini de Sa”] = {}
dict[“Camila Zolini de Sa”][“organizador”] = True
dict[“Camila Zolini de Sa”][“monitor”] = False
```

slide 222 -- Tipos de variáveis

```
for nome in dict:
    print(f"{nome}:")
    for ocupacao in dict[nome]:
        print(f“\tEh {ocupacao}")
            
```

 slide 223 -- Tipos de variáveis

```
for nome in dict:
    print(f"{nome}:")
    for ocupacao in dict[nome]:
        if dict[nome][ocupacao]:
            print(f“\tEh {ocupacao}")
```
