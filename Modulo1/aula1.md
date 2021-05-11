# Módulo 1 - SED/AWK

## Aula 1 - SED  (24/05/2021)

**Profa. Dra.** **Fernanda S. Kehdy**

Neste documento estão disponíveis os códigos demonstrados nos slides da aula 1.

As saídas dos comandos são precedidas por #.

### Slide 5

1. **Estrutura básica**

```bash
sed 'comando' input_file
```

Estrutura básica de um comando do `sed`. Por padrão, o resultado da operação é impresso na saída padrão e nada é salvo no disco.

```bash
sed 'comando' input_file > output_file
```

Desta vez, o resultado da operação estipulada pelo ` comando` sobre o arquivo `input_file` será redirecionado para um arquivo `output_file`. Obs.: Este arquivo será criado contendo a saída do comando `sed` e sobrescreverá um outro com mesmo nome sem confirmação.

Se nenhum arquivo de entrada for fornecido, o `sed` busca pela entrada padrão, o que permite encadeamento de comandos usando por exemplo o *pipe* `|`. 

```bash
cat input_file | sed 'comando' > output_file
```

### Slide 7

2. **Substituição**

```bash
sed 's/DNA/RNA/' texto.txt

# Uma sequencia de RNA e composta por nucleotideos A, G, C ou T.
# Sendo que, os nucleotideos sao complementares, A:T, G:C.
```

Este comando irá substituir `s` a cadeia de texto `DNA` contidas no arquivo `texto.txt` por `RNA`. 
Note que os comandos em `sed` são sempre envoltos por aspas simples `'comando'`. 
O padrão a ser substituído poderia ser numérico (inteiros ou racionais).
Da forma como está, o termo `DNA` será substituído apenas **na primeira ocorrência** de cada uma das linhas do arquivo.

### Slide 9

```bash
sed 's/T/U/' dna.txt

# AUGCATGCTACTGATCGTAGTCATCGTCGTAGCAGTGCTAGCTGATGC
# AUGCATGCTACTGATCGTAGTCATCGTCGTAGCAGTGCTAGCTGATGC
```


Como antes, o comando acima irá substituir `s` a primeira ocorrência de `T` por `U` em todas as linhas.

Por outro lado, para alterar o comportamento anterior de substituição apenas na primeira ocorrência de cada linha, utilize o `/g`:

```bash
sed 's/T/U/g' dna.txt

# AUGCAUGCUACUGAUCGUAGUCAUCGUCGUAGCAGUGCUAGCUGAUGC
# AUGCAUGCUACUGAUCGUAGUCAUCGUCGUAGCAGUGCUAGCUGAUGC
```

Agora, **todas as ocorrências** de `T` são substituídas por `U` em todas as linhas.

### Slide 11

3. **Deleção de linhas**

```bash
sed '/nao_essencial/d' aa_codons.txt

# aminoacido	abreviatura_3-letras	abreviatura_1-letra	codons	tipo
# Lisina	Lys	K	AAA AAG	essencial
# Histidina	His	H	CAC CAU	essencial
# Treonina	Thr	T	ACA ACC ACG ACU	essencial
# Valina	Val	V	GUA GUC GUG GUU	essencial
# Leucina	Leu	L	CUA CUC CUG CUU UUA UUG	essencial
# Fenilanina	Phe	F	UUC UUU	essencial
# Isoleucina	Ile	I	AUA AUC AUU	essencial
# Metionina	Met	M	AUG	essencial
# Triptofano	Trp	W	UGG	essencial
# Terminacao			UAA UAG UGA	essencial
```

O comando acima remove `d` (*delete*) as **linhas** que contenham o padrão `nao_essencial`. 

### Slide 13

```bash
sed '/^$/d' exemplo1.txt

# TACGTAGCTAGCTACGTAGACTAGC
# TCGATGCTAGCTAGCTATC
# YCGAYAGYCAYCG
# TCGTATGCGTCAGTCGTCAGTCAGT
# NNNNNN
# NNNNNNNNNNNNNNNNN
# NNNNNNNNNNNNNNNNNNNNNNNNN%
```

O comando anterior remove `d`  as linhas que contenham o marcador de fim de linha `S` no início da linha `^`. Dessa forma, isso pode ser útil para remover linhas em branco de um arquivo.

### Slide 15

Um arquivo `.fa` utiliza o caractere `>` para demarcar a linha identificadora, isto é, o nome ou descrição da sequência adiante. Dessa forma, o comando a seguir irá remover as linhas que contenham correspondência para `>` no início da linha `^`:

```bash
sed '/^>/d' fasta.fa

# GGCAGATTCCCCCTAGACCCGCCCGCACCATGGTCAGGCATGCCCCTCCTCATCGCTGGGCACAGCCCAGAGGGT
# ATAAACAGTGCTGGAGGCTGGCGGGGCAGGCCAGCTGAGTCCTGAGCAGCAGCCCAGCGCAGCCACCGAGACACC
# ATGAGAGCCCTCACACTCCTCGCCCTATTGGCCCTGGCCGCACTTTGCATCGCTGGCCAGGCAGGTGAGTGCCCC
# CACCTCCCCTCAGGCCGCATTGCAGTGGGGGCTGAGAGGAGGAAGCACCATGGCCCACCTCTTCTCACCCCTTTG
# GCTGGCAGTCCCTTTGCAGTCTAACCACCTTGTTGCAGGCTCAATCCATTTGCCCCAGCTCTGCCCTTGCAGAGG
# GAGAGGAGGGAAGAGCAAGCTGCCCGAGACGCAGGGGAAGGAGGATGAGGGCCCTGGGGATGAGCTGGGGTGAAC
# CAGGCTCCCTTTCCTTTGCAGGTGCGAAGCCCAGCGGTGCAGAGTCCAGCAAAGGTGCAGGTATGAGGATGGACC
# TGATGGGTTCCTGGACCCTCCCCTCTCACCCTGGTCCCTCAGTCTCATTCCCCCACTCCTGCCACCTCCTGTCTG
# GCCATCAGGAAGGCCAGCCTGCTCCCCACCTGATCCTCCCAAACCCAGAGCCACCTGATGCCTGCCCCTCTGCTC
# CACAGCCTTTGTGTCCAAGCAGGAGGGCAGCGAGGTAGTGAAGAGACCCAGGCGCTACCTGTATCAATGGCTGGG
# [...]
```

### Slide 17

O sed também pode ser utilizado para remover linhas inteiras por índice, isto é, por posição.
Os comandos abaixo demonstram alguns casos:

Remove `d` a terceira linha `3` do arquivo `exemplo2.csv2`.

```bash
sed '3d' exemplo2.csv2

# SYMBOL;ENTREZID;GENENAME;MAP
# PTX3;5806;pentraxin 3;3q25.32
# TNF;7124;tumor necrosis factor;6p21.33
# BIRC3;330;baculoviral IAP repeat containing 11q22.2
# XIST;7503;X inactive specific transcript;Xq13.2
# "UTY;7404;ubiquitously transcribed tetratricopeptide repeat containing, Y-linked;Yq11.221"
# GAPDH;2597;glyceraldehyde-3-phosphate dehydrogenase;12p13.31
```

Remove as linhas do intervalo `,` de 2 a 4 de modo inclusivo, isto é, as linhas 2,3 **E** 4.

```bash
sed '2,4d' exemplo2.csv2
```

Neste caso, 3 comandos de remoção são executados sequencialmente `;`. Desta forma, as linhas 1,3 e 5 serão removidas `d`. 

```bash
sed '1d;3d;5d' exemplo2.csv2

# SYMBOL;ENTREZID;GENENAME;MAP
# BIRC3;330;baculoviral IAP repeat containing 11q22.2
# XIST;7503;X inactive specific transcript;Xq13.2
# "UTY;7404;ubiquitously transcribed tetratricopeptide repeat containing, Y-linked;Yq11.221"
# GAPDH;2597;glyceraldehyde-3-phosphate dehydrogenase;12p13.31
```

### Slide 19

4. **Imprimir linhas específicas através de correspondência **  

```bash
sed -n '/>/p' fasta.fa

# >HSBGPG Human gene for bone gla protein (BGP)
# >HSGLTH1 Human theta 1-globin gene
```

Por padrão o sed imprime na tela o resultado dos comandos. Todavia, quando se deseja **imprimir linhas específicas**, isso deve ser desativado com a opção `-n` (ou `--silent` ou `--quiet`). Em seguida, o comando busca por linhas contendo o caractere `>`, que se encontrado, `p` imprime a linha.

Neste exemplo, apenas as linhas com os nomes das sequências de um arquivo `.fa` são impressas.

### Slide 21

5. **Imprimir linhas por índice ou posição**

Conforme visto anteriormente, a impressão de linhas específicas pode também ser especificada utilizando as posições/índices ou intervalos:

Imprime `p` **apenas** a primeira linha `1`do arquivo `aa_codons.txt`.

```bash
sed -n '1p' aa_codons.txt

# aminoacido	abreviatura_3-letras	abreviatura_1-letra	codons	tipo
```

  Imprime **apenas** as linhas de 1 a 7 do arquivo, i.e, linhas ${1,2,3,4,5,6~\text{e}~7}$.

```bash
sed -n '1,7p' aa_codons.txt

# aminoacido	abreviatura_3-letras	abreviatura_1-letra	codons	tipo
# Ac.aspartico	Asp	D	GAC GAU	nao_essencial
# Ac.glutamico	Glu	E	GAA GAG	nao_essencial
# Arginina	Arg	R	CGA CGC CGG CGU AGA AGG	nao_essencial
# Lisina	Lys	K	AAA AAG	essencial
# Asparagina	Asn	N	AAC AAU	nao_essencial
# Histidina	His	H	CAC CAU	essencial
```

 Imprime **apenas** as linhas 1 **E** 7 do arquivo.

``` bash
sed -n '1p;7p' aa_codons.txt

# aminoacido	abreviatura_3-letras	abreviatura_1-letra	codons	tipo
# Histidina	His	H	CAC CAU	essencial
```

### Slide 23

6. **Transliteração**

O argumento `y/` faz a transliteração dos caracteres da cadeia <u>fonte</u> pela cadeia de <u>destino</u>. Em termos mais simples, ele possibilita trocar caracteres e padrões.

```bash
sed 'y/ACTG/actg/' fasta.fa

# >HSBgPg Human gene for bone gla protein (BgP)
# ggcagattccccctagacccgcccgcaccatggtcaggcatgcccctcctcatcgctgggcacagcccagagggt
# ataaacagtgctggaggctggcggggcaggccagctgagtcctgagcagcagcccagcgcagccaccgagacacc
# atgagagccctcacactcctcgccctattggccctggccgcactttgcatcgctggccaggcaggtgagtgcccc
# cacctcccctcaggccgcattgcagtgggggctgagaggaggaagcaccatggcccacctcttctcacccctttg
# gctggcagtccctttgcagtctaaccaccttgttgcaggctcaatccatttgccccagctctgcccttgcagagg
# gagaggagggaagagcaagctgcccgagacgcaggggaaggaggatgagggccctggggatgagctggggtgaac
# caggctccctttcctttgcaggtgcgaagcccagcggtgcagagtccagcaaaggtgcaggtatgaggatggacc
# tgatgggttcctggaccctcccctctcaccctggtccctcagtctcattcccccactcctgccacctcctgtctg
# gccatcaggaaggccagcctgctccccacctgatcctcccaaacccagagccacctgatgcctgcccctctgctc
# [...]
```

O comando acima irá transliterar, ou seja, substituir por mapeamento os caracteres **fonte** (`ACTG`) pelos caracteres de **destino** `actg`.  

**Atente-se que:**

*  O número de caracteres na lista fonte e de destino **deve ser igual**;
* A transliteração **não** corresponde a cadeia de caracteres **como um todo**, mas sim caractere a caractere, ou seja, A → a e C → c, e assim por diante.

Para negar uma correspondência, o ponto de exclamação `!` é utilizado. Veja um exemplo:

```bash
sed '/>/!y/ACTG/actg/' fasta.fa

# >HSBGPG Human gene for bone gla protein (BGP)
# ggcagattccccctagacccgcccgcaccatggtcaggcatgcccctcctcatcgctgggcacagcccagagggt
# ataaacagtgctggaggctggcggggcaggccagctgagtcctgagcagcagcccagcgcagccaccgagacacc
# atgagagccctcacactcctcgccctattggccctggccgcactttgcatcgctggccaggcaggtgagtgcccc
# cacctcccctcaggccgcattgcagtgggggctgagaggaggaagcaccatggcccacctcttctcacccctttg
# gctggcagtccctttgcagtctaaccaccttgttgcaggctcaatccatttgccccagctctgcccttgcagagg
# gagaggagggaagagcaagctgcccgagacgcaggggaaggaggatgagggccctggggatgagctggggtgaac
# caggctccctttcctttgcaggtgcgaagcccagcggtgcagagtccagcaaaggtgcaggtatgaggatggacc
# tgatgggttcctggaccctcccctctcaccctggtccctcagtctcattcccccactcctgccacctcctgtctg
# gccatcaggaaggccagcctgctccccacctgatcctcccaaacccagagccacctgatgcctgcccctctgctc
# [...]
```

Para todas as linhas **não** contendo **>** `/>/!`
transliterar `ACTG` por `actg`.

O comando acima omitindo o `!`seria para **apenas** as linhas **contendo** **>**  `/>/`. 
Logo, sem a parte inicial, isto é, removendo `/>/!` o comando seria executado em **todas** as linhas do arquivo.

### Slide 25

Veja um exemplo da aplicação do comando de substituição `s` do `sed`:

```bash
sed 's/;/\t/g' exemplo2.csv2

# SYMBOL	ENTREZID	GENENAME	MAP
# PTX3	5806	pentraxin 3	3q25.32
# IFNG	3458	interferon gamma	12q15
# TNF	7124	tumor necrosis factor	6p21.33
# BIRC3	330	baculoviral IAP repeat containing 11q22.2
# XIST	7503	X inactive specific transcript	Xq13.2
# "UTY	7404	ubiquitously transcribed tetratricopeptide repeat containing, Y-linked	Yq11.221"
# GAPDH	2597	glyceraldehyde-3-phosphate dehydrogenase	12p13.31
```

O comando acima utiliza o sed para trocar o delimitador de campos do arquivo `.csv2`, o qual é delimitado por `;`, para o delimitador Tab ↹ representado pelo caractere de escape `\t`.  

### Slide 27

7. **Múltiplos comandos**

O `sed` permite encadear múltiplos comandos sem a necessidade de invocar o programa repetidamente. Para isso, o argumento utilizado é `-e` ou `--expression`. Veja o exemplo:

```bash
sed -e 's/ATG/*ATG*/g' -e '/^>/d' fasta.fa

# GGCAGATTCCCCCTAGACCCGCCCGCACC*ATG*GTCAGGC*ATG*CCCCTCCTCATCGCTGGGCACAGCCCAGAGGGT
# ATAAACAGTGCTGGAGGCTGGCGGGGCAGGCCAGCTGAGTCCTGAGCAGCAGCCCAGCGCAGCCACCGAGACACC
# *ATG*AGAGCCCTCACACTCCTCGCCCTATTGGCCCTGGCCGCACTTTGCATCGCTGGCCAGGCAGGTGAGTGCCCC
# CACCTCCCCTCAGGCCGCATTGCAGTGGGGGCTGAGAGGAGGAAGCACC*ATG*GCCCACCTCTTCTCACCCCTTTG
# GCTGGCAGTCCCTTTGCAGTCTAACCACCTTGTTGCAGGCTCAATCCATTTGCCCCAGCTCTGCCCTTGCAGAGG
# GAGAGGAGGGAAGAGCAAGCTGCCCGAGACGCAGGGGAAGGAGG*ATG*AGGGCCCTGGGG*ATG*AGCTGGGGTGAAC
# CAGGCTCCCTTTCCTTTGCAGGTGCGAAGCCCAGCGGTGCAGAGTCCAGCAAAGGTGCAGGT*ATG*AGG*ATG*GACC
# TG*ATG*GGTTCCTGGACCCTCCCCTCTCACCCTGGTCCCTCAGTCTCATTCCCCCACTCCTGCCACCTCCTGTCTG
# GCCATCAGGAAGGCCAGCCTGCTCCCCACCTGATCCTCCCAAACCCAGAGCCACCTG*ATG*CCTGCCCCTCTGCTC
# CACAGCCTTTGTGTCCAAGCAGGAGGGCAGCGAGGTAGTGAAGAGACCCAGGCGCTACCTGTATCA*ATG*GCTGGG
# [...]
```

A linha acima executa dois comandos, o primeiro de substituição `s`, e o segundo de deleção `d`. Note que o input é passado somente ao final da cadeia, a qual é sempre separada pelo argumento `-e`.  

### Slides 29 e 30

8. **Comandos em um *script***

Além do encadeamento, múltiplos comandos em `sed` podem ser escritos em um *script* e invocados pela linha de comando. Isso facilita a leitura, manutenção, portabilidade e reutilização.

```bash
cat > script.sed
nano script.sed
```

```bash
s/ATG/*ATG*/g
/^>/d
```

No primeiro bloco de código, um arquivo `script.sed` é criado no diretório de trabalho e, em seguida, aberto com o editor de texto `nano`.  
O segundo bloco contém o conteúdo do *script* sed com os 2 comandos desejados. Veja que eles são separados por quebras de linha.
O próximo bloco invoca o sed com o argumento `-f`, seguido do arquivo `.sed` <sup>[1](#myfootnote1)</sup> contendo os comandos. 

```bash
sed -f script.sed fasta.fa

# GGCAGATTCCCCCTAGACCCGCCCGCACC*ATG*GTCAGGC*ATG*CCCCTCCTCATCGCTGGGCACAGCCCAGAGGGT
# ATAAACAGTGCTGGAGGCTGGCGGGGCAGGCCAGCTGAGTCCTGAGCAGCAGCCCAGCGCAGCCACCGAGACACC
# *ATG*AGAGCCCTCACACTCCTCGCCCTATTGGCCCTGGCCGCACTTTGCATCGCTGGCCAGGCAGGTGAGTGCCCC
# CACCTCCCCTCAGGCCGCATTGCAGTGGGGGCTGAGAGGAGGAAGCACC*ATG*GCCCACCTCTTCTCACCCCTTTG
# GCTGGCAGTCCCTTTGCAGTCTAACCACCTTGTTGCAGGCTCAATCCATTTGCCCCAGCTCTGCCCTTGCAGAGG
# GAGAGGAGGGAAGAGCAAGCTGCCCGAGACGCAGGGGAAGGAGG*ATG*AGGGCCCTGGGG*ATG*AGCTGGGGTGAAC
# CAGGCTCCCTTTCCTTTGCAGGTGCGAAGCCCAGCGGTGCAGAGTCCAGCAAAGGTGCAGGT*ATG*AGG*ATG*GACC
# TG*ATG*GGTTCCTGGACCCTCCCCTCTCACCCTGGTCCCTCAGTCTCATTCCCCCACTCCTGCCACCTCCTGTCTG
# GCCATCAGGAAGGCCAGCCTGCTCCCCACCTGATCCTCCCAAACCCAGAGCCACCTG*ATG*CCTGCCCCTCTGCTC
# CACAGCCTTTGTGTCCAAGCAGGAGGGCAGCGAGGTAGTGAAGAGACCCAGGCGCTACCTGTATCA*ATG*GCTGGG
# [...]
```

<a name="myfootnote1">1</a>: A extensão `.sed` não é obrigatória ao criar o arquivo do script.