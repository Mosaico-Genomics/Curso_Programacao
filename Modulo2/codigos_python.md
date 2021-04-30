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



