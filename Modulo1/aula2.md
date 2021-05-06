# Módulo 1 - SED/AWK

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
:warning: <span style="color:red">**Atenção**</span>, o padrão é buscado em todos os campos e **não** apenas nas colunas 1 e 4.

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

### Slide 26

O código abaixo é muito parecido com o anterior. A única diferença é a presença do caractere `!` antes de `~/X/`. Esse caractere indica a <span style="color:red">**negação**</span> do próximo, isto é, **na coluna 4**, busque pelo **inverso de** X (ou seja, **tudo** **que não** corresponda a X), então imprima as colunas 4 e 1. 

```bash
awk '$4!~/X/{print $4,$1}' hgmd_brca1.txt

# codon Accession
# M1R CM014520
# M1I CM960163
# M1T CM041678
# M1V CM021503
# V11A CM940170
# I15T CM041679
# M18K CM012906
# M18T CM004187
# I21V CM940171
# [...]
```

Agora, o caractere de negação `!` está antes do padrão a ser buscado.  Como não há indicação de qual coluna isso deve ser correspondente, **para qualquer linha não contendo X**, imprima a a quarta `$4` coluna.

```bash
awk '!/X/{print $4}' hgmd_brca1.txt

# codon
# M1R
# M1I
# M1T
# M1V
# V11A
# I15T
# M18K
# M18T
# I21V
# [...]
```

### Slide 30

O AWK também permite múltiplos critérios para filtrar linhas. No exemplo abaixo, se algum dos valores da quarta coluna forem iguais `==` a `"JunD"` **E** algum valor da coluna 5 for maior `>` que 500, imprima todas as linhas. **Lembre-se, por padrão, se nenhuma ação for especificada, todas as linhas serão impressas**. Neste caso, todas as linhas obedecendo as regras anteriores são retornadas. 

```bash
awk '$4=="JunD" && $5 > 500' tfbs.bed

# chr7	936178	936581	JunD	757	+
# chr4	38567056	38567601	JunD	630	+
# chr10	73319031	73319084	JunD	658	+
# chr11	121774119	121774448	JunD	1000	+
# chr22	28938533	28939199	JunD	529	+
# chr21	34025863	34025966	JunD	655	+
# chr7	104081848	104082054	JunD	558	+
```

```bash
awk '$4=="SIX5" || $4=="STAT2"' tfbs.bed

# chr7	106043557	106044007	STAT2	145	+
# chr17	37194878	37195184	STAT2	156	+
# chr19	40347918	40348201	STAT2	366	+
# chr13	102295919	102296480	STAT2	135	+
# chr3	9379407	9380161	STAT2	148	+
# chr19	55464702	55465081	STAT2	129	+
# chr19	3713461	3713789	SIX5	471	+
# chr1	32346019	32346260	SIX5	46	+
# chr11	45163370	45163819	STAT2	303	+
```

No comando acima, para linhas contendo `"SIX5"` na quinta coluna **OU** `"STAT2"` na quarta coluna, imprima as linhas. Veja que as elas atendem os critérios.

### Slide 33

No exemplo abaixo, três critérios são aplicados, sendo que os dois primeiros estão agrupados por parênteses. Para a terceira instrução ser executada,  uma das duas inicias agrupadas deve ser correspondida. Passo-a-passo, este código lê-se: Para as linhas da coluna 4 contendo `"SIX5"` **OU** `"STAT2"` **E** que tenham valores maiores que 300 na coluna 5, imprima as linhas.

```bash
awk '($4=="SIX5" || $4=="STAT2") && $5>300' tfbs.bed

# chr19	40347918	40348201	STAT2	366	+
# chr19	3713461	3713789	SIX5	471	+
# chr11	45163370	45163819	STAT2	303	+
```

O exemplo a seguir é similar. Desta vez, algum valor da quinta coluna deverá ser menor que 35 **E** `"SREBP1" `**não** ` !` deve estar na quarta coluna. Veja que o caractere de negação foi utilizado para especificar valores da quarta coluna diferentes de `"SREBP1" `.

```bash
awk '$5<35 && $4!="SREBP1"' tfbs.bed 

# chr4	47713796	47714292	TAF1	33	+
# chr16	24928497	24928514	SREBP2	26	+
# chr14	42844745	42844884	GABP	27	+
# chr6	100075411	100076513	STAT1	34	+
# chr2	224450765	224451409	NFKB	33	+
```

### Slide 36

O código abaixo é similar aos anteriores, todavia, desta vez o caractere de negação `!` está aplicado a um grupo de instruções. O comando especifica que: para as linhas da coluna 5 que sejam menores de 35 **E** valores da 4ª coluna que não são iguais a `"SREBP1"` *nem* `"SREBP2"`, imprima as linhas.

```bash
awk '$5<35 && !($4=="SREBP1" || $4=="SREBP2")' tfbs.bed

# chr4	47713796	47714292	TAF1	33	+
# chr14	42844745	42844884	GABP	27	+
# chr6	100075411	100076513	STAT1	34	+
# chr2	224450765	224451409	NFKB	33	+
```

### Slide 38

O AWK é capaz de diversas funções, entre elas ele pode realizar operações matemáticas. No código abaixo, os valores da segunda coluna são subtraídos da terceira. Veja que essas operações acontecem entre `{}`. Após a subtração, o `$0` indica que o resultada da operação deve ser **retornado** como uma <span style="color:green">**nova coluna** </span>na **primeira** posição. Se o `$0` fosse **omitido**, <u>apenas</u> a nova coluna seria retornada por padrão. 

```bash
awk '{print $3-$2, $0}' tfbs.bed 

# 100 chr6	31740766	31740866	FOXP2	1000	+
# 396 chrX	105496791	105497187	BCL3	368	+
# 446 chr19	733449	733895	p300	340	+
# 368 chr1	6506253	6506621	USF-1	277	+
# 1148 chr5	124024209	124025357	STAT1	78	+
# 491 chr1	210175342	210175833	TCF12	672	+
# 375 chr10	22650206	22650581	NRSF	44	+
# 208 chr19	53613876	53614084	c-Jun	518	+
# 1212 chr1	1679539	1680751	BAF155	825	+
# 274 chr1	151714434	151714708	FOSL2	664	+
```

### Slide 40

Para **criar** uma nova coluna ou **substituir**, o símbolo de igual `=` funciona como operador de atribuição. 
No exemplo abaixo, o resultado da subtração entre os valores da 3ª e 2ª colunas será armazenado em uma nova coluna (sétima). Além disso, a instrução `print $0` é necessária  para retornar o resultado completo. Alternativamente, apenas `print`também será suficiente. 

```bash
awk '{$7=$3-$2; print $0}' tfbs.bed

# chr6 31740766 31740866 FOXP2 1000 + 100
# chrX 105496791 105497187 BCL3 368 + 396
# chr19 733449 733895 p300 340 + 446
# chr1 6506253 6506621 USF-1 277 + 368
# chr5 124024209 124025357 STAT1 78 + 1148
# chr1 210175342 210175833 TCF12 672 + 491
# chr10 22650206 22650581 NRSF 44 + 375
# chr19 53613876 53614084 c-Jun 518 + 208
# chr1 1679539 1680751 BAF155 825 + 1212
# chr1 151714434 151714708 FOSL2 664 + 274
# [...]
```

O próximo comando **substitui** a sexta coluna, ao invés de criar outra nova. Além disso, veja que a instrução `print` após ponto-vírgula foi utilizada.
:warning:<span style = "color:red">**Atenção**</span>, no caso de substituir, o AWK o fará **sem aviso ou confirmação**. 

```bash
awk '{$6=$3-$2; print}' tfbs.bed

# chr6 31740766 31740866 FOXP2 1000 100
# chrX 105496791 105497187 BCL3 368 396
# chr19 733449 733895 p300 340 446
# chr1 6506253 6506621 USF-1 277 368
# chr5 124024209 124025357 STAT1 78 1148
# chr1 210175342 210175833 TCF12 672 491
# chr10 22650206 22650581 NRSF 44 375
# chr19 53613876 53614084 c-Jun 518 208
# chr1 1679539 1680751 BAF155 825 1212
# chr1 151714434 151714708 FOSL2 664 274
# [...]
```

### Slide 43

O comando abaixo possui apenas uma instrução de imprimir seguida da variável interna `NF`. O AWK atribui o **número de campos** do arquivo a essa variável. Logo, ao solicitar sua impressão, ela mostra o número de campos/colunas por linha. Note que cada linha mostra um número diferente de colunas. Seria um erro? 


```bash
awk '{print NF}' hgmd_brca1.txt

# 16
# 15
# 14
# 18
# 17
# 14
# 13
# 18
# 14
# 13
# [...]
```

**O exemplo abaixo indica que sim.** 
:heavy_exclamation_mark: Lembre-se que, por padrão, o AWK considera espaços e/ou tabulações e/ou finais de linha como delimitador. Como o arquivo é delimitado por tabulações, isso pode ser especificado utilizando o argumento `-F`. 

```bash
awk -F'\t' '{print NF}' hgmd_brca1.txt

# 8
# 8
# 8
# 8
# 8
# 8
# 8
# 8
# 8
# 8
# [...]
```

Veja que o número correto de campos/colunas do arquivo foi mostrado. 

### Slide 46

Ao solicitar a **impressão** da variável `$NF` o AWK irá imprimir o último campo/coluna do arquivo. Veja que sem especificar o delimitador, o resultado funcionou **parcialmente**, todavia, não conte com essa sorte. Parcialmente porque embora os valores estejam corretos, o campo está incompleto, os valores deveriam ser precedidos da fonte `"PubMed 11595708"`, e assim por diante.

```bash
awk '{print $NF}' hgmd_brca1.txt

# Source
# 11595708
# 8807330
# 15235020
# 11802209
# 7894491
# 12491499
# 15235020
# 11748848
# 9544766
# [...]
```

O próximo código simplesmente imprime a **penúltima** coluna. Isso é feito subtraindo 1 da variável `$NF`. Perceba que a operação está entre parênteses. Veja também que o mesmo **problema** anterior ocorre, sem especificar o delimitador, a coluna retornada está incorreta.

```bash
awk '{print $(NF-1)}' hgmd_brca1.txt

# Reference
# PubMed
# PubMed
# PubMed
# PubMed
# PubMed
# PubMed
# PubMed
# PubMed
# PubMed
# [...]
```

### Slide 49

A `$NR` é outra variável que armazena o número de cada linha (ou *record*) no arquivo. O código abaixo imprime esse número em uma **nova coluna** no início `$0 ` do arquivo.

```bash
awk '{print NR,$0}' hgmd_brca1.txt

# 1 Accession Number	HGMD codon change	HGMD amino acid change	HGVS (protein) [...]
# 2 CM014520	ATG-AGG	Met1Arg	M1R [...]
# 3 CM960163	ATGg-ATT	Met1Ile	M1I [...]
# 4 CM041678	ATG-ACG	Met1Thr	M1T [...]
# 5 CM021503	aATG-GTG	Met1Val	M1V [...]
# 6 CM940170	GTA-GCA	Val11Ala	V11A [...]
# 7 CM031646	aCAA-TAA	Gln12Term	Q12X [...]
# 8 CM041679	ATT-ACT	Ile15Thr	I15T [...]
# 9 CM012906	ATG-AAG	Met18Lys	M18K [...]
# 10 CM004187	ATG-ACG	Met18Thr	M18T [...]
# [...] 
```

### Slide 54

```bash
awk -F'\t' 'NR>1{print $6}' hgmd_brca1.txt

```

Para excluir o cabeçalho.

### Slide 56/58

Os múltiplos comandos abaixo foram encadeados para descobrir o índice das colunas e seu nome (primeira linha). Para simplificar, eles serão ilustrados passo-a-passo:

----

Imprima a primeira linha do arquivo com `head`:

```bash
head -1 hgmd_brca1.txt
```

Agora, utilize o utilitário `tr` para **substituir** todos os delimitadores de tabulação `\t` para novas linhas `\n`:

```bash
tr '\t' '\n'
```

Adicione uma coluna na primeira posição do arquivo com o número de linhas:

```bash
awk '{print NR, $0}'
```

**Agora, o comando completo encadeado com os pipes `|`:**

1. O cabeçalho do arquivo é extraído;
2.  as tabulações são substituídas por marcadores de nova linha (transpõe a linha em coluna);
3. o número de cada linha é adicionado à primeira posição do arquivo. 

```bash
head -1 hgmd_brca1.txt | tr '\t' '\n' | awk '{print NR, $0}'

# 1 Accession Number
# 2 HGMD codon change
# 3 HGMD amino acid change
# 4 HGVS (protein)
# 5 HGVS (nucleotide)
# 6 Phenotype
# 7 Reference
# 8 Source
```

A operação anterior é muito útil antes de começar a trabalhar com um arquivo, especialmente se ele for muito grande para ser aberto em um processador de tabelas. Dessa forma, você pode inspecionar quais e quantos campos esse arquivo contém e quais deles você precisar manipular.

