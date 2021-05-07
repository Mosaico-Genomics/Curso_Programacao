# Módulo 1 - VCF/VCFtools

## Aula 6 - A ferramenta VCFTools  (07/06/2021)

**Prof. Dr.** **Giordano Bruno Soares Souza**

Neste documento estão disponíveis os códigos demonstrados nos slides da aula 6.

A saída dos comandos é representada em forma de comentários (após #).

### Slide 9

```bash
wget http://sourceforge.net/projects/vcftools/files/vcftools_0.1.6.tar.gz/download –O vcftools_0.1.6.tar.gz

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
tabix –p vcf snps.vcf.gz
ls –lht

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
> No exemplo abaixo, as três primeiras variantes do cromossomo 1 seriam mantidas com `--mask` e excluídas com `--invertmask`; 
>`--mask-min` permite indicar o valor de corte para o filtro (0 a 9).
> 
> \>chr1
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
vcftools --gzvcf snps.vcf.gz --chr 128 --recode -c | bgzip -c > snps.chr128.vcf.gz ; tabix –p vcf snps.chr128.vcf.gz
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
--out snps100.eur.22.vcf 

# After filtering, kept 60 out of 60 Individuals
# Outputting VCF file...
# After filtering, kept 100 out of a possible 101568 Sites
# Run Time = 0.00 seconds
```

Neste exemplo, desejamos filtrar 100 SNPs listados no arquivo `chr22.100rs.txt`.

`--gzvcf snps.vcf.gz` Leitura do arquivo compactado
`--snps chr22.100rs.txt` Filtra as variantes listadas no arquivo `chr22.100rs.txt`
`--recode` Gera um novo arquivo VCF.
`--out snps.chr61` Nomeia o arquivo de saída.


### Slide 20

```bash
vcftools --vcf <file> 
	--maf <float> / --max-maf <float>
	--mac <float> / --max-mac <float>
	--min-alleles <integer> / --max-alleles <integer>
	--non-ref-af <float> / --max-ref-af / --non-ref-af-any / --max-ref-af-any
	--non-ref-ac <integer> / --max-ref-ac / --non-ref-ac-any / --max-ref-ac-any
```



### Slide 21

```bash
vcftools --gzvcf eur.22.vcf.gz --maf 0.05 --recode --out maf005.eur.22

# After filtering, kept 60 out of 60 Individuals
# Outputting VCF file...
# After filtering, kept 73176 out of a possible 101568 Sites
# Run Time = 12.00 seconds
```



### Slide 22

```bash
vcftools --gzvcf eur.22.vcf.gz \
--min-alleles 2 --max-alleles 2 --recode \
--out biallelic.eur.22.vcf 

# After filtering, kept 60 out of 60 Individuals
# Outputting VCF file...
# After filtering, kept 77848 out of a possible 77867 Sites
# Run Time = 14.00 seconds
```



### Slide 23

```bash
vcftools --vcf <file>
	--min-mean-DP <float> / --max-mean-DP <float>
	--hwe <float>
	--max-missing <float>
	--max-missing-count <integer>
	--phased
	--minGQ
```

### Slide 24

```bash
vcftools --vcf snps.vcf --min-meanDP 10 --hwe 0.05 --max-missing 0.1 --recode --out qc.snps

# After filtering, kept 30 out of 30 Individuals
# Outputting VCF file...
# After filtering, kept 324 out of a possible 2846 Sites
# Run Time = 0.00 seconds
```

### Slide 25

```bash
vcftools --vcf <file>
	--remove-INFO <string> / --keep-INFO <string>
	--remove-filtered <string> / --keep-filtered <string>
	--remove-filtered-all (PASS)
```

### Slide 26

```bash
vcftools --gzvcf eur.22.vcf.gz --keep-INFO HM3 --recode --out hm3.eur.22

# After filtering, kept 60 out of 60 Individuals
# Outputting VCF file...
# After filtering, kept 15071 out of a possible 101568 Sites
# Run Time = 1.00 seconds
```

### Slide 27

```bash
vcftools --vcf <file>
	--indv <string> / --remove-indv <string>
	--keep <filename>
	--remove <filename>
	--max-indv <integer>
```

### Slide 28

```bash
vcftools --gzvcf eur.22.vcf.gz --max-indv 30 --recode --out 30ind.eur.22

# Filtering Individuals Randomly
# After filtering, kept 30 out of 60 Individuals
# Outputting VCF file...
# After filtering, kept 101568 out of a possible 101568 Sites
# Run Time = 9.00 seconds
```

### Slide 29

```bash
vcftools --vcf <file> --diff <file>
	--diff-site
	--diff-indv
	--diff-site-discordance
	--diff-indv-discordance
	--diff-indv-map <filename> (ex. Sample1_Seq1   Sample1_Seq2)
	--diff-discordance-matrix
	--diff-switch-error (erros de fase)
```

### Slide 30

```bash
vcftools --gzvcf 30ind.eur.22.recode.vcf \
--diff 30ind.asia.22.recode.vcf \
--diff-site --out eur_asia_sites_diff

# Comparing sites in VCF files...
# Found 59122 sites common to both files.
# Found 42446 sites only in main file.
# Found 18745 sites only in second file.
# Found 0 non-matching overlapping sites.
# After filtering, kept 101568 out of a possible 101568 Sites
# Run Time = 3.00 seconds
```

### Slide 31

```bash
vcftools --vcf <file>
	--freq
	--counts
	--derived (dependente do alelo ancestral)
```

### Slide 32

```bash
vcftools --gzvcf eur.22.vcf.gz --freq --derived --out eur.22.frq
 
# After filtering, kept 60 out of 60 Individuals
# Outputting Frequency Statistics...
#         Warning: Cannot output derived allele frequencies without Ancestral Alleles (AA)
# After filtering, kept 101568 out of a possible 101568 Sites
# Run Time = 2.00 seconds
```

### Slide 33

```bash
vcftools --vcf <file>
	--depth (por indivíduo)
	--site-depth (por sítio)
	--site-mean-depth (média por sítio)
	--geno-depth (por genótipo)
```

### Slide 34

```bash
vcftools --gzvcf eur.22.vcf.gz --depth --out eur.22.depth 

# After filtering, kept 60 out of 60 Individuals
# Outputting Mean Depth by Individual
# After filtering, kept 101568 out of a possible 101568 Sites
# Run Time = 3.00 seconds
```

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

### Slide 36

```bash
vcftools --gzvcf eur.22.vcf.gz --hap-r2 --out eur.22.ld 

# After filtering, kept 60 out of 60 Individuals
# Outputting Pairwise LD (phased bi-allelic only)
# After filtering, kept 101568 out of a possible 101568 Sites
# Run Time =
```

### Slide 37

```bash
vcftools --vcf <file>
	--TsTv <integer> (tamanho do bin, loci bialélicos)
	--TsTv-summary
	--TsTv-by-count
	--TsTv-by-qual
```

### Slide 38

```bash
vcftools --gzvcf eur.22.vcf.gz --TsTv-summary --out eur.22.tstv

# After filtering, kept 60 out of 60 Individuals
# Outputting Ts/Tv summary
# Ts/Tv ratio: 2.265
# After filtering, kept 101568 out of a possible 101568 Sites
# Run Time = 1.00 seconds
```

### Slide 39

```bash
vcftools --vcf <file>
	--relatedness / --relatedness2  
	--missing-indv
	--missing-site
	--singletons (mapeamento, posição e indivíduo)
```

### Slide 40

```bash
vcftools --gzvcf eur.vcf.gz --missing-indv --out eur.22.missing

# After filtering, kept 60 out of 60 Individuals
# Outputting Individual Missingness
# After filtering, kept 101568 out of a possible 101568 Sites
# Run Time = 2.00 seconds
```

### Slide 41

```bash
vcftools --gzvcf eur.vcf.gz --relatedness --out eur.22.relatedness

# After filtering, kept 60 out of 60 Individuals
# Outputting Individual Relatedness
		# Relatedness: Only using biallelic sites.
# After filtering, kept 101568 out of a possible 101568 Sites
# Run Time = 5.00 seconds
```

### Slide 42

```bash
vcftools --vcf <file>
	--weir-fst-pop <filename> (lista de indíviduos de uma população)  
	--fst-window-size <int> / --fst-window-step <int>
	--het
	--hardy
	--LROH
```

### Slide 43

```bash
vcftools --gzvcf eur.vcf.gz --hardy --out eur.22.hardy

# After filtering, kept 60 out of 60 Individuals
# Outputting HWE statistics (but only for biallelic loci)
#         HWE: Only using biallelic SNPs.
# After filtering, kept 101568 out of a possible 101568 Sites
# Run Time = 5.00 seconds
```

### Slide 44

```bash
vcftools --vcf <file>
	--012
	--IMPUTE
	--ldhat / --ldhat-geno
	--BEAGLE-GL / --BEAGLE-PL
	--plink / --plink-tped / --chrom-map
```

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

### Slide 46

```bash
vcf-merge <file1> <file2> | bgzip –c > <output>
```

### Slide 47

```bash
vcf-merge eur.22.15indv.recode.vcf.gz asia.22.15indv.recode.vcf.gz \
| bgzip -c > eur_asia.22.vcf.gz
```

