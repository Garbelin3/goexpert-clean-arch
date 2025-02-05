# Curso GO Expert - Clean Architecture

### Como usar

O projeto utiliza `Docker` então é necessário o `Docker` e `Docker Compose` instalado em sua máquina.

Para iniciar o projeto siga os passos:

1. Na raiz do projeto execute o comando `docker compose up --build` e aguarde os `containers` do `mysql` e `rabbitmq` iniciarem;
2. Para acessar o `rabbitmq` acesse: `http://localhost:15672` com `guest` para `username / password`;
3. Adicione a fila clicando em `Queues and Streams` no campo `name` coloque `orders` e clique em `Add queue`;
4. Criada a fila acesse ela e em `Bindings` no campo `From exchange` coloque `amq.direct`;
5. Para rodar as `migrations` é necessário ter instalado a `CLI` do `golang-migrate` siga essa documentação: https://github.com/golang-migrate/migrate/tree/master/cmd/migrate;
6. Com a `CLI` instalada na raiz do projeto execute o comando `make migrateup` para criar a tabela e `make migratedown` para excluir a tabela;
7. Entre o diretório `cmd/ordersystem` e execute o comando `go run main.go wire_gen.go`;

Com isso o sistema já está pronto para o uso, para testar existe algumas formas:

1. `REST API`:
    - No diretório `api` tem um arquivo `create_order.http` que usa um `plugin` do `vscode` de `client rest` https://github.com/Huachao/vscode-restclient basta executar as `requests` por esse arquivo.
2. `GRPC`:
    - Para utilizar o `GRPC` é necessário um `client`, o que foi utilizado nesse projeto é esse: https://github.com/ktr0731/evans mas pode consumir com algum outro caso queira, para utilizar o `Evans` execute o comando `evans -r repl` digite `call` e ao dar um espaço já irá aparecer os serviços diponíveis, `CreateOrder` cria um novo registro e `ListOrder` lista as ordens;
3. `GraphQL`:
    - Para utilizar `GraphQL` acesse `http://localhost:8080/` e cria a `mutation` para inserir dados:
    ```graphql
        mutation createOrder {
            createOrder(input: { id: "abc", Price: 12.2, Tax: 2.0 }) {
                id
                Price
                Tax
                FinalPrice
            }
        }

        query queryOrders {
            orders {
                id
                Price
                Tax
                FinalPrice
            }
        }
    ```
