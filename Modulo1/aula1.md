# Módulo 1 - SED/AWK

## Aula 1 - SED  (24/05/2021)

**Profa. Dra.** **Fernanda S. Kehdy**

Neste documento estão disponíveis os códigos demonstrados nos slides da aula 1.

### Slide 5

```bash
sed 'comando' input_file
```

Estrutura básica de um comando do SED. Por padrão, o resultado da operação é impresso na saída padrão e nada é salvo no disco.

```bash
sed 'comando' input_file > output_file
```

Desta vez, o resultado da operação estipulada pelo ` comando` sobre o arquivo `input_file` será redirecionado para um arquivo `output_file`. Obs.: Este arquivo será criado contendo a saída do comando `sed` e sobrescreverá em outro com mesmo nome sem confirmação.

### Slide 10

```bash
sed 's/DNA/RNA/' texto.txt
```

Este comando irá substituir `s` a cadeia de texto `DNA` contidas no arquivo `texto.txt` por `RNA`. 
Note que os comandos em `sed` são sempre envoltos por aspas simples `'comando'`. 
O padrão a ser substituído poderia ser numérico (inteiros ou racionais).
Da forma como está, o termo `DNA`será substituído apenas **na primeira ocorrência** de cada uma das linhas do arquivo.

### Slide 12

Para alterar o comportamento anterior, utilize o argumento `/g` ao final do comando.

```bash
sed 's/T/U' dna.txt
```


Como antes, o comando acima irá substituir `s` a primeira ocorrência de `T` por `U` em todas as linhas.

Por outro lado,

```bash
sed 's/T/U/g' dna.txt
```

**todas as ocorrências** de `T` por `U` em todas as linhas.







 

 





