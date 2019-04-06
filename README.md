# Configuração para execução do Adonis em Docker

## Arquivos necesários para que um projeto AdonisJS + MySQL seja executado em containers Docker.

###Com a adição desses arquivos no seu projeto, serão construído 3 containers:

adonis-docker - Onde estará executando o seu servidor web (nodeJS + AdonisJS).

mysql-docker - Onde estará executnado o seu servidor MySQL5.7.

phpmyadmin-docker - Onde estará executando o PHPMyAdmin para alterações via browser (localhost:8080).

## 1º - PASSO

###Se ainda não existir, projeto basta executar:

```js
adonis new nome-do-projeto
```

####ATENÇÃO - Copie a APP_KEY= do seu arquivo .env para adicionar no que será adicionado ao seu projeto
Copiar todos os arquivos para a raiz do projeto AdonisJS. (Atenção: O .env substituirá o já existente na raiz do seu projeto.)

###Caso o projeto já exista:

####ATENÇÃO - Copie a APP_KEY= do seu arquivo .env para adicionar no que será adicionado ao seu projeto

Copiar todos os arquivos para a raiz do projeto AdonisJS. (Atenção: O .env substituirá o já existente na raiz do seu projeto.)

## 2º - PASSO

Realizar as configurações no arquivo .env relativas as informações de banco de dados.

```js
// Define qual engine será utilizada para a conexão com o banco de dados.
DB_CONNECTION = mysql;
// O HOST tem que apontar para o nome do serviço no qual o banco está sendo levantado no container, essa configuração vem do nome do serviço no arquivo docker-composer.yml
DB_HOST = mysql;
DB_PORT = 3306;
DB_USER = root;
DB_PASSWORD = 12345;
// Base de dados que será criada assim que o container levantar
DB_DATABASE = adonis;
```

## 3º - PASSO

Executar o docker-compose:

```js
docker-compose up --build
```

## 4º - PASSO

Instalar o engine mysql dentro do container onde está rodando a aplicação AdonisJS (adonis-docker):

```js
docker exec adonis-docker npm i mysql
```

## 5º - PASSO

Rodar as migrations, para a criação das tabelas no banco de dados (esse passo também serve para atualizar o banco quando novas migrations forem criadas.)

```js
docker exec adonis-docker adonis migration:run
```
