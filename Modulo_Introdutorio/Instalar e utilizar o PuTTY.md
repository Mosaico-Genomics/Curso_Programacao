# PuTTY

É um programa para acessar outros computadores através de vários protocolos, incluindo SSH e SCP. Está disponível para computadores Linux, MacOS e Windows.

## Instalação

### Windows
Acesse o [site oficial](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) e faça o download do instalador apropriado para o seu computador (provavelmente x64). Então, abra o arquivo de instalação:

![image](https://user-images.githubusercontent.com/58569730/117375068-bf29f680-aea4-11eb-8a8c-db3e38be91b9.png)

Escolha a pasta de destino

![image](https://user-images.githubusercontent.com/58569730/117375159-d79a1100-aea4-11eb-9c81-66f6e5e486d9.png)

Instale

![image](https://user-images.githubusercontent.com/58569730/117375182-e385d300-aea4-11eb-9594-0cf228793b22.png)

### Linux
Abra o terminal
`Ctrl+Alt+T`

###### Distros baseadas em Debian/Ubuntu
```bash
sudo apt install putty
```

###### Arch e Manjaro
```bash
sudo pacman -S putty
```

### Mac
Este método assume que você tenha o `brew` instalado. Abra o terminal e instale com o seguinte comando:

```bash
brew install putty
```
## Utilização
Uma vez instalado, vamos ver como utiliza-lo. O primeiro passo é abrir o programa.
Em hostname, na categoria Session, coloque o endereço do servidor que você recebeu.

![image](https://user-images.githubusercontent.com/58569730/117376102-d4a02000-aea6-11eb-813e-9a5f3a38df4f.png)

Clique em Open
A seguinte mensagem aparecerá na primeira vez que você se conectar. Aceite
![image](https://user-images.githubusercontent.com/58569730/117377202-1cc04200-aea9-11eb-8437-6977e8d9edb8.png)

Após isso, uma tela de terminal aparecerá perguntando seu login e depois a sua senha.

![image](https://user-images.githubusercontent.com/58569730/117376939-89870c80-aea8-11eb-92c1-3e862a1c6535.png)

Pronto, você está conectado no servidor.

## Estou no servidor. E agora?
A primeira coisa que você deve ter em mente, é que nosso servidor, [assim como a maior parte de servidores, _mainframes_ e supercomputadores](https://en.wikipedia.org/wiki/Usage_share_of_operating_systems#Public_servers_on_the_Internet), utiliza linux. Portanto, uma vez dentro do servidor, utilize [comandos apropriados.](https://github.com/Mosaico-Genomics/Curso_Programacao/blob/main/Modulo_Introdutorio/ComandosLinux.md)
Uma coisa que também devemos ficar atentos, o tempo de inatividade. Após determinado período sem utilizar o servidor, ele te deconectará, e no caso especifico do windows, o seu console vai travar e você fecha-lo e abrir um novo para poder se conectar de novo.

### Transferindo arquivos entre o servidor e o seu computador

Aqui, o comando é `scp`, de secure copy. A documentação pode ser acessada [aqui.](https://man.openbsd.org/scp)
Sua utilização básica é:
```bash
scp login@servidor:<Arquivo> <Destino> <Parâmetros>
```
_E.g.:_ 
```bash
scp aluno1@127.0.0.1:/home/aluno1/exemplo D:\
```

![image](https://user-images.githubusercontent.com/58569730/117373982-af111780-aea2-11eb-8de4-afa9c762b100.png)
