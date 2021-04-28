# Executando o projeto

Projeto do desafio PFA  estudo sem fazer uso do docker-composer

## Rodando imagens

No terminal digite os seguintes comandos

```bash
docker network create pfanet &&
docker run --rm -d --name=pfa-mysql --network pfanet taranttini/pfa-mysql &&
docker run --rm -d --name=pfa-go --network pfanet taranttini/pfa-go &&
docker run --rm -d --name=pfa-nginx --network pfanet -p 80:80 taranttini/pfa-nginx &&
echo 'servicos iniciados acesse http://localhost/api/modules'
```

### Rotas possíveis

- Listando todos módulos

    - GET `http://localhost/api/modules`

- Listandos todos módulos que tenham no nome o texto `go`

    - GET `http://localhost/api/modules?name=go`

- Listando um módulo específico

    - GET `http://localhost/api/modules/1`

- Atualizando um módulo

    - PUT `http://localhost/api/modules/1`

    ```json
    {
        "name": "atualizando_nome",
        "active": false
    }
    ```

- Criando um novo módulo

    - POST `http://localhost/api/modules`
    ```json
    {
        "name": "novo_nome",
        "active": true
    }
    ```

- Removendo um módulo

    - DELETE `http://localhost/api/modules/20`


**OBS**

*O PUT, POST e DELETE necessita de uma ferramenta tipo **POSTMAN**, **INSOMINA**, ou linha de comando **curl** para execução das rotas*

## Criando imagens se necessário reconstruir os containters

No terminal digite os seguintes comandos

```bash
cd mysql && docker build -t <seu_usuario_dockerhub>/pfa-mysql:latest . &&
cd ../go && docker build -t <seu_usuario_dockerhub>/pfa-go:latest . &&
cd ../nginx && docker build -t <seu_usuario_dockerhub>/pfa-nginx:latest . &&
cd .. && echo 'imagens criadas..., crie a network e execute as imagens'
```

Crie a network caso ela não exista com o seguinte comando no terminal

```bash
docker network create pfanet &&
echo 'execute as imagens'
```

Executando as imagens 

```bash
docker run --rm -d --name=pfa-mysql --network pfanet <seu_usuario_dockerhub>/pfa-mysql &&
docker run --rm -d --name=pfa-go --network pfanet <seu_usuario_dockerhub>/pfa-go &&
docker run --rm -d --name=pfa-nginx --network pfanet -p 80:80 <seu_usuario_dockerhub>/pfa-nginx &&
echo 'servicos iniciados acesse http://localhost/api/modules'
```

## Criando imagens isoladamente se necessário

Crie a network caso ela não exista com o seguinte comando no terminal

```bash
docker network create pfanet
```

### MySql

Acesse a pasta do mysql e digite o comando para criar a imagem

```bash
docker build -t <seu_usuario_dockerhub>/pfa-mysql:latest . &&
docker run --rm --name=pfa-mysql --network pfanet <seu_usuario_dockerhub>/pfa-mysql
```

### Go

Acesse a pasta do go e digite os comandos

```bash
docker build -t <seu_usuario_dockerhub>/pfa-go:latest . &&
docker run --rm --name=pfa-go --network pfanet <seu_usuario_dockerhub>/pfa-go
```

## Nginx

Acesse a pasta do go e digite os comandos

```bash
docker build -t <seu_usuario_dockerhub>/pfa-nginx:latest . &&
docker run --rm --name=pfa-nginx --network pfanet -p 80:80 <seu_usuario_dockerhub>/pfa-nginx
```