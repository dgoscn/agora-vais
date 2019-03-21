# CARGOX GIS API TEST

A aplicação da qual o atual projeto se destina, é baseada no projeto GIS. Nela, foram abstraídas algumas funcionalidades, como por exemplo o uso de Frete e Empresas. Contudo, o foco se deu no uso das ferramentas exigidas no teste. É possível visualizar com um Front End a busca pelos caminhoneiros mais próximos a seu dispor baseado em sua geolocalização, usando latitude e longitude.

### Aplicação Final
![frontpage](https://user-images.githubusercontent.com/8397519/54754881-5ba8b600-4bc3-11e9-8082-fffa88b2adf4.PNG)

*Como exibido acima, nós podemos digitar a latitude e longitude que serão mostrados os caminhoneiros ninjas mais próximos*

Na descrição do projeto raiz, é indicado o uso do banco PostgreSQL por conta das ferramentas de geolocalização já disponibilizadas para facilitar a vida.Sendo que, no projeto atual foi utilizadoo banco de dados NoSQL MongoDB. O fato do seu uso se deu por algumas tentativas no uso com o PostgreSQL e algumas falhas técnicas que me permitiram migrar para o Mongo e também pelo limitação do tempo.

## Iniciando

A estrutura do projeto tem as seguintes características:

![sampleproject](https://user-images.githubusercontent.com/8397519/54755777-7a0fb100-4bc5-11e9-844d-611bb090b9ab.png)

Temos o **MongoDB** como banco de dados, o **Node.js** como provisão da API e o **Express**, do qual nos ajuda nas requisições, manipulações e conexões dos estados.

![comunicacao](https://user-images.githubusercontent.com/8397519/54755955-f0acae80-4bc5-11e9-83c9-eb50c2ad10f1.png)

Acima, temos o comportamento dos dados dentro do nosso cenário.

A caracterísica do **Mongo** de modelagem pode ser descrita resumidamente:

**Models**

- Models são representados por **collections** no **MongoDB**, o que pode ser similar ao **TableSQL**

- User model representa uma **collection** de Users

- Shipping Model para representar uma **collection** de Transportadoras

Abaixo, podemos visualizar melhor como seria representado no plano:

![objectcollection](https://user-images.githubusercontent.com/8397519/54756449-040c4980-4bc7-11e9-943b-54a36e35029f.png)

Então vemos uma variedade de trucker(s) com **objectIds** setados automaticamente pelo **MongoDB**. Isso nada mais é do que um identificador único, gerado automaticamente pelo banco.

Dado isso, temos a representação desses objetos no formato json que por sua vez tem sua característica dentro do banco sendo utilizado o **Schema** que por sua vez, nada mais é do que a definição da estrutura dos nossos objetos de daods.

Finalizando a parte de estruturação do projeto, podemos entender como a comunicação acontece e quais possíveis retornos.

![middleware](https://user-images.githubusercontent.com/8397519/54757015-20f54c80-4bc8-11e9-90d8-0560e6f91e92.png)

Então no middleware da aplicação, temos o seguinte cenário. Os requests acontecem, a propriedade do body-parser nos permite ler e utilizar os dados dentro do formato json, como temos o cenário de rotas para as URLs e também a Handling de erros.

## Setup do Projeto

Uma vez que entendemos o funcionamento macro da nossa aplicação, podemos seguir com a configuração do ambiente para execução do projeto em máquina local.

````
Preencher por último
````

```
Falar sobre o mongoose
```

```
Falar sobre o Robo 3T
```

## Testes
Para base de testes, como estamos lidando com uma **API** diretamente e o uso de um Front End para acesso aos dados é apenas perfumaria, usaremos a ferramenta **Postman**. Com ela, podemos utilizar os respectivos requests para a **API** usando os métodos **REST**


### USANDO O MÉTODO POST

Uma vez que temos o sistema sendo executado localmente, podemos manipular nossa **API** começando com o método **POST**, pois uma vez que ele é executado, podemos localizar os **Caminas Ninjas** vulgo *caminhoneiros*, pois os caminhoneiros da nossa plataforma são verdadeiros ninjas.

Para isso, dentro do **Postman** iremos preencher nossos objetos já setados dentro do banco de dados e demonstrados no nosso **Schema**

*Exemplo 1*
``` 
      {
        
        "name": "Rita Lee",
        "geometry": {
            "type": "point",
            "coordinates": [
                -46.576194763183594,
                -23.510005940931347
            ]
       }
```

*Exemplo 2*

Agora dentro do Postman

![post1](https://user-images.githubusercontent.com/8397519/54774156-d71d5e00-4be9-11e9-9dfb-02bf02d8479f.PNG)

Temos a formatação esperada dentro do sistema para o envio dos dados para a **API**.

E por conseguinte, temos o response de criação do item!

![post2](https://user-images.githubusercontent.com/8397519/54774271-177cdc00-4bea-11e9-8cfd-d20f1ab386c3.PNG)

### USANDO O MÉTODO GET

Como temos o sistema rodando e o banco já preenchido com os **Caminas Ninjas**, *poderemos* usar o **GET**. Como nossa arquitetura está voltada para responder com as características de **latitude** e **longitude**, a nossa **URL** acaba sendo um pouco especial, mas nada que complique nossa vida, pelo contrário, acaba facilitando.
Por exemplo, com a rota a seguir, é possível obter o Caminhoneiro Ninja da aplicação.

*Exemplo 1*

````
localhost:4000/gis/shippings/?lng=--46.576194763183594&lat=-23.510005940931347
````

![getresponse](https://user-images.githubusercontent.com/8397519/54773112-a3413900-4be7-11e9-87f1-6f027e732e58.PNG)

Como podemos observar no Postman, temos um resultado de chamado **200 OK** mostrando que realmente o nosso objeto está presente na solitação.

### USANDO O MÉTODO PUT
O método **put** para entrar em funcionamento, é necessário passar um **ID**, esse **ID** representa o **Objeto** dentro do Banco, garantindo que realmente ele responde por aquela identificação. O exemplo abaixo mostra como podemos obtê-lo.

#### Temos duas maneiras de poder verificar o *_id*

1. Robo 3T - é uma ferramenta gratuita para se trabalhar com o MongoDB de forma gráfica.

Uma vez conectado no Banco, podemos seguir os passos a seguir:

![robo3t](https://user-images.githubusercontent.com/8397519/54780339-3bdfb500-4bf8-11e9-8ec3-2137a3334eef.PNG)

Ao abrir o Robot 3T e nos conectarmos com o banco, temos a estrutura exibida acima, onde podemos ver o nosso Model criado; isso é feito pelo uso do **Mongoose**, a interface de omunicação entre o **Nodejs** e o **MongoDB**. Com ele, via funções pre-definidas dentro do código, podemos utilizá-las e agilizar o processo de desenvolvimento.

Abaixo vemo a estrutra exibda pelo **Robo 3T** onde temos o **_id** que procuramos:

![robo3t2](https://user-images.githubusercontent.com/8397519/54780347-400bd280-4bf8-11e9-8303-67e33667a506.PNG)

2. Via Postman alterando o **name** da Collection

![belchior](https://user-images.githubusercontent.com/8397519/54782258-346eda80-4bfd-11e9-857f-c1e8d9d1d347.PNG)

Vá novamente ao Robo 3T e clique no símbolo de play :arrow_forward: isso fará com que o banco seja atualizado.

![belchiorbg](https://user-images.githubusercontent.com/8397519/54782603-0e960580-4bfe-11e9-8f93-de520bf2b992.PNG)

Com isso, podemos conferir e checar a alteração do objeto.

### USANDO O MÉTODO DELETE

O método **delete** tem em sua estrutura de código praticamente o mesmo conceito do **put** necessitando de um identificador para manipula-lo.

![delete](https://user-images.githubusercontent.com/8397519/54782994-05596880-4bff-11e9-9a54-0a398460021a.PNG)

Vemos o mesmo aspecto, apenas mudando a chamada do método na aba do **Postman**. Vemos o resultado de um requisição **OK** por parte do **Postman**. Agora podemos conferir no **Robo 3T**

![deleted](https://user-images.githubusercontent.com/8397519/54783175-726cfe00-4bff-11e9-95b4-a694bacf6510.PNG)

Por fim, temos por fim a execução de todos os métodos dentro da **API**.

## Conclusão

## Agradecimentos

Agradecimento a toda equipe CargoX envolvida nos testes; em especial, a Gabriela Rossi! Todos foram de suma importância.

