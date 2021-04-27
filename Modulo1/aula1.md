# Módulo 1 - SED/AWK

## Aula 1 - SED  (24/05/2021)

**Profa. Dra.** **Fernanda S. Kehdy**

Neste documento estão disponíveis os códigos demonstrados nos slides da aula 1.

### Slide 5

1. **Estrutura básica**

```bash
sed 'comando' input_file
```

Estrutura básica de um comando do SED. Por padrão, o resultado da operação é impresso na saída padrão e nada é salvo no disco.

```bash
sed 'comando' input_file > output_file
```

Desta vez, o resultado da operação estipulada pelo ` comando` sobre o arquivo `input_file` será redirecionado para um arquivo `output_file`. Obs.: Este arquivo será criado contendo a saída do comando `sed` e sobrescreverá em outro com mesmo nome sem confirmação. 

Se nenhum arquivo de entrada for fornecido, o `sed` busca pela entrada padrão, o que permite encadeamento de comandos. 

```bash
cat input_file | sed 'comando' > output_file
```

### Slide 10

2. **Substituição**

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

### Slide 14

3. **Deleção de linhas**

```bash
sed '/nao_essencial/d' aa_codons.txt
```

O comando acima remove `d` (*delete*) as **linhas** que contenham o padrão `nao_essencial`. 

### Slide 16

```bash
sed '/^$/d'
```

O comando anterior remove `d`  as linhas que contenham o marcador de fim de linha `S` no início da linha `^`. Dessa forma, isso pode ser útil para remover linhas em branco.

### Slide 18

Um arquivo `.fasta` utiliza o caracter `>` para demarcar a linha identificadora, isto é, o nome ou descrição da sequência adiante. Dessa forma, o comando a seguir irá remover as linhas que contenham correspondência para `>` no início da linha `^`:

```bash
sed '/^>/d' fasta.fa
```

Exemplo de um arquivo fasta com uma sequência:

### Slide 20

O sed também pode ser utilizado para remover linhas inteiras por índice, isto é, por posição.
Os comandos abaixo demonstram alguns casos:

```bash
sed '3d' exemplo2.csv2
```

Remove `d` a terceira linha `3` do arquivo `exemplo2.csv2`.

```bash
sed '2,4d' exemplo2.csv2
```

Remove as linhas do intervalo de 2 a 4 de modo inclusivo, isto é, as linhas 2,3 **E** 4.

```bash
sed '1d;3d;5d' exemplo2.csv2
```

Neste caso, 3 comandos de remoção são executados sequencialmente. Desta forma, as linhas 1,3 e 5 serão removidas `d`. 

### Slide 22

4. **Imprimir linhas específicas**

```bash
sed -n '/>/p' fasta.fa
```

Por padrão o sed imprime na tela o resultado dos comandos. Todavia, quando se deseja **imprimir linhas específicas**, isso deve ser desativado com a opção `-n` (ou `--silent` ou `--quiet`). Em seguida, o comando busca por linhas contendo o caractere `>`, que se encontrado, `p` imprime a linha.



 

 





