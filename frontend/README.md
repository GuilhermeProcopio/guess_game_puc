# Projeto de Aplicação Web

## Sumário
- [Visão Geral](#visão-geral)
- [Opções de Design](#opções-de-design)
- [Instalação](#instalação)
- [Execução](#execução)
- [Atualização](#atualização)
- [Componentes](#componentes)

## Visão Geral
Este projeto é uma aplicação web composta por um frontend em React e um backend em Python. Utilizamos Docker para facilitar a configuração e a execução dos serviços.

## Opções de Design

### Serviços
Optamos por dividir a aplicação em dois serviços principais:
- **Frontend**: Implementado em React, localizado na pasta `frontend/`.
- **Backend**: Implementado em Python, localizado na pasta `guess/` e `repository/`.

### Volumes
Utilizamos volumes Docker para persistir dados importantes e facilitar o desenvolvimento:
- Volume para persistir dados do banco de dados.
- Volume para compartilhar código-fonte entre o host e os containers.

### Redes
Criamos uma rede Docker personalizada para permitir a comunicação entre os containers do frontend e backend.

### Estratégia de Balanceamento de Carga
Utilizamos o Nginx como proxy reverso para balancear a carga entre múltiplas instâncias do backend, garantindo alta disponibilidade e escalabilidade.

## Instalação
Para instalar o projeto, siga os passos abaixo:

1. Clone o repositório:
    ```sh
    git clone https://github.com/seu-usuario/seu-repositorio.git
    cd seu-repositorio
    ```

2. Instale as dependências do frontend:
    ```sh
    cd frontend
    npm install
    cd ..
    ```

3. Construa as imagens Docker:
    ```sh
    docker-compose build
    ```

## Execução
Para rodar o projeto, utilize o Docker Compose:

```sh
docker-compose up
```

Componentes
Frontend
O frontend é uma aplicação React localizada na pasta frontend/. Para atualizar o frontend, você pode modificar o código-fonte em frontend/src/ e reconstruir a imagem Docker.

Backend
O backend é uma aplicação Python localizada nas pastas guess/ e repository/. Para atualizar o backend, você pode modificar o código-fonte e reconstruir a imagem Docker.

Banco de Dados
Utilizamos diferentes bancos de dados, como DynamoDB, PostgreSQL e SQLite, localizados na pasta repository/. Para atualizar a configuração do banco de dados, modifique os arquivos correspondentes e reinicie os serviços.