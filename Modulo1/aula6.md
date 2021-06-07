# Módulo 1 - VCF/VCFtools

## Aula 6 - A ferramenta VCFTools  (07/06/2021)

**Prof. Dr.** **Giordano Bruno Soares Souza**

Neste documento estão disponíveis os códigos demonstrados nos slides da aula 6.

A saída dos comandos é representada em forma de comentários (após #).


### Slide 9

```bash
wget http://sourceforge.net/projects/vcftools/files/vcftools_0.1.6.tar.gz/download -O vcftools_0.1.6.tar.gz

tar xzvf vcftools_0.1.6.tar.gz
cd vcftools_0.1.6
make
make install
```

É possível instalar a suíte de aplicativos VCFtools através do download de um arquivo *tarball* (conjunto de arquivos aglutinados através do comando tar e, geralmente, compactados - extensão tar.gz).

O comando `wget` permite realizar o *download* de arquivos a partir de um endereço na internet especificado pelo usuário. No exemplo acima, utilizamos o *link* http://sourceforge.net/projects/vcftools/files/vcftools_0.1.6.tar.gz/download acompanhado pelo parâmetro `-O` que nos permite renomear o arquivo<sup>1</sup>.

O comando `tar xzvf` permite descompactar o arquivo baixado, sendo o significado dos parâmetros: `x` extrair os arquivos; `z` descompactar; `v` imprimir o nome dos arquivos no *shell* e `f` indica o nome do arquivo a ser processado.

O comando `cd` permite trocar o diretório (*change directory*).

Os comandos `make` e `make install` realizarão a instalação do VCFtools. (O comando *make* permite a configuração e a atualização dos arquivos necessários para a instalação, sendo esta efetivamente realizada pelo comando *make install*.)  

> <sup>1</sup>(**Obs.** o parâmetro `-O` permite concatenar diferentes arquivos em único arquivo de saída e não apenas para renomear o arquivo, utilize  apenas quando necessário, não é compulsório).


### Slide 10

```bash
git clone https://github.com/vcftools/vcftools.git  
cd vcftools
./autogen.sh
./configure
make
make install
```
Uma maneira alternativa para instalar o VCFtools envolve o uso do repositório [GitHub](https://docs.github.com/en/github) e da ferramenta para controle de versão [Git](https://git-scm.com/).

O comando `git clone` realiza o *download* dos arquivos associados ao projeto/ferramenta VCFtools.

Os comandos `./autogen.sh` e `./configure` permitem a criação e configuração de trechos do programa a ser instalado e os comandos `make` e `make install` foram sucintamente explicados no *slide* anterior.

> **Obs:** Pode ser necessário poderes de superusuário `sudo` para realizar a instalação.


### Slide 11

```bash
./vcftools

# VCFtools (0.1.16)
# © Adam Auton and Anthony Marcketta 2009

# Process Variant Call Format files

# For a list of options, please go to:
#         https://vcftools.github.io/man_latest.html

# Alternatively, a man page is available, type:
#         man vcftools

# Questions, comments, and suggestions should be emailed to:
#         vcftools-help@lists.sourceforge.net
```

A execução do comando `./vcftools` ou `./vcftools --help` permite verificar se a instalação foi concluída com sucesso. O `./` deve ser utilizado quando o diretório onde se encontra o comando a ser executado não estiver presente no `$PATH` (lista de diretórios onde o sistema busca pelos executáveis). O `./` indica ao sistema para procurar o programa no diretório em que o usuário se encontra (instalação local). 

>**Obs:** Nas aulas não é necessário o uso do `./` pois a instalação do VCFtools foi realizada de maneira global, ou seja, as pastas onde  encontram-se os executáveis estão presentes no `$PATH`.


### Slide 12

```bash
vcftools --vcf snps.vcf

# VCFtools - 0.1.16
# (C) Adam Auton and Anthony Marcketta 2009

# Parameters as interpreted:
#       --vcf populations.snps.vcf

# After filtering, kept 30 out of 30 Individuals
# After filtering, kept 2846 out of a possible 2846 Sites
# Run Time = 0.00 seconds
```

O comando `vcftools --vcf <nome_do_arquivo>` permite ao usuário obter informações básicas sobre o arquivo VCF: número de indivíduos e loci presentes.

Utilize `--vcf` para arquivos VCF não compactados e `--gzvcf` para arquivos compactados.


### Slide 13

```bash
bgzip snps.vcf
tabix -p vcf snps.vcf.gz
ls -lht

# -rw-r--r--  1 giordanob Nativos 415K Jan 25 23:40 snps.vcf.gz
# -rw-r--r--  1 giordanob Nativos  24K Jan 25 23:45 snps.vcf.gz.tbi
```

`bgzip <nome_do_arquivo>` - O comando `bgzip` permite a compactação do arquivo VCF.

> A utilização de outros programas de compactação - tais como `gzip` e `zip` - pode originar erros durante a etapa de indexação.

`tabix -p <formato> <nome_do_arquivo>` - O comando `tabix` permite a indexação do arquivo compactado e a *flag* `-p` indica o formato do arquivo.

`ls -lht` - O comando `ls` lista os arquivos e subdiretórios contidos no diretório, os parâmetros adicionais representam: `-l` formato longo (nome do arquivo e dados adicionais como tipo, tamanho, data e permissões); `-h` apresenta as informações em um formato de fácil leitura para humanos; `-t` ordena os arquivos pelo horário de alteração. Neste exemplo, o comando é utilizado para confirmar que as etapas de compactação e indexação ocorreram conforme o esperado.


### Slide 14

```bash
vcftools --vcf <file> 
	--chr <chrom> / --not-chr <chrom>
	--from-bp <integer> / --to-bp <integer>
	--positions <filename> / --exclude-positions <filename>
	--thin <integer> (distância minima entre loci)
	--bed <filename> --exclude-bed <filename>
	--mask <filename> / --invert-mask <filename> / --mask-min <integer>
```

Filtros baseados na posição das variantes: 

**Comando:** `vcftools --vcf <nome_do_arquivo> --<filtro> <número ou nome_do_arquivo> --recode --out <nome_do_arquivo_saída>`



`--chr` Filtra as variantes presentes no(s) cromossomo(s) indicado(s).

`--not-chr` Filtra as variantes que não estão presentes no(s) cromossomo(s) indicado(s).

`--from-bp <posição_início> / --to-bp <posição_final>` Filtra as variantes presentes entre a posição de início e a posição final.
> Devem ser utilizadas em conjunto com a *flag* `--chr`

`--positions <nome_do_arquivo>` Seleciona as posições listadas no arquivo.
`--exclude-positions <nome_do_arquivo>` Exclui as posições listadas no arquivo.
> A lista de posições deve ser apresentar o cromossomo e a posição separados por tab, uma por linha.

`--thin <inteiro>` Filtra a partir de uma distância mínima entre as variantes.

`--bed <nome_do_arquivo>` e `--exclude-bed <nome_do_arquivo>` Seleciona ou exclui um conjunto de variantes a partir de um arquivo [BED](https://genome.ucsc.edu/FAQ/FAQformat.html#format1)

`--mask <nome_do_arquivo>`, `--invert-mask <nome_do_arquivo>` e `--mask-min <inteiro>` Permitem filtrar o VCF a partir de uma sequência (*fasta-like*) de números.
> No exemplo abaixo, as três primeiras variantes do cromossomo 1 seriam mantidas com `--mask` e excluídas com `--invertmask` 
>`--mask-min` permite indicar o valor de corte para o filtro (0 a 9).
> 
> \>chr1
> 
> 000111222


### Slide 15

```bash
vcftools --gzvcf snps.vcf.gz --chr 61 --from-bp 30 --to-bp 180 --recode --out snps.chr61

# (…)
# After filtering, kept 30 out of 30 Individuals
# After filtering, kept 5 out of a possible 2846 Sites
# Run Time = 0.00 seconds
```

Neste exemplo, são selecionadas todas as variantes do cromossomo 61 entre a posição 30 e a 180.

`--gzvcf snps.vcf.gz` Leitura do arquivo compactado (usar `--vcf` para arquivos não compactados).

`--chr 61` Seleciona apenas as variantes presentes no cromossomo 61.

`--from-bp 30 --to-bp 180` Seleciona as variantes presentes entre as posições 30 e 180.
> Mandatório o uso conjunto com `--chr`.

`--recode` Gera um novo arquivo VCF.
> Obrigatório para a criação de um novo arquivo VCF.

`--out snps.chr61` Nome do arquivo de saída.


### Slide 16

```bash
vcftools --gzvcf snps.vcf.gz --chr 128 --recode -c | bgzip -c > snps.chr128.vcf.gz ; tabix -p vcf snps.chr128.vcf.gz
```

Neste exemplo, demonstra-se como realizar uma sequência de comandos para filtrar e obter um arquivo compactado e indexado, usando uma única linha e sem a necessidade de arquivos intermediários.

`-c` ou `--stdout` Permite redirecionar o *output* para um novo programa.
> O primeiro uso permite redirecionar o *output* de VCFtools diretamente para o `bgzip`; o segundo uso `bgzip -c` permite nomear o *output* deste programa.

`|` Realiza a ligação entre dois comandos, o comando anterior ao *pipe* - `vcftools` - redireciona o *output* para o comando posterior - `bgzip`.

`;` Atua como um separador de comandos permitindo a execução sequencial de comandos, mas não há intercâmbio de informações entre os programas.


### Slide 17

```bash
vcftools --vcf <file> 
	--snp <string> 
	--snps <filename> / --exclude <filename>
	--keep-indels-only / --remove-indels
```

Filtros para variantes:

`--snp` Filtra as variantes de acordo com identificador. Pode ser usado múltiplas vezes.

`--snps <nome_do_arquivo> / --exclude <nome_do_arquivo>` Filtra ou excluí as variantes listadas em um arquivo de texto.
> Um identificador por linha.

`--keep-indels-only / --remove-indels` Mantém ou exclui os indels presentes no arquivo.


### Slide 18

```bash
vcftools --gzvcf indels.eur.22.vcf.gz --remove-indels --recode --out noindels.eur.22

# After filtering, kept 60 out of 60 Individuals
# Outputting VCF file...
# After filtering, kept 101568 out of a possible 102304 Sites
# Run Time = 14.00 seconds
```
Neste exemplo, desejamos excluir as InDels presentes no arquivo `indels.eur.22.vcf.gz` através da *flag* `--remove-indels`.

`--gzvcf indels.eur.22.vcf.gz` Leitura do arquivo compactado

`--remove-indels` Remove as InDels presentes no arquivo `indels.eur.22.vcf.gz`

`--recode` Gera um novo arquivo VCF.

`--out noindels.eur.22` Nomeia o arquivo de saída.

Após a utilização do comando, **736** InDels foram excluídos.


### Slide 19

```bash
vcftools --gzvcf eur.22.vcf.gz \
--snps chr22.100rs.txt --recode \
--out snps100.eur.22 

# After filtering, kept 60 out of 60 Individuals
# Outputting VCF file...
# After filtering, kept 100 out of a possible 101568 Sites
# Run Time = 0.00 seconds
```

Neste exemplo, desejamos filtrar 100 SNPs listados no arquivo `chr22.100rs.txt`.

`--gzvcf snps.vcf.gz` Leitura do arquivo compactado

`--snps chr22.100rs.txt` Filtra as variantes listadas no arquivo `chr22.100rs.txt`

`--recode` Gera um novo arquivo VCF.

`--out snps100.eur.22` Nomeia o arquivo de saída.


### Slide 20

```bash
vcftools --vcf <file> 
	--maf <float> / --max-maf <float>
	--mac <int> / --max-mac <int>
	--min-alleles <integer> / --max-alleles <integer>
	--non-ref-af <float> / --max-non-ref-af / --non-ref-af-any / --max-non-ref-af-any
	--non-ref-ac <integer> / --max-non-ref-ac / --non-ref-ac-any / --max-non-ref-ac-any
```

Filtros para alelos

`--maf <decimal<sup>1</sup>> / --max-maf <decimal>` Filtros baseados na frequência relativa do alelo menos comum. `--maf` <= Frequência relativa <= `--max-maf`

`--mac <inteiro> / --max-mac <inteiro>` Filtros baseados na frequência absoluta do alelo menos comum. `--mac` <= Frequeência absoluta <= `--max-mac`

`--min-alleles <inteiro> / --max-alleles <inteiro>` Filtros baseados no número de alelos de uma variante. `--min-alleles` <= Número de alelos <= `--max-alleles`

`--non-ref-af <decimal> / --max-non-ref-af <decimal>` Filtros baseados na frequência relativa do(s) alelo(s) alternativo(s) (não-referência). `--non-ref-af` <= Freq. Rel. <= `--max-non-ref-af`
> Todos os alelos alternativos devem satisfazer o critério de filtragem.

`--non-ref-af-any <decimal> / --max-non-ref-af-any <decimal>` Filtros baseados na frequência relativa de ao menos um alelo alternativo. `--non-ref-af-any` <= Freq. Rel. <= `--max-non-ref-af-any`
> Apenas um dos alelos alternativos deve satisfazer o critério de filtragem.

`--non-ref-ac <inteiro> / --max-non-ref-ac <inteiro>` Filtros baseados na frequência absoluta do(s) alelo(s) alternativo(s) (não-referência). `--non-ref-ac` <= Freq. Rel. <= `--max-non-ref-ac`
> Todos os alelos alternativos devem satisfazer o critério de filtragem.

`--non-ref-ac-any <inteiro> / --max-non-ref-ac-any <inteiro>` Filtros baseados na frequência absoluta de ao menos um alelo alternativo. `--non-ref-ac-any` <= Freq. Rel. <= `--max-non-ref-ac-any`
> Apenas um dos alelos alternativos deve satisfazer o critério de filtragem.

> <sup>1</sup>Por simplicidade denota-se *float* como um valor decimal, entretanto, o conceito de *float* é mais complexo e não será abordado neste momento.


### Slide 21

```bash
vcftools --gzvcf eur.22.vcf.gz --maf 0.05 --recode --out maf005.eur.22

# After filtering, kept 60 out of 60 Individuals
# Outputting VCF file...
# After filtering, kept 73176 out of a possible 101568 Sites
# Run Time = 12.00 seconds
```

Neste exemplo, deseja-se selecionar variantes nas quais o alelo menos comum possua frequência relativa maior ou igual à 0,05.

`--gzvcf eur.22.vcf.gz` Leitura do arquivo compactado

`--maf 0.05` Filtra as variantes comuns, ou seja, onde a frequência do alelo menos comum é maior ou igual à 0,05.

`--recode` Gera um novo arquivo VCF.

`--out maf005.eur.22` Nomeia o arquivo de saída.

> Ao final, 73.176 variantes com MAF maior ou igual à 0,05 foram mantidas e 28.392 foram excluídas.


### Slide 22

```bash
vcftools --gzvcf eur.22.vcf.gz \
--min-alleles 2 --max-alleles 2 --recode \
--out biallelic.eur.22 

# After filtering, kept 60 out of 60 Individuals
# Outputting VCF file...
# After filtering, kept 77848 out of a possible 77867 Sites
# Run Time = 14.00 seconds
```

Neste exemplo, deseja-se selecionar variantes bialélicas.

`--gzvcf eur.22.vcf.gz` Leitura do arquivo compactado

`--min-alleles 2` Filtra as variantes com dois ou mais alelos.

`--max-alleles 2` Filtra as variantes com dois ou menos alelos.
> O valor **2** é o único a atender aos dois filtros que estão ativos: `min-alleles` e `max-alleles`. Dessa forma, só serão selecionadas variantes com dois alelos.  

`--recode` Gera um novo arquivo VCF.

`--out biallelic.eur.22` Nomeia o arquivo de saída.

> O resultado indica a exclusão de 19 variantes monomórficas ou com três ou mais alelos.


### Slide 23

```bash
vcftools --vcf <file>
	--min-mean-DP <float> / --max-mean-DP <float>
	--hwe <float>
	--max-missing <float>
	--max-missing-count <integer>
	--phased
	--minQ
```

Filtros baseados em genótipos

`--min-mean-DP <decimal> / --max-mean-DP <decimal>` Filtros baseados na profundidade média do sequenciamento. `--min-mean-DP`<= Profundidade Média <= `--max-mean-DP`

`--hwe <decimal>` Calcula o Equilíbrio de [Hardy-Weinberg](https://pt.wikipedia.org/wiki/Equil%C3%ADbrio_de_Hardy-Weinberg) e exclui os loci para os quais o p-valor do teste foi inferior ao especificado pelo usuário.
	
`--max-missing <decimal>` Indica a proporção máxima de dados ausentes estipulada pelo usuário. O valor é calculado para cada variante e aquelas apresentando valor superior ao definido são excluídas.

`--max-missing-count <inteiro>` Indica a contagem máxima de dados ausentes estipulada pelo usuário. O valor é calculado para cada variante e aquelas apresentando valor superior ao definido são excluídas.

`--phased` Exclui variantes para as quais a [fase](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3753045/) não está determinada.

`--minQ <decimal>` Seleciona apenas variantes com valores de qualidade superior ao estipulado.


### Slide 24

```bash
vcftools --gzvcf snps.vcf.gz --min-meanDP 10 --hwe 0.05 --max-missing 0.1 --recode --out qc.snps

# After filtering, kept 30 out of 30 Individuals
# Outputting VCF file...
# After filtering, kept 324 out of a possible 2846 Sites
# Run Time = 0.00 seconds
```

Neste exemplo, deseja-se simular um controle de qualidade e selecionar variantes: 1) Profundidade de sequenciamento de ao menos 10x; 2) Sob o Equilíbrio de Hardy-Weinberg (p-valor de corte = 0.05); 3) quantidade máxima de dados ausentes de 10% (por locus).

`--gzvcf eur.22.vcf.gz` Leitura do arquivo compactado

`--min-meanDP 10` Filtra os sítios com profundidade de sequenciamento maior ou igual à 10.

`--hwe 0.05` Exclui variantes onde o p-valor do teste E-HW é menor do que 0,05.

`--max-missing 0.1` Exclui variantes com 10% ou mais de dados ausentes.

`--recode` Gera um novo arquivo VCF.

`--out qc.snps` Nomeia o arquivo de saída.

> A partir dos filtros aplicados, foram mantidas 324 variantes.


### Slide 25

```bash
vcftools --vcf <file>
	--remove-INFO <string> / --keep-INFO <string>
	--remove-filtered <string> / --keep-filtered <string>
	--remove-filtered-all (PASS)
```
Fitros baseados nos metadados (anotações) contidos nas colunas `INFO` e `FILTER`

`--remove-INFO <caracteres> / --keep-INFO <caracteres>` Exclui `--remove-INFO` ou seleciona `--keep-INFO` variantes associadas ao metadado.
> O filtro é baseado na presença do metadado, mas não no valor (nos casos onde a anotação é representada por uma chave associada à um valor).
	
`--remove-filtered <caracteres> / --keep-filtered <caracteres>` Exclui `--remove-filtered` ou seleciona `--keep-filtered` variantes associadas à um filtro.
	
`--remove-filtered-all (PASS)` Remove todas as variantes para as quais o valor do campo FILTER seja diferente de *PASS*.


### Slide 26

```bash
vcftools --gzvcf eur.22.vcf.gz --keep-INFO HM3 --recode --out hm3.eur.22

# After filtering, kept 60 out of 60 Individuals
# Outputting VCF file...
# After filtering, kept 15071 out of a possible 101568 Sites
# Run Time = 1.00 seconds
```

Neste exemplo, deseja-se selecionar apenas as variantes associadas ao metadado HM3.

`--gzvcf eur.22.vcf.gz` Leitura do arquivo compactado

`--keep-INFO HM3` Seleciona apenas as variantes que apresentam a informação HM3 no campo `INFO`

`--recode` Gera um novo arquivo VCF.

`--out hm3.eur.22` Nomeia o arquivo de saída.

> Ao final, 15.071 variantes associadas ao metadado HM3 foram mantidas.


### Slide 27

```bash
vcftools --vcf <file>
	--indv <string> / --remove-indv <string>
	--keep <filename>
	--remove <filename>
	--max-indv <integer>
```

Filtros baseados em indivíduos

`--indv <caracteres> / --remove-indv <caracteres>` Seleciona `--indv` ou exclui `--remove-indv` indivíduos de acordo com a identificação dos mesmos.
> Pode ser utilizado múltiplas vezes. O filtro `--indv` é aplicado antes do `--remove-indv`.
	
`--keep <nome_do_arquivo> / --remove <nome_do_arquivo>` Seleciona `--keep` ou exclui `--remove` indivíduos presentes em um arquivo. A lista necessita deve ter um único indivíduo por linha.
> Podem ser usados em conjunto. O filtro `--keep` é aplicado antes do `--remove`.

`--max-indv <inteiro>` Seleciona, aleatoriamente, uma quantidade `N` de indivíduos.


### Slide 28

```bash
vcftools --gzvcf eur.22.vcf.gz --max-indv 30 --recode --out 30ind.eur.22

# Filtering Individuals Randomly
# After filtering, kept 30 out of 60 Individuals
# Outputting VCF file...
# After filtering, kept 101568 out of a possible 101568 Sites
# Run Time = 9.00 seconds
```

Neste exemplo, deseja-se selecionar apenas as variantes associadas ao metadado HM3.

`--gzvcf eur.22.vcf.gz` Leitura do arquivo compactado

`--max-indv 30` Seleciona 30 indivíduos aleatoriamente

`--recode` Gera um novo arquivo VCF.

`--out 30ind.eur.22` Nomeia o arquivo de saída.

> Ao final, 30 indivíduos selecionados aleatoriamente foram mantidos.


### Slide 29

```bash
vcftools --vcf <file> --diff <file> / --gzvcf <file> --gzdiff <file>
	--diff-site
	--diff-indv
	--diff-site-discordance
	--diff-indv-discordance
	--diff-indv-map <filename> (ex. Sample1_Seq1   Sample1_Seq2)
	--diff-discordance-matrix
	--diff-switch-error (erros de fase)
```
Comparando dois arquivos VCFs

Para comparar dois arquivos VCFs é necessário usar os parâmetros `--vcf` e `--diff` (ou `--gzvcf`e `--gzdiff`, para as versões compactadas) e utilizar umas das opções de comparação disponíveis.

Estrutura: `vcftools --vcf <nome_do_arquivo_1> --diff <nome_do_arquivo_2> --diff-<opção> --out <nome_arquivo_saída>`

`--diff-site` Identifica as variantes que são únicas e comuns aos dois arquivos.

`--diff-indv`  Identifica os indivíduos que são únicas e comuns aos dois arquivos.
	
`--diff-site-discordance` Calcula a discordância entre as variantes, base por base.
	
`--diff-indv-discordance` Calcula a discordância entre os indivíduos.
	
`--diff-indv-map <nome_do_arquivo>` Permite realizar o mapeamento de indivíduos entre dois arquivos VCF. O arquivo com o mapeamento dos códigos deve conter uma correspondência por linha, separada por tabulação (ex. Amostra1_Codigo1	Amostra1_Codigo2).
	
`--diff-discordance-matrix` Calcula uma matrix de discordância entre os dois arquivos.
> Apenas para loci bialélicos e para os quais os alelos sejam os mesmos nos dois arquivos.
	
`--diff-switch-error` Estima [erros de fase](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3415548/) (ou troca de fita)


### Slide 30

```bash
vcftools --gzvcf 30ind.eur.22.recode.vcf.gz \
--gzdiff 30ind.asia.22.recode.vcf.gz \
--diff-site --out eur_asia_sites_diff

# Comparing sites in VCF files...
# Found 59122 sites common to both files.
# Found 42446 sites only in main file.
# Found 18745 sites only in second file.
# Found 0 non-matching overlapping sites.
# After filtering, kept 101568 out of a possible 101568 Sites
# Run Time = 3.00 seconds
```
Neste exemplo, deseja-se identificar as variantes únicas e comuns aos arquivos `30ind.eur.22.recode.vcf.gz` e `30ind.asia.22.recode.vcf.gz`

`--gzvcf eur.22.vcf.gz` Leitura do primeiro arquivo compactado

`--gzdiff` Leitura do segundo arquivo compactado

`--diff-site` Identifica e estima a quantidade de loci únicos e comuns aos arquivos VCFs.

`--out eur_asia_sites_diff` Nomeia o arquivo de saída.

> Ao final, foram identificados 59.122 loci comuns aos dois arquivos, 42.446 loci presentes apenas no primeiro arquivo `30ind.eur.22.recode.vcf.gz` e 18.745 loci presentes apenas no segundo arquivo `30ind.asia.22.recode.vcf.gz`. 


### Slide 31

```bash
vcftools --vcf <file>
	--freq
	--counts
	--derived (dependente do alelo ancestral)
```

Estatísticas relativas à frequência alélica

`--freq` Calcula a frequência alélica relativa.

`--freq2` Calcula a frequência alélica relativa, sem imprimir outras informações relativas aos alelos.

`--counts` Calcula a frequência alélica absoluta.

`--counts2` Calcula a frequência alélica absoluta, sem imprimir outras informações relativas aos alelos.

`--derived` Deve ser utilizada em conjunto com alguma das quatro opções anteriores; as frequências são estimadas e organizadas com base no alelo ancestral (este deve estar especificado com a anotação `AA` e alelo ancestral no campo `INFO`.


### Slide 32

```bash
vcftools --gzvcf eur.22.vcf.gz --freq --derived --out eur.22.frq
 
# After filtering, kept 60 out of 60 Individuals
# Outputting Frequency Statistics...
#         Warning: Cannot output derived allele frequencies without Ancestral Alleles (AA)
# After filtering, kept 101568 out of a possible 101568 Sites
# Run Time = 2.00 seconds
```

Neste exemplo, deseja-se identificar as variantes únicas e comuns aos arquivos `30ind.eur.22.recode.vcf.gz` e `30ind.asia.22.recode.vcf.gz`

`--gzvcf eur.22.vcf.gz` Leitura do primeiro arquivo compactado

`--freq` Estima a frequência alélica relativa para cada locus.

`--derived` As frequências alélicas são organizadas de acordo com a informação do alelo ancestral.

`--out eur.22.frq` Nomeia o arquivo de saída.

> A frequência alélica relativa foi calculada para os 101.568 loci, entretanto um aviso informa que a falta de informação sobre o alelo ancestral não permite a aplicação da *flag* `--derived`. 


### Slide 33

```bash
vcftools --vcf <file>
	--depth (por indivíduo)
	--site-depth (por sítio)
	--site-mean-depth (média por sítio)
	--geno-depth (por genótipo)
```

Estatísticas relativas à profundidade de sequenciamento

`--depth` Estima a profundidade média por indivíduo.

`--site-depth` Estima a profundidade por posição a partir da soma de todos os indivíduos.
	
`--site-mean-depth` Estima a profundidade média por posição a partir de todos os indivíduos.
	
`--geno-depth` Estima a profundidade por genótipo a partir de todos os indivíduos. 


### Slide 34

```bash
vcftools --gzvcf eur.22.vcf.gz --depth --out eur.22.depth 

# After filtering, kept 60 out of 60 Individuals
# Outputting Mean Depth by Individual
# After filtering, kept 101568 out of a possible 101568 Sites
# Run Time = 3.00 seconds
```

Neste exemplo, deseja-se calcular a profundidade média por indivíduo.

`--gzvcf eur.22.vcf.gz` Leitura do arquivo VCF compactado

`--depth` Calcula a profundidade média por indivíduo.

`--out eur.22.depth` Nomeia o arquivo de saída.


### Slide 35

```bash
vcftools --vcf <file>
	--hap-r2 (r2, D, D’)
	--geno-r2 (plink-like)
	--geno-chisq (> 2 alelos)
	--hap-r2-positions <lista de posições> / --geno-r2-positions <lista>
	--ld-window <int> (nº SNPs) / --ld-window-bp <int> (nº de pares de bases)
	--min-r2 <float>
```

Estatísticas relativas ao [desequilíbrio de ligação](https://www.nature.com/articles/nrg2361) (DL).

`--hap-r2` Calcula o desequilíbrio de ligação baseando-se na informação de fase. São calculadas as estatísticas [r<sup>2</sup>, D e D'.](https://academic.oup.com/bib/article-pdf/5/4/355/738693/355.pdf)

`--geno-r2` Calcula o desequilíbrio de ligação entre genótipos. É calculada a estatística r<sup>2</sup>.
> D e D' podem ser calculadas, mas estão disponíveis apenas para genótipos em fase.

`--geno-chisq` A partir do qui-quadrado. permite calcular a independência entre genótipos para variantes com mais de dois alelos.

`--hap-r2-positions <lista_de_posições>` Estima o desequilíbrio de ligação entre as variantes presentes em uma lista e as demais presentes no arquivo VCF.

`--geno-r2-positions <lista_de_posições>` Estima o desequilíbrio de ligação entre os genótipos das variantes presentes em uma lista e os das demais presentes no arquivo VCF.

`--ld-window <int>` Estipula uma quantidade máxima de SNVs entre os SNVs a serem utilizados para o cálculo do DL.

`--ld-window-bp <int>` Estipula um limite máximo de distância (em pares de bases) entre os SNVs para o cálculo do DL.

`--ld-window-min <int>` Estipula uma quantidade mínima de SNVs entre os SNVs a serem utilizados para o cálculo do DL.

`--ld-window-bp-min <int>` Estipula um limite mínimo de distância (em pares de bases) entre os SNVs para o cálculo do DL.

`--min-r2 <decimal> ` Define um valor mínimo de r<sup>2</sup> para que o programa imprima os resultados.

`--interchrom-hap-r2 / --interchrom-geno-r2` Permitem o cálculo de DL para variantes em cromossomos distintos.


### Slide 36

```bash
vcftools --gzvcf eur.22.vcf.gz --hap-r2 --out eur.22.ld 

# After filtering, kept 60 out of 60 Individuals
# Outputting Pairwise LD (phased bi-allelic only)
# After filtering, kept 101568 out of a possible 101568 Sites
# Run Time =
```

Neste exemplo, calcula-se o desequilíbrio de ligação para todas as variantes do arquivo de entrada.

`--gzvcf eur.22.vcf.gz` Leitura do primeiro arquivo compactado

`--hap-r2` Estima o desequilíbrio de ligação levando em conta a fase dos alelos.

`--out eur.22.ld` Nomeia o arquivo de saída.

> As estatísticas de desequilíbrio de ligação, em geral, consumem muito tempo de processamento e geram arquivos de saída grandes, por esse motivo, essa análise não será finalizada durante as aulas. Caso tenha interesse em realizar essa análise em outro momento e o VCF a ser utilizado contenha mais do que algumas centenas de SNVs, é aconselhável utilizar as funções [`screen`](https://www.gnu.org/software/screen/) ou [`nohup`](https://en.wikipedia.org/wiki/Nohup) para correr a análise.


### Slide 37

```bash
vcftools --vcf <file>
	--TsTv <integer> (tamanho do bin, loci bialélicos)
	--TsTv-summary
	--TsTv-by-count
	--TsTv-by-qual
```

Estatísticas de Transição e Transversão

`--TsTv <inteiro>` Calcula a proporção de transições/transversões em conjuntos de tamanho definido pelo usuário.
> Apenas para loci bialélicos.

`--TsTv-summary` Calcula um resumo sobre a quantidade transições e transversões.

`--TsTv-by-count` Calcula a proporção de transições/transversões em função da contagem do alelo alternativo.
> Apenas para loci bialélicos.

`--TsTv-by-qual` Calcula a proporção de transições/transversões em função de limiares de qualidade dos SNPs.

`--FILTER-summary` Calcula um sumário de transições e transversões para cada categoria de `FILTER`.


### Slide 38

```bash
vcftools --gzvcf eur.22.vcf.gz --TsTv-summary --out eur.22.tstv

# After filtering, kept 60 out of 60 Individuals
# Outputting Ts/Tv summary
# Ts/Tv ratio: 2.265
# After filtering, kept 101568 out of a possible 101568 Sites
# Run Time = 1.00 seconds
```

Neste exemplo, obtemos um sumário do cálculo de todos os eventos de transição (Ti) e transversão (Tv).

`--gzvcf eur.22.vcf.gz` Leitura do primeiro arquivo compactado

`--TsTv-summary` Identifica os eventos de transição e transversão e imprime um sumário destes cálculos.

`--out eur.22.tstv` Nomeia o arquivo de saída.

> Nesse conjunto de dados, a proporção média de transições/transversões foi de 2,265, valor próximo ao esperado no genoma humano (esse valor pode variar em outras espécies e tipo de dado, por ex., aproximadamente 3 para exomas). A proporção de Ti/Tv pode ser utilizada na validação de polimorfismos [(ver mais)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4308666/).


### Slide 39

```bash
vcftools --vcf <file>
	--relatedness / --relatedness2  
	--missing-indv
	--missing-site
	--singletons (mapeamento, posição e indivíduo)
```

Estatísticas genético-populacionais (Parte 1)

`--relatedness` Calcula a estatística [Ajk](https://www.nature.com/articles/ng.608) que infere o grau de parentesco entre os indivíduos a partir do grau de compartilhamento genético.
> Valores próximos a zero, indicam a inexistência de parentesco, o valor de 1 indica total compartilhamento genético (um indivíduo consigo mesmo).

`--relatedness2` Calcula o [coeficiente de parentesco](https://academic.oup.com/bioinformatics/article/26/22/2867/228512).

`--missing-indv` Gera um relatório sobre a ausência de dados genotípicos para cada indivíduo.

`--missing-site` Gera um relatório sobre a ausência de dados genotípicos para cada locus.

`--singletons` Gera um relatório informando a localização genômica e os indivíduos onde *singletons* são encontrados.
> Reporta *singletons* e *dubletons*


### Slide 40

```bash
vcftools --gzvcf eur.vcf.gz --missing-indv --out eur.22.missing

# After filtering, kept 60 out of 60 Individuals
# Outputting Individual Missingness
# After filtering, kept 101568 out of a possible 101568 Sites
# Run Time = 2.00 seconds
```

Neste exemplo, intenta-se estimar a proporção de dados ausentes em cada um dos indivíduos do conjunto de dados.

`--gzvcf eur.22.vcf.gz` Leitura do primeiro arquivo compactado

`--missing-indv` Estima a proporção de dados ausentes por indivíduo.

`--out eur.22.missing` Nomeia o arquivo de saída.

> No relatório gerado, nenhum indivíduo apresentava alta proporção de dados ausentes.



### Slide 41

```bash
vcftools --gzvcf eur.vcf.gz --relatedness --out eur.22.relatedness

# After filtering, kept 60 out of 60 Individuals
# Outputting Individual Relatedness
		# Relatedness: Only using biallelic sites.
# After filtering, kept 101568 out of a possible 101568 Sites
# Run Time = 5.00 seconds
```

Neste exemplo, é calculada a estatística Ajk que nos permite estimar o grau de compartilhamento genético entre dois indivíduos e, assim, inferir o grau de parentesco.

`--gzvcf eur.22.vcf.gz` Leitura do primeiro arquivo compactado

`--relatedness` Calcula a estatística Ajk (compartilhamento genético).

`--out eur.22.relatedness` Nomeia o arquivo de saída.

> Nenhuma estimativa entre dois indivíduos apresenta altos valores de AjK, o que nos permite concluir que não há relação de parentesco nesta amostra.


### Slide 42

```bash
vcftools --vcf <file>
	--weir-fst-pop <filename> (lista de indíviduos de uma população)  
	--fst-window-size <int> / --fst-window-step <int>
	--het
	--hardy
	--LROH
```

Estatísticas genético-populacionais (Parte 2)

`--weir-fst-pop <lista_de_individuos>` Realiza o cálculo do F<sub>ST</sub> (Weir e Cockerham, 1984) por variante. O parâmetro `--weir-fst-pop` pode ser utilizado múltiplas vezes, um por população.
> O F<sub>ST</sub> permite calcular uma estimativa de diferenciação genética entre populações a partir das frequências alélicas.

`--fst-window-size <int>` Utilizado em conjunto com `--weir-fst-pop`, o F<sub>ST</sub> será calculado por janela de tamanho a ser definido pelo usuário.
	
`--fst-window-step <int>` Utilizado em conjunto com `--weir-fst-pop`, indica o tamanho dos passos entre as janelas para o cálculo do F<sub>ST</sub>.

`--het` Estima a heterozigosidade média por indivíduo e coeficiente de endocruzamento (F).

`--hardy` Calcula o p-valor do teste do Equilíbrio de Hardy-Weinberg para cada variante.

`--LROH` Identifica trechos em homozigose nos indivíduos (*Long runs of homozigosity*).


### Slide 43

```bash
vcftools --gzvcf eur.vcf.gz --hardy --out eur.22.hardy

# After filtering, kept 60 out of 60 Individuals
# Outputting HWE statistics (but only for biallelic loci)
#         HWE: Only using biallelic SNPs.
# After filtering, kept 101568 out of a possible 101568 Sites
# Run Time = 5.00 seconds
```

Neste exemplo, para cada sítio é estimado o p-valor do teste exato para cálculo do Equilíbrio de Hardy-Weinberg.

`--gzvcf eur.22.vcf.gz` Leitura do primeiro arquivo compactado

`--hardy` Realiza o cálculo do teste para o Equilíbrio de Hardy-Weinberg e gera um relatório para cada variante.

`--out eur.22.hardy` Nomeia o arquivo de saída.

> Além do p-valor para cada teste realizado, o relatório gerado também apresenta os números observados e esperados de homozigotos e heterozigtos.



### Slide 44

```bash
vcftools --vcf <file>
	--012
	--IMPUTE
	--ldhat / --ldhat-geno
	--BEAGLE-GL / --BEAGLE-PL
	--plink / --plink-tped / --chrom-map
```

Formatos de saída/ Conversão de formatos

`--012` É impressa uma matriz de genótipos (indivíduos x variantes). Os genótipos são representados por 0, 1 ou 2 (estes números representam a contagem de alelos não-referência). Dois arquivos adicionais são gerados: `.012.indv` representa a lista de indivíduos e `.012.pos` representa a lista de posições. Dados ausentes são representados por -1.

`--IMPUTE` Imprime os dados no formato de painel de referência do programa IMPUTE. Requer dados em fase.

`--ldhat` Imprime os dados no formato requirido pelo programa LDhat. Requer dados em fase e o uso da *flag* `--chr`.

`--ldhat-geno` Imprime os dados no formato requirido pelo programa LDhat. Requer o uso da *flag* `--chr`. Os dados não necessitam estar em fase.

`--BEAGLE-GL` Imprime os dados no formato utilizado pelo programa BEAGLE. Requer o uso da *flag* `--chr` e a anotação `GL` (*genotype likelihood*) no campo `FORMAT`. 

`--BEAGLE-PL` Imprime os dados no formato utilizado pelo programa BEAGLE. Requer o uso da *flag* `--chr` e a anotação `PL` (*phred-scaled genotype likelihoods*) no campo `FORMAT`.

`--plink` Imprime os dados no formato plink (ped, map).

`--plink-tped` Imprime os dados no formato plink transposto (tped, tfam).

`--chrom-map` Permite mapear nomes de cromossomos não-numéricos a um número desejado, um por linha, separado por tabulação (ex. scaffold12	12).


### Slide 45

```bash
vcftools --gzvcf eur.22.vcf.gz --plink --out eur.22.plink

# After filtering, kept 60 out of 60 Individuals
# Writing PLINK PED and MAP files ...
#         PLINK: Only outputting biallelic loci.
# Done.
# After filtering, kept 101568 out of a possible 101568 Sites
# Run Time = 5.00 seconds
```

Neste exemplo, deseja-se converter o formato VCF ao formato ped/map do programa de epidemiologia genética [plink](http://zzz.bwh.harvard.edu/plink/).

`--gzvcf eur.22.vcf.gz` Leitura do primeiro arquivo compactado

`--plink` Imprime os dados no formato ped/map do *software* plink.

`--out eur.22.plink` Nomeia o arquivo de saída.

> Ao final, são gerados dois arquivos: 1) arquivo PED que contém informações sobre os indivíduos nas primeiras 6 colunas e os genótipos nas demais); e 2) o arquivo MAP, com informações sobre as variantes, tais como, cromossomo, identificador, distância genética e posição.


### Slide 46

```bash
vcf-merge <file1> <file2> | bgzip -c > <output>
```

Rotina para unir dois arquivos VCF

Esse é um dos scritps em Perl que fazem parte da suíte VCFtools. 
> [Clique aqui](https://vcftools.github.io/perl_module.html) para conhecer mais scripts do módulo em Perl e [aqui](https://vcftools.github.io/perl_examples.html) para ver exemplos de uso.

> Para realizar a união dos dois arquivos é necessário que ambos VCF estejam compactados e indexados.


### Slide 47

```bash
vcf-merge eur.22.15indv.vcf.gz asia.22.15indv.vcf.gz \
| bgzip -c > eur_asia.22.vcf.gz
```

Neste exemplo, deseja-se unir dois arquivos VCF. É indispensável que ambos estejam compactados e indexados.

`vcf-merge eur.22.15indv.vcf.gz asia.22.15indv.vcf.gz` Indica os dois arquivos a serem mesclados.

`| bgzip ` Redireciona a saída do *script* `vcf-merge` para o programa `bgzip` que irá realizar a compactação, 

`-c > eur_asia.22.vcf.gz` Nomeia o arquivo resultante da mescla.

