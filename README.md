----------------------------------------------------------------

DOCKER

Após baixar e instalar o docker, abra o programa: Docker Desktop

Baixando e executando sua primeira imagem em docker

1 - Para baixar a imagem:

Abra o terminal e digite;
	
	docker pull hello-world
		
O comando pull é utilizado para baixar a imagem que deseja executar, é feito o download da maior biblioteca de docker, acesse para mais detalhes:
dockerhub.com

2 - Executar a imagem baixada:
	
	docker run hello-world 

3 - A imagem está sendo executada e você pode ver os dados no terminal.

----------------------------------------------------------------

DOCKER/SQL

1 - Baixar a imagem mssql:

Abra o terminal e baixe a imagem de MSSQL server 
	docker pull mcr.microsoft.com/mssql/server

Caso necessário uma versão específica, ao final da imagem adicionar a tag, por exemplo .../mssql/server:2019-CU16-ubuntu-20.04

2 - Executar a imagem baixada e salvar database dentro do CONTAINER:
	
	docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=SenhaDeExemplo" -p 14033:1433 --name sql1 -h sql1 -d mcr.microsoft.com/mssql/server
		
-e "ACCEPT_EULA=Y" == aceito contrato microsoft
-e "SA_PASSWORD..." == senha de acesso ao server
1433 == porta interna dentro da imagem
14033 == porta da máquina (Desta maneira, basta trocar a porta 14033 por outra para executar um segundo container.)
--name para nomear o container com o nome desejado
-d == nome da imagem
	
Qualquer Database será salva dentro do container, caso o mesmo seja deletado, todos os dados também seram apagados.

3 - Executar a imagem baixada e salvar database em disco externo ao container:

	docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=SenhaDeExemplo" -p 14033:1433 -v C:PastaDeDestino:/var/opt/mssql/data -v C:PastaDeDestino:/var/opt/mssql/log -v C:PastaDeDestino:/var/opt/mssql/secrets --name sql1 -h sql1 -d mcr.microsoft.com/mssql/server
		
-v == para direcionar e dizer o que salvar dos dados da Database, dessa maneira os arquivos estarao salvos localmente no disco C:\

4 - Conectando ao server 
	
Abrir o Microsoft SQL Server Management 

	Digitar a porta salva do container, usuario e senha definidos na criação do container

Você pode verificar qual a porta do server do servidor dentro do Docker Desktop no menu Containers.

COMANDOS ÚTEIS

* Para restaurar uma Database backup
	
	docker cp LOCAL/NomedoArquivo.bak ID CONTAINER:/var/opt/mssql/data

LOCAL... indicando onde está a Database e para qual ID deve-se restaurar

Depois no Editor MSSQL basta restaurar a Database

Como verificar o ID CONTAINER
	Terminal --> docker ps

* Criando uma imagem 
Colocar o terminal na pasta que está o arquivo Dockerfile(.txt) com os parâmetros da imagem 

	docker build -t NomeDeSuaEscolha .

docker run - ... executar a imagem de acordo com o item 2 ou item 3.

----------------------------------------------------------------

GIT/github

Após baixar e instalar git e criar uma conta no github;

Abra o terminal git bash e acesse a pasta com os arquivos desejados

Pode-se acessar a pasta desejada pelo comando cd, exemplo: cd teste/ (Acessa a pasta teste), ou dentro da pasta desejada, botão direito do mouse e abrir com git bash (abrirá com o caminho de pasta desejado)

1 - Iniciar o repositório dentro da pasta desejada

	git init 

2 - Verificar quais arquivos estão na pasta, foram modificados e não salvos
	
	git status  

3 - Adicionar os arquivos ao repositório

	git add .

O ponto . adiciona todos os arquivos, mas manualmente você pode escrever o nome do arquivo e adiconar os desejados

4 - Salvar os arquivos no repositório local

	git commit -m "...comentário..." - Adicionar o commit

Uma breve e clara explicação do que está sendo salvo no momento, algo que foi modificado ou adicionado

Após isso os arquivos estão salvos na branch master do seu repositório local, agora vamos salvar em um repositório no github para acesso remoto

Você deve criar um novo repositório no github para os seus aqruivos;

5 - Criando conexão do repositório local com o repositório remoto
	
	git remote add origin <link>

link do repositório criado

6 - Enviar os arquivos do repositório local para o remoto

	git push -u origin master 

Pronto, seus arquivos estão também em um repositório remoto

ADICIONAIS

* Depois de criar a conexão e subir os aqruivos, as proximas vezes pode-se utilizar o comando

	git push origin master

Pois a conexão foi estabelecida

* Baixar as alterações do github ou baixar todos os arquivos para um novo repositório

	git pull

* Limpar a timeline do git bash

	clear 