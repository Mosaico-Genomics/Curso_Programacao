# Bem vindos ao curso de programação da Mosaico

Nesta seção, vocês encontrarão os codigos das bibliotecas PANDAS e PyVCF utilizadas durantes as aulas.


# PANDAS

* Pandas é uma biblioteca utilizada para análise e manipulação de dados.
* Uma das principais bibliotecas utilizadas por cientistas de dados.
* Pode ser usada em conjunto com outras bibliotecas como Sklearn (IA).

* slide 228
```
import pandas as pd
data=pd.read_csv('C:/Users/Cliente/Desktop/Titanic.csv', sep='\t')
```
* slide 229
```
data.info()
```
* slide 230
```
data.head()
```
* slide 232
```
data.tail(6)
```
* slide 233
```
data.index

data.head()
```
* slide 234
```
data.set_index("PassengerId", inplace=True)
data.head()
```
* slide 235
```
data.columns
```
* slide 236
```
data.describe()
```
* slide 237
```
data.values
```
* slide 239
```
data.loc[[1,2,3]]
```
* slide 240
```
data60= data.loc[1:60]
data60.tail()
```
* slide 241
```
IDPar=data.loc[2:860:2]
IDPar.head()
```
* slide 242
```
data.loc[[1,3,5],["Name","Sex","Fare"]]
```
* slide 243
```
sortedByFare=data.sort_values("Fare")
sortedByFare.head()
```
* slide 244
```
sortedByFare=data.sort_values("Fare",ascendig=False)
sortedByFare[["Name","Fare"]].head(15)
```
* slide 245
```
data["Sex"].value_counts()
data["Age"].value_counts()
```
* slide 246
```
data.query("Age == 0.42")
```
* slide 247
```
data.query('Sex == "male" & Age >= 18').head()
HomensAdultos=data.query('Sex == "male" & Age >= 18')
HomensAdultos["Survived"].value_counts()
```
* slide 248
```
data.query('Sex == "Female" | Age < 18')
MulheresOuCriancas=data.query('Sex == "female" | Age < 18')
MulheresOuCriancas["Survived"].value_counts()
```
* slide 249
```
data.query('Age in [24, 22,18]')
```
* slide 250
```
data.isnull().sum()
```
* slide 251
```
data.drop(labels = ["Cabin"], axis=1, inplace= True)
data.head()
```
* slide 252
```
data["Age"].fillna("Unknown").value_counts()
```
* slide 253
```
data["Age"].fillna(data["Age"].mean()).value_counts()
```
* slide 254
```
data["Age"].fillna(data["Age"].median()).value_counts()
```
* slide 255
```
withoutAgeNA=data.query('Age != "NAN"')
withoutAgeNA.isnull().sum()
withoutAgeNA.describe()
```
* slide 256
```
withoutAgeNA.isnull().sum()
```
* slide 257
```
withoutNA= data.dropna()
withoutNA.isnull().sum()
```
* slide 258
```
withoutNA.describe()
```
* slide 259
```
withoutNA['Pclass'].as_type('string')
withoutNA['Sex'] = withoutNA['Sex'].str.replace('male','1')
withoutNA['Sex'] = withoutNA['Sex'].str.replace('female','2')
```
***

* PyVCF

![image](https://user-images.githubusercontent.com/11162991/117059386-25244b80-acf6-11eb-862f-ea51582e70bb.png)

* slide 268
```
import vcf
vcfFile = vcf.Reader(open('VCF.vcf', 'r'))
for data in vcfFile:
  print(data)
  
```
* slide 269
```
vcfFile = vcf.Reader(open('VCF.vcf', 'r'))
record = next(vcfFile)
print(record.POS)
```

* slide 270 - Metadata
```
#Metadata
data=vcfFile.metadata['fileDate']
print(f'A data deste VCF eh: {data}')
print(f'As amostras que temos eh: {vcfFile.samples}')
print(f'Vamos ver os filtros que foram utilizados:')
for filtro in vcfFile.filters:
  print (f'\tO id do filtro eh {vcfFile.filters[filtro].id} e a descricao eh : {vcfFile.filters[filtro].desc}')

```

* slide 271
```
print(f'Quais os infos que este VCF possui?')
for info in vcfFile.infos:
  print(f'\t{vcfFile.infos[info].id}: O tipo eh \"{vcfFile.infos[info].type}\" e a descricao eh: {vcfFile.infos[info].desc}')

```

* slide 272
```
print(record.ID)
```

* slide 273
```
#Numero de called
print(f'Num called :{record.num_called}')
print(f'Call rate :{record.call_rate}')
print(f'Unknown call :{record.num_unknown}')
```

* slide 274
```
print(record.INFO)
print(record.INFO['AF'])
```
* slide 275
```
print(f'Homozigoto para alelo de referencia : {record.num_hom_ref}')
print(f'Heterozigoto :{record.num_het}')
print(f'Homozigoto para alelo alternativo :{record.num_hom_alt}')
```

* slide 276
```
print(f'Alternative alele frequency :{record.aaf}')
print(f'Heterozigosidade :{record.heterozygosity}')
```

* slide 277
```
print(f'Eh um SNP? {record.is_snp}')
print(f'Eh um indel? {record.is_indel}')
print(f'Eh uma variação estrutural? {record.is_sv}')
print(f'Eh uma deleção? {record.is_deletion}')
```

* slide 278
```
print(f'Meu tipo eh {record.var_type}')
```

* slide 279
```
for sample in record:
  print(sample)
```

* slide 280
```
print(record.genotype('NA00003')['GT'])
call = record.genotype('NA00003')
```


* slide 281
```
print(f'Dados do call {call.site}')
print(f'Tipo do genotipo (0 - Hom ref, 1 - Het, 2 - Hom alt) {call.gt_type}')
print(f'Dado do genotipo {call.gt_bases}')
print(f'Eh Phased? {call.phased}')
```




