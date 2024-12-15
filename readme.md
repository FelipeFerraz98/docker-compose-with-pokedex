# Docker React With Pokedex

Este é um projeto de estudos utilizando **Docker** para rodar um **website React** (Pokedex) dentro de um container Apache. O objetivo deste projeto é aprender a configurar e orquestrar containers com o Docker e Docker Compose, utilizando uma arquitetura simples com o **Apache** como servidor web.

## Estrutura do Projeto

Este repositório contém a configuração necessária para rodar um aplicativo React (Pokedex) em um container Apache utilizando `docker-compose.yml`. O site será servido através do Apache, com os arquivos da aplicação React sendo copiados para o container via volume.

## Tecnologias Utilizadas

- **Docker**: Plataforma de contêineres para desenvolver, transportar e executar aplicações.
- **Docker Compose**: Ferramenta para definir e rodar aplicações Docker multi-container.
- **Apache HTTP Server**: Servidor web que irá servir a aplicação React.
- **React**: Biblioteca JavaScript para construção de interfaces de usuário.

## Como Rodar o Projeto

### Pré-requisitos

- **Docker** e **Docker Compose** instalados na sua máquina.
  
  Caso não tenha o Docker e o Docker Compose, você pode instalar seguindo os tutoriais oficiais:
  
  - [Instalar Docker](https://docs.docker.com/get-docker/)
  - [Instalar Docker Compose](https://docs.docker.com/compose/install/)

## Passos para Execução

1. Clone este repositório para sua máquina:

   ```bash
   git clone https://github.com/SeuUsuario/docker-react-pokedex.git
   cd docker-react-pokedex
   ```

2. Certifique-se de que o diretório `./website` contém os arquivos da sua aplicação React (Pokedex) já compilados. Se não estiverem compilados, siga os seguintes passos para compilar:

   ```bash
   cd website
   npm install
   npm run build
   cd ..
   ```

3. Após garantir que o diretório `./website` está com os arquivos da aplicação compilados, execute o Docker Compose para iniciar o ambiente:

   ```bash
   docker-compose up
   ```

4. Acesse o website através de seu navegador, indo para `http://localhost`.

### Arquivo `docker-compose.yml`

Aqui está o conteúdo do arquivo `docker-compose.yml` que orquestra o container Apache e a aplicação React:

```yaml
version: '3.9'

services:
  apache:
    image: httpd:latest
    container_name: my-apache-app
    ports:
      - '80:80'
    volumes:
      - ./website:/usr/local/apache2/htdocs
```

### Explicação do `docker-compose.yml`

- **`version: '3.9'`**: Define a versão do Docker Compose que está sendo utilizada.
- **`services`**: Define os serviços (containers) que serão executados no projeto.
  - **`apache`**: Nome do serviço que será responsável por rodar o servidor Apache.
    - **`image: httpd:latest`**: Utiliza a imagem oficial mais recente do Apache.
    - **`container_name: my-apache-app`**: Nome do container Apache.
    - **`ports: '80:80'`**: Mapeia a porta 80 do host para a porta 80 do container (acesso à aplicação através da porta 80).
    - **`volumes: ./website:/usr/local/apache2/htdocs`**: Monta o diretório `./website` do seu projeto para dentro do container, no diretório onde o Apache espera os arquivos (`/usr/local/apache2/htdocs`).

## Como Funciona

1. O Docker Compose cria um container Apache.
2. O Apache é configurado para servir os arquivos estáticos da aplicação React, que estão no diretório `./website`.
3. Ao acessar `http://localhost` no seu navegador, o Apache irá servir os arquivos da aplicação React, que foram montados no container através do volume configurado no `docker-compose.yml`.