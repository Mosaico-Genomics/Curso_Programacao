Um compilado dos comandos apresentados durante as aulas.
## Listar
Se você estiver se sentindo perdido, esse comando deve ser o primeiro a ser utilizado. Sua função principal é listar todos os arquivos e pastas no diretório que você está.

uso: ```ls```

Alguns parâmetros úteis do ls:

    -S: arquivos ordenados por tamanho.
    -r: arquivos listados na ordem inversa.
    -a: todos arquivos incluindo os ocultos.
 
## Caminho do diretório atual
Mais um comando útil para se localizar. O pwd (_print working directory_) imprime na tela o diretório que você está no momento.

uso: ```pwd```

## Criar um novo diretório
O mkdir (make directory) é responsável por criar uma nova pasta.

uso:```mkdir [nome da pasta]```

## Mudar de diretório
O comando cd (change directory) leva o usuário ao diretório especificado.

uso: ```cd [caminho]```

***Dicas:***
Para ir à pasta /home/ a partir de qualquer diretório:
```cd ~```

Para ir ao diretório que contém o diretório atual:
```cd ..```

## Copiar
O comando cp (copy) é utilizado para copiar um arquivo ou diretório. É necessário o uso do parâmetro ```-r``` (recursive) para copiar os arquivos de dentro de uma pasta.

uso: ```cp <Origem> <Destino> <Parâmetros>```


## Contar linhas
O comando wc (word count) é um comando para contar palavras e, por extensão, bytes e linhas.

uso: ```wc <Arquivo> <Parâmetros>```

Alguns parâmetros úteis:

    -c: conta bytes.
    -l: conta linhas.
    -m: conta caracteres.
    -w: conta palavras.

## Ver as primeiras linhas de um arquivo
O comando head mostra, por padrão, as primeiras dez linhas de um arquivo.

uso: ```head <Arquivo> <Parâmetros>```

Para um numero de linhas diferente de dez, utilizar o parâmetro ```-n``` seguido pelo valor de linhas desejado

## Ver as últimas linhas de um arquivo
Assim como o comando anterior, o comando tail mostra, por padrão, as primeiras dez linhas de um arquivo.

uso: ```tail <Arquivo> <Parâmetros>```

Para um numero de linhas diferente de dez, utilizar o parâmetro ```-n``` seguido pelo valor de linhas desejado

## Concatenar
O comando cat (con***cat***enate) é um comando usado para unir, criar e exibir arquivos.

Para exibir o conteúdo de um arquivo na tela: ```cat <Arquivo>```

Para concatenar (juntar) dois arquivos: ```cat Arquivo1 Arquivo2 > Arquivo3```

***Obs. 1***: é possível usar esse comando com vários arquivos ao mesmo tempo.

***Obs. 2***: note o uso da expressão ```>```. Neste caso (e em inúmeros outros) siginifica _output_. Ou seja, o Arquivo1 e Arquivo2 serão concatenados em um novo arquivo, o Arquivo3.

## Vizualizar grandes textos
O comando more é utilizado para fazer paginação de arquivos e permitir a leitura de arquivos grandes

uso: ```more <Arquivo>```

## Editor de textos
O comando nano abre um editor de textos nativo do LINUX para editar um arquivo ou criar um novo.

Para editar texto existente: ```nano <Arquivo>```

Para abrir o editor vazio e criar novo texto: ```nano```

## Mover e renomear arquivos
O comando mv move e renomeia arquivos e/ou diretórios de uma origem para um destino

uso: ```mv <Origem> <Destino>```

## Compactação e descompactação

### Compactação
O principal algoritmo de compactação utilizado no LINUX é o gzip.

uso: ```gzip <Arquivo>```

Infelizmente, o gzip é capaz de compactar apenas um arquivo por vez. Para compactar mais de um arquivo, utilizamos o comando tar para junta-los em um só.

uso: ```tar -zcvf  <Nome do arquivo compactado> <Lista de arquivos a compactar>```

### Descompactação

Para descompactar um arquivo compactado pelo gzip (geralmente com sufixo “.gz”) nós utilizamos o gunzip.

uso: ```gunzip <Arquivo>```

No caso de um arquivo tar compactado com o gzip, nós utilizamos o comando abaixo:
uso: ```tar -zcvf```

## Deletar
O comando rm remove arquivos que cujo o nome dá match com o escolhido. _Utilize com cautela_

uso: ```rm <Nome do arquivo e/ou expressão>```

Opções úteis do comando:

    -f : apaga sem pedir confirmação.
    -i : apaga após pedir confirmação.
    -r : apaga arquivos e subdiretórios.
    -v : lista arquivos deletados.

## Download de arquivos
O comando scp (Secure Copy) é um protocolo de rede para transferência de arquivos. É útil, por exemplo, para fazer o download de arquivos do servidor para o seu computador.

uso: ```scp <Origem> <Destino> <Parâmetros>```

## Ordenação
O comando sort ordena uma entrada. Essa entrada pode ser um arquivo ou a saída de outro comando. 

uso: ```sort <Input> <Parâmetros>```

Por padrão, a ordenação é alfabética. Outras opções são:

    -b : ignora espaços em branco.
    -c : retorna uma mensagem de erro se o arquivo não estiver ordenado.
    -f : ignora a diferença entre letras maiúsculas e letras minúsculas.
    -r : organiza em ordem decrescente.
    –n : para ordenação numérica
    –h : para ordenação numérica humana (K(quilo), G(giga), T(tera))

## Linhas repetidas
O comando uniq retorna o conteúdo do input sem exibir as linhas repetidas.

uso: ```uniq <Input> <Parâmetros>```

Alguns parâmetros úteis:

    -u : Exibe somente as linhas que não se repetem
    -c : Imprime a quantidade de vezes cada repetição foi encontrada
