# Primeiros passos para o acesso ao servidor.


Antes de darmos inicio às atividades no servidor, caso você esteja usando Windows, devemos nos certificar que nossa máquina está devidamente preparada para isso.

Para isso, precisaremos nos certivicar que o OpenSSH está instalado em nosso computador. 

Este link levará diretamente para a página oficial da Microsoft com o tutorial de instalação para o Windows caso não deseje seguir o tutorial a seguir.

> https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse

# OpenSSH


O OpenSSH é é uma ferramenta de conectividade para login remoto que usa o protocolo SSH. Ele criptografa todo o tráfego entre cliente e servidor para eliminar espionagem,
sequestro de conexão e outros ataques. Portanto, devemos intalá-lo em nosso computador para termos acesso ao servidor. Vamos primeiramente verificar se o OpenSSH já está presente em nossa máquina.


Devemos abrir o PowerShell como administrador usando o atalho: Windows+X

No nosso lado esquerdo aparecerá a seguinte aba:

![alt text](https://github.com/lcsfaria/Teste/blob/main/cbd4c2fd-98c1-45df-a78e-8609df65ed93.jpg)


Clique agora em "Windows PowerShell (Admin)" - Isso fará com que o PowerShell seja executado no modo Administrador.


**É DE EXTREMA IMPORTÂNCIA QUE O POWERSHELL ESTEJA NO MODO ADMIN, CASO CONTRÁRIO NENHUM PASSO ADIANTE PODERÁ SER EXECUTADO.**


Após a ação anterior, essa tela irá aparecer: 

![alt text](https://github.com/lcsfaria/Teste/blob/main/7b7bd833-bc66-45a9-b4bc-ddea162cb8a6.jpg)

Pronto, agora você está dentro do Terminal PowerShell!


# Verificando se o OpenSSH já está em seu computador.


Com o PowerShell aberto, vamos COPIAR e COLAR esse comando no nosso terminal. 

> Get-WindowsCapability -Online | ? Name -like 'OpenSSH*'

**ATENÇÃO**: Por padrão, o CTRL+V não funciona dentro do Terminal PowerShell. Após copiarmos um conteúdo com nosso CTRL+C, para colarmos dentro do PowerShell deveremos clicar com o BOTÃO DIREITO DO MOUSE.
 
Assim o conteúdo será colado.

Com o conteúdo colado, aperte ENTER para executá-lo.

Agora, duas mensagemns poderão aparecer:

```diff

Name  : OpenSSH.Client~~~~0.0.1.0
State : NotPresent
Name  : OpenSSH.Server~~~~0.0.1.0
State : NotPresent
```
Ou
```diff
Name  : OpenSSH.Client~~~~0.0.1.0
State : Installed
Name  : OpenSSH.Server~~~~0.0.1.0
State : Installed
```

É necessário que tanto **OpenSSH.Client** quanto **OpenSSH.Server** constem como **"Installed"**.

Se constar como **"Installed"**, sua tarefa aqui já terminou, caso contrário, vamos continuar o nosso Tutorial.


# Instalando o OpenSSH.Client


Para instalarmos o OpenSSH.Client, basta executarmos esse comando em nosso Terminal PowerShell:

> Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0

*Isso pode levar alguns minutos*

Terminada a instalação, podemos seguir para o próximo passo.


# Instalando o OpenSSH.Server


Da mesma forma, para instalarmos o OpenSSH.Server, basta executarmos esse comando em nosso Terminal PowerShell:

> Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0

*Isso pode levar alguns minutos*


# Terminadas as instalações


Após termos terminadas as instalações de *.Client* e *.Server*, verifique agora se tudo ocorreu bem e que eles estão presentes em seu computador:

> Get-WindowsCapability -Online | ? Name -like 'OpenSSH*'


