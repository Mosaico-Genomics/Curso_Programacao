# Módulo 1 - VCF/VCFtools

## Aula 6 - A ferramenta VCFTools  (07/06/2021)

**Prof. Dr.** **Giordano Soares**

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

Descrição do comando acima.

### Slide 10

```bash
git clone https://github.com/vcftools/vcftools.git  
cd vcftools
./autogen.sh
./configure
make
make install
```



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



### Slide 13

```bash
bgzip snps.vcf
tabix –p vcf snps.vcf.gz
ls –lht

# -rw-r--r--  1 giordanob Nativos 415K Jan 25 23:40 snps.vcf.gz
# -rw-r--r--  1 giordanob Nativos  24K Jan 25 23:45 snps.vcf.gz.tbi
```



### Slide 14

```bash
vcftools --vcf <file> 
	--chr <chrom> / --not-chr <chrom>
	--from-bp <integer> / --to-bp <integer>
	--positions <filename> / --exclude-positions <filename>
	--thin <integer> (distância minima entre loci)
	--bed <filename>
	--mask <filename> / --invert-mask <filename> / --mask-min <integer>
```



### Slide 15

```bash
vcftools --gzvcf snps.vcf.gz --chr 61 --from-bp 30 --to-bp 180 --recode --out snps.chr61.vcf

# (…)
# After filtering, kept 30 out of 30 Individuals
# After filtering, kept 5 out of a possible 2846 Sites
# Run Time = 0.00 seconds
```

### Slide 16

```bash
vcftools --gzvcf snps.vcf.gz --chr 128 --recode -c | bgzip -c > snps.chr128.vcf.gz ; tabix –p vcf snps.chr128.vcf.gz
```

### Slide 17

```bash
vcftools --vcf <file> 
	--snp <string> 
	--snps <filename> / --exclude <filename>
	--keep-indels-only / --remove-indels
```

### Slide 18

```bash
vcftools --gzvcf indels.eur.22.vcf.gz --remove-indels --recode --out noindels.eur.22

# After filtering, kept 60 out of 60 Individuals
# Outputting VCF file...
# After filtering, kept 101568 out of a possible 102304 Sites
# Run Time = 14.00 seconds
```

### Slide 19

```bash
vcftools --gzvcf eur.22.vcf.gz \
--snps chr22.100rs.txt --recode \
--out snps100.eur.22.vcf 

# After filtering, kept 60 out of 60 Individuals
# Outputting VCF file...
# After filtering, kept 100 out of a possible 77867 Sites
# Run Time = 0.00 seconds
```



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

