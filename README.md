# Guess Game

## Visão Geral

Este projeto é um jogo de adivinhação de senha desenvolvido com um backend em Flask e um frontend em React. O projeto utiliza Docker e Docker Compose para facilitar a configuração e execução dos serviços.

## Estrutura do Código

### Rotas:

- **`/create`**: Cria um novo jogo. Armazena a senha codificada em base64 e retorna um `game_id`.
- **`/guess/<game_id>`**: Permite ao usuário adivinhar a senha. Compara a adivinhação com a senha armazenada e retorna o resultado.

### Classes Importantes:

- **`Guess`**: Classe responsável por gerenciar a lógica de comparação entre a senha e a tentativa do jogador.
- **`WrongAttempt`**: Exceção personalizada que é levantada quando a tentativa está incorreta.

## Opções de Design

### Serviços

- **Backend**: Implementado em Flask, gerencia a lógica do jogo e a comunicação com o banco de dados.
- **Frontend**: Implementado em React, fornece a interface do usuário.
- **Banco de Dados**: Utiliza PostgreSQL para armazenar os dados do jogo.
- **Nginx**: Utilizado como um proxy reverso para balancear a carga entre o frontend e o backend.

### Volumes

- **db_data**: Volume para persistir os dados do banco de dados PostgreSQL.

### Redes

- **default**: Rede padrão criada pelo Docker Compose para permitir a comunicação entre os serviços.

### Estratégia de Balanceamento de Carga

- **Nginx**: Configurado para rotear as requisições para o backend e servir o frontend.

## Configuração

### Pré-requisitos

- Docker
- Docker Compose

### Instalação

1. Clone o repositório:

    ```sh
    git clone https://github.com/GuilhermeProcopio/guess_game.git
    cd guess_game
    ```

2. Instale as dependências do frontend:

    ```sh
    cd frontend
    npm install
    cd ..
    ```

### Configuração do Ambiente

1. Crie um arquivo `.env` na raiz do projeto e adicione as seguintes variáveis de ambiente:

    ```env
    POSTGRES_DB=postgres
    POSTGRES_USER=postgres
    POSTGRES_PASSWORD=secretpass
    DATABASE_URL=postgres://postgres:secretpass@db:5432/postgres
    ```

## Como Iniciar

1. Construa e inicie os serviços com Docker Compose:

    ```sh
    docker-compose up --build
    ```

2. Acesse o frontend em `http://localhost:3000`.

## Como Jogar

### 1. Criar um novo jogo

- Acesse a URL do frontend `http://localhost:3000`.
- Digite uma frase secreta e envie.
- Salve o `game_id` gerado.

### 2. Adivinhar a senha

- Acesse a URL do frontend `http://localhost:3000`.
- Vá para o endpoint `breaker`.
- Entre com o `game_id` que foi gerado pelo Creator.
- Tente adivinhar a senha.

## Como Testar

### Testes Automatizados

1. **Frontend**: No terminal, navegue até o diretório `frontend` e execute:

    ```sh
    npm test
    ```

2. **Backend**: No terminal, navegue até o diretório raiz do projeto e execute:

    ```sh
    pytest
    ```

## Atualização dos Serviços

### Atualização das Imagens Docker

Para atualizar qualquer componente, basta alterar a versão da imagem Docker no arquivo `docker-compose.yml` e reconstruir os serviços.

Por exemplo, para atualizar a versão do Node.js no frontend:

1. Abra o arquivo `frontend/Dockerfile` e altere a linha:

    ```Dockerfile
    FROM node:16 as build
    ```

    para

    ```Dockerfile
    FROM node:18 as build
    ```

2. Reconstrua e reinicie os serviços:

    ```sh
    docker-compose up --build
    ```

### Atualização do Backend

Para atualizar o backend, altere a versão da imagem base no arquivo [Dockerfile]():

1. Abra o arquivo [Dockerfile]() e altere a linha:

    ```Dockerfile
    FROM python:3.9-slim
    ```

    para

    ```Dockerfile
    FROM python:3.10-slim
    ```

2. Reconstrua e reinicie os serviços:

    ```sh
    docker-compose up --build
    ```

