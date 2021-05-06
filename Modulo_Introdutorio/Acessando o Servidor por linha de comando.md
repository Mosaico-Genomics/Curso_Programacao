# Conectando ao servidor através de linha de comando (CLI)
Como todos os três principais sistemas operacionais (MacOS, Linux e Windows) utilizam OpenSSH, os comandos são os mesmos nas três plataformas. A diferença está em como acessar o interpretador de linha de comando de cada um dos sistemas.
#
#### Windows 10
Desde o update “Fall Creators” de 17 de outubro de 2017, o Windows 10 tem o recurso OpenSSH instalado e habilitado por padrão. Por isso, é provável que você seja capaz de acessar o Servidor através de seu computador sem nenhuma instalação extra. Caso seja necessário, veja [como instalar o OpenSSH](https://github.com/Mosaico-Genomics/Curso_Programacao/blob/main/Modulo_Introdutorio/Instalando%20OpenSSH%20no%20Windows.md) ou [como instalar o PuTTY](https://github.com/Mosaico-Genomics/Curso_Programacao/blob/main/Modulo_Introdutorio/Instalar%20e%20utilizar%20o%20PuTTY.md).
Uma vez que você tem o OpenSSH instalado, você pode utilizar o comando no prompt de comando (CMD) ou powershell. Para acessalos basta abrir o menu de iniciar do windows e buscar por CMD ou Powershell. Caso não ache, pressione `win+r` no seu teclado, digite cmd e aperte enter.

#### Linux
Computadores GNU/Linux, em geral, vem com OpenSSH por padrão. Os comandos são utilizados no terminal, que na maioria das distros pode ser acessado através do atalho `Ctrl+Alt+T`.

#### Mac
Exatamente o mesmo caso do Linux. Para acessar o terminal, abra o Spotlight com `cmd+espaço` e digite terminal.

## Acessando o servidor

Uma vez que seu interpretador de linha de comando está aberto, a sintaxe é a mesma nos três sistemas operacionais. O comando simplificado para acessar um servidor é o seguinte:

```bash
ssh user@IP <Parâmetros>
```


_E.g._: `ssh aluno1@127.168.0.1`

Após digitar o comando e pressionar enter, você pode se deparar com a seguinte mensagem:

![image](https://user-images.githubusercontent.com/58569730/116618420-6ba03180-a915-11eb-86b4-2ed0c7b3e83e.png)


Basta digitar yes e essa mensagem não aparecerá mais. Por fim, você vai precisar digitar sua senha. Quando estiver digitando, não aparecerá nenhum caractere. Não se preocupe, é normal. Digite sua senha com calma e dê enter. Se tudo ocorrer bem, você verá que se conectou ao servidor. Deve se deparar com algo paracido com:

![image](https://user-images.githubusercontent.com/58569730/117374522-b258d300-aea3-11eb-9406-804ddb371e9c.png)

Você pode ler mais a respeito  [no site oficial](https://www.openssh.com/) e também acessar a documentação de uso [aqui.](https://man.openbsd.org/ssh)

## Estou no servidor. E agora?
A primeira coisa que você deve ter em mente, é que nosso servidor, [assim como a maior parte de servidores _mainframes_ e supercomputadores](https://en.wikipedia.org/wiki/Usage_share_of_operating_systems#Public_servers_on_the_Internet), utiliza linux. Portanto, uma vez dentro do servidor, utilize [comandos apropriados.](https://github.com/Mosaico-Genomics/Curso_Programacao/blob/main/Modulo_Introdutorio/ComandosLinux.md)
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
