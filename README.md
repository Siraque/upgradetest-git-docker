----------------------------------------------------------------

DOCKER

Ap�s baixar e instalar o docker, abra o programa: Docker Desktop

Baixando e executando sua primeira imagem em docker

1 - Para baixar a imagem:

Abra o terminal e digite;
	
	docker pull hello-world
		
O comando pull � utilizado para baixar a imagem que deseja executar, � feito o download da maior biblioteca de docker, acesse para mais detalhes:
dockerhub.com

2 - Executar a imagem baixada:
	
	docker run hello-world 

3 - A imagem est� sendo executada e voc� pode ver os dados no terminal.

----------------------------------------------------------------

DOCKER/SQL

1 - Baixar a imagem mssql:

Abra o terminal e baixe a imagem de MSSQL server 
	docker pull mcr.microsoft.com/mssql/server

Caso necess�rio uma vers�o espec�fica, ao final da imagem adicionar a tag, por exemplo .../mssql/server:2019-CU16-ubuntu-20.04

2 - Executar a imagem baixada e salvar database dentro do CONTAINER:
	
	docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=SenhaDeExemplo" -p 14033:1433 --name sql1 -h sql1 -d mcr.microsoft.com/mssql/server
		
-e "ACCEPT_EULA=Y" == aceito contrato microsoft
-e "SA_PASSWORD..." == senha de acesso ao server
1433 == porta interna dentro da imagem
14033 == porta da m�quina (Desta maneira, basta trocar a porta 14033 por outra para executar um segundo container.)
--name para nomear o container com o nome desejado
-d == nome da imagem
	
Qualquer Database ser� salva dentro do container, caso o mesmo seja deletado, todos os dados tamb�m seram apagados.

3 - Executar a imagem baixada e salvar database em disco externo ao container:

	docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=SenhaDeExemplo" -p 14033:1433 -v C:PastaDeDestino:/var/opt/mssql/data -v C:PastaDeDestino:/var/opt/mssql/log -v C:PastaDeDestino:/var/opt/mssql/secrets --name sql1 -h sql1 -d mcr.microsoft.com/mssql/server
		
-v == para direcionar e dizer o que salvar dos dados da Database, dessa maneira os arquivos estarao salvos localmente no disco C:\

4 - Conectando ao server 
	
Abrir o Microsoft SQL Server Management 

	Digitar a porta salva do container, usuario e senha definidos na cria��o do container

Voc� pode verificar qual a porta do server do servidor dentro do Docker Desktop no menu Containers.

COMANDOS �TEIS

* Para restaurar uma Database backup
	
	docker cp LOCAL/NomedoArquivo.bak ID CONTAINER:/var/opt/mssql/data

LOCAL... indicando onde est� a Database e para qual ID deve-se restaurar

Depois no Editor MSSQL basta restaurar a Database

Como verificar o ID CONTAINER
	Terminal --> docker ps

* Criando uma imagem 
Colocar o terminal na pasta que est� o arquivo Dockerfile(.txt) com os par�metros da imagem 

	docker build -t NomeDeSuaEscolha .

docker run - ... executar a imagem de acordo com o item 2 ou item 3.

----------------------------------------------------------------

GIT/github

Ap�s baixar e instalar git e criar uma conta no github;

Abra o terminal git bash e acesse a pasta com os arquivos desejados

Pode-se acessar a pasta desejada pelo comando cd, exemplo: cd teste/ (Acessa a pasta teste), ou dentro da pasta desejada, bot�o direito do mouse e abrir com git bash (abrir� com o caminho de pasta desejado)

1 - Iniciar o reposit�rio dentro da pasta desejada

	git init 

2 - Verificar quais arquivos est�o na pasta, foram modificados e n�o salvos
	
	git status  

3 - Adicionar os arquivos ao reposit�rio

	git add .

O ponto . adiciona todos os arquivos, mas manualmente voc� pode escrever o nome do arquivo e adiconar os desejados

4 - Salvar os arquivos no reposit�rio local

	git commit -m "...coment�rio..." - Adicionar o commit

Uma breve e clara explica��o do que est� sendo salvo no momento, algo que foi modificado ou adicionado

Ap�s isso os arquivos est�o salvos na branch master do seu reposit�rio local, agora vamos salvar em um reposit�rio no github para acesso remoto

Voc� deve criar um novo reposit�rio no github para os seus aqruivos;

5 - Criando conex�o do reposit�rio local com o reposit�rio remoto
	
	git remote add origin <link>

link do reposit�rio criado

6 - Enviar os arquivos do reposit�rio local para o remoto

	git push -u origin master 

Pronto, seus arquivos est�o tamb�m em um reposit�rio remoto

ADICIONAIS

* Depois de criar a conex�o e subir os aqruivos, as proximas vezes pode-se utilizar o comando

	git push origin master

Pois a conex�o foi estabelecida

* Baixar as altera��es do github ou baixar todos os arquivos para um novo reposit�rio

	git pull

* Limpar a timeline do git bash

	clear 