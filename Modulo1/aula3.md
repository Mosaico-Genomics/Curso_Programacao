# Módulo 1 - SED/AWK

## Aula 3 - Apresentação e manipulação de formatos especíﬁcos de dados genéticos   (27/05/2021)

**Profa. Dra.** **Fernanda S. Kehdy**

Neste documento estão disponíveis os códigos demonstrados nos slides da aula 2. As saídas dos comandos, sempre que mostradas, são iniciados por #.

### Slide 13

```bash
cat toy_S1_L001_R1_001.fastq | wc -l | awk '{d=$1;print d/4}'
# 25000
```

No exemplo acima, o conteúdo do arquivo FASTQ é enviado para o `wc` que conta o número de linhas `-1`.  Esse número é passado como *input* para o `awk`, o qual armazena o primeiro campo contendo o valor `25000` na variável `d`. Por fim, o resultado da divisão de 2500 :heavy_division_sign: 4​ é impresso na saída padrão. Esse valor é o número de **sequências** no FASTQ, visto que cada sequência ocupa 4 linhas de acordo com esse formato.

### Slide 29

```bash
head -1 variant_summary.txt | tr '\t' '\n' | awk '{print NR, $0}' > lista_clinvar

# 1 #AlleleID
# 2 Type
# 3 Name
# 4 GeneID
# 5 GeneSymbol
# 6 HGNC_ID
# 7 ClinicalSignificance
# 8 ClinSigSimple
# 9 LastEvaluated
# 10 RS# (dsSNP)
# [...]
```

No código acima, a primeira linha do arquivo é passado ao utilitário `tr` que troca as **tabulações por novas linhas** (transpõe). O resultado disso é enviado ao `awk`, o qual adicionará uma nova coluna na primeira posição `$0` com o número de cada linha (através do conteúdo da variável interna `NR`). Finalmente, o resultado é salvo no disco.