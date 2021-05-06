# bMódulo 1 - SED/AWK

## Aula 2 - AWK  (25/05/2021)

**Profa. Dra.** **Fernanda S. Kehdy**

Neste documento estão disponíveis os códigos demonstrados nos slides da aula 2. As saídas dos comandos, sempre que mostradas, são iniciados por #.

### Slide 7

```bash
awk 'padrao {acao}' input.file
```

Estrutura básica de um comando do AWK. A primeira parte invoca o interpretador `awk`, seguido de um padrão a ser procurado (por exemplo) e uma ação entre `{}`. Veja que todo o bloco padrão e ação estão envoltos em aspas simples ou apóstrofo.

### Slide 8

```bash
awk '/Ovar/' hgmd_brca1.txt

# CM014520	ATG-AGG	Met1Arg	M1R	2T>G	Ovarian cancer	[...]
# CM012906	ATG-AAG	Met18Lys	M18K	53T>A	Ovarian cancer	[...]
# CM001645	aCAA-TAA	Gln172Term	Q172X	514C>T	Ovarian cancer	[...]
# CM004754	aCAG-TAG	Gln310Term	Q310X	928C>T	Ovarian cancer	[...]
# [...]
```

Se nenhuma ação for fornecida, o AWK irá procurar por linhas contendo a cadeia de texto presente entre as barras. Se alguma correspondência for encontrada, a linha contendo-a é impressa na saída padrão.  Assim como no SED, nenhuma alteração foi feita no arquivo de entrada.

```bash
awk '/[Oo]var/' hgmd_brca1.txt

# CM014520	ATG-AGG	Met1Arg	M1R	2T>G	Ovarian cancer	Sekine [...]
# CM012906	ATG-AAG	Met18Lys	M18K	53T>A	Ovarian cancer	[...]
# [...]
# M041680	CTG-CCG	Leu28Pro	L28P	83T>C	Breast and/or ovarian cancer [...]
# CM041681	ACA-AGA	Thr37Arg	T37R	110C>G	Breast and/or ovarian cancer ?	[...]
# [...]
```

Neste exemplo, o padrão a ser buscado pode conter tanto `O` maiúsculo quanto o minúsculo `o`. Isso foi especificado através de expressões regulares. Veja que desta vez, algumas correspondências para "*ovarian cancer*" foram encontradas.

### Slide 11

```bash
awk '{print $1, $3, $4}' hgmd_brca1.txt

# Accession HGMD codon
# CM014520 Met1Arg M1R
# CM960163 Met1Ile M1I
# CM041678 Met1Thr M1T
# CM021503 Met1Val M1V
# CM940170 Val11Ala V11A
# CM031646 Gln12Term Q12X
# CM041679 Ile15Thr I15T
# CM012906 Met18Lys M18K
# CM004187 Met18Thr M18T
# CM081536 Gln19Term Q19X
# [...]
```

O comando acima não faz nenhuma busca por padrões nas linhas do arquivo. Por outro lado, uma ação de imprimir é explicitamente fornecida. O caractere `$` significa um campo do arquivo (neste caso, e na maioria de arquivos de tabelas, esse campo é uma coluna). Por padrão, o GNU AWK procura por caractere(s) de espaço(s) e/ou tabulações e/ou marcador de fim de linha, e os utiliza como delimitador de campo. Note que, no arquivo acima, o primeiro campo, isto é -- a primeira coluna, foi impressa através do seu índice `$1`. Múltiplos campos são delimitados por vírgulas. Observe também que a ação está envolta em chaves `{}`.

### Slide 11 

No exemplo abaixo, as colunas do arquivo são reordenadas apenas por trocar a ordem dos índices:

```bash
awk '{print $4, $1, $3}' hgmd_brca1.txt 

# codon Accession HGMD
# M1R CM014520 Met1Arg
# M1I CM960163 Met1Ile
# M1T CM041678 Met1Thr
# M1V CM021503 Met1Val
# V11A CM940170 Val11Ala
# Q12X CM031646 Gln12Term
# I15T CM041679 Ile15Thr
# M18K CM012906 Met18Lys
# [...]
```

### Slide 13

```bash
awk '{print $1, $7}' hgmd_brca1.txt

# Accession amino
# CM014520 cancer
# CM960163 cancer
# CM041678 and/or
# CM021503 and/or
# CM940170 cancer
# CM031646 cancer
# CM041679 and/or
# CM012906 cancer
# CM004187 cancer
# [...]
```

O comando acima exemplifica como é simples a **seleção de colunas** de um arquivo delimitado com o AWK. Neste caso, apenas as colunas`$1` e `$7` foram selecionadas e impressas na saída padrão. Repare que a segunda coluna tem como nome "amino", porém o conteúdo não condiz com o esperado.

### Slide 19

```bash
awk -F'\t' '{print $1, $7}' hgmd_brca1.txt 

# Accession Number Reference
# CM014520 Sekine (2001) Clin Cancer Res 7:3144
# CM960163 Couch (1996) Hum Mutat 8:8
# CM041678 Abkevich (2004) J Med Genet 41:492
# CM021503 Meindl (2002) Int J Cancer 97:472
# CM940170 Castilla (1994) Nat Genet 8:387
# CM031646 Adem (2003) Cancer 97:1
# CM041679 Abkevich (2004) J Med Genet 41:492
# CM012906 Machackova (2001) Hum Mutat 18:545
# CM004187 Malone (1998) JAMA 279:922
# [...]
```

Para informar ao AWK qual delimitador deve ser utilizado como separador dos campos, utilize o argumento `-F` passado após a invocação do executável `awk`.  **Veja que desta vez o conteúdo foi extraído corretamente**. O que ocorreu foi que, no exemplo do slide 13, o delimitador utilizado pelo AWK foi o espaço em branco, enquanto que o delimitador do arquivo é a tabulação. Portanto, a sétima coluna do arquivo `hgmd_brca1.txt` contém referências. 

### Slide 21

```bash
awk '/X/' hgmd_brca1.txt

# C44G CM985510
# G275S CM076033
# R496C CM065005
# Q657X CM068262
# Q1396X CM024467
# Y1429X CM024468
# A1708V CM065004
# A1752P CM011913
# [...]
```

O código acima busca por linhas que contenham o padrão separado entre barras, logo, o **caractere maiúsculo X** (apenas). 

```bash
awk '/X/{print $4,$1}' hgmd_brca1.txt

# Q12X CM031646
# Q19X CM081536
# L30X CM077509
# Q60X CM973715
# L63X CM950140
# Q74X CM970167
# Q81X CM044860
# Y101X CM077508
# Y130X CM055102
# E143X CM014321
# [...]
```

O comando acima busca por linhas contendo X maiúsculo e, em seguida, imprime as colunas 4 e 1.
:warning:<span style="color:red">**Atenção**</span>, o padrão é buscado em todos os campos e **não** apenas nas colunas 1 e 4.

### Slide 24

```bash
awk '$4~/X/{print $4,$1}' hgmd_brca1.txt

# Q12X CM031646
# Q19X CM081536
# L30X CM077509
# Q60X CM973715
# L63X CM950140
# Q74X CM970167
# Q81X CM044860
# Y101X CM077508
# Y130X CM055102
# E143X CM014321
# [...]
```

O comando acima **restringe** a busca na coluna 4. Isso é feito através da sintaxe `$4~//`,  onde lê-se: na coluna quatro `$4~` busque pelo padrão `X`. Embora a saída truncada [...] esteja igual a segunda do slide 21,  elas **não são iguais**. Para confirmar isso, inspecione as duas saídas na íntegra, ou conte o número de linhas de cada resultado utilizado este comando **adicional** após os comandos originais acima: `| wc -l` (conte as linhas `-l` da saída anterior redirecionada `|` ao utilitário ` wc`).  